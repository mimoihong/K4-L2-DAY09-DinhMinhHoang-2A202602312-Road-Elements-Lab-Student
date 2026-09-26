# So sánh drivable

> Các số dưới đây là số của công cụ so sánh, không phải ngưỡng chấm.

Polygon BDD100K đổi từ toạ độ normalized sang pixel 1280×720. BDD không có tag needs_review.

Trùng từng đỉnh với reference: 0/9 shape (<= 0,5 px).

## bb5cc516-c98d1fbe.jpg

- direct: IoU 0.392; chỉ reference 253 px; chỉ bạn 63259 px
- direct: vùng hình học khác reference (253 px thiếu, 63259 px thừa) — gợi ý `geometry`
- alternative: IoU 0.000; chỉ reference 48786 px; chỉ bạn 0 px
- alternative: vùng hình học khác reference (48786 px thiếu, 0 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.854; chỉ reference 535 px; chỉ bạn 14755 px
- mọi vùng: vùng hình học khác reference (535 px thiếu, 14755 px thừa) — gợi ý `geometry`

## be860305-899a96c3.jpg

- direct: IoU 0.590; chỉ reference 26435 px; chỉ bạn 129 px
- direct: vùng hình học khác reference (26435 px thiếu, 129 px thừa) — gợi ý `geometry`
- alternative: IoU 0.714; chỉ reference 8129 px; chỉ bạn 4385 px
- alternative: vùng hình học khác reference (8129 px thiếu, 4385 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.640; chỉ reference 34564 px; chỉ bạn 4514 px
- mọi vùng: vùng hình học khác reference (34564 px thiếu, 4514 px thừa) — gợi ý `geometry`

## c068a67b-03b6e200.jpg

- direct: IoU 0.962; chỉ reference 770 px; chỉ bạn 3445 px
- direct: vùng hình học khác reference (770 px thiếu, 3445 px thừa) — gợi ý `geometry`
- alternative: IoU 0.418; chỉ reference 707 px; chỉ bạn 80810 px
- alternative: vùng hình học khác reference (707 px thiếu, 80810 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.657; chỉ reference 1477 px; chỉ bạn 84255 px
- mọi vùng: vùng hình học khác reference (1477 px thiếu, 84255 px thừa) — gợi ý `geometry`

## c3cd6c82-b5d52beb.jpg

- direct: IoU 0.555; chỉ reference 4734 px; chỉ bạn 58558 px
- direct: vùng hình học khác reference (4734 px thiếu, 58558 px thừa) — gợi ý `geometry`
- alternative: IoU 0.000; chỉ reference 48138 px; chỉ bạn 0 px
- alternative: vùng hình học khác reference (48138 px thiếu, 0 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.891; chỉ reference 4909 px; chỉ bạn 10595 px
- mọi vùng: vùng hình học khác reference (4909 px thiếu, 10595 px thừa) — gợi ý `geometry`

## c723ad21-efed33e5.jpg

- direct: IoU 0.909; chỉ reference 6026 px; chỉ bạn 7059 px
- direct: vùng hình học khác reference (6026 px thiếu, 7059 px thừa) — gợi ý `geometry`
- alternative: IoU 0.848; chỉ reference 2647 px; chỉ bạn 1567 px
- alternative: vùng hình học khác reference (2647 px thiếu, 1567 px thừa) — gợi ý `geometry`
- mọi vùng: IoU 0.899; chỉ reference 8673 px; chỉ bạn 8626 px
- mọi vùng: vùng hình học khác reference (8673 px thiếu, 8626 px thừa) — gợi ý `geometry`

## Dòng gợi ý cho comparison_log.csv

```csv
task,sample,object,difference,error_type,who_is_right,action,note
drivable,bb5cc516-c98d1fbe.jpg,direct,"direct: vùng hình học khác reference (253 px thiếu, 63259 px thừa)",geometry,,,
drivable,bb5cc516-c98d1fbe.jpg,alternative,"alternative: vùng hình học khác reference (48786 px thiếu, 0 px thừa)",geometry,,,
drivable,bb5cc516-c98d1fbe.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (535 px thiếu, 14755 px thừa)",geometry,,,
drivable,be860305-899a96c3.jpg,direct,"direct: vùng hình học khác reference (26435 px thiếu, 129 px thừa)",geometry,,,
drivable,be860305-899a96c3.jpg,alternative,"alternative: vùng hình học khác reference (8129 px thiếu, 4385 px thừa)",geometry,,,
drivable,be860305-899a96c3.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (34564 px thiếu, 4514 px thừa)",geometry,,,
drivable,c068a67b-03b6e200.jpg,direct,"direct: vùng hình học khác reference (770 px thiếu, 3445 px thừa)",geometry,,,
drivable,c068a67b-03b6e200.jpg,alternative,"alternative: vùng hình học khác reference (707 px thiếu, 80810 px thừa)",geometry,,,
drivable,c068a67b-03b6e200.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (1477 px thiếu, 84255 px thừa)",geometry,,,
drivable,c3cd6c82-b5d52beb.jpg,direct,"direct: vùng hình học khác reference (4734 px thiếu, 58558 px thừa)",geometry,,,
drivable,c3cd6c82-b5d52beb.jpg,alternative,"alternative: vùng hình học khác reference (48138 px thiếu, 0 px thừa)",geometry,,,
drivable,c3cd6c82-b5d52beb.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (4909 px thiếu, 10595 px thừa)",geometry,,,
drivable,c723ad21-efed33e5.jpg,direct,"direct: vùng hình học khác reference (6026 px thiếu, 7059 px thừa)",geometry,,,
drivable,c723ad21-efed33e5.jpg,alternative,"alternative: vùng hình học khác reference (2647 px thiếu, 1567 px thừa)",geometry,,,
drivable,c723ad21-efed33e5.jpg,mọi vùng,"mọi vùng: vùng hình học khác reference (8673 px thiếu, 8626 px thừa)",geometry,,,
```

Hãy điền `who_is_right`, `action`, `note`; loại lỗi chỉ là gợi ý.
