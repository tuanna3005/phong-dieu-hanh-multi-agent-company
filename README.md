# Gói chuyển giao Phòng Điều Hành Multi Agent Company

*Dành cho học viên chương trình Multi Agent Company của Nguyễn Anh Tuấn. Bạn nhận được bản này, làm theo 3 bước ở Phần 2 là có ngay một Phòng Điều Hành của riêng mình, chạy trên Muse của chính bạn.*

---

## Phần 1 — Phòng Điều Hành là gì?

Phòng Điều Hành Multi Agent Company là **phòng điều hành trực quan cho đội AI Agent của bạn** — nơi bạn nhìn thấy cả "công ty một người" của mình đang làm việc, thay vì chỉ đọc các đoạn chat rời rạc.

Bên trong Phòng Điều Hành có:

- **Một đội AI Agent:** agent **Điều Phối** ngồi ở trung tâm, xung quanh là các agent chuyên trách (bán hàng, nội dung, video, chăm sóc khách hàng, nghiên cứu…). Mỗi agent có biểu tượng robot riêng và màu nhận diện riêng.

- **Bảng quản lý việc 4 cột:** **Hàng chờ → Đang làm → Chờ duyệt → Hoàn thành**. Việc nào đang ở đâu, do agent nào làm, kết quả ra sao — nhìn một cái là biết.

- **Thanh ra lệnh:** bạn gõ một lệnh (ví dụ: "Viết 3 bài Facebook giới thiệu chương trình tuần này"), Điều Phối tự chia lệnh thành các việc con, giao cho đúng agent, và bạn **xem workflow chạy trực tiếp (realtime)** ngay trên màn hình: nhánh nào đang sáng, agent nào đang làm, việc nào vừa xong.

- **Quyền duyệt nằm ở bạn:** mọi kết quả đều dừng ở cột **Chờ duyệt**. Chỉ bạn bấm duyệt thì việc mới chuyển sang Hoàn thành; chưa ưng thì yêu cầu làm lại.

### Vì sao cài đặt bằng cách "dán prompt cho Muse của bạn tự xây"?

Mỗi tài khoản Muse là **một môi trường riêng, tách biệt hoàn toàn**. Phòng Điều Hành là một ứng dụng chạy thật: nó cần lưu dữ liệu (việc, agent, lịch sử chạy) và cần chạy workflow thật ngay trong môi trường của người dùng.

Vì vậy, cách chuyển giao đúng và hiệu quả nhất là:

> Bạn dán **Prompt cài đặt ở Phần 3** vào Muse của chính bạn, và Muse của bạn sẽ **tự xây một Phòng Điều Hành giống hệt** ngay trong môi trường của bạn — lưu dữ liệu của bạn, chạy việc của bạn, và chỉ bạn mới truy cập được.

### Gói này gồm gì, không gồm gì?

**Gói này gồm:** tài liệu hướng dẫn này và Prompt cài đặt đầy đủ ở Phần 3 — đủ để Muse của bạn xây lại toàn bộ Phòng Điều Hành với đầy đủ tính năng như bản gốc.

**Gói này không gồm:** dữ liệu của bất kỳ ai. Lịch sử việc, kết quả đã duyệt, thông tin cá nhân và nội dung công việc của người khác **không** được đóng gói hay chuyển theo. Phòng Điều Hành của bạn sẽ bắt đầu **trắng, sạch, và là của riêng bạn**.

---

## Phần 2 — Hướng dẫn cài đặt 3 bước

### Bước 1: Mở Muse của bạn, tạo đoạn chat mới

Đăng nhập Muse bằng tài khoản của bạn, mở một cuộc trò chuyện mới. Không cần cài thêm phần mềm, không cần biết lập trình.

### Bước 2: Copy toàn bộ Prompt cài đặt ở Phần 3, dán vào và gửi

Kéo xuống Phần 3, copy **nguyên khối prompt** (không sửa, không cắt bớt), dán vào ô chat và gửi cho Muse của bạn.

### Bước 3: Chờ Muse xây xong, mở ứng dụng và dùng thử

Muse sẽ tự xây ứng dụng trong ít phút. Khi xong:

1. Mở ứng dụng **Phòng Điều Hành Multi Agent Company** trong mục **Thư viện (Library)** của Muse.
2. Gõ thử một lệnh vào **thanh ra lệnh**, ví dụ: *"Nghiên cứu 3 đối thủ đang dạy về AI Agent và gợi ý ý tưởng nội dung cho tôi"*.
3. Ngồi xem các agent làm việc trực tiếp trên màn hình, rồi vào cột **Chờ duyệt** để xem kết quả và bấm duyệt.

Thấy kết quả hiện ở Chờ duyệt và duyệt được sang Hoàn thành là bạn đã cài đặt thành công.

### Cách dùng hằng ngày

- **Ra lệnh ngay trên Phòng Điều Hành:** gõ lệnh vào thanh ra lệnh, Điều Phối chia việc và các agent chạy thật ở nền, kết quả nộp về Chờ duyệt kèm báo cáo tổng hợp.

- **Giao việc trong chat:** cứ giao việc cho Muse như bình thường, và nói thêm *"ghi lên Phòng Điều Hành nhé"*. Muse sẽ đồng thời ghi việc lên Hub theo diễn biến thật: tạo việc, chuyển **Đang làm** khi bắt đầu, chuyển **Chờ duyệt kèm kết quả** khi làm xong — bạn mở Hub là thấy ngay.

- **Duyệt việc ở cột Chờ duyệt:** đọc kết quả, ưng thì duyệt sang Hoàn thành, chưa ưng thì yêu cầu làm lại.

