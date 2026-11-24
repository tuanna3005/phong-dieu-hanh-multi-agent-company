# Đặc tả kỹ thuật — Phòng Điều Hành Multi Agent Company

*Bản hiện tại, cập nhật ngày 24/11/2026. Tài liệu này mô tả đầy đủ ứng dụng Phòng Điều Hành Multi Agent Company đúng trạng thái đang chạy, đủ chi tiết để một trợ lý Muse khác dựng lại một bản tương đương chạy thật (web app fullstack có lưu dữ liệu) trong môi trường Muse của người nhận. Đây là tài liệu đi kèm `PROMPT-CAI-DAT.txt` (prompt để dán cho Muse tự xây) và `README.md` (hướng dẫn cho học viên).*

## 1. Mục đích và tổng quan

Phòng Điều Hành vừa là **công cụ quản lý công việc** của một đội AI Agent, vừa là **màn hình theo dõi realtime**: người dùng (gọi là "sếp") ra lệnh và nhìn thấy workflow chạy trực tiếp — lệnh đi qua agent nào, agent nào đang làm gì, việc nào vừa xong — thay vì một bảng việc tĩnh.

Ứng dụng gồm 5 khối trên một màn hình chính:

1. **Dải số liệu (stats strip)** ở trên cùng: số liệu thật của toàn hệ thống (số agent, số việc theo trạng thái, số lượt chạy...), trình bày dạng viên kính, số chạy count-up khi thay đổi, có chấm pulse ở chỉ số realtime.
2. **Sàn agent (agent floor)**: agent Điều Phối ở trung tâm (hub), các agent còn lại xếp quanh; mỗi agent là một quả cầu kính robot có màu riêng và biểu tượng robot vẽ riêng theo vai trò; đường nối từ hub tới từng agent; agent đang làm có hiệu ứng thở/zoom và hạt sáng bay quanh quỹ đạo; nhánh đang chạy có dòng sáng chảy (đốm sáng di chuyển kèm vệt mờ dần kiểu sao chổi) từ hub tới agent đó.
3. **Đường ray giai đoạn (StageRail)**: Hàng chờ → Đang làm → Hoàn thành, dạng track phát sáng; khi một việc chuyển giai đoạn, một xung sáng chạy dọc đường ray tới node giai đoạn mới; node Hoàn thành bùng sáng khi có việc hoàn tất.
4. **Bảng kanban 3 cột**: Hàng chờ (queued) / Đang làm (working) / Hoàn thành (done), kính mờ, thẻ việc có viền trái theo màu agent phụ trách, hover nhấc nhẹ, chuyển cột có chuyển động mượt. Thẻ việc hiển thị tiêu đề, chi tiết rút gọn, agent phụ trách (màu + biểu tượng), mức ưu tiên và văn bản kết quả khi đã xong.
5. **Thanh ra lệnh (command bar) + dòng sự kiện (activity feed)**: thanh ra lệnh để sếp gõ lệnh cho Điều Phối; dòng sự kiện hiển thị timeline phát sáng của mọi hoạt động (tạo việc, giao việc, từng bước chạy, hoàn thành...) theo thời gian thực.

Ứng dụng **tự làm mới khoảng mỗi 4 giây** để mọi thay đổi hiện realtime. Giao diện tiếng Việt, dùng tốt trên điện thoại (không tràn ngang ở bề rộng điện thoại ngoài một khối trang trí nội bộ bị cắt có chủ ý).

## 2. Đội agent mặc định (dữ liệu hạt giống)

Khi dựng mới, tạo sẵn 11 agent sau (id cố định theo thứ tự này vì giao thức đồng bộ chat tham chiếu theo id):

