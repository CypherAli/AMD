## 📜 README.md: URL Shortener Service (Microservices Project)

### 🚀 1. Tổng Quan Dự Án

Đây là dự án phát triển dịch vụ rút gọn URL, được xây dựng theo yêu cầu của Assignment AMD201. Dự án tập trung vào việc áp dụng kiến trúc hiện đại, nguyên tắc DevOps toàn diện, và đảm bảo chất lượng bằng Testing.

**Mục tiêu điểm:** **Mức Merit (7-8.5 điểm)**, với các tính năng bổ sung về quản lý người dùng và tối ưu hiệu suất.

#### Tính năng Chính

  * **Rút gọn URL:** Chuyển đổi URL dài thành mã ngắn duy nhất.
  * [cite\_start]**Chuyển hướng (Redirect):** Chuyển hướng người dùng từ link ngắn sang URL gốc (HTTP 302 Found)[cite: 28, 16].
  * [cite\_start]**Quản lý Người dùng:** Hỗ trợ Đăng nhập/Đăng ký bằng **Firebase Authentication**[cite: 32].
  * [cite\_start]**Lưu trữ thông minh:** Link được lưu vĩnh viễn và cho phép **Custom Code** khi có tài khoản; link dùng thử không lưu khi không đăng nhập[cite: 30, 17].
  * **Mã QR:** Tự động tạo mã QR cho link đã rút gọn.
  * [cite\_start]**API RESTful:** Cung cấp các endpoint để tương tác với dịch vụ[cite: 31].

#### Yêu Cầu Kỹ thuật Bắt buộc

  * [cite\_start]**Containerization:** Ứng dụng Back-end phải được đóng gói bằng **Dockerfile**[cite: 34].
  * [cite\_start]**CI/CD Tự động:** Triển khai Pipeline hoàn chỉnh bằng **GitHub Actions**[cite: 35].
  * [cite\_start]**Testing:** Bắt buộc có **Unit Testing** [cite: 52] [cite\_start]và **Integration Testing**[cite: 52].
  * [cite\_start]**Caching (Merit):** Sử dụng **Redis** để tăng tốc độ truy cập link[cite: 52].
  * [cite\_start]**Tối ưu Deployment (Merit):** Sử dụng **Multi-stage Docker builds** để giảm kích thước image[cite: 52].

-----

### 2\. 🛠️ Công Nghệ Sử Dụng

| Thành Phần | Công Nghệ Chính | Mục Đích |
| :--- | :--- | :--- |
| **Back-end/API** | [cite\_start]C\# / **ASP.NET Core Web API** [cite: 18] | Cung cấp dịch vụ cốt lõi và các Controllers. |
| **Database** | [cite\_start]**EF Core**, SQL Database [cite: 40] | Lưu trữ URL, metadata và thông tin người dùng. |
| **Caching** | **Redis** | [cite\_start]Caching các truy vấn đọc thường xuyên (Merit)[cite: 52]. |
| **Authentication** | **Firebase Authentication** | Quản lý người dùng và phân quyền API. |
| **Front-end (UI)** | [cite\_start]**Vue.js** hoặc **React** [cite: 32] | Giao diện người dùng để rút gọn và quản lý link. |
| **DevOps/CI/CD** | [cite\_start]**Docker**, **GitHub Actions** [cite: 35, 34] | [cite\_start]Tự động hóa quá trình Build, Test, Push (Docker Hub) [cite: 37][cite\_start], và Deploy (Render/Azure)[cite: 38]. |

-----

### 3\. 👥 Phân Công Trách Nhiệm Nhóm (3 Thành Viên)

| Ứng viên | Vai Trò Chính | Thư mục/Component Chính | Nhiệm Vụ Đặc trưng |
| :--- | :--- | :--- | :--- |
| **Ứng viên 1** | Kiến trúc & Back-end Core | `/src/backend/URLShortener.Core`, `/URLShortener.Data` | [cite\_start]Logic rút gọn/Custom, EF Core, Caching (Redis), **Unit Tests**[cite: 52]. |
| **Ứng viên 2 (LEAD)** | **API & DevOps** | `/src/backend/URLShortener.Api`, `/.github/workflows` | [cite\_start]**API Controllers**, **Dockerfile (Multi-stage)**[cite: 52], **CI/CD Pipeline**, Tích hợp Firebase Auth. |
| **Ứng viên 3** | Front-end & Kiểm thử | `/src/frontend`, `/tests/URLShortener.IntegrationTests` | [cite\_start]Phát triển **Web UI** (Vue/React) [cite: 32][cite\_start], Quản lý Dashboard, **Integration Tests**[cite: 52]. |

-----

### 4\. 🚀 Hướng Dẫn Thiết Lập Môi Trường Phát Triển

#### A. Thiết lập Back-end (Ứng viên 1 & 2)

1.  **Clone Repository:**
    ```bash
    git clone [Your-GitHub-Repo-URL]
    ```
2.  **Mở Solution:** Mở file `URLShortener.sln` bằng Visual Studio 2022.
3.  **Tạo Database:**
    ```bash
    cd src/Backend/URLShortener.Data
    dotnet ef database update --project ..\URLShortener.Data
    ```
4.  **Cấu hình Secret:** Thêm Connection String cho SQL Server và cấu hình **Firebase Service Account** vào User Secrets hoặc `appsettings.Development.json` của `URLShortener.Api`.
5.  **Chạy:** Thiết lập `URLShortener.Api` làm Startup Project và chạy (F5). API Documentation (Swagger) sẽ có tại `/swagger`.

#### B. Thiết lập Front-end (Ứng viên 3)

1.  **Di chuyển vào thư mục:**
    ```bash
    cd src/frontend
    ```
2.  **Cài đặt Dependencies:**
    ```bash
    npm install
    ```
3.  **Cấu hình API Endpoint:** Cập nhật file cấu hình (ví dụ: `.env` hoặc tương đương) để trỏ đến endpoint API Back-end (`http://localhost:5000` hoặc tương đương).
4.  **Chạy:**
    ```bash
    npm run dev
    ```

-----

### 5\. 🐳 Hướng Dẫn Build & Deploy (Ứng viên 2)

Quá trình Build và Deploy hoàn toàn tự động hóa thông qua GitHub Actions.

1.  **Commit Code:** Đảm bảo tất cả code đã được kiểm thử và commit vào nhánh chính (`main`).
    ```bash
    git add .
    git commit -m "feat: complete feature X and ready for deployment"
    git push origin main
    ```
2.  [cite\_start]**CI/CD Tự động:** GitHub Actions sẽ tự động thực hiện các bước trong file `/.github/workflows/ci-cd-pipeline.yml`[cite: 35]:
      * [cite\_start]**Build & Test:** Build Solution và chạy Unit/Integration Tests[cite: 52].
      * [cite\_start]**Docker Build:** Build Docker Image bằng **Multi-stage Dockerfile**[cite: 52].
      * [cite\_start]**Push:** Push image lên **Docker Hub** với tag version[cite: 37].
      * [cite\_start]**Deploy:** Kích hoạt Deploy Hook tới PaaS (Render/Azure)[cite: 38].

-----
