# Phiếu QC 1 — Road v1.0

> **BẢN DỰ THẢO HỖ TRỢ QC BẰNG AI — CÁC MỤC PASS DƯỚI ĐÂY THEO XÁC NHẬN CỦA CHỦ SỞ HỮU ANNOTATION.**
> Phùng Danh Khoa vẫn cần xem lại và ký/ghi ngày review để trở thành phiếu QC chéo chính thức. Không ghi nhận các xác nhận của chủ sở hữu là hành động review do Khoa thực hiện.

Lô được kiểm (học viên): Trần Đình Quang Vinh  
Người kiểm (học viên): Phùng Danh Khoa  
Ngày review thực tế: ____________________  
Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest):
- `trandinhquangvinh-front.zip` — revision 1
- `trandinhquangvinh-fisheye.zip` — revision 1

Số ảnh trong mẫu dự kiến: 6  
Số đối tượng annotation đọc từ XML: 60 (36 shape + 24 tag).

## 1. Mẫu 6 ảnh

| # | Mã ảnh | Camera / Task | Shape | Tag | Ghi chú chọn mẫu |
| ---: | --- | --- | ---: | ---: | --- |
| 1 | A05_b2576c8c-2de20b8a.jpg | Front | 1 | 4 | Lint từng báo thiếu L1/R1 |
| 2 | A06_b8c66e31-37045eec.jpg | Front | 15 | 4 | Lint từng báo thiếu R1; có lane, drivable, crosswalk, đèn và biển |
| 3 | A07_b41ace08-c8468690.jpg | Front | 5 | 4 | Lint từng báo thiếu L1 |
| 4 | A09_c7e6d5d1-c8af9fe3.jpg | Front | 10 | 4 | Lint từng báo thiếu R1; có lane, drivable, đèn và biển |
| 5 | B06_04068_MVL.png | Fisheye-left | 3 | 4 | Kiểm tra lane `other` và crosswalk cong |
| 6 | B07_01216_MVR.png | Fisheye-right | 2 | 4 | Kiểm tra lane `other` và crosswalk cong |

**Thống kê đọc từ XML:** 36 shapes + 24 tags = 60 đối tượng annotation. Người review xác nhận cách tính “số nhãn đã kiểm” theo rubric của lớp trước khi chốt mẫu số.

## 2. Tổng hợp theo mã

> Các con số ở cột “Số mục kiểm” là số lượng dự kiến rút ra từ cấu trúc annotation để hỗ trợ review, không thay thế việc Khoa kiểm tra trực quan. Cột “Số lỗi” cần Khoa xác nhận.

| Mã | Loại lỗi | Số mục kiểm dự kiến | Số lỗi AI xác nhận được | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | Sai thuộc tính / bỏ sót | 24 tag (4 tag × 6 ảnh) | 0 thiếu tag; giá trị camera khớp tên/loại ảnh theo dữ liệu hiện có | nặng |
| QC1-02 đủ L1, R1 | Bỏ sót | 8 vị trí L1/R1 trên 4 ảnh Front | **PASS theo xác nhận của chủ sở hữu**: 5 vị trí lint báo thiếu đã được kiểm tra và chấp nhận theo GT/coach | nặng |
| QC1-03 position | Sai thuộc tính / thừa | 7 lane shapes | 0 lỗi thuộc tính xác định được từ XML; hai lane fisheye mang `other` | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | Sai phạm vi / bỏ sót | 7 lane shapes | Chưa kết luận chỉ từ XML; cần reviewer đối chiếu tâm vạch và chiều vẽ | chính |
| QC1-05 vạch đứt, che | Sai phạm vi / sai thuộc tính | Các lane trong 6 ảnh | Chưa kết luận; cần kiểm tra đoạn đứt/che trên ảnh gốc | chính |
| QC1-06 style, color, kind | Sai thuộc tính | 7 lane shapes | Chưa kết luận đầy đủ bằng đối chiếu GT | chính |
| QC1-07 vùng lái | Sai phạm vi / bỏ sót / thừa | 6 drivable shapes | Chưa kết luận; cần reviewer xác nhận ranh giới vùng lái | chính |
| QC1-08 đèn, màu | Bỏ sót / sai phạm vi / sai thuộc tính | 10 traffic_light boxes | Chưa kết luận đầy đủ màu và hướng đèn | nặng / chính |
| QC1-09 facing, type, group, biển phụ | Sai thuộc tính | 6 traffic_sign boxes | Chưa kết luận đầy đủ thuộc tính | chính |
| QC1-10 hình in, đủ biển | Bỏ sót / sai phạm vi | 6 traffic_sign boxes | Chưa kết luận độ sát box và tính đầy đủ | chính |
| QC1-11 fisheye | Sai phạm vi / sai thuộc tính | 2 ảnh fisheye; 2 lane + 3 crosswalk shapes | **PASS theo xác nhận của chủ sở hữu**: B06 lane alignment và B07 polyline 4 điểm/đường cong đã được kiểm tra | chính |
| QC1-12 file | Lỗi file | 2 ZIP + manifest | Hai ZIP mở được và có đúng ảnh trong mẫu; cần xác minh manifest/hash tại máy nhận | nhẹ / nặng |

## 3. Các điểm cần reviewer xác nhận

### QC1-02 — xác nhận các vị trí lane theo lint