| ID | Tên | Vai trò | Màu | Chuyên môn |
|----|-----|--------|-----|-----------|
| 1 | Điều Phối | Tổng điều phối | Cyan #22D3EE | Nhận việc từ sếp, chia nhỏ và giao cho đúng agent, tổng hợp kết quả cuối cùng |
| 2 | Bán Hàng | Tư vấn & chốt đơn | Vàng #FBBF24 | Soạn kịch bản tư vấn, trả lời khách, xử lý câu hỏi về giá và đăng ký |
| 3 | Content | Nội dung & bài viết | Ngọc lục #34D399 | Viết bài Facebook, kịch bản video, caption và nội dung truyền thông |
| 4 | Video | Sản xuất video | Hồng #FB7185 | Dựng kịch bản cảnh, tạo clip quảng cáo và ghép video hoàn chỉnh |
| 5 | Chăm Sóc | Chăm sóc khách hàng | Xanh trời #38BDF8 | Theo dõi học viên, nhắc lịch, giải đáp thắc mắc sau bán hàng |
| 6 | Nghiên Cứu | Nghiên cứu thị trường | Cam #FB923C | Tìm hiểu đối thủ, xu hướng và ý tưởng nội dung mới cho chương trình |
| 7 | Thiết Kế App | Thiết kế & xây dựng ứng dụng | Tím #A78BFA | Thiết kế, xây dựng và nâng cấp các ứng dụng/webapp của công ty |
| 8 | Vận Hành | Vận hành đăng bài và phân phối nội dung | Xanh lime #A3E635 | Chốt canh giờ đăng bài, hàng chờ đăng nhóm Facebook, bình luận link dưới bài, đối soát lịch đăng Page và nhóm |
| 9 | Email | Email marketing và chăm sóc qua email | Teal #2DD4BF | Chuỗi email bán hàng và chăm sóc, bản tin định kỳ, kịch bản email, tiêu đề thu hút, tỉ lệ mở và tỉ lệ nhấp |
| 10 | Trợ Lý | Trợ lý cá nhân của sếp | Chàm #818CF8 | Sắp xếp lịch và danh sách việc, nhắc hạn quan trọng, tổng hợp thông tin nhanh, chuẩn bị tài liệu và báo cáo ngắn cho sếp |
| 11 | Landing Page | Thiết kế và xây dựng landing page | Hồng #EC4899 | Trang đích chuyển đổi, bố cục bán hàng, tiêu đề và lời kêu gọi hành động, tốc độ tải trang, kết nối form và đo lường chuyển đổi |

Mỗi agent có **biểu tượng robot vẽ riêng theo vai trò** (SVG), tuyệt đối không dùng chữ viết tắt (ĐP, CS...) trong vòng tròn. Người dùng có thể thêm/sửa/xoá agent, đổi tên, vai trò, chuyên môn và màu. Việc của agent bị xoá trở thành chưa gán.

## 3. Mô hình dữ liệu

**Agent**: id, name (tên), role (vai trò), specialty (chuyên môn), color (mã màu hex). Trạng thái bận/rảnh của agent suy ra từ các việc/lượt chạy đang gán cho agent đó.

**Task (việc)**: id, title (tiêu đề, bắt buộc), detail (mô tả chi tiết), priority (mức ưu tiên), agent_id (agent phụ trách, có thể trống), run_id (thuộc lượt chạy nào, nếu việc do một lệnh sinh ra), status, result (văn bản kết quả, nộp khi hoàn thành), mốc thời gian tạo/cập nhật.

- Luồng trạng thái chuẩn của task: `queued` (Hàng chờ) → `working` (Đang làm) → `done` (Hoàn thành). Việc xong là chuyển thẳng sang `done` kèm `result` — **không có bước chờ duyệt**.
- Giá trị `review` vẫn tồn tại ở tầng dữ liệu để tương thích ngược với dữ liệu cũ và được hiển thị trong cột Hoàn thành; luồng vận hành hiện tại không dừng ở trạng thái này.

**Run (lượt chạy)**: một lệnh từ thanh ra lệnh sinh ra một run: id, command (nguyên văn lệnh), status ∈ {running, done} (có thể mở lại về running từ thẻ báo cáo), summary (báo cáo tổng hợp do worker nộp khi hoàn tất — khi nộp, run chuyển thẳng sang done), các step và các task con liên kết bằng run_id.

