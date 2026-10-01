# Music Streaming Platform (tên tạm, chưa chốt)

Web nghe nhạc kiểu Spotify. Thư mục này tạo ngày 2026-10-01 để lưu lại ý tưởng/quyết định qua các session, tránh mất ngữ cảnh khi đóng terminal.

## Ràng buộc quan trọng
Không thể phát nhạc có bản quyền của ca sĩ/hãng thu âm lớn (Universal, Sony, Warner...) — chi phí license quá lớn, cá nhân/startup nhỏ không license được, tự ý stream là vi phạm pháp luật (DMCA, kiện tụng). Vì vậy hướng đi là học **kiến trúc kỹ thuật** của Spotify (streaming, playlist, recommendation) nhưng áp dụng cho nội dung mà mình **có quyền phát**.

## 3 hướng đang cân nhắc (chưa chốt)
1. **Nền tảng cho nghệ sĩ độc lập/indie** (kiểu BandCamp/SoundCloud thu nhỏ) — nghệ sĩ tự upload nhạc gốc, nền tảng lo streaming/playlist/gợi ý, ăn chia doanh thu hoặc subscription. Né được vấn đề bản quyền vì nghệ sĩ tự chịu trách nhiệm nội dung, cần cơ chế DMCA takedown.
2. **Nhạc royalty-free/nhạc nền cho creator** (kiểu Epidemic Sound) — bán license nhạc nền cho YouTuber/TikToker, mô hình subscription rõ ràng.
3. **Audio platform cho podcast/audiobook tiếng Việt** — thị trường ít người làm tốt ở VN, dùng chung hạ tầng streaming audio.

Hướng 1 gần với use-case "giống Spotify" nhất.

## Thách thức kỹ thuật cốt lõi (áp dụng cho mọi hướng)
- **Streaming audio** — không phát nguyên file, cần transcode ra HLS/DASH + CDN.
- **Recommendation/playlist cá nhân hoá** — cần dữ liệu hành vi nghe đủ lớn mới có ý nghĩa.
- **Bảo mật nội dung** — dùng signed URL có thời hạn để tránh người dùng tải lậu file nhạc trực tiếp.

## Checklist bảo mật cần áp dụng khi build (rút từ thảo luận trước)
- Secret key (API key, service role key) chỉ nằm ở server, không bao giờ lộ ra client.
- Bật RLS / security rules cho mọi bảng database, test bằng 2 tài khoản khác nhau trước khi launch.
- Mọi API tự kiểm tra quyền ở server, không dựa vào việc ẩn UI.
- Dùng auth library có sẵn (NextAuth, Supabase Auth, Clerk...), không tự viết hệ thống đăng nhập.
- Rate limit cho login, upload, API tốn phí.
- HTTPS bắt buộc, tắt debug mode ở production.
- Giá tiền/logic thanh toán tính lại ở server, không tin dữ liệu từ client.
- File nhạc upload: giới hạn loại file + dung lượng, lưu ở storage riêng không chạy được code.

## Việc cần quyết tiếp theo
- [ ] Chốt 1 trong 3 hướng (hoặc hướng khác)
- [ ] Đặt tên dự án chính thức, đổi tên thư mục nếu cần
- [ ] Chọn stack (frontend/backend/database/storage/CDN)
- [ ] Đặc tả tính năng MVP
