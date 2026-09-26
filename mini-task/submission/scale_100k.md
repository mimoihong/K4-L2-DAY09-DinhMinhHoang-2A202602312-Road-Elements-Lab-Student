# Nếu scale lên 100k frames

Họ tên: Đinh Minh Hoàng

Mỗi mini-task trả lời một câu: "Nếu scale lên 100k frames, lỗi nào sẽ trở thành systematic defect?"

## Lane

- Lỗi: Dừng polyline không nhất quán tại các đoạn vạch sơn bị mờ hoặc cát bụi phủ (b75f355e).
- Vì sao lặp lại: Annotator có xu hướng tự phỏng đoán nối tiếp vạch theo quán tính nếu không có quy định cứng về ngưỡng độ tương phản.
- Cách phát hiện sớm: Oversample các khung hình có độ chiếu sáng thấp, mưa, chói lóa; thiết lập rule kiểm tra độ dài đứt quãng và mức độ suy giảm pixel.

## Drivable area

- Lỗi: Nhầm lẫn ranh giới alternative area giữa làn cùng chiều và làn ngược chiều có vạch kẻ liền (bb5cc516).
- Vì sao lặp lại: Thiếu rule ngữ nghĩa về luật giao thông khiến annotator chỉ nhìn vào mặt đường nhựa mà coi mọi làn đường đều là xe chạy được.
- Cách phát hiện sớm: Kiểm tra chéo lớp drivable area với lớp lane marking; phát hiện polygon alternative lấn qua vạch liền vàng/trắng.

## Traffic sign

- Lỗi: Nhầm lẫn giữa các biến thể của biển cấm tốc độ hoặc biển phụ không đọc được (00026.png).
- Vì sao lặp lại: Biển ở xa có kích thước nhỏ dưới 20px khiến mắt người dễ nhầm giữa các con số (ví dụ 30 vs 80).
- Cách phát hiện sớm: Thiết lập rule bắt buộc gán `readable = false` khi kích thước biển nhỏ hơn ngưỡng 16px; oversample các biển báo ở cự ly xa.

## Traffic light

- Lỗi: Lệch frame chuyển đổi trạng thái tín hiệu (frame 14 vs 15 trong dayClip5).
- Vì sao lặp lại: Hiện tượng rolling shutter của camera hoặc tần số quét LED khiến đèn có 1–2 frame chuyển giao vừa sáng vừa tối.
- Cách phát hiện sớm: Kiểm tra tính liên tục theo thời gian (temporal consistency check); gắn cờ cảnh báo nếu state thay đổi đột ngột không theo chu kỳ chuẩn (xanh -> vàng -> đỏ).