**Step (bước chạy)**: các mốc diễn biến trong một run: khâu lập kế hoạch, giao việc, ghi chú đang làm, việc con hoàn thành, ghi chú khác — hiển thị trong dòng sự kiện để sếp xem workflow chạy realtime.

**Event (sự kiện)**: bản ghi timeline cho mọi hành động đáng kể (tạo việc, đổi trạng thái, giao việc, tạo agent, hoàn thành...), hiển thị ở dòng sự kiện; bản đọc toàn cục trả về 60 sự kiện gần nhất và tối đa 100 việc gần nhất.

## 4. Các hành động (actions) ứng dụng công bố

Ứng dụng công bố đúng 12 hành động sau cho trợ lý Muse gọi (đây là kênh để agent ghi việc lên Hub từ chat và để worker nền báo cáo):

1. `getboard` — Trả về toàn bộ phòng điều hành: danh sách agent, tối đa 100 việc gần nhất, 60 sự kiện mới nhất. (Không tham số.)
2. `createtask` — Tạo việc, gán agent tuỳ chọn, ghi vào dòng sự kiện. Tham số: `title` (bắt buộc), `detail`, `priority`, `agent_id`, `run_id`.
3. `settaskstatus` — Chuyển việc giữa các trạng thái; chuyển sang done mang theo văn bản kết quả. Tham số: `id`, `status`, `result`.
4. `assigntask` — Giao hoặc giao lại việc cho một agent (hoặc bỏ gán).
5. `deletetask` — Xoá một việc khỏi bảng.
6. `createagent` — Thêm agent mới với tên, vai trò, chuyên môn và màu nhấn.
7. `updateagent` — Sửa tên, vai trò, chuyên môn hoặc màu của agent.
8. `deleteagent` — Xoá agent khỏi đội; các việc của agent đó trở thành chưa gán.
9. `dispatch` — Sếp ra lệnh: tạo một run, yêu cầu Điều Phối chia lệnh thành việc con, và khởi động một **agent worker chạy nền thật** để thực thi, báo tiến độ trực tiếp trong lúc chạy.
10. `addstep` — Ghi một bước trực tiếp của run (kế hoạch, giao việc, ghi chú đang làm, việc con xong, ghi chú) vào dòng sự kiện.
11. `completerun` — Báo cáo cuối của worker nền cho một run: lưu bản tổng hợp và chuyển run **thẳng sang done (Hoàn thành)**.
12. `setrunstatus` — Chuyển run sang done, hoặc mở lại về running từ thẻ báo cáo của run khi cần làm lại.

## 5. Luồng workflow chạy thật (thanh ra lệnh)

Đây là phần "chạy thật", không mô phỏng:

1. Sếp gõ một lệnh vào thanh ra lệnh, ứng dụng gọi `dispatch`: tạo run, Điều Phối chia lệnh thành các việc con (task có run_id), mỗi việc giao đúng agent theo loại việc.
2. Một agent worker chạy nền **thực thi thật** các việc con (làm nội dung, nghiên cứu, chuẩn bị sản phẩm thật tuỳ loại việc), trong lúc chạy dùng `addstep` ghi diễn biến vào dòng sự kiện và `settaskstatus` cập nhật trạng thái từng việc, để màn hình Hub sáng theo đúng nhánh đang chạy.
3. Khi xong, worker gọi `completerun`: nộp báo cáo tổng hợp, run chuyển thẳng sang **Hoàn thành** kèm summary; từng việc con cũng chuyển thẳng sang Hoàn thành kèm kết quả của chúng.
4. Nếu sếp chưa ưng, sếp mở lại run về running (`setrunstatus`) để làm lại — đây là thao tác tuỳ chọn, không phải bước duyệt bắt buộc.

## 6. Chuẩn trình bày hiện hành (bắt buộc khi dựng lại)

Bản gốc đã qua nhiều vòng nâng cấp trình bày; bản dựng lại phải đạt chuẩn này ngay từ đầu:

