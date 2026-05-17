# MEMORY.md

> **LƯU Ý:** File này CHỈ GHI THÊM, KHÔNG ĐƯỢC XÓA. Dùng để lưu trữ toàn bộ bối cảnh, lịch sử, lỗi đã gặp và quyết định kiến trúc.

## 2026-05-14: Khởi tạo và Phân tích Moodle-Docker

**Tác dụng của Repository `moodle-docker`:**
Repository này cung cấp một môi trường Docker được cấu hình sẵn để phục vụ cho việc phát triển và kiểm thử hệ thống Moodle.

**Công nghệ & Tính năng:**
- Hỗ trợ đầy đủ các hệ quản trị cơ sở dữ liệu phổ biến (PostgreSQL, MySQL, Microsoft SQL Server, Oracle).
- Tích hợp Behat và Selenium (Chrome/Firefox) cho mục đích tự động hoá kiểm thử giao diện (Automated Testing).
- Tích hợp Mailpit (như một catch-all SMTP server và có giao diện web) để test tính năng gửi nhận email của Moodle.
- Các PHP Extensions được cấu hình sẵn phục vụ cho dịch vụ bên ngoài (solr, ldap).

**Giải quyết Usecase:**
- Thiết lập nhanh môi trường test/dev mà không cần tự build từ đầu.
- Hỗ trợ kiểm thử ứng dụng Moodle Mobile.
- Dùng cho manual testing và chạy automated scripts (PHPUnit, Behat) ổn định.

**Quyết định kỹ thuật đã thực hiện:**
- Gộp các cấu hình (base.yml, db.pgsql.yml, service.mail.yml, webserver.port.yml) thành một file `docker-compose.yml` duy nhất. 
- Thiết lập cho chạy PostgreSQL và PHP 8.3 mặc định.
- Cho phép start toàn bộ project chỉ bằng 1 lệnh `docker compose up -d`.

## 2026-05-17: Khắc phục lỗi tương thích và tối ưu tốc độ
**Các lỗi đã gặp và cách xử lý:**
1. **Lỗi `tables already present` và sai mật khẩu:** Lệnh cài đặt DB có thể đã được chạy một phần từ trước với mật khẩu mặc định là `test`, do đó lệnh gán mật khẩu mới `m@0dl3ing` bị bỏ qua. 
   - Giải pháp: Chạy script CLI `reset_password.php` để ép đổi lại mật khẩu.
2. **Lỗi PHP version không tương thích:** Moodle 4.3 (bản STABLE clone về) chỉ hỗ trợ tối đa PHP 8.2. Môi trường mặc định chạy PHP 8.3 khiến webserver báo lỗi Fatal. 
   - Giải pháp: Hạ image php trong `docker-compose.yml` từ `8.3` xuống `8.2`.
3. **Lỗi giao diện lag, tràn ngập text log:** Bản chất repo này bật sẵn `Developer Debugging` (`debug`, `perfdebug`, `debugpageinfo`). 
   - Giải pháp: Cập nhật `config.php` để gán toàn bộ flag debug về `0`, giúp trang load mượt mà (<1s) như Production.
