# Gói chuyển giao Phòng Điều Hành Multi Agent Company

*Dành cho học viên chương trình Multi Agent Company của Nguyễn Anh Tuấn. Làm theo 3 bước ở Phần 2 là có ngay một Phòng Điều Hành của riêng mình, chạy trên Muse của chính bạn.*

*Bản hiện tại — cập nhật ngày 24/11/2026: đội 11 agent, bảng việc 3 cột, việc xong chuyển thẳng sang Hoàn thành (không còn bước Chờ duyệt).*

---

## Phần 1 — Phòng Điều Hành là gì?

Phòng Điều Hành Multi Agent Company là **phòng điều hành trực quan cho đội AI Agent của bạn** — nơi bạn nhìn thấy cả "công ty một người" của mình đang làm việc, thay vì chỉ đọc các đoạn chat rời rạc.

Bên trong Phòng Điều Hành có:

- **Một đội 11 AI Agent:** agent **Điều Phối** ngồi ở trung tâm, xung quanh là 10 agent chuyên trách: Bán Hàng, Content, Video, Chăm Sóc, Nghiên Cứu, Thiết Kế App, Vận Hành, Email, Trợ Lý và Landing Page. Mỗi agent có biểu tượng robot riêng và màu nhận diện riêng.

- **Bảng quản lý việc 3 cột:** **Hàng chờ → Đang làm → Hoàn thành**. Việc nào đang ở đâu, do agent nào làm, kết quả ra sao — nhìn một cái là biết. Việc làm xong chuyển thẳng sang Hoàn thành kèm kết quả, không kẹt ở bước chờ duyệt nào.

- **Thanh ra lệnh:** bạn gõ một lệnh (ví dụ: "Viết 3 bài Facebook giới thiệu chương trình tuần này"), Điều Phối tự chia lệnh thành các việc con, giao cho đúng agent, và bạn **xem workflow chạy trực tiếp (realtime)** ngay trên màn hình: nhánh nào đang sáng, agent nào đang làm, việc nào vừa xong.

- **Báo cáo tổng hợp:** mỗi lượt chạy kết thúc bằng một báo cáo tổng hợp của Điều Phối ngay trong ứng dụng. Chưa ưng, bạn mở lại lượt chạy để làm lại.

### Vì sao cài đặt bằng cách "dán prompt cho Muse của bạn tự xây"?

Mỗi tài khoản Muse là **một môi trường riêng, tách biệt hoàn toàn**. Phòng Điều Hành là một ứng dụng chạy thật: nó cần lưu dữ liệu (việc, agent, lịch sử chạy) và cần chạy workflow thật ngay trong môi trường của người dùng. Mã nguồn của ứng dụng gắn với môi trường chạy của Muse nên không đóng gói thành file cài đặt kiểu truyền thống được.

Vì vậy, cách chuyển giao đúng và hiệu quả nhất là:

> Bạn dán **Prompt cài đặt** (file `PROMPT-CAI-DAT.txt` trong gói này) vào Muse của chính bạn, và Muse của bạn sẽ **tự xây một Phòng Điều Hành giống hệt** ngay trong môi trường của bạn — lưu dữ liệu của bạn, chạy việc của bạn, và chỉ bạn mới truy cập được.

### Gói này gồm những file gì?

| File | Nội dung |
|------|----------|
| `README.md` | Tài liệu bạn đang đọc: giới thiệu, hướng dẫn cài đặt 3 bước, cách dùng hằng ngày |
| `PROMPT-CAI-DAT.txt` | **Prompt cài đặt đầy đủ** — copy nguyên văn, dán vào Muse của bạn là Muse tự xây xong Phòng Điều Hành đúng bản hiện tại (11 agent, đúng màu, đúng luồng việc) |
| `DAC-TA-KY-THUAT.md` | Đặc tả kỹ thuật chi tiết: mô hình dữ liệu, đủ 12 hành động (actions) của ứng dụng, luồng workflow chạy thật, chuẩn trình bày giao diện và giao thức đồng bộ chat → Hub. Dùng khi bạn muốn hiểu sâu, tuỳ biến nâng cao, hoặc kiểm tra Muse của bạn xây có đúng chuẩn không |

**Gói này không gồm:** dữ liệu của bất kỳ ai. Lịch sử việc, kết quả công việc, thông tin cá nhân và nội dung công việc của người khác **không** được đóng gói hay chuyển theo. Phòng Điều Hành của bạn sẽ bắt đầu **trắng, sạch, và là của riêng bạn** — chỉ có sẵn đội 11 agent mặc định.

---

## Phần 2 — Hướng dẫn cài đặt 3 bước

### Bước 1: Mở Muse của bạn, tạo đoạn chat mới

Đăng nhập Muse bằng tài khoản của bạn, mở một cuộc trò chuyện mới. Không cần cài thêm phần mềm, không cần biết lập trình.

### Bước 2: Copy toàn bộ Prompt cài đặt, dán vào và gửi

Mở file `PROMPT-CAI-DAT.txt`, copy **nguyên văn toàn bộ nội dung** (không sửa, không cắt bớt), dán vào ô chat và gửi cho Muse của bạn.

### Bước 3: Chờ Muse xây xong, mở ứng dụng và dùng thử

Muse sẽ tự xây ứng dụng trong ít phút. Khi xong:

