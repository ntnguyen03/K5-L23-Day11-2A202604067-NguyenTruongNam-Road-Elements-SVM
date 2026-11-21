# Phiếu QC 1 — Road v1.0

| Thông tin | Nội dung |
| --- | --- |
| Lô được kiểm | Đỗ Tuấn Long — 2A202604066 |
| Người kiểm | Nguyễn Trường Nam — 2A202604067 |
| Ngày kiểm | 21/11/2026 |
| Guideline | Road v1.0 |
| File front | `DoTuanLong-front.zip` · SHA-256 bắt đầu `925b20df595d4fb5` |
| File fisheye | `DoTuanLong-fisheye.zip` · SHA-256 bắt đầu `01cb962a14fde2fc` |
| Phiên bản bàn giao | `revision=1` theo log lint Long gửi. Hai file ZIP là bản dùng để kiểm. |
| Mẫu kiểm | 6 ảnh bắt buộc, 0 ảnh thêm. Tổng cộng 59 nhãn, gồm 35 shape và 24 tag. |

## Mẫu kiểm

| Ảnh | Tên trong XML | Camera | Shape | Tag |
| --- | --- | --- | ---: | ---: |
| A01 | `A01_bc5fadac-fa6dd225.jpg` | `front` | 8 | 4 |
| A03 | `A03_b1c66a42-6f7d68ca.jpg` | `front` | 12 | 4 |
| A09 | `A09_c7e6d5d1-c8af9fe3.jpg` | `front` | 4 | 4 |
| B01 | `B01_02688_FV.png` | `fisheye_front` | 3 | 4 |
| B02 | `B02_03177_FV.png` | `fisheye_front` | 4 | 4 |
| B08 | `B08_05783_MVR.png` | `fisheye_right` | 4 | 4 |
| **Tổng** | | | **35** | **24** |

## Tổng hợp theo mã

| Mã | Nội dung kiểm | Số mục kiểm | Số lỗi xác nhận | Mức theo guideline |
| --- | --- | ---: | ---: | --- |
| QC1-01 | Camera và các tag ảnh | 24 | 0 | Nặng |
| QC1-02 | Hai vị trí L1, R1 trên 3 ảnh front | 6 | 0 | Nặng |
| QC1-03 | `position` của 8 nhãn `lane` | 8 | 0 | Nặng |
| QC1-04 | Tâm vạch, chiều vẽ và điểm dừng trên 7 nhãn `lane` front | 7 | 5 | Chính |
| QC1-05 | Vạch đứt và các đoạn nối qua chỗ che trên 8 nhãn `lane` | 8 | 0 | Chính |
| QC1-06 | `style`, `color`, `kind` trên 8 nhãn `lane` | 8 | 1 | Chính |
| QC1-07 | 11 vùng lái, 3 vùng qua đường và 4 mép vỉa | 18 | 1 | Chính |
| QC1-08 | 8 box đèn hiện có và 6 lượt rà cụm đèn trên ảnh | 14 | 1 | Nặng / chính |
| QC1-09 | Thuộc tính của 8 box đèn và 1 box biển hiện có | 9 | 0 | Chính |
| QC1-10 | 1 box biển hiện có và 6 lượt rà biển trên ảnh | 7 | 0 | Chính |
| QC1-11 | 1 `lane`, 2 `road_curb` và 1 box đèn fisheye | 4 | 0 | Chính |
| QC1-12 | 2 ZIP đọc được và 6 bản ghi ảnh đối chiếu được | 8 | 0 | Nhẹ / nặng |

Một nhãn có thể được kiểm theo nhiều mã. Mẫu số tính tỷ lệ là 59 nhãn trong bảng mẫu kiểm. Hai ZIP đều đọc được và mỗi ZIP chứa `annotations.xml`. Lint trên cả lô đọc được 28 bản ghi ảnh và báo 32 cờ, gồm 25 ở ảnh bắt buộc và 7 ở ảnh thêm. Ba cờ box dưới 8 px ở A03 là nhắc tự kiểm theo guideline. Bảng tổng hợp đếm các lỗi đã xác nhận khi đối chiếu ảnh mẫu.

## Danh sách lỗi