- **Nền vũ trụ sâu**: navy đậm nhiều lớp, quầng tinh vân aurora rất nhẹ (cyan, tím, ngọc lục bảo) trôi chậm, bầu trời sao li ti nhấp nháy, quầng sáng radial mềm sau hub trung tâm, hạt nhiễu (grain) cực mịn tạo chất liệu cao cấp. Nền phải mượt — cảm giác premium nằm ở chiều sâu và ánh sáng, không phải họa tiết rối.
- **Chữ sang**: font hiển thị hỗ trợ tiếng Việt đầy đủ dấu (ưu tiên **Be Vietnam Pro**), tiêu đề có chữ gradient, số liệu dùng số tabular đều chân, letter-spacing tinh chỉnh, thứ bậc chữ rõ ràng.
- **Viên kính số liệu**: glass capsule có viền gradient mảnh theo màu từng chỉ số, số count-up mượt khi đổi, chấm pulse sống.
- **Quả cầu robot của agent**: kính nhiều lớp có chiều sâu thật — hào quang màu riêng từng agent, điểm sáng specular, cung sáng conic xoay chậm liền mạch khi agent bận; agent đang làm phải thở zoom in/out và có hạt sáng nhỏ bay quanh quỹ đạo. **Không dùng nét đứt (dashed) ở bất cứ đâu** — đây là lỗi từng bị loại bỏ qua 2 vòng sửa.
- **Dòng sáng trên nhánh đang chạy**: đốm sáng di chuyển dọc đường nối kèm vệt mờ dần (sao chổi), nhìn phát biết ngay nhánh nào đang chạy — không chấp nhận kiểu chỉ làm đậm đường kẻ.
- **Đường ray giai đoạn phát sáng**: xung sáng chạy dọc track khi việc chuyển giai đoạn, node đang hoạt động phát sáng theo màu giai đoạn, node Hoàn thành bùng sáng khi có việc hoàn tất.
- **Kanban kính mờ (frosted glass)**: thẻ việc bóng mềm, viền trái theo màu agent, hover nhấc nhẹ, chuyển cột có animation mượt, không nhảy hình. Tiêu đề cột kèm số đếm.

## 7. Giao thức đồng bộ chat → Hub (bật sau khi dựng)

Để agent bên nhận ghi việc từ các cuộc trò chuyện lên Hub giống bản gốc, áp dụng quy tắc sau (đây là thao tác agent làm thủ công trong lúc xử lý tin nhắn, không phải đồng bộ tự động ngầm):

- Mọi việc người dùng giao trong chat đều được tạo trên Hub bằng `createtask`, phân công theo loại việc: Điều Phối = 1, Bán Hàng = 2, Content = 3, Video = 4, Chăm Sóc = 5, Nghiên Cứu = 6, Thiết Kế App = 7, Vận Hành = 8, Email = 9, Trợ Lý = 10, Landing Page = 11.
- Cập nhật **realtime tại từng bước**: tạo việc và chuyển `working` **trước khi** bắt đầu làm; ghi các bước chính trong lúc làm; chuyển thẳng `done` kèm văn bản kết quả ngay khi làm xong — không qua trạng thái chờ duyệt.
- Mọi lịch chạy định kỳ (cron) được tạo cho người dùng cũng phải báo cáo lên Hub theo cùng cách: tạo việc khi bắt đầu, cập nhật khi chạy, chuyển `done` kèm kết quả khi xong.

## 8. Nguyên tắc vận hành đi kèm

- Dữ liệu của Hub là của riêng tài khoản sở hữu; bản dựng mới bắt đầu trắng, chỉ có 11 agent hạt giống ở mục 2 — tuyệt đối không đóng gói dữ liệu vận hành của bất kỳ ai vào bản chuyển giao.
- Việc nhạy cảm (đăng bài, gửi tin cho khách, giá, cam kết, thanh toán) vẫn cần người dùng duyệt ở ngoài Hub theo quy trình riêng của họ; Hub chỉ là nơi ghi và theo dõi việc.