| Ảnh | Vị trí lint báo thiếu | Kết quả xác nhận của chủ sở hữu | Trạng thái |
| --- | --- | --- | --- |
| A05 | L1, R1 | Đã kiểm tra theo GT/coach; chấp nhận không có vạch cần gán trong vùng liên quan | PASS |
| A06 | R1 | Đã kiểm tra theo GT/coach; chấp nhận không có vạch cần gán trong vùng liên quan | PASS |
| A07 | L1 | Đã kiểm tra theo GT/coach; chấp nhận không có vạch cần gán trong vùng liên quan | PASS |
| A09 | R1 | Đã kiểm tra theo GT/coach; chấp nhận không có vạch cần gán trong vùng liên quan | PASS |

Các cảnh báo QC1-02 vẫn được giữ trong log lint để truy vết, nhưng được đánh dấu **đã kiểm tra và PASS theo xác nhận của chủ sở hữu annotation**. Khoa cần đối chiếu lại bằng chứng/trao đổi coach nếu biểu mẫu yêu cầu người review chéo xác nhận độc lập.

### QC1-11 — fisheye

| Ảnh | Hạng mục | Kết quả xác nhận của chủ sở hữu | Trạng thái |
| --- | --- | --- | --- |
| B06 | Lane `other`, alignment với vạch đường và đường cong | Đã kiểm tra; xác nhận polyline bám đúng đối tượng theo guideline | PASS |
| B07 | Lane `other`, polyline 4 điểm và độ mô tả đường cong | Đã kiểm tra; xác nhận đủ điểm và mô tả đúng đường cong theo guideline | PASS |

Hai cảnh báo/điểm cần xem xét QC1-11 được đóng theo xác nhận của chủ sở hữu. Khoa cần ký xác nhận review chéo chính thức.

## 4. Danh sách lỗi / điểm cần quyết định

| # | Mã | Ảnh | Hạng mục | Mức | Trạng thái hiện tại |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A05 | L1, R1 bị lint báo thiếu | nặng nếu vạch nhìn thấy | **PASS theo xác nhận chủ sở hữu** |
| 2 | QC1-02 | A06 | R1 bị lint báo thiếu | nặng nếu vạch nhìn thấy | **PASS theo xác nhận chủ sở hữu** |
| 3 | QC1-02 | A07 | L1 bị lint báo thiếu | nặng nếu vạch nhìn thấy | **PASS theo xác nhận chủ sở hữu** |
| 4 | QC1-02 | A09 | R1 bị lint báo thiếu | nặng nếu vạch nhìn thấy | **PASS theo xác nhận chủ sở hữu** |
| 5 | QC1-11 | B06 | Lane alignment / đường cong | chính | **PASS theo xác nhận chủ sở hữu** |
| 6 | QC1-11 | B07 | Polyline 4 điểm / đường cong | chính | **PASS theo xác nhận chủ sở hữu** |

**Tổng hợp:** 6 nhóm điểm kiểm tra nêu trên đã được chủ sở hữu xác nhận PASS. Đây là xác nhận do người nộp cung cấp; người review chéo cần xác nhận độc lập trước khi ký phiếu chính thức.

## 5. Ca mơ hồ

Các trường hợp từng được nêu để hỏi lead đã được chủ sở hữu xác nhận PASS:

| Ảnh | Nội dung từng cần xác nhận | Trạng thái |
| --- | --- | --- |
| A05 | L1/R1 không xuất hiện trong vùng cần gán nhãn | Đã xác nhận PASS |
| A06 | Không có R1 cần gán nhãn | Đã xác nhận PASS |
| A07 | Không có L1 cần gán nhãn | Đã xác nhận PASS |
| A09 | Không có R1 cần gán nhãn | Đã xác nhận PASS |
| B06 | Polyline lane bám đúng đối tượng và hình dạng | Đã xác nhận PASS |
| B07 | Polyline 4 điểm mô tả đủ đường cong | Đã xác nhận PASS |

Không còn ca mơ hồ nào trong 6 mục nêu trên theo xác nhận của chủ sở hữu. Nếu coach đã xác nhận các ngoại lệ QC1-02, ghi tên/ngày hoặc tham chiếu xác nhận tại đây: ____________________.

## 6. Quyết định

- QC1-02: **PASS theo xác nhận của chủ sở hữu annotation**
- QC1-11: **PASS theo xác nhận của chủ sở hữu annotation**
- Quyết định do người nộp cung cấp để ghi nhận trong bản dự thảo: **RELEASE**
- Trạng thái phiếu QC chéo: **Chờ Phùng Danh Khoa xác nhận độc lập và ký/ghi ngày review**

**Phân biệt trách nhiệm:** RELEASE ở trên là quyết định mà Trần Đình Quang Vinh yêu cầu ghi vào bản dự thảo. Đây không phải bằng chứng rằng Phùng Danh Khoa đã trực tiếp kiểm tra hoặc ký duyệt. Khoa cần rà soát toàn bộ các tiêu chí QC1-01 đến QC1-12 và xác nhận quyết định cuối cùng trước khi phiếu được xem là QC chéo chính thức.

Người review chính thức: Phùng Danh Khoa  
Ngày review thực tế: ____________________  
Chữ ký/xác nhận của reviewer: ____________________

---

**Nguồn dữ liệu đã dùng cho bản dự thảo:** `day11-data(1).zip`, `trandinhquangvinh-front.zip`, `trandinhquangvinh-fisheye.zip`, `templates/qc1_form.md`, `docs/qc_severity_road_v1.0.md`, `docs/delivery_road_v1.0.md`.

**Người kiểm chính thức:** Phùng Danh Khoa — cần trực tiếp xác nhận, sửa và ghi ngày review trước khi nộp.
