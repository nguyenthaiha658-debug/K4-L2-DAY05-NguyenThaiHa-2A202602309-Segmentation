# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: K4-L2-DAY05-NguyenThaiHa-2A202602309
- Ngày / CVAT local: 18/9/2026
- Công cụ đã dùng: CVAT, SAM

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `submissions/easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `submissions/medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `submissions/hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý
Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.
- Ảnh: `data/tiers/medium_instance/images/` (ảnh 1)
- Vị trí và class: Chiếc xe con (`car`) ở góc tiền cảnh phía trước bên trái khung hình
- Quy tắc biên bạn tự đặt ra: Vẽ ôm sát mép vỏ thân xe, gương chiếu hậu và lốp xe chạm mặt đường; tính trọn phần kính chắn gió vào xe; dừng mask tại mép tiếp đất của lốp xe, không đưa bóng đổ dưới đường vào mask của xe
- Nếu sau đó dùng gợi ý, ghi một lỗi hoặc lý do bạn giữ đề xuất: Gợi ý AI (SAM) bị nhận diện lem phần bóng đen dưới gầm xe vào mask của xe, tôi phải dùng Brush thủ công tẩy bớt phần bóng đổ để trả lại ranh giới mặt đường
## 3. Một lỗi và hành động sửa
Mô tả một lỗi bạn gặp phải trong quá trình làm (vẽ nhãn, chọn lớp, hoặc export) và cách bạn đã xử lý để ra kết quả đúng.
- Lỗi: Chọn nhầm định dạng export của task `easy_semantic` thành COCO 1.0 thay vì Segmentation mask 1.1
- Phát hiện lúc nào / bằng cách nào: Phát hiện lúc kiểm tra file zip trước khi nộp và đối chiếu lại yêu cầu trong GUIDE.md
- Hành động sửa: Vào lại CVAT task `easy_semantic`, chọn Export task dataset đúng định dạng `Segmentation mask 1.1`, tải về đổi tên thành `easy_semantic.zip` và lưu vào thư mục `submissions/`
## 4. Ba ca chưa chắc
Ghi lại ba trường hợp ranh giới hoặc phân loại mà bạn thấy mơ hồ nhất, kèm theo cách bạn đã quyết định và lý do.
### Ca 1
- Tier / ảnh / đối tượng hoặc vùng: Easy semantic / ảnh 1 / Ranh giới giữa `road` và `sidewalk`
- Phân vân giữa: Gộp phần vỉa hè bị bóng cây che tối vào `road` hay tách riêng thành `sidewalk`
- Quyết định cuối: Tách riêng thành `sidewalk` theo đường thẳng kéo dài của gờ bó vỉa hè
- Lý do: Đảm bảo giữ đúng ranh giới cấu trúc vật lý của vỉa hè và lòng đường ngay cả khi bị bóng râm làm tối màu
### Ca 2
- Tier / ảnh / đối tượng hoặc vùng: Medium instance / ảnh 2 / Chiếc xe bị che khuất một phần phía sau
- Phân vân giữa: Vẽ phỏng đoán trọn vẹn cả chiếc xe hay chỉ vẽ phần thân xe nhìn thấy
- Quyết định cuối: Chỉ vẽ mask cho phần thân xe thực sự lộ diện trên ảnh
- Lý do: Tuân thủ đúng nguyên tắc Instance Segmentation là chỉ gán nhãn cho các pixel nhìn thấy được, không vẽ đè lên vật cản phía trước
### Ca 3
- Tier / ảnh / đối tượng hoặc vùng: Hard panoptic / ảnh 1 / Tán lá cây giao với nền trời (`vegetation` và `sky`)
- Phân vân giữa: Vẽ bao trọn cả tán cây bao gồm các kẽ hở hay tỉa từng lỗ hở nhỏ của bầu trời
- Quyết định cuối: Vẽ bao tán lá lớn và chỉ trừ các khoảng trống bầu trời có kích thước lớn nhìn rõ
- Lý do: Cân đối giữa độ mịn của ranh giới mask và tránh tạo ra quá nhiều viền răng cưa nhỏ gây nhiễu cho mô hình