1. Mở ứng dụng **Phòng Điều Hành Multi Agent Company** trong mục **Thư viện (Library)** của Muse.
2. Kiểm tra đội agent: phải đủ **11 agent** với đúng tên và màu như bảng ở Phần 3.
3. Gõ thử một lệnh vào **thanh ra lệnh**, ví dụ: *"Nghiên cứu 3 đối thủ đang dạy về AI Agent và gợi ý ý tưởng nội dung cho tôi"*.
4. Ngồi xem các agent làm việc trực tiếp trên màn hình; việc xong sẽ hiện ở cột **Hoàn thành** kèm kết quả và báo cáo tổng hợp.

Thấy workflow chạy thật và kết quả hiện ở cột Hoàn thành là bạn đã cài đặt thành công.

> [!TIP]
> Nếu Muse của bạn hỏi thêm điều gì trong lúc xây, cứ trả lời ngắn gọn theo đúng nhu cầu của bạn. Nếu bản dựng ra chưa đúng (thiếu agent, sai màu, còn cột Chờ duyệt), mở file `DAC-TA-KY-THUAT.md`, copy đoạn mô tả phần chưa đúng và gửi cho Muse của bạn để sửa theo đặc tả.

### Cách dùng hằng ngày

- **Ra lệnh ngay trên Phòng Điều Hành:** gõ lệnh vào thanh ra lệnh, Điều Phối chia việc và các agent chạy thật ở nền, kết quả và báo cáo tổng hợp hiện ngay trong ứng dụng.

- **Giao việc trong chat:** cứ giao việc cho Muse như bình thường — Muse sẽ đồng thời ghi việc lên Phòng Điều Hành theo diễn biến thật và realtime: tạo việc, chuyển **Đang làm** trước khi bắt đầu, chuyển thẳng **Hoàn thành kèm kết quả** khi làm xong. Bạn mở Hub là thấy ngay.

- **Thêm, sửa agent theo nhu cầu:** đổi tên, đổi vai trò, đổi màu hoặc thêm agent mới ngay trong ứng dụng, tuỳ theo mô hình kinh doanh của bạn.

---

## Phần 3 — Đội 11 agent mặc định

| # | Agent | Vai trò | Màu |
|---|-------|---------|-----|
| 1 | Điều Phối | Tổng điều phối | Cyan #22D3EE |
| 2 | Bán Hàng | Tư vấn & chốt đơn | Vàng #FBBF24 |
| 3 | Content | Nội dung & bài viết | Ngọc lục #34D399 |
| 4 | Video | Sản xuất video | Hồng #FB7185 |
| 5 | Chăm Sóc | Chăm sóc khách hàng | Xanh trời #38BDF8 |
| 6 | Nghiên Cứu | Nghiên cứu thị trường | Cam #FB923C |
| 7 | Thiết Kế App | Thiết kế & xây dựng ứng dụng | Tím #A78BFA |
| 8 | Vận Hành | Vận hành đăng bài và phân phối nội dung | Xanh lime #A3E635 |
| 9 | Email | Email marketing và chăm sóc qua email | Teal #2DD4BF |
| 10 | Trợ Lý | Trợ lý cá nhân của sếp | Chàm #818CF8 |
| 11 | Landing Page | Thiết kế và xây dựng landing page | Hồng #EC4899 |

Khi bạn giao việc trong chat, Muse tự phân công theo đúng số thứ tự này: việc nội dung giao Content (3), việc nghiên cứu giao Nghiên Cứu (6), việc đăng bài và phân phối giao Vận Hành (8), việc xây ứng dụng giao Thiết Kế App (7), và cứ thế.

---

## Phần 4 — Lưu ý và tuỳ biến

### Tuỳ biến theo mô hình kinh doanh của bạn

Phòng Điều Hành là khung làm việc, không phải khuôn cứng. Bạn hoàn toàn có thể:

- **Đổi tên và vai trò agent** cho khớp với công việc của mình, ví dụ thêm agent Kế Toán, agent Tuyển Dụng, agent Livestream…
- **Đổi màu** từng agent để dễ nhận diện.
- **Thêm hoặc xoá agent** khi đội của bạn lớn lên hoặc thu gọn lại.

Đội 11 agent mặc định là điểm khởi đầu đã được vận hành thật và kiểm chứng, hợp với hầu hết mô hình kinh doanh một người.

### Nguyên tắc vận hành

- Phòng Điều Hành là nơi **ghi và theo dõi việc**: việc xong được ghi thẳng sang Hoàn thành kèm kết quả để bạn nắm tiến độ trong nháy mắt.
- Với những việc nhạy cảm — **đăng bài, gửi tin nhắn cho khách, cam kết về giá, đơn hàng, thanh toán hay lịch học** — hãy luôn tự xem lại kết quả trước khi để agent thực thi ra bên ngoài. AI Agent làm nhanh và làm nhiều, nhưng **quyền quyết định cuối cùng là của bạn**.

### Về bản chuyển giao này

Đây là bản chuyển giao phục vụ học tập trong **chương trình Multi Agent Company của Nguyễn Anh Tuấn**, dành cho học viên của chương trình sử dụng với tài khoản Muse của riêng mình. Chúc bạn sớm có một "công ty một người" vận hành trơn tru với đội AI Agent của chính bạn.
