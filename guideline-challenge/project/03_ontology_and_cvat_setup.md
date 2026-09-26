# Ontology + CVAT setup

## Ontology table

| Name | Geometry | Type (class / attribute) | Allowed values | Default | Mutable? | Rationale |
|---|---|---|---|---|---|---|
| `traffic_light` | rectangle | class | — | — | — | Đối tượng hộp đèn giao thông vật lý điều khiển xe cơ giới |
| `state` | — | attribute | `__undefined__`, `red`, `yellow`, `green`, `off`, `unknown` | `__undefined__` | true | Trạng thái tín hiệu phát sáng; có thể thay đổi theo từng frame video |
| `relevance` | — | attribute | `__undefined__`, `relevant`, `not_relevant`, `unknown` | `__undefined__` | false | Đèn có điều khiển trực tiếp làn đường của xe chủ hay không; cố định theo track |
| `pictogram` | — | attribute | `__undefined__`, `circle`, `arrow_left`, `arrow_straight`, `arrow_right`, `other`, `unknown` | `__undefined__` | false | Hình dáng ký hiệu bên trong bóng đèn; cố định theo track |
| `needs_review` | — | attribute | `false` (checkbox unchecked/checked) | `false` | true | Cờ đánh dấu ca mơ hồ / escalation cần reviewer cấp cao kiểm tra lại |

## Class hay attribute

- **`traffic_light` là Class duy nhất:** Vì tất cả các đối tượng đều có cùng bản chất vật lý (hộp đèn giao thông) và cùng quy chuẩn vẽ Bounding Box.
- **`state`, `relevance`, `pictogram` là Attributes:** 
  - Nếu tách thành từng class riêng (ví dụ `traffic_light_red_arrow_left_relevant`), taxonomy sẽ bùng nổ lên tới hàng chục tổ hợp class, gây quá tải cho annotator khi chọn trong giao diện CVAT và dễ nhầm lẫn.
  - Tách thành attribute giúp annotator gán nhãn mạch lạc từng chiều thông tin.
- **Giá trị Default `__undefined__`:** Bắt buộc để `__undefined__` làm giá trị mặc định cho tất cả các trường select để ngăn ngừa hiện tượng **confirmation bias** (annotator vẽ xong quên không chọn mà hệ thống tự động gán giá trị đầu tiên).

## CVAT

- **Phiên bản CVAT** (`make cvat-status`): CVAT 2.75.1 tại http://localhost:8080
- **Tên task calibration**: `traffic-light-calib-v1`
- **Guide của task đã dán `02_guideline.md`?**: Có (đã dán vào tab Guide của task trên CVAT)
- **Nhóm dùng Track hay Shape, vì sao:** Dùng **Shape** đối với tập ảnh tĩnh (BDD100K) và dùng **Track** đối với chuỗi frame liên tiếp (LISA clip) để tận dụng cơ chế nội suy bounding box tự động và bảo toàn danh tính đối tượng qua thời gian.

## Setup test

Một thành viên chưa tham gia setup mở task và trả lời: label gì, dùng tool nào, gán attribute nào, khi nào escalate. Ghi lại ai test và chỗ họ vấp:

- **Người thực hiện test:** Đinh Minh Hoàng
- **Kết quả kiểm tra:** 
  - Nhận diện đúng công cụ vẽ: Rectangle (phím N).
  - Thuộc tính hiển thị trực quan: 3 dropdown menu và 1 checkbox.
  - Điểm vấp được phát hiện: Khi mới vẽ xong box, các trường đang là `__undefined__`, annotator cần chuyển sang chế độ *Attribute Annotation Mode* hoặc chọn trên sidebar bên phải để gán đủ 3 thuộc tính.
