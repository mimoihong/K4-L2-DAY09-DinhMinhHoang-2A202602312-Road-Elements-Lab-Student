# Edge-case library

Tối thiểu 8 card đa dạng phục vụ đào tạo và đánh giá annotator:

---

CASE ID: EC-01
Sample: BDD07
Scene: Giao lộ đường cao tốc ban ngày
Observation: Cụm đèn có mũi tên rẽ trái màu đỏ đang sáng rõ, trong khi xe chủ đang chạy ở làn thuần đi thẳng
Decision: LABEL
Expected: label=traffic_light, state=red, pictogram=arrow_left, relevance=not_relevant
Rationale: Tránh lỗi Phantom Braking - xe tự hành đi thẳng không được phanh theo tín hiệu đèn rẽ của làn phụ
Common mistake: Gán relevance=relevant chỉ vì thấy đèn màu đỏ ở ngay phía trước tầm mắt
Diversity: critical / conflict

---

CASE ID: EC-02
Sample: BDD18
Scene: Đường phố ban đêm ánh sáng yếu
Observation: 2 đầu đèn sáng xanh, nhìn thấy lờ mờ hình dáng viền vỏ hộp đèn 3 bóng trong bóng tối
Decision: LABEL
Expected: geometry: box bao đủ toàn bộ chiều cao của hộp đèn 3 bóng, state=green, relevance=relevant
Rationale: Hướng dẫn mô hình học kích thước thật của vật thể (full bounding box) khi vẫn còn dấu vết thị giác
Common mistake: Chỉ vẽ một box nhỏ xíu quanh đốm sáng xanh mà bỏ qua phần vỏ hộp nhìn thấy
Diversity: night / geometry

---

CASE ID: EC-03
Sample: BDD26
Scene: Ban đêm đường tối hoàn toàn
Observation: Đèn đỏ ở khoảng cách xa phát sáng, bóng tối bao trùm hoàn toàn, không có bất kỳ dấu vết viền vỏ hộp đèn nào
Decision: LABEL
Expected: geometry: box ôm sát quầng sáng đỏ phát ra, không ước lượng thêm vỏ hộp, state=red
Rationale: Ngăn chặn annotator tự bịa kích thước vật thể khi không có bằng chứng (chống hallucination)
Common mistake: Tự vẽ một box dài ước lượng theo tỷ lệ 3:1 trong khoảng không gian tối đen
Diversity: night / critical

---

CASE ID: EC-04
Sample: BDD10
Scene: Giao lộ ngã tư thành phố ban ngày
Observation: Cột đèn giao thông trên vỉa hè có 1 hộp đèn 3 bóng cho xe cơ giới và 1 hộp đèn 2 bóng hình người đi bộ
Decision: LABEL cụm đèn xe cơ giới, IGNORE đèn người đi bộ
Expected: label=traffic_light chỉ gán cho cụm đèn xe, không tạo box cho đèn người đi bộ
Rationale: Tránh làm nhiễu mô hình điều khiển xe bằng các tín hiệu dành cho người đi bộ ở vỉa hè
Common mistake: Vẽ luôn cả hộp đèn đi bộ và gán pictogram=other
Diversity: ambiguity / exclusion

---

CASE ID: EC-05
Sample: BDD12
Scene: Đường phố ban ngày, hàng cây ven đường
Observation: Đèn giao thông bị cành cây rậm rạp che mất 85% diện tích hộp đèn, chỉ thấy một chấm xanh le lói
Decision: IGNORE
Expected: Không vẽ bounding box cho đèn này
Rationale: Quy tắc loại trừ khi bị che khuất quá mức (> 80%) vì không đủ thông tin hình học cho mô hình học tập
Common mistake: Cố gắng vẽ một box nhỏ xíu hoặc vẽ xuyên qua cành cây
Diversity: occlusion / edge

---

CASE ID: EC-06
Sample: BDD17
Scene: Đường phố trời mưa, kính chắn gió bị ướt
Observation: Ánh đèn phản xạ chói lóa trên mặt đường ướt và kính xe, không chắc chắn giữa đèn vàng hay đỏ
Decision: ESCALATE
Expected: state=unknown, needs_review=true
Rationale: Khi thiếu bằng chứng thị giác do thời tiết xấu, phải đưa vào luồng kiểm tra của chuyên gia
Common mistake: Đoán đại một màu để tránh gán unknown
Diversity: low_visibility / escalation

---

CASE ID: EC-07
Sample: BDD22
Scene: Đường cao tốc lúc chạng vạng
Observation: Đèn giao thông trên giá long môn bị ánh sáng mặt trời chiếu trực diện gây lóa phản quang, cả 3 mắt kính đều phát sáng nhẹ
Decision: ESCALATE
Expected: state=unknown, relevance=relevant, needs_review=true
Rationale: Hiện tượng chóa nắng (sun glare) làm giả tín hiệu đèn, không thể kết luận an toàn
Common mistake: Nhầm lẫn với trạng thái off hoặc đoán bóng xanh sáng
Diversity: ambiguity / escalation

---

CASE ID: EC-08
Sample: BDD13
Scene: Đường phố góc nhìn xa
Observation: Cụm đèn ở ngã tư tiếp theo cách xe > 150m, chiều cao chỉ khoảng 5 pixels trên ảnh
Decision: IGNORE
Expected: Không tạo bounding box
Rationale: Ngưỡng kích thước tối thiểu (≥ 8 pixels) để đảm bảo chất lượng nhãn cho bài toán phát hiện vật thể
Common mistake: Vẽ những chấm điểm ảnh cực nhỏ gây bất đồng cao giữa các annotator
Diversity: small_far / edge
