# Peer feedback + owner response

- **Nhóm peer:** team_reviewer
- **Người label blind:** peer_annotator

## 1. Peer trả lời

1. Rule nào rõ nhất / giúp quyết định nhanh nhất? 
   - Quy tắc phân biệt rõ ràng giữa `state = off` (tối đen hoàn toàn) và `state = unknown` (lóa chói/sáng bất thường).
2. Rule nào mơ hồ hoặc phải tự suy diễn? 
   - Trường hợp ban đêm khi không gian vỏ hộp đèn không thấy rõ, cần xem kỹ ví dụ minh họa để không vẽ đoán vỏ.
3. Sample nào khiến guideline "vỡ"? 
   - Không có sample nào làm vỡ guideline, bộ quy tắc hoạt động rất nhất quán trên cả 4 ảnh blind.
4. Attribute / default nào trong CVAT dễ gây thao tác sai? 
   - Mặc định ban đầu `__undefined__` rất hữu ích giúp nhắc nhở phải chọn đủ 3 dropdown, không bị quên.
5. Một thay đổi cụ thể giúp annotator mới ít hỏi hơn? 
   - Bổ sung thêm hình ảnh screenshot trực tiếp trong CVAT của các ca ban đêm và chói lóa vào mục ví dụ.

## 2. Owner phân loại

Owner không tranh luận để bảo vệ guideline. Mỗi feedback và mỗi decision peer làm sai được xếp vào một hướng xử lý.

| Feedback / decision sai | Nguyên nhân (guideline gap / data ambiguity / execution error) | Xử lý (accept + revise / reject with evidence / add escalation rule) | Bằng chứng |
|---|---|---|---|
| Cần thêm hình ảnh trực quan cho ca ban đêm | guideline_gap | accept + revise | Bổ sung screenshot trực quan vào Mục 9 của Guideline v3 |
| Nhầm lẫn nhẹ góc chụp xe rẽ | data_ambiguity | add escalation rule | Nhắc lại quy tắc đặt góc nhìn POV của người lái xe |
| Quên tick needs_review khi gặp thời tiết xấu | execution_error | coaching | Nhắc nhở annotator tuân thủ checklist Self-QC trước khi export |
