Vai trò của UserDetailsService và PasswordEncoder trong Spring Security

UserDetailsService:

Là interface trung tâm để Spring Security lấy thông tin người dùng từ nguồn dữ liệu (database, LDAP, API…).

Khi người dùng đăng nhập, Spring Security gọi loadUserByUsername() để truy xuất thông tin UserDetails (username, mật khẩu, roles).

Nhờ đó, hệ thống có thể xác thực và phân quyền dựa trên dữ liệu thực tế trong DB, thay vì user cứng trong bộ nhớ.

PasswordEncoder:

Đảm nhiệm việc mã hóa và kiểm tra mật khẩu.

Khi người dùng nhập mật khẩu, Spring Security dùng PasswordEncoder.matches(rawPassword, encodedPassword) để so sánh với mật khẩu đã lưu trong DB.

Đảm bảo mật khẩu không bao giờ được lưu hoặc xử lý dưới dạng plain text.

 Nguy hiểm khi lưu mật khẩu plain text hoặc dùng NoOpPasswordEncoder

Nếu database bị lộ, hacker có ngay toàn bộ mật khẩu thật của người dùng.

Người dùng thường tái sử dụng mật khẩu cho nhiều dịch vụ → nguy cơ lan truyền sang email, ngân hàng, mạng xã hội.

Dù database có firewall, VPN, IDS/IPS… thì một lỗ hổng SQL Injection hoặc rò rỉ nội bộ vẫn khiến dữ liệu plain text trở thành thảm họa.

 Tại sao nên dùng BCryptPasswordEncoder

BCrypt là thuật toán mã hóa mật khẩu hiện đại, có cơ chế salt ngẫu nhiên để chống rainbow table.

Có thể cấu hình độ phức tạp (strength) để tăng chi phí tính toán, làm chậm brute-force.

Được Spring Security hỗ trợ mặc định, dễ tích hợp và được khuyến nghị rộng rãi trong các ứng dụng web hiện đại.