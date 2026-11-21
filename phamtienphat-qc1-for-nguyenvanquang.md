# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Văn Quang        Người kiểm (học viên): Phạm Tiến Phát (03063)  
Ngày: 21/11/2026                     Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `front.zip`, `front-extra.zip`, `fisheye.zip`, `fisheye-extra.zip` (CVAT for images 1.1, export 21/11/2026); không nhận được manifest nên không có `revision`  
Số ảnh kiểm: 6 (+ 4 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 85 (61 shape + 24 tag)  

Ảnh trong mẫu: A01, A04, A07 (front) và B01, B05, B06 (fisheye). Chọn theo các điểm coach kiểm: ảnh đầu tiên, vàng đôi + direct/alternative, đèn/biển, ảnh fisheye đầu tiên, camera hai bên.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 2 | nặng (1) / nhẹ (1) |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 15 | 2 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 15 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 15 | 3 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 15 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 23 | 3 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 23 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 15 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 18 | 4 | chính |
| QC1-12 file | lỗi file | 4 | 0 | nhẹ / nặng |

Số mục kiểm: QC1-01 = số tag; QC1-02 = L1 + R1 cần có ở 3 ảnh front; QC1-03 đến QC1-06 = số polyline `lane`; QC1-07 = `drivable` + `crosswalk` + `road_curb`; QC1-08 = đèn; QC1-09 = đèn + biển; QC1-10 = biển; QC1-11 = shape trên 3 ảnh fisheye; QC1-12 = số file.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-01 | B01 | tag camera | nặng | Ghi `fisheye_rear`; ảnh `02688_FV` là camera trước (thấy capo phía trước xe) → `fisheye_front` |
| 2 | QC1-03 | B06 | lane #2 @(612,39) | nặng | Camera trái (MVL) nhưng `position = L1`; camera hai bên luôn `other` |
| 3 | QC1-03 | B06 | lane #3 @(162,261) | nặng | Như trên: `position = L1` trên MVL → `other` |
| 4 | QC1-05 | A01 | lane #3 + #6 (L2) | chính | Vạch trắng mép trái vẽ thành 2 polyline cùng `L2`; một vạch (kể cả vạch đôi) chỉ là một polyline |
| 5 | QC1-05 | A04 | lane #7 + #15 (L1) | chính | Vàng đôi vẽ mỗi vệt một polyline; phải là 1 polyline `kind = double` đặt giữa hai vệt |
| 6 | QC1-05 | A04 | lane #11 + #13 (R2) | chính | Vạch trắng đôi bên phải cũng tách thành 2 polyline cùng `R2` |
| 7 | QC1-07 | A01 | drivable #2 | chính | Làn ngoài cùng bên trái (giữa L2 và L1) gán `direct`; xe đang ở làn giữa nên làn này là `alternative` (ảnh có 2 polygon `direct`) |
| 8 | QC1-07 | A04 | drivable #10 (alternative) | chính | Phủ dải giữa R2 và vỉa hè (làn xe đạp có vạch đôi ngăn), ô tô không chạy vào: tràn vùng |
| 9 | QC1-07 | B05 | crosswalk (bỏ sót) | chính | Vạch ngựa vằn lớn ngay cạnh xe (trọng tâm của B05) không có polygon `crosswalk`; chỉ có 2 polygon nhỏ ở mép ảnh |
| 10 | QC1-11 | B05 | traffic_sign #4 | chính | Tâm hộp cách tâm ảnh ≈ 518 px > 512 px (80 % bán kính) nhưng `edge_zone = false` |
| 11 | QC1-11 | B05 | traffic_sign #5 | chính | Như trên, ≈ 532 px, chưa bật `edge_zone` |
| 12 | QC1-11 | B05 | traffic_sign #6 | chính | Như trên, ≈ 522 px, chưa bật `edge_zone` |
| 13 | QC1-11 | B06 | lane #3 @(162,261) | chính | Polyline fisheye chỉ có 3 điểm, không theo cung |
| 14 | QC1-01 | A07 | tag weather | nhẹ | Ghi `overcast`; mặt đường ướt rõ, kính có giọt mưa → `rain` |

Ảnh A07: ngoài tag weather, phần làn, vùng lái, đèn, biển không thấy lỗi. A07 không có L1 vì bên trái là dải bê tông, không có vạch sơn: không tính QC1-02.

## Ngoài mẫu 6 ảnh (ghi riêng, không tính vào tỉ lệ)
Chạy `road_check lint` trên cả 4 file thấy thêm, nên sửa luôn:
- B02, B09: tag camera sai (B02 `fisheye_rear`, B09 `front`; tên file FV → `fisheye_front`).
- B03, B04: thiếu cả 4 tag (camera, timeofday, weather, source).
- B08: lane #6 trên camera phải (MVR) có `position` khác `other`.
- Nhiều polyline vẽ từ xa về gần (điểm đầu ở trên): A02, A06, A09–A16. Guideline yêu cầu vẽ từ gần xe ra xa.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A04 | Có gán `road_curb` cho vỉa hè phía làn ngược chiều không (lô có 4 đoạn, 2 đoạn chỉ 2 điểm)? Coach dặn chỉ gán đường xe đi | |

Ca này không đổi kết luận: lô đã Rework vì lỗi nặng.

## Quyết định
Lỗi nặng: 3   Lỗi chính: 10 / 85 nhãn = 11,8 %   Lỗi nhẹ: 1   Ca chờ lead: 1  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có 3 lỗi nặng (tag camera sai ở B01; `position` sai trên camera hai bên ở B06 ×2), một lỗi nặng là đủ Rework. Tỉ lệ lỗi chính 11,8 % cũng vượt ngưỡng 5 %. Ca mơ hồ còn lại không ảnh hưởng kết luận nên không Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
