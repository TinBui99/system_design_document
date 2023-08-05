# system_design_document
Tài liệu thiết kế hệ thống 
> Link bài viết: https://viblo.asia/p/bai-dich-thiet-ke-he-thong-cho-hang-trieu-nguoi-dung-ByEZkA7W5Q0

**Thiết kế hệ thống đơn (single server setup)**
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://images.viblo.asia/f9bb47f5-a345-49b7-8760-47c9825e2ecf.png">
  <source media="(prefers-color-scheme: light)" srcset="https://images.viblo.asia/f9bb47f5-a345-49b7-8760-47c9825e2ecf.png">
  <div align="center">
    <img style="border: 5px solid green" width="500px" alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://images.viblo.asia/f9bb47f5-a345-49b7-8760-47c9825e2ecf.png">
</div>  
</picture>

**Tiến trình xử lý**
1. User truy cập website thông qua địa chỉ api.mysite.com, địa chỉ này được gửi tới DNS
> DNS (Domain Name System): có nhiệm vụ phân giải địa chỉ dạng chữ sang dạng IP. DNS thường là dịch vụ trả phí bên thứ 3 và không được đặt ở server của chúng ta.
2. Địa chỉ IP (ở đây là 15.125.23.214) được trả về cho thiết bị của user
3. Sau khi có được địa chỉ IP, 1 HTML request sẽ được gửi đến web server
4. Web server thực hiện quá trình xử lý và trả về user device một reponse dạng JSON hoặc HTML page.

**Nguồn lưu lượng truy cập (traffic source)** 
<br>Nguồn lưu lượng truy cập đến từ 2 nguồn: web app và mobile app
  - Web app: sử dụng ngôn ngữ server-side (Java, PHP, Python,...) để xử lý dữ liệu và ngôn ngữ client-side (HTML, JS,...) để hiển thị.
  - Mobile app: sử dụng API (thường là format JSON) để transfer data vs Web app

**Database**
<br>
Khi số lượng user tăng lên, 1 web server không đủ để đáp ứng. Ví vậy cần có thêm 1 database server để có thể dễ dàng mở rộng hệ thống.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://images.viblo.asia/41684f83-42df-4b61-a03d-fd93781ceef7.png">
  <source media="(prefers-color-scheme: light)" srcset="https://images.viblo.asia/41684f83-42df-4b61-a03d-fd93781ceef7.png">
  <div align="center">
    <img style="border: 5px solid green" width="500px" alt="Shows an illustrated sun in light mode and a moon with stars in dark mode." src="https://images.viblo.asia/41684f83-42df-4b61-a03d-fd93781ceef7.png">
</div>  
</picture>

**Chọn Database**
<br>
Có thể chọn database language SQL và NoSQL
- CSDL SQL (còn gọi là  RDBMS (Relational database management system)):
  MySQL, Oracle, PostgreSQL,…
  Lưu trữ dữ liệu trong các table và hàng. Có thể thực hiện JOIN các table.
- CSDL NoSQL: MongoDB, Cassandra, Neo4j, Redis,… Có 4 loại cơ sở dữ liệu phi quan hệ là: dạng key-value, hướng tài liệu (document), hướng cột (column) và hướng đồ thị (graph). Thao tác join không được hỗ trợ trong NoSQL.

 >Với hầu hết dev, SQL là lựa chọn tốt hơn bởi vì nó đã có hơn 40 năm phát triển, nó có nhiều tài liệu và cộng đồng lớn mạnh. Tuy nhiên, trong các trường hợp đặc biệt ta có thể chọn NoSQL thay thế. Vd như:
>- Ứng dụng yêu cầu độ trễ rất thấp. 
>- Dữ liệu phi cấu trúc hoặc không có quan hệ với nhau.
>- Bạn chỉ cần serialize và deserialize dữ liệu (JSON, XML,…)
>- Bạn cần lưu trữ một lượng dữ liệu khổng lồ.
 
**Mở rộng hệ thống scale up và scale out**
- Scale up: mở rộng hệ thống bằng cách thêm phần cứng (RAM, CPU,...) vào server
  - Ưu điểm: giải quyết nhanh vấn đề mở rộng hệ thống khi lượng user tăng
  - Nhược điểm:
    - Không thể thêm vô hạn phần cứng vào server
    - Không có chuyển đổi tự động và dự phòng. Nếu 1 server ngừng hoạt động thì web app và mobile app sẽ sập hoàn toàn
    - Scale out phù hợp vs app hơn là scale up
- Scale out: thêm nhiều hơn 1 server vào nguồn tài nguyên


