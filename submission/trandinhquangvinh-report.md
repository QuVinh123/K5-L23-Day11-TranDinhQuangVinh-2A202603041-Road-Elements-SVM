# Báo cáo cá nhân — Ngày 11

Họ tên: Trần Đình Quang Vinh    Mã học viên: 2A202603041  
Phiên bản CVAT (Help → About): Không rõ phiên bản (không lưu lại thông tin)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 (giờ chính xác chưa lưu)    Số lần nộp lại sau Rework: 1

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đã sử dụng | `lane` / `road_curb`: polyline; `crosswalk` / `drivable`: polygon; `traffic_light` / `traffic_sign`: rectangle |
| Thuộc tính và giá trị | Đã cấu hình và chỉnh sửa | `lane`: `position`, `style`, `color`, `kind`; `drivable`: `area_type`; `traffic_light` và `traffic_sign`: thuộc tính theo taxonomy |
| 4 tag ảnh | Có | `camera`, `timeofday`, `weather`, `source`; manifest ghi nhận tất cả ảnh có tag |
Cách kết thúc polyline trên bản CVAT này: Đã tạo và chỉnh sửa polyline trực tiếp trên giao diện CVAT. Phím tắt/cách kết thúc chính xác theo phiên bản chưa được lưu lại nên không ghi phỏng đoán.  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ Tag ở thanh bên trái → chọn label tag → nhấn dấu `+` → chọn giá trị thuộc tính trong phần Details → Save.

## 2. Số lượng đã gán
Thống kê dưới đây được tổng hợp từ kết quả lint theo từng ảnh mà người nộp đã cung cấp. `front` và `fisheye` là các lô chính; `extra` là các ảnh bonus đã gộp vào ZIP cuối.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 31 | 7 | 6 | 28 | 31 | 42 |
| front-extra (đã làm 4 / 4) | 4 | 12 | 0 | 1 | 8 | 7 | 10 |
| fisheye | 8 | 9 | 5 | 11 | 0 | 6 | 10 |
| fisheye-extra (đã làm 4 / 4) | 4 | 2 | 1 | 4 | 0 | 0 | 1 |

Tổng cộng: 28 ảnh (16 Front + 12 Fisheye). Số liệu là số shape theo thống kê lint, không bao gồm image-level tags.

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05, A06, A07, A09 | `lane.position` | Thiếu L1/R1 theo cảnh báo lint hay thực sự không có vạch tương ứng | PASS sau khi kiểm tra | Người nộp xác nhận đã đối chiếu ảnh/GT; không tự thêm lane nếu không có vạch phù hợp |
| B02–B05 | `traffic_light` / `traffic_sign.edge_zone` | Bật hay tắt `edge_zone` | Đã chỉnh theo từng đối tượng | Đối chiếu vị trí box/tâm box với vùng ngoại vi fisheye; lint chỉ là gợi ý |
| B06 | `lane.position` / polyline | Lane của camera bên và đường cong | `position = other`; PASS theo xác nhận | Đối chiếu quy tắc camera hai bên và kiểm tra polyline bám vạch đường |
| B07 | `lane.position` / polyline | Polyline 4 điểm có mô tả đủ đường cong hay không | PASS theo xác nhận | Người nộp xác nhận đã kiểm tra lại hình học đường cong |
| B07 | Tag `camera` | `fisheye_left` hay `fisheye_right` | Đã chỉnh theo camera phải / MVR | Đối chiếu tên ảnh và hướng camera |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Phùng Danh Khoa (theo thông tin người nộp cung cấp).  Quyết định nhận được: PASS theo xác nhận của người nộp.

| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-02 | 0 lỗi còn lại theo xác nhận PASS | Có | Đã kiểm tra; không còn lỗi cần sửa |
| QC1-11 | 0 lỗi còn lại theo xác nhận PASS | Có | Đã kiểm tra; không còn lỗi cần sửa |
| QC1-12 | Chưa có số liệu chi tiết trên phiếu trong hồ sơ hiện tại | Chưa đối chiếu được | Cần lưu bằng chứng kiểm tra tại máy nhận |

Ghi chú: Người nộp xác nhận đã nhận phiếu QC chéo và các nội dung nêu trên đều đạt. Cần lưu bản phiếu QC có ngày review/xác nhận của Phùng Danh Khoa trong `submission/qc/` để làm bằng chứng chính thức.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `trandinhquangvinh_front.zip` | Đã kiểm tra ZIP và XML sau khi gộp | Chưa ghi nhận / chưa đối chiếu riêng | Chưa ghi nhận / chưa đối chiếu riêng | Có theo manifest: 16/16 ảnh có tag |
| `trandinhquangvinh_fisheye.zip` | Đã kiểm tra ZIP và XML sau khi gộp | Chưa ghi nhận / chưa đối chiếu riêng | Chưa ghi nhận / chưa đối chiếu riêng | Có theo manifest: 12/12 ảnh có tag |

Manifest: `manifests/trandinhquangvinh-manifest.json` — revision 1. Hai ZIP cuối gồm 16 ảnh Front và 12 ảnh Fisheye. SHA256 trong manifest được tính trên hai ZIP đã gộp bonus; cần chạy lại `Get-FileHash` ngay trong thư mục repo sau khi copy file để xác nhận bản trên máy/repo đúng với manifest.

Lệnh kiểm tra:

```powershell
Get-FileHash .\trandinhquangvinh_front.zip -Algorithm SHA256
Get-FileHash .\trandinhquangvinh_fisheye.zip -Algorithm SHA256
Get-Content .\manifests\trandinhquangvinh-manifest.json
```

## 6. Ảnh chụp màn hình
1. Tab Labels của project — cần đính kèm ảnh chụp.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển) — cần đính kèm ảnh chụp.
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong — cần đính kèm ảnh chụp.
4. Một đoạn XML có `<polyline label="lane">` — cần trích xuất và đính kèm.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Các nhóm cần chú ý nhiều là QC1-02 (cảnh báo thiếu L1/R1), QC1-03 (`position` của lane theo camera), QC1-04/QC1-05 (chiều vẽ và cách tách polyline), QC1-11 (`edge_zone` và hình học polyline fisheye). Để tránh lặp lại: kiểm tra thuộc tính ngay sau khi tạo shape; đối chiếu ảnh gốc và guideline trước khi sửa theo lint; kiểm tra đủ 4 tag ảnh; chạy lint trên đúng ZIP cuối sau mỗi lần export/chỉnh sửa.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Annotation được dùng làm ground truth để huấn luyện/đánh giá model perception. Ví dụ, nếu `lane.position` bị gán sai, model có thể học sai quan hệ giữa vạch làn và hướng camera, dẫn đến dự đoán vị trí làn thiếu nhất quán. Nếu vùng `drivable` lấn lên vỉa hè, model segmentation có thể học sai ranh giới vùng mặt đường có thể di chuyển.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi |  |  |  |  |  |
| x của bạn kia |  |  |  |  |  |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?  
   Chưa có tọa độ polyline cụ thể để xác định hàng bị ảnh hưởng.
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?  
   Chưa có tọa độ của hai người trên cùng ảnh nên chưa thể tính độ lệch.
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?  
   Chưa có tên script/bằng chứng triển khai cụ thể trong hồ sơ để kết luận theo bài lab; cần bổ sung theo nội dung giảng viên hướng dẫn.
