# Báo cáo cá nhân — Ngày 11 · Road Elements & SVM

- **Họ tên:** Nguyễn Trường Nam
- **Mã học viên:** 2A202604067
- **CVAT:** 2.74.1
- **Guideline:** Road v1.0
- **Revision nộp:** 1, theo manifest bàn giao.
- **Mốc tạo XML do CVAT ghi (giờ Việt Nam):** front 20/11/2026 19:20:38, fisheye 20/11/2026 18:59:20.

## 1. Kiểm project

| Mục | Kết quả |
| --- | --- |
| Sáu label hình | Có lane và road_curb dạng polyline, crosswalk và drivable dạng polygon, traffic_light và traffic_sign dạng hộp. |
| Thuộc tính và giá trị | Lint không báo sai tên hoặc giá trị. Lane dùng position, style, color, kind. Tag dùng thuộc tính value. |
| Bốn tag ảnh | 20/20 ảnh có camera, timeofday, weather và source. Không có cảnh báo camera sai. |
| Trạng thái job | Đã xác nhận Job 21 (front) và Job 22 (fisheye) ở trạng thái completed. |

Khi vẽ polyline, đặt điểm từ gần xe ra xa, bấm N hoặc Done để kết thúc. Khi đặt tag, chọn nhãn kiểu Tag rồi kiểm tra giá trị trên ảnh. Tôi đã tự rà 20 ảnh bắt buộc trong hai job.

## 2. Số lượng đã gán

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 25 | 6 | 3 | 5 | 12 | 6 |
| front-extra | 0/4 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 3 | 5 | 6 | 3 | 2 | 0 |
| fisheye-extra | 0/4 | 0 | 0 | 0 | 0 | 0 | 0 |

Số liệu lấy từ hai export CVAT cuối và manifest đi kèm. Bản front lúc 19:20 có thêm một nhãn đèn ở A06 so với lần export trước.

## 3. Bảng ca khó

| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A04 | lane | Hai nét riêng hay một vạch đôi | Một nhãn double | Hai nét vàng gần nhau cùng tạo ranh giới dọc. |
| A05 | lane L1/R1 | Mép lề hay tâm vệt sơn | Để trống L1/R1 | Có thể nhận ra mép lề và xe đỗ, chưa xác định được tâm hai vạch sơn. |
| A06 | lane L1/R1 | Vạch ngựa vằn hay vạch dọc | Giữ crosswalk, để trống L1/R1 | Vạch ngang rõ hơn dấu sơn dọc dưới vùng bóng. Chưa xác định đủ hai tuyến tâm vạch. |
| A07 | lane L1 | Rào bê tông hay vạch làn | Giữ road_curb và R1, để trống L1 | Nhìn được chân rào bên trái, chưa tách được vệt sơn riêng để đặt L1. |
| A10 | lane R1 | Vệt phản chiếu hay đoạn sơn | Giữ đoạn vạch phải nhìn được | Bám đoạn sơn thấy trên mặt đường ướt và dừng trước vùng không xác định. |
| A12 | lane L1/R1 | Vạch ngang ở nút giao hay vạch dọc xác định làn | Giữ crosswalk, chưa thêm L1/R1 | Sau khi rà, chưa xác định được cặp biên làn đủ rõ để gán qua nút giao. |
| B03 | lane | Nối thẳng hay bám cung | Nhiều điểm theo tâm vạch | Phối cảnh fisheye làm vệt sơn cong. Điểm được đặt dày hơn ở phần cong. |
| B04 | drivable và crosswalk | Kéo tới thân xe hay dừng trước | Dừng ở ranh giới mặt đường | Thân xe ở sát mép dưới không thuộc vùng lái. |

**QC1-02 chờ coach xác nhận:** A05 (L1, R1), A06 (L1, R1), A07 (L1), A12 (L1, R1). Tôi đã rà ảnh và chưa xác định được tâm vạch để thêm nhãn.

## 4. Phiếu QC 1 nhận được và sửa đổi

