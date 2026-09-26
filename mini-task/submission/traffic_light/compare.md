# So sánh traffic_light

> Các số dưới đây là số của công cụ so sánh, không phải ngưỡng chấm.

Track LISA dayClip5, 30 frame. LISA không gán nhãn đèn nhỏ ở ngã tư phía xa và không có relevance — box không khớp GT chưa chắc là thừa.

Trùng từng đỉnh với reference: 0/150 shape (<= 0,5 px).

## dayClip5--01606.jpg

- R#2/B#0: cả reference và bạn đều không đổi state
- B#0: relevance=relevant (không so với GT)
- R#0/B#1: frame đổi state reference 15; bạn 15
- B#1: relevance=relevant (không so với GT)
- R#1/B#2: frame đổi state reference 15; bạn 15
- B#2: relevance=relevant (không so với GT)
- B#3: không có trong reference (LISA không gán đèn xa) — ghi relevance và lý do vào light_log.md — gợi ý `guideline_gap`
- B#3: relevance=not_relevant (không so với GT)
- B#4: không có trong reference (LISA không gán đèn xa) — ghi relevance và lý do vào light_log.md — gợi ý `guideline_gap`
- B#4: relevance=not_relevant (không so với GT)

## Dòng gợi ý cho comparison_log.csv

```csv
task,sample,object,difference,error_type,who_is_right,action,note
traffic_light,dayClip5--01606.jpg,B#3,B#3: không có trong reference (LISA không gán đèn xa) — ghi relevance và lý do vào light_log.md,guideline_gap,,,
traffic_light,dayClip5--01606.jpg,B#4,B#4: không có trong reference (LISA không gán đèn xa) — ghi relevance và lý do vào light_log.md,guideline_gap,,,
```

Hãy điền `who_is_right`, `action`, `note`; loại lỗi chỉ là gợi ý.
