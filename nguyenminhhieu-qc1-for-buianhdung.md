# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên):Bùi Anh Dũng        Người kiểm (học viên):  Nguyễn Minh Hiếu
Ngày:    20/11/2026                      Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest):  buianhdung-front.zip, buianhdung-fisheye.zip
Số ảnh kiểm: 6 (+ __ ảnh thêm, ghi riêng) A03, A05, A06 (front); B02, B03, B06 (fisheye).   
Số nhãn đã kiểm (shape + tag):  29 shapes + 24 tags = 53 nhãn.

## Tổng hợp theo mã
| Ảnh | Shapes | Tags | Tổng |
| --- | ---: | ---: | ---: |
| A03 | 5 | 4 | 9 |
| A05 | 3 | 4 | 7 |
| A06 | 9 | 4 | 13 |
| B02 | 5 | 4 | 9 |
| B03 | 4 | 4 | 8 |
| B06 | 3 | 4 | 7 |
| **Tổng** | **29** | **24** | **53** |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id tham chiếu) | Mức | Mô tả ngắn và yêu cầu sửa |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-07 | A03 | `drivable`, shape thứ 3, `area_type=direct` | chính | Polygon kéo về sát toàn bộ phía phải đường, bao gồm khu vực có dãy xe đỗ; giới hạn lại đúng làn xe đang đi, không gộp dải đỗ vào `direct`. |
| 2 | QC1-07 | A05 | `drivable`, shape thứ 3, `area_type=direct` | chính | Polygon mở rộng gần trọn bề rộng lòng đường giữa hai hàng xe đỗ; chưa tách dải đỗ sát lề khỏi làn đi thẳng. Vẽ lại biên `direct` theo chức năng sử dụng mặt đường. |
| 3 | QC1-08 | B02 | `traffic_light`, shape thứ 5 (đèn bên phải), box `(1110,72)–(1183,234)` | chính | Rectangle chưa ôm sát vỏ đèn trên mép ảnh fisheye: chứa nền/cột và không bám đầy đủ cụm đèn; điều chỉnh box theo housing nhìn thấy, kiểm lại `edge_zone`. Không ghi lỗi sai màu vì chưa có căn cứ. |
| 4 | QC1-07 | B03 | `drivable`, shape thứ 4, `area_type=direct` | chính | Một polygon `direct` trải rộng nhiều làn trong hình rear, chưa tách vùng làn chính và làn khác có thể lái thành `alternative` theo guideline. Thu hẹp direct phù hợp làn đang xét. |
| 5 | QC1-07 | B06 | `drivable`, shape thứ 2, `area_type=direct` | chính | Polygon chạy sang phần đảo nổi/khối phân cách nổi phía phải (vùng xấp xỉ x≈920–1160, y≈360–580 trong ảnh); loại phần không thể lái khỏi vùng `direct`, giữ ranh theo ảnh fisheye. |
## Ca mơ hồ
| Ảnh | Câu hỏi cho lead/coach | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Không thấy vạch L1/R1 riêng biệt trong đường đô thị hẹp, có được miễn QC1-02 thay vì tự vẽ vạch giả không? | **Chưa có**; 2 cảnh báo L1/R1, chưa chuyển thành lỗi nặng đã xác nhận. |
| A06 | Vạch L1/R1 có thực sự hiện diện dưới cầu/qua nút giao, hay cả hai bên đều không có vạch kẻ rõ để gán? | **Chưa có**; 2 cảnh báo L1/R1, chưa chuyển thành lỗi nặng đã xác nhận. |
| B03 | Camera fisheye_rear: xác định `direct` theo dải đường tương ứng hướng di chuyển của xe thế nào khi góc nhìn hướng ra phía sau? | **Chưa có**; phần polygon quá rộng đã được ghi QC1-07 theo đánh giá mô phỏng, coach có thể điều chỉnh khi đối chiếu GT. |

## Quyết định
- Lỗi nặng đã xác nhận: 0 (còn 4 cảnh báo QC1-02 chờ coach xem ảnh A05 và A06).
- Lỗi chính: 5 / 53 nhãn = 9,43%.
- Lỗi nhẹ đã xác nhận: 0 trên ZIP/XML hiện có (tình trạng chưa có manifest được ghi là giới hạn hồ sơ nháp, không đếm như lỗi export chính thức).
- Ca chờ lead: 3 nhóm câu hỏi, trong đó có 2 ảnh với tổng 4 cảnh báo QC1-02.
- Quyết định (mô phỏng): Rework.
- Lý do: Tỉ lệ lỗi chính 9,43% > 5%, nên kết luận Rework theo thang của Road v1.0, dù các cảnh báo QC1-02 chưa được xác minh. Không kết luận Release khi các vùng lái còn sai phạm vi.
