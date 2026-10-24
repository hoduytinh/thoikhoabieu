# Thời khóa biểu học sinh — GitHub Pages + JSON

Bản demo tĩnh, không dùng Firebase. Dữ liệu chung lưu trong `timetable.json`; người có quyền sửa đăng nhập bằng tài khoản cấu hình trong `index.html`, nhập GitHub Fine-grained Personal Access Token khi lưu.

## Trước khi dùng

1. Trong `index.html`, sửa `FIXED_USERS`: đổi toàn bộ username/password mẫu.
2. Sửa `GITHUB.owner`, `GITHUB.repo`, `GITHUB.branch`, `GITHUB.path` cho đúng repository và file JSON.
3. Đảm bảo `timetable.json` nằm ở thư mục gốc của website được xuất bản.
4. Đẩy hai file `index.html` và `timetable.json` lên nhánh được GitHub Pages dùng.
5. Vào Settings → Pages để bật triển khai. Tài khoản GitHub Free chỉ hỗ trợ Pages từ repository public; dùng repository private cần gói hỗ trợ phù hợp. Dù repository nguồn private, website Pages thường vẫn công khai trên Internet trừ một số cấu hình Enterprise.
6. Tài khoản cần ghi dữ liệu: tạo Fine-grained Personal Access Token, giới hạn vào đúng repository, cấp Repository permissions → Contents: Read and write. Không cấp quyền rộng hơn cần thiết.
7. Đăng nhập trên website → “Cấu hình token GitHub” → dán token → “Lưu trong phiên”. Token chỉ lưu trong `sessionStorage` của tab hiện tại, không nằm trong file HTML. Đóng tab sẽ xóa token khỏi phiên đó.

## Tài khoản mẫu — PHẢI ĐỔI

- `admin` / `change-me-admin`
- `parent1` / `change-me-parent1`
- `student1` / `change-me-student1`
- `student2` / `change-me-student2`

Các tài khoản này chỉ là khóa giao diện. Mật khẩu được đưa vào JavaScript phía client và có thể bị xem bởi người truy cập website. Không dùng cho dữ liệu nhạy cảm.

## Lưu ý về đồng bộ

- Người xem tải `timetable.json` từ website Pages khi mở trang và tự kiểm tra mỗi 60 giây; có thể bấm “Đồng bộ”.
- Người sửa thay đổi bản nháp cục bộ rồi bấm “Lưu & đồng bộ lên GitHub”.
- Ghi dữ liệu cần GitHub token; token không được nhúng vào mã nguồn.
- Mỗi lần lưu tạo một commit trong repository.
- Sau khi cập nhật file trên nhánh nguồn, GitHub Pages cần thời gian để triển khai lại. Vì vậy, tự kiểm tra 60 giây không đảm bảo mọi người thấy thay đổi ngay sau khi commit.
- Nếu người khác đã cập nhật phiên bản JSON, ứng dụng phát hiện revision khác nhau và từ chối ghi đè mù quáng.

## Giới hạn bảo mật — đọc kỹ

1. Đăng nhập cố định ở frontend không phải xác thực bảo mật. Người biết mã có thể đọc mật khẩu và bỏ qua kiểm tra giao diện.
2. Không nhúng GitHub token vào `index.html`, repository, query string hoặc file JSON. Token chỉ nhập tại thời điểm chạy và giữ trong `sessionStorage`; vẫn không nên dùng trên thiết bị công cộng.
3. GitHub Pages từ repository private không có nghĩa nội dung website được bảo vệ. Các file được xuất bản, bao gồm `timetable.json`, có thể truy cập công khai nếu Pages site là public.
4. Nếu cần dữ liệu riêng tư thực sự hoặc cần giới hạn ai được ghi, cần dịch vụ trung gian có xác thực phía server; cấu hình hiện tại không đáp ứng mức đó.
5. Không lưu thông tin nhạy cảm của học sinh. Hãy dùng repository thử nghiệm trước khi đưa lịch thật lên.
