# QA plan + quality gates

## Flow

Quy trình bảo đảm chất lượng tuân theo mô hình 7 bước:
`Guideline v1 → Calibration nội bộ → Refinement v2 → Production / Blind Test → Self-QC → QA Review → Quality Gate`.

- **Ai review, review bao nhiêu:**
  - QA Lead (Đinh Minh Hoàng) thực hiện review 100% các mẫu trong tập `blind` và lấy mẫu ngẫu nhiên 30% các mẫu trong quá trình sản xuất thông thường.
- **Chọn sample theo rule nào:**
  - 100% các sample có tag `critical`, `night`, `low_visibility`, `ambiguity` (nhóm rủi ro cao).
  - 100% các sample được annotator đánh cờ `needs_review = true`.
  - 20% các sample có tag `normal` được chọn ngẫu nhiên để giám sát độ lệch hình học cơ bản.
- **Issue được ghi ở đâu, đóng thế nào:**
  - Mọi lỗi phát hiện trong quá trình review được ghi trực tiếp vào `06_calibration_report.csv` (cho calibration) hoặc `transfer_score.csv` / `clarification_log.csv` (cho blind test).
  - Issue chỉ được đóng khi annotator thực hiện rework đạt yêu cầu hoặc có rule cập nhật trong guideline.
- **Khi phát hiện guideline gap thì update và version ra sao:**
  - Nếu phát hiện điểm hở trong guideline khiến 2 annotator hiểu khác nhau, QA Lead triệu tập thảo luận, chốt quyết định dựa trên downstream contract, nâng version guideline (v1 → v2 → v3) và ghi rõ nguyên nhân vào `08_revision_log.md`.

## Defect severity

| Severity | Định nghĩa cho project này | Ví dụ | Action mặc định |
|---|---|---|---|
| Critical | Lỗi trực tiếp gây ra quyết định sai lầm thảm khốc cho xe tự hành (vượt đèn đỏ hoặc phanh gấp đột ngột) | Nhầm `red` thành `green`/`off`; Gán `relevant` cho đèn rẽ của làn phụ khi xe đi thẳng | REWORK ngay lập tức toàn bộ batch và kiểm tra lại 100% ảnh |
| Major | Sai lệch trạng thái hoặc bỏ sót đối tượng nhưng không dẫn tới va chạm ngay lập tức | Bỏ sót 1 cụm đèn ở ngã tư; Gán nhầm `circle` thành `arrow_straight` | REWORK mẫu cụ thể |
| Minor | Lệch hình học nhỏ không làm thay đổi ngữ nghĩa điều khiển | Bounding box lệch 3–5 px, bao thừa một phần nhỏ cần vươn | Chấp nhận (ACCEPT) hoặc chỉnh sửa nhanh |
| Question | Trường hợp mơ hồ cao do chất lượng ảnh | Ánh sáng phản quang chói lóa không rõ màu | Escalation: Gán `unknown` + bật `needs_review = true` |

## Metrics

| Metric | Cách tính | Vì sao phù hợp với bài toán |
|---|---|---|
| **Decision Accuracy (D)** | $\frac{\text{Số decision phi hình học đúng}}{\text{Tổng số decision}}$ | Đo lường độ hiểu đúng luật về trạng thái và làn đường |
| **Critical Defect Escape Rate** | $\frac{\text{Số lỗi Critical lọt lưới}}{\text{Tổng số đối tượng Critical}} \times 100\%$ | Thước đo an toàn sống còn đối với xe tự hành |
| **Geometry Compliance Rate (G)** | $\frac{\text{Số box đạt chuẩn Tight/Tolerance}}{\text{Tổng số box}}$ | Đảm bảo mô hình Object Detection học đúng kích thước vật thể |
| **Clarification Independence (I)** | Điểm phạt dựa trên số lần annotator phải hỏi thêm ngoài guideline | Đánh giá độ hoàn thiện và khả năng tự vận hành của guideline |

Metric high-risk tách riêng: **Critical Defect Escape Rate bắt buộc phải bằng 0%** (không dung thứ cho việc nhầm lẫn đèn đỏ xe mình).

## Quality gate

```text
PASS if:
  - Critical Defect Escape Rate == 0%
  - Decision Accuracy (D) >= 85%
  - Geometry Compliance (G) >= 80%
  - 100% các đối tượng được gán đủ thuộc tính (không còn '__undefined__')

REWORK if:
  - Xuất hiện 1 lỗi Critical HOẶC
  - Decision Accuracy nằm trong khoảng 70% - 84% HOẶC
  - Quên kết thúc track (thiếu outside) trong video

REJECT / ESCALATE if:
  - Decision Accuracy < 70% (chứng tỏ annotator chưa đọc hoặc guideline bị vỡ hoàn toàn) HOẶC
  - Xuất hiện >= 2 lỗi Critical trong cùng một batch nhỏ
```

Trade-off: Chấp nhận dung sai nhỏ về hình học (cho phép lệch vài pixel vỏ hộp) để tập trung tối đa nguồn lực vào độ chính xác tuyệt đối của `state` và `relevance` vì đây là hai yếu tố quyết định an toàn tính mạng.