Tôi đã nhận Phiếu QC 1 của **Đỗ Tuấn Long (2A202604066)**, đề ngày 20/11/2026. Long ghi đã chạy lint và xem thủ công 20 ảnh trong hai ZIP revision 1. Kết luận trên phiếu là **HOLD**. Phiếu ghi 7 cảnh báo nặng tiềm năng QC1-02, 0 lỗi chính và 0 lỗi nhẹ. Ở phần lý do, Long ghi “Không đồng ý với cảnh báo tự kiểm tra”.

| Ảnh | Vị trí được cảnh báo | Phản hồi sau tự rà |
| --- | --- | --- |
| A05 | L1, R1 | Chưa xác định được tâm vệt sơn ở hai bên. Giữ nhãn mép vỉa hiện có. |
| A06 | L1, R1 | Vạch qua đường rõ hơn dấu sơn dọc trong vùng bóng. Giữ nhãn crosswalk. |
| A07 | L1 | Nhìn thấy chân rào ở bên trái. Chưa tách được vệt sơn để đặt L1. |
| A12 | L1, R1 | Chưa xác định được hai biên làn đủ rõ qua nút giao. Giữ nhãn crosswalk. |

Tôi giữ nguyên revision 1 sau khi nhận phiếu và để 7 vị trí trên chờ coach xác nhận. Nếu coach chỉ ra vạch sơn đủ rõ, tôi sẽ bổ sung nhãn ở vị trí đó và xuất lại. Trước khi nhận phiếu, tôi đã xóa một đỉnh trùng trong polygon crosswalk của A12, giữ nguyên hình bao rồi lưu và xuất lại từ CVAT.

Phiếu của Long ghi 13 nhãn đèn. Manifest và hai ZIP bàn giao có 14 nhãn đèn (12 front, 2 fisheye). Số lượng ở mục 2 và mục 5 lấy trực tiếp từ bản export bàn giao.

## 5. Kiểm file export

| File | Mở lại bằng checker | Số shape hai ảnh đầu | Tag camera trong XML | Kèm ảnh |
| --- | --- | --- | --- | --- |
| nguyentruongnam-front.zip | Có | A01: 4, A02: 4 | front | Không |
| nguyentruongnam-fisheye.zip | Có | B01: 1, B02: 3 | fisheye_front | Không |

Lint cuối trên 20 ảnh ghi **7 cảnh báo mức nặng (đều QC1-02), 0 chính, 0 nhẹ**. SHA-256 trong manifest khớp cả hai ZIP. Lint kiểm định dạng và đưa gợi ý, không đo độ khớp với GT.

## 6. Bằng chứng từ bản export CVAT

Cấu hình đọc trực tiếp từ metadata XML của task 21 có 10 nhãn: lane (polyline); road_curb (polyline); crosswalk (polygon); drivable (polygon); traffic_light (rectangle); traffic_sign (rectangle); camera (tag); timeofday (tag); weather (tag); source (tag).

Hai hình minh họa từ bản export gồm A10 (vạch làn, vùng lái và biển báo) và B03 (polyline bám cung fisheye). Chưa có ảnh chụp trực tiếp tab Labels và hai job trong hồ sơ này.

Đoạn XML thật của một polyline trong export front:

```xml
<polyline label="lane" source="file" occluded="0" points="107.40,720.00;211.90,633.70;254.00,595.90;302.30,554.30;336.60,526.80;366.40,504.30" z_order="0">
      <attribute name="position">L1</attribute>
      <attribute name="style">dashed</attribute>
      <attribute name="color">white</attribute>
      <attribute name="kind">single</attribute>
    </polyline>
```

## 7. Tự đánh giá

Tín hiệu self-QC nổi bật là QC1-02 khi vạch mờ hoặc bố cục nút giao khó đọc. Lần sau tôi sẽ rà cả hai biên ở mức zoom cao, phân biệt vệt sơn dọc với mép lề và vạch ngựa vằn, rồi nhờ coach chốt ca không thấy vạch ngay trong lúc gán. Với model row-anchor, polyline làn cung cấp x tại từng hàng neo. Bỏ sót đoạn vạch nhìn thấy khiến các hàng neo tương ứng có thể bị đánh thành không có làn. Nếu gán nhầm mép lề làm làn, model có thể học tọa độ x sai ở ảnh có cấu trúc tương tự.
