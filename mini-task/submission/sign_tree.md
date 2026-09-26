# Traffic sign tree

Họ tên: Đinh Minh Hoàng · Chế độ: cá nhân

Viết sau mini-task traffic sign (phút ~155). Dựa vào những biển bạn đã vẽ trong 7 ảnh core, không chép danh sách 43 class.

## 1. Cây của bạn

Chỉ liệt kê class có trong ảnh core. Đếm số box của từng class. Class có 1 box trong cả batch là ứng viên "hiếm".

| family | class (`sign_class`) | Số box trong core | Phổ biến / hiếm | Ảnh ví dụ |
|---|---|---|---|---|
| prohibitory | 01 speed limit 30 | 3 | Phổ biến | 00026.png |
| mandatory | 38 keep right | 2 | Phổ biến | 00054.png |
| danger | 27 pedestrian crossing | 2 | Phổ biến | 00054.png |
| other | 12 priority road | 2 | Phổ biến | 00054.png |

## 2. Hai quyết định merge/split

**Quyết định 1 — `09 no overtaking` và `10 no overtaking (trucks)`: tách hay gộp?**
Tách hai class riêng biệt. Rationale: Đối với xe tự hành cá nhân (passenger car), biển cấm xe tải vượt không có hiệu lực cấm xe mình vượt. Nếu gộp chung, xe tự hành sẽ bị lỗi phantom deceleration (không dám vượt xe chậm dù luật cho phép).

**Quyết định 2 — nhóm `other` của GTSDB khi dùng ở Việt Nam.**
Theo cách tiếp cận của QCVN 41:2024/BGTVT, xếp biển hết mọi lệnh cấm vào nhóm biển báo cấm để giữ tính nhất quán về hình thức chế tài. Rule để hai người label giống nhau: Mọi biển có viền tròn màu trắng hoặc gạch chéo xám hủy bỏ hạn chế đều được đưa vào taxonomy cấm (prohibitory) với attribute `sub_type = cancellation`.

## 3. Chính sách cho class hiếm và biển không đọc được

Khi gặp biển không có trong 43 class hoặc quá nhỏ/mờ để đọc:
Gán `sign_family = other`, `sign_class = other`, và đặt thuộc tính `readable = false`.
Bằng chứng: Biển phụ hình chữ nhật nhỏ dưới biển chính trong ảnh 00054.png, kích thước quá bé để đọc rõ nội dung chữ viết.

## 4. Dòng decision log tương ứng

Id của dòng trong `decision_log.csv` ghi rule ở mục 2 hoặc 3: 4
