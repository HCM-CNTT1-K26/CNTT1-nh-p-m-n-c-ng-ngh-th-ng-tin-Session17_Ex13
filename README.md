# CNTT1-nh-p-m-n-c-ng-ngh-th-ng-tin-Session17_Ex13
### **Phần A – Profile & Bookmark**

1. **Xung đột Session:** Dùng chung 1 `User Data` làm đè Cookie của domain `github.com`. Kết quả là tài khoản cá nhân bị văng (Logout) hoặc push code nhầm danh tính.
2. **Mô hình 3 Profile:**
* `Dev_Personal`: Mail, mảng xã hội, GitHub cá nhân.
* `Dev_CompanyWork`: GitHub công ty, Jira, Slack, web nội bộ.
* `Dev_Sandbox`: Test app, môi trường thử nghiệm, test extension.


3. **Cấu trúc Bookmark:** `01_Company_Internal`, `02_Dev_Tools`, `03_Docs_Reference`.
4. **Mượn máy:** Mở **Guest Profile** vì nó cô lập hoàn toàn môi trường, không dính tới Bookmark/History/Cookie của máy và tự xóa sạch khi tắt.

---

### **Phần B – Extensions**

1. **Nhóm tiện ích:** Chọn **Dev Suite** (tiện ích **JSON Formatter**). Hai nhóm *Productivity* và *Security* không chọn vì chỉ làm việc quản lý task hoặc bảo mật, không hỗ trợ parse/format dữ liệu JSON thô.
2. **Quyền Site Access:** Chọn **On click** (áp dụng chuẩn Least Privilege) để tránh extension đọc ngầm dữ liệu trên các trang khác.

---

### **Phần C – HTTP Request Flow**

1. **4 Giai đoạn xử lý:** DNS Lookup $\rightarrow$ TCP/TLS Handshake $\rightarrow$ HTTP Request & Processing $\rightarrow$ HTTP Response & DOM Rendering.
2. **Phân tích Mã trạng thái:**
* **404 Not Found:** Lỗi do Client gõ sai URL hoặc rớt route $\rightarrow$ *Debug:* Sửa lại đường dẫn API/file tĩnh.
* **500 Internal Server Error:** Lỗi phía Server (crash code backend) $\rightarrow$ *Debug:* Đọc kĩ Response Body và check log Server.


3. **Tab xem mã trạng thái:** Tab **Network** (vì các tab Elements, Console, Application không chuyên quản lý luồng truyền nhận Request/Response).

---

### **Phần D – Cache & Cookies**

1. **Dính Cache CSS:** Do trình duyệt vẫn load file cũ từ Browser Cache $\rightarrow$ *Xử lý:* Mở DevTools (F12), chuột phải vào biểu tượng Reload chọn **Empty Cache and Hard Reload**.
2. **Thiếu HttpOnly:** Dễ bị dính lỗi **XSS (Cross-Site Scripting)**. Kẻ gian dùng đoạn code JS `document.cookie` để lấy mất `session_id` và chiếm phiên đăng nhập.
3. **Chỉ xóa Cookie:** F12 $\rightarrow$ tab **Application** $\rightarrow$ mục **Cookies** $\rightarrow$ nhấp chuột phải xóa riêng dòng `session_id` của domain đó.

---

### **Phần E – Kỹ năng Debug DevTools**

1. **Test màu nút:** Bấm `Ctrl + Shift + C` click vào nút $\rightarrow$ nhìn sang tab **Elements** $\rightarrow$ khung **Styles** bên dưới rồi đổi trực tiếp mã màu HEX để xem trước.
2. **4 bước Debug API lỗi (dòng đỏ):**
* *Bước 1 (Identify):* Nhìn cột Status xem mã lỗi $4xx$ hay $5xx$.
* *Bước 2 (Inspect):* Check URL, Method, Payload trong tab **Headers**.
* *Bước 3 (Analyze):* Đọc thông báo lỗi cụ thể ở tab **Response**.
* *Bước 4 (Action):* Lỗi $4xx$ tự chỉnh lại client; lỗi $5xx$ văng log cho phía Backend.


3. **Lọc API & Bypass Cache:** Bật filter **Fetch/XHR** và tích chọn ô **Disable cache** trên tab Network.