- **Thêm, sửa agent theo nhu cầu:** đổi tên, đổi vai trò, đổi màu hoặc thêm agent mới ngay trong ứng dụng, tuỳ theo mô hình kinh doanh của bạn.

---

## Phần 3 — Prompt cài đặt

Copy **toàn bộ** nội dung trong khung dưới đây, dán vào đoạn chat mới với Muse của bạn và gửi. Không cần sửa bất cứ chữ nào.

```text
Hãy xây cho tôi một ứng dụng web tên là "Phòng Điều Hành Multi Agent Company" — phòng điều hành trực quan cho đội AI Agent của tôi, gồm:

(1) Đội agent mặc định 6 người: Điều Phối (tổng điều phối, màu cyan #22D3EE), Bán Hàng (tư vấn & chốt đơn, #FBBF24), Content (nội dung & bài viết, #34D399), Video (sản xuất video, #FB7185), Chăm Sóc (chăm sóc khách hàng, #38BDF8), Nghiên Cứu (nghiên cứu thị trường, #FB923C). Mỗi agent có biểu tượng robot vẽ riêng theo vai trò, KHÔNG dùng chữ viết tắt trong vòng tròn. Cho phép thêm/sửa/xoá agent và đổi màu.

(2) Màn hình chính kiểu "trung tâm tín hiệu": agent Điều Phối ở trung tâm, các agent còn lại trên vòng quỹ đạo, đường nối phát sáng; agent đang làm thì nhánh nối tới agent đó có luồng sáng/sao chổi chạy liên tục từ trung tâm tới agent, node agent nhấp nháy phát sáng và zoom nhẹ; giao diện tối màu navy, nhiều màu neon, kính mờ, vòng tròn liền mạch mượt mà (không nét đứt), hiệu ứng đẳng cấp, nhìn realtime đã mắt.

(3) Dải số liệu thật trên cùng và "Đường ray giai đoạn" Hàng chờ → Đang làm → Chờ duyệt → Hoàn thành: khi một việc chuyển giai đoạn phải có xung ánh sáng chạy dọc đường ray tới giai đoạn mới, node Hoàn thành bùng sáng khi có việc được duyệt xong.

(4) Bảng quản lý việc 4 cột Hàng chờ / Đang làm / Chờ duyệt / Hoàn thành: tạo việc, giao việc cho agent, chuyển trạng thái, nộp kết quả vào Chờ duyệt, và chỉ người dùng mới duyệt chuyển sang Hoàn thành hoặc yêu cầu làm lại.

(5) Thanh ra lệnh: người dùng gõ một lệnh, Điều Phối tự chia thành việc con giao cho các agent, các agent chạy THẬT ở nền và nộp sản phẩm thật vào cột Chờ duyệt (không mô phỏng), có dòng sự kiện/bước chạy realtime và báo cáo tổng hợp cuối cùng chờ duyệt.

(6) Ứng dụng phải lưu được dữ liệu (việc, agent, sự kiện, lượt chạy) trong môi trường Muse của tôi, tự làm mới vài giây một lần để xem realtime, giao diện tiếng Việt, dùng tốt trên điện thoại.

Sau khi xây xong, hãy bật thêm quy tắc làm việc: mỗi việc tôi giao trong chat, bạn đồng thời ghi lên Phòng Điều Hành theo diễn biến thật (tạo việc → Đang làm khi bắt đầu → Chờ duyệt kèm kết quả khi xong), cập nhật ngay tại từng bước để tôi mở là thấy realtime.
```

> [!TIP]
> Nếu Muse của bạn hỏi thêm điều gì trong lúc xây, cứ trả lời ngắn gọn theo đúng nhu cầu của bạn. Xây xong, hãy thử ngay một lệnh nhỏ để kiểm tra workflow chạy thật trước khi giao việc lớn.

---

## Phần 4 — Lưu ý và tuỳ biến

### Tuỳ biến theo mô hình kinh doanh của bạn

Phòng Điều Hành là khung làm việc, không phải khuôn cứng. Bạn hoàn toàn có thể:

- **Đổi tên và vai trò agent** cho khớp với công việc của mình, ví dụ thêm agent Kế Toán, agent Tuyển Dụng, agent Livestream…
- **Đổi màu** từng agent để dễ nhận diện.
- **Thêm hoặc xoá agent** khi đội của bạn lớn lên hoặc thu gọn lại.

Đội 6 agent mặc định chỉ là điểm khởi đầu tốt cho hầu hết mô hình kinh doanh một người.

### Nguyên tắc duyệt: việc quan trọng luôn dừng ở Chờ duyệt

Hãy giữ nguyên tắc này ngay từ ngày đầu:

- Việc **đăng bài, gửi tin nhắn cho khách, cam kết về giá, đơn hàng, thanh toán hay lịch học** luôn phải dừng ở cột **Chờ duyệt** để chính bạn xem và chốt.
- AI Agent làm nhanh và làm nhiều, nhưng **quyền quyết định cuối cùng là của bạn**. Đừng cấu hình cho bất kỳ agent nào tự ý chuyển những việc như vậy sang Hoàn thành.

### Về bản chuyển giao này

Đây là bản chuyển giao phục vụ học tập trong **chương trình Multi Agent Company của Nguyễn Anh Tuấn**, dành cho học viên của chương trình sử dụng với tài khoản Muse của riêng mình. Chúc bạn sớm có một "công ty một người" vận hành trơn tru với đội AI Agent của chính bạn.