`#n` là thứ tự shape trong XML của ảnh, đếm từ 0 và bỏ qua tag. Tọa độ tính theo pixel ảnh gốc từ góc trên trái, làm tròn đến pixel gần nhất.

| # | Mã | Ảnh | Nhãn và vị trí | Mức | Quan sát và cách sửa |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A01 | `lane #1`, L1, điểm đầu `(354, 514)` | Chính | Bắt đầu ở phía xa, gần điểm tụ, rồi đi xuống đoạn gần xe. Đảo thứ tự điểm để bắt đầu ở đoạn vạch gần xe và đi ra xa. |
| 2 | QC1-04 | A01 | `lane #2`, R1, điểm đầu `(434, 522)` | Chính | Vẽ từ đoạn xa về đoạn gần xe. Đảo thứ tự điểm theo chiều gần → xa. |
| 3 | QC1-04 | A01 | `lane #4`, L2, điểm đầu `(329, 504)` | Chính | Điểm đầu nằm ở đoạn xa bên trái. Đảo thứ tự điểm để bắt đầu từ đoạn nhìn thấy sát xe nhất. |
| 4 | QC1-04 | A03 | `lane #2`, L1, điểm đầu `(544, 375)` | Chính | Đường bắt đầu gần điểm tụ và kết thúc sát mép dưới ảnh. Đảo thứ tự điểm để đi từ chân vạch gần xe lên phía xa. |
| 5 | QC1-04 | A03 | `lane #4`, R1, điểm đầu `(597, 387)` | Chính | Đường đi từ đoạn xa của vạch trắng về sát mép dưới ảnh. Đảo thứ tự điểm, giữ vạch đứt thành một polyline. |
| 6 | QC1-06 | A01 | `lane #3`, R2, mép phải gần `(1280, 712)` | Chính | Vệt sơn liền sát lề phải có màu vàng nhưng XML đặt `color=white`. Đổi thành `color=yellow` trong CVAT. |
| 7 | QC1-07 | A09 | `drivable #0`, `alternative`, gần `(487, 642)` | Chính | Polygon bên trái lấn qua vạch trắng đôi và bao phần làn có xe hướng về camera. Thu hẹp polygon về phần làn kề cùng chiều nếu có. Xóa shape nếu không có phần làn kề cùng chiều. |
| 8 | QC1-08 | B02 | Thiếu `traffic_light`, góc trên phải, ngay sau người đi bộ ở gần `(1105, 130)` | Chính | Có một cụm đèn cho người đi bộ kích thước trên 8 px ở mép phải. B02 chỉ có một box đèn ở mép trái. Thêm box sát phần vỏ nhìn thấy và kiểm thuộc tính `color`, `facing`, `type`, `edge_zone` trên ảnh gốc. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp |
| --- | --- | --- |
| A09 | Sau khi đối chiếu ảnh gốc, mép phải có vạch sơn đủ rõ để bổ sung R1 không? Ở mẫu hiện tại chỉ nhận ra mép vỉa phía phải. | Chờ coach xác nhận. |
| B01 | Dải mép trái có đường ray hiện được gán `drivable alternative`. Đây có phải làn ô tô cùng chiều được phép dùng ở đoạn này không? | Chờ coach xác nhận. |

**Ảnh đối chứng B08** có camera `fisheye_right` và `lane #0` dùng `position=other`, đúng quy tắc camera bên. Chưa ghi nhận lỗi xác nhận trong ảnh này khi rà các nhãn hiện có.

## Quyết định

| Lỗi nặng | Lỗi chính | Lỗi nhẹ | Ca chờ lead | Quyết định |
| ---: | ---: | ---: | ---: | --- |
| 0 | 8 / 59 = 13,56% | 0 | 2 | **Rework** |

Tỷ lệ lỗi chính trên mẫu vượt ngưỡng 5% của Road v1.0. Sửa các vị trí trong bảng, kiểm tiếp chiều vẽ trên các ảnh front còn lại và rà đèn ở hai mép ảnh fisheye. Nhờ coach xác nhận hai ca mơ hồ trước khi xuất lại. Đề xuất kiểm lại lỗi #1, #6, #8 và ảnh đối chứng B08.
