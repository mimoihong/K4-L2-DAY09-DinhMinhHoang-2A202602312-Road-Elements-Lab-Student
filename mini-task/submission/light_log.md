# Traffic light log

Họ tên: Đinh Minh Hoàng

Viết mục 1–3 trong mini-task traffic light, trước khi chạy `make compare TASK=traffic_light`; mục 4 viết sau compare. Mỗi track là một đầu đèn bạn đã vẽ.

## 1. Các track

| Track (#id CVAT) | pictogram | state theo frame | relevance | Bằng chứng cho relevance |
|---|---|---|---|---|
| Track 0 | circle | green 0–29 | relevant | Đèn treo chính giữa làn xe đang di chuyển |
| Track 1 | circle | green 0–14, yellow 15–29 | relevant | Đèn chính làn đi thẳng đổi màu ở frame 15 |
| Track 2 | circle | green 0–14, yellow 15–29 | relevant | Đèn bên phải làn đi thẳng đổi màu ở frame 15 |

## 2. Điểm chuyển state

- Đèn đổi state ở frame nào? Frame liền trước trông ra sao (đèn tắt, hai màu cùng sáng, mờ)?
  Đèn đổi state tại frame 15 (từ green sang yellow). Frame 14 đèn xanh bắt đầu mờ nhẹ và bóng vàng bắt đầu phát sáng ở frame 15.
- Bạn đặt keyframe ở đâu, và bạn đã kiểm tra mọi frame giữa hai keyframe chưa?
  Đặt keyframe tại frame 0 (bắt đầu track) và frame 15 (chuyển trạng thái). Đã tua kiểm tra bằng phím D/F trên CVAT đảm bảo box bám khít đèn qua tất cả 30 frame.

## 3. Các đầu đèn nhỏ ở ngã tư phía xa

Bạn có vẽ không? Nếu có: `relevance` là gì, `state` đọc được ở frame nào? Nếu không: vì sao?
Có vẽ (Track 3 và Track 4). Gán `relevance = not_relevant` vì đây là các cụm đèn thuộc giao lộ tiếp theo phía xa, trạng thái mờ đọc được ở dạng yellow. Việc vẽ giúp hệ thống nhận diện từ xa.

## 4. Sau khi so với reference

- Khác biệt về state/pictogram, và ai đúng:
  Thời điểm chuyển state ở frame 15 khớp hoàn hảo giữa bài tôi và reference (cả hai đều xác định frame 15 chuyển màu).
- Track của bạn không có trong reference: giữ hay bỏ, vì sao:
  Giữ nguyên các track đèn xa vì LISA chỉ bỏ qua do quy ước hạn chế khoảng cách của dataset gốc, trong khi thực tế xe tự hành cần nhận biết đèn từ sớm để lập kế hoạch giảm tốc.
