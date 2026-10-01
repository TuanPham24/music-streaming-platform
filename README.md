# Music Streaming Platform

Nền tảng nghe nhạc trực tuyến lấy cảm hứng từ Spotify, tập trung xây dựng lại các bài toán kỹ thuật cốt lõi của một hệ thống streaming audio hiện đại: phát nhạc theo thời gian thực, quản lý playlist, và gợi ý nội dung cá nhân hoá.

> 🚧 Dự án đang trong giai đoạn phát triển ban đầu.

## Tính năng định hướng

- **Streaming audio thời gian thực** — phát nhạc qua HLS/DASH kết hợp CDN, không phát trực tiếp file gốc.
- **Playlist & thư viện cá nhân** — tạo, chỉnh sửa, chia sẻ playlist.
- **Gợi ý cá nhân hoá** — đề xuất bài hát/playlist dựa trên hành vi nghe.
- **Bảo mật nội dung** — truy cập file media qua signed URL có thời hạn, tránh tải lậu trực tiếp.

## Nguyên tắc kỹ thuật

- Mọi secret key (API key, service role key...) chỉ tồn tại ở server, không lộ ra client.
- Áp dụng row-level security / access rules cho toàn bộ dữ liệu, kiểm tra quyền ở từng API.
- Dùng giải pháp auth đã được kiểm chứng (NextAuth, Supabase Auth, Clerk...) thay vì tự xây hệ thống đăng nhập.
- Rate limiting cho các endpoint nhạy cảm (đăng nhập, upload, API tốn tài nguyên).
- Bắt buộc HTTPS, tắt debug mode ở production.
- Logic thanh toán/giá luôn được tính và xác thực lại ở server.
- File media upload được giới hạn loại/dung lượng và lưu ở storage cách ly, không thực thi được code.

## Stack

Đang trong quá trình lựa chọn và sẽ được cập nhật khi kiến trúc được chốt.

## Trạng thái

Dự án mới khởi tạo, các tính năng ở trên là mục tiêu kỹ thuật dài hạn, chưa phải checklist đã hoàn thành.
