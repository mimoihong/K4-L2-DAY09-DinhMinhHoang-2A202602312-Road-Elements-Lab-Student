# Problem statement + downstream contract

## Bài toán

Nhận diện trạng thái (`state`), ký hiệu (`pictogram`) và tính liên quan tới làn xe chủ (`relevance`) của cụm đèn tín hiệu giao thông (Traffic Light) tại các nút giao thông đô thị và đường cao tốc, xử lý các thách thức đặc thù: chói lóa nắng, thiếu sáng ban đêm, nhiều đầu đèn điều khiển các làn rẽ khác nhau, và đèn ở khoảng cách xa.

## Downstream contract

1. **Downstream task / model / user là ai?**
   - Hệ thống lập kế hoạch hành vi và quỹ đạo xe tự hành (Autonomous Driving Motion Planner & Trajectory Controller).
2. **Output annotation nào thực sự cần?**
   - Geometry: 2D Bounding Box bám khít phần hộp đèn nhìn thấy (visible housing).
   - Label: `traffic_light`.
   - Attributes: `state` (red, yellow, green, off, unknown), `relevance` (relevant, not_relevant, unknown), `pictogram` (circle, arrow_left, arrow_straight, arrow_right, other, unknown), và cờ `needs_review` (boolean).
3. **Failure nào gây hậu quả lớn nhất?**
   - Critical Failure 1 (Lỗi đâm va thảm khốc): Nhận diện nhầm đèn đỏ thành đèn xanh/off hoặc gán nhầm đèn đỏ của xe mình thành `not_relevant`, khiến xe tự hành vượt đèn đỏ cắt ngang dòng phương tiện.
   - Critical Failure 2 (Lỗi phanh gấp ảo - Phantom Braking): Gán nhầm đèn đỏ của làn rẽ phụ / đường nhánh thành `relevant` cho làn đi thẳng của xe mình, khiến xe phanh gấp đột ngột trên đường thông thoáng dẫn đến nguy cơ bị xe sau đâm đuôi.
4. **Khi ambiguity không resolve được, ai / ở đâu là escalation path?**
   - Khi không đủ bằng chứng (bị che khuất > 80%, lóa sáng không phân biệt được bóng nào cấp điện, hoặc bố trí ngã tư xung đột không xác định được làn): gán `state = unknown` hoặc `relevance = unknown` và bật checkbox `needs_review = true` để đưa vào hàng đợi chuyên gia Review Level 2 xử lý.

## Scope

- **Trong scope (bắt buộc label):** Mọi cụm đèn tín hiệu giao thông cho phương tiện cơ giới đường bộ có mặt đèn hướng về phía xe chủ (nhìn thấy được bóng hoặc mặt trước của hộp đèn).
- **Ngoài scope (ignore):**
  - Đèn quay lưng hoặc quay ngang vuông góc (không điều khiển chiều xe đang di chuyển).
  - Đèn tín hiệu dành riêng cho người đi bộ (nằm ngang tầm mắt ở vỉa hè, chỉ có 2 bóng hình người).
  - Đèn quá nhỏ/xa (chiều cao hộp đèn < 8 pixels) hoặc đốm sáng mờ không còn nhận ra cấu trúc cụm đèn.
- **Geometry tolerance:** Bounding box bao trọn phần vỏ hộp đèn nhìn thấy (bao gồm visor che nắng nếu thấy rõ), lệch ≤ 2 px mỗi cạnh so với mép thực tế. Không lấy cột đèn hay dây cáp.

## Output chấm được

Mọi quyết định phải nhìn thấy được trực tiếp trong file export XML/JSON của CVAT:
- `LABEL`: Tạo box `traffic_light` với đầy đủ các thuộc tính.
- `IGNORE`: Không tạo box (được kiểm chứng qua âm tính / negative test trong gold).
- `UNKNOWN`: Giá trị `unknown` ở các trường `state`, `relevance`, `pictogram`.
- `ESCALATE`: Checkbox `needs_review = true` được đánh dấu trong export.

## Dữ liệu và giới hạn

- Nguồn ảnh: Dữ liệu ảnh thực tế từ `gtsdb` và chuỗi video `lisa` trong thư mục data/.
- Giới hạn: Dữ liệu ảnh 2D từ camera đơn phía trước (Front Camera POV), không có thông tin bản đồ HD Map kèm theo nên việc suy luận `relevance` phải dựa 100% vào ngữ cảnh thị giác (vạch kẻ đường, biển báo làn, hướng di chuyển của các xe xung quanh).
