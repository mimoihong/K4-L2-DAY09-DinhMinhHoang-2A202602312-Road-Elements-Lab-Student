# QC report

Họ tên: Đinh Minh Hoàng · Chế độ: cá nhân
Guideline dùng: `GUIDE.md` + 4 card, bản phát ngày học.

Viết ở phút 205–225.

## 1. Sample plan

Không đủ thời gian xem hết. Chọn 6 sample theo lát dễ lỗi (ngã tư, crosswalk, đêm/mưa, lóa, biển nhỏ, điểm chuyển state).

| # | Task | Sample (ảnh / frame) | Lát (vì sao chọn) |
|---|---|---|---|
| 1 | lane | bb890202 | Cao tốc nhiều làn, vạch đứt chia làn |
| 2 | lane | c1589305 | Ngã tư phức tạp có vạch qua đường và vạch dừng |
| 3 | drivable | bb5cc516 | Đường phố trời mưa ướt, có phân chia làn ngược chiều |
| 4 | drivable | c068a67b | Ngã tư rộng có nhiều góc cua và vỉa hè |
| 5 | traffic_sign | 00054.png | Cột biển báo hỗn hợp gồm nhiều loại biển báo khác nhau |
| 6 | traffic_light | dayClip5--01606.jpg | Chuỗi frame có chuyển đổi trạng thái tín hiệu tại ngã tư |

## 2. Lỗi tìm thấy

| Task | Sample | Object | Mô tả lỗi | error_type | severity | action | Downstream sai gì nếu bỏ qua |
|---|---|---|---|---|---|---|---|
| lane | bb890202 | Vạch đứt | Chưa gán đủ thuộc tính laneStyle dashed | attribute | major | rework | Model không phân biệt được vạch được phép chuyển làn |
| drivable | bb5cc516 | Mặt đường | Vẽ lấn vào ranh giới làn ngược chiều | geometry | critical | rework | Xe tự hành có nguy cơ đi lấn làn đối đầu |
| traffic_sign | 00054.png | Biển phụ | Biển phụ quá mờ không đọc được nhưng chưa đặt readable=false | attribute | minor | accept | Không ảnh hưởng nghiêm trọng đến an toàn di chuyển |

## 3. Kết luận cho batch

- Accept / rework / escalate cả batch, và lý do: Rework các lỗi critical về drivable area và hoàn thiện các attribute còn thiếu ở lane marking.
- Note cho người label: Luôn kiểm tra kỹ vạch kẻ liền chia tim đường trước khi khoanh vùng drivable area để tránh lấn làn ngược chiều.
- Known limitation phải ghi khi handoff: Đối với các vạch sơn bị bào mòn quá 50% diện tích, cần có cơ chế escalation rõ ràng hơn giữa dừng polyline hay nối tiếp theo quán tính.
