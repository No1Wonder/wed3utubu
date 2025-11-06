<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6fc86ab0-3cb9-468b-85f8-70b46302bf9b" />Yêu cầu     : LẬP TRÌNH ỨNG DỤNG WEB trên nền linux
1. Cài đặt môi trường linux: SV chọn 1 trong các phương án
 - enable wsl: cài đặt docker desktop
 - enable wsl: cài đặt ubuntu
 - sử dụng Hyper-V: cài đặt ubuntu
 - sử dụng VMware : cài đặt ubuntu
 - sử dụng Virtual Box: cài đặt ubuntu
2. Cài đặt Docker (nếu dùng docker desktop trên windows thì nó có ngay)
3. Sử dụng 1 file docker-compose.yml để cài đặt các docker container sau: 
   mariadb (3306), phpmyadmin (8080), nodered/node-red (1880), influxdb (8086), grafana/grafana (3000), nginx (80,443)
4. Lập trình web frontend+backend:
 SV chọn 1 trong các web sau:
 4.1 Web thương mại điện tử
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - Có tính năng liệt kê các sản phẩm bán chạy ra trang chủ
 - Có tính năng liệt kê các nhóm sản phẩm
 - Có tính năng liệt kê sản phẩm theo nhóm
 - Có tính năng tìm kiếm sản phẩm
 - Có tính năng chọn sản phẩm (đưa sản phẩm vào giỏ hàng, thay đổi số lượng sản phẩm trong giỏ, cập nhật tổng tiền)
 - Có tính năng đặt hàng, nhập thông tin giao hàng => được 1 đơn hàng.
 - Có tính năng dành cho admin: Thống kê xem có bao nhiêu đơn hàng, call để xác nhận và cập nhật thông tin đơn hàng. chuyển cho bộ phận đóng gói, gửi bưu điện, cập nhật mã COD, tình trạng giao hàng, huỷ hàng,...
 - Có tính năng dành cho admin: biểu đồ thống kê số lượng mặt hàng bán được trong từng ngày. (sử dụng grafana)
 - backend: sử dụng nodered xử lý request gửi lên từ javascript, phản hồi về json.
 4.2 Web IOT: Giám sát dữ liệu IOT.
 - Tạo web dạng Single Page Application (SPA), chỉ gồm 1 file index.html, toàn bộ giao diện do javascript sinh động.
 - Có tính năng login, lưu phiên đăng nhập vào cookie và session
   Thông tin login lưu trong cơ sở dữ liệu của mariadb, được dev quản trị bằng phpmyadmin, yêu cầu sử dụng mã hoá khi gửi login.
   Chỉ cần login 1 lần, bao giờ logout thì mới phải login lại.
 - hiển thị giá trị mới nhất của các thông số đang giám sát, khi click vào thì hiển thị đồ thị lịch sử quá trình thay đổi (gọi grafana iframe để hiển thị)
 - backend: Sử dụng nodered để đọc dữ liệu từ các cảm biến (có thể dùng api online để lấy dữ liệu theo giời gian thực), 
   nodered sẽ lưu dữ liệu mới nhất (dạng update) vào cơ sở dữ liệu mariadb (sử dụng phpmyadmin để tạp table và quản trị lần đầu)
   nodered sẽ lưu dữ liệu (insert) vào influxdb để lưu giá trị lịch sử, để cho grafana dùng để hiển thị biểu đồ.
5. Nginx làm web-server
 - Cấu hình nginx để chạy được website qua url http://fullname.com  (thay fullname bằng chuỗi ko dấu viết liền tên của bạn)
 - Cấu hình nginx để http://fullname.com/nodered truy cập vào nodered qua cổng 80, (dù nodered đang chạy ở port 1880)
 - Cấu hình nginx để http://fullname.com/grafana truy cập vào grafana qua cổng 80, (dù grafana đang chạy ở port 3000)  
  
  ## CÀI ĐẶT MÔI TRƯỜNG LINUX
  # phương án cài đặt WSL2 - utubu
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/21f7d290-44c8-410e-9062-d843d73e0e04" />

  @ cập nhật utubu
  <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6fdaaae6-5e7b-4e83-8238-39758588fe1b" />
# sau khi cài đặt ta có
<img width="666" height="193" alt="Screenshot 2025-11-05 152829" src="https://github.com/user-attachments/assets/d104af20-7e8e-46f9-bd0d-caac7f4e99c0" />

# tải các extention thêm

<img width="1664" height="769" alt="Screenshot 2025-11-05 160518" src="https://github.com/user-attachments/assets/b3ac78b6-73c6-4320-b107-82acb49316bf" />

## thiết kế web phương án 4.1

# tạo cơ sở dữ liệu
 


## em xin phép thầy rằng là bài này em quá yếu và thiết bị của e xuất hiện quá nhiều lỗi với nahu dẫn đến hiện tại em không setup đc nodered và nginx để hiện host cho bài tập
## em đã setup môi trường đủ nhưng do lỗi ẩn ở bt 2 hoặc những bt trước dẫn đến giờ máy em mỗi khi truy cập vào các truy cập admin đều dẫn đến màn hình xanh và không thể làm bài cũng như setup đc 
## hiện tại 22h 6/11/2025 em vẫn đang cố kahcs phục để kịp tiến đọ mặc dù e biết sẽ ko đảm bảo hoàn thiện ạ
## và em ko hiểu sao mỗi khi em treo 1 lúc nodered em bị reset và ko đăng nhập tại tk mk được em cũng đang phải fix nó :< 
![Uploading Screenshot (561).png…]()


## em bất lực r 




  
