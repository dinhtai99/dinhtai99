<div align="center">
  <img src="https://via.placeholder.com/150" alt="SmartRent Logo" width="120" height="120">
  <h1>🏢 SmartRent Ecosystem</h1>
  <p><strong>A Comprehensive B2B2C SaaS Platform for Property Management</strong></p>

  <p>
    <img src="https://img.shields.io/badge/Next.js-16.2-black?style=for-the-badge&logo=next.js" alt="Next.js" />
    <img src="https://img.shields.io/badge/Flutter-3.x-02569B?style=for-the-badge&logo=flutter" alt="Flutter" />
    <img src="https://img.shields.io/badge/FastAPI-0.100+-009688?style=for-the-badge&logo=fastapi" alt="FastAPI" />
    <img src="https://img.shields.io/badge/Supabase-Database-3ECF8E?style=for-the-badge&logo=supabase" alt="Supabase" />
  </p>
</div>

## 📖 Về Dự Án (About The Project)

**SmartRent** không chỉ là một ứng dụng quản lý nhà trọ đơn thuần, mà là một **Hệ sinh thái B2B2C Microservices** hoàn chỉnh. Dự án giải quyết trọn vẹn bài toán vận hành, dòng tiền và quản lý tài sản cho các chủ trọ, đồng thời mang lại trải nghiệm minh bạch cho người thuê thông qua sức mạnh của AI.

Hệ thống bao gồm 3 phân hệ chính (Repositories):
1. 🌐 **[Core Backend & Web Dashboard (Next.js)](link-toi-repo-nextjs)**: Nơi các Chủ trọ (Landlords) và Super Admin quản lý hàng trăm căn hộ, hoá đơn, hợp đồng và doanh thu.
2. 📱 **[Mobile App (Flutter)](link-toi-repo-flutter)**: Ứng dụng dành riêng cho Cư dân (Tenants), giúp họ theo dõi điện nước, thanh toán hoá đơn và báo sự cố.
3. 🧠 **[AI Microservice (FastAPI)](link-toi-repo-fastapi)**: Bộ não xử lý OCR (Nhận diện CCCD, Đọc chỉ số đồng hồ) và Phân tích tự động (AI Ticket Categorization).

---

## 🚀 Các Tính Năng Kỹ Thuật Đáng Chú Ý (Highlight Features)

Thay vì làm các chức năng CRUD cơ bản, dự án này tập trung vào các bài toán của một hệ thống thương mại thực tế (Production-ready):

### 1. Kiến trúc Bảo mật Mức độ Doanh nghiệp (Enterprise-grade Security)
*   **Row Level Security (RLS)**: Tận dụng sức mạnh của Supabase PostgreSQL để phân lập dữ liệu SaaS. Dữ liệu giữa các Chủ trọ (Organizations) bị cách ly hoàn toàn ở tầng Database.
*   **Edge Middleware Authentication**: Xác thực JWT token ngay tại Edge Server của Vercel (`proxy.ts`), chặn đứng truy cập trái phép trước khi page render.
*   **Secure Mobile Storage**: Sử dụng `flutter_secure_storage` lưu trữ token an toàn trong Apple Keychain và Android Keystore.

### 2. Tự động hóa & Tối ưu Dòng tiền (Automated Cashflow)
*   **Cronjobs & Background Workers**: Tích hợp **Upstash QStash** tự động thức dậy, tính toán hoá đơn hằng tháng và gọi API bắn Push Notification (Firebase) nhắc nợ cư dân.
*   **Payment Gateway Integration**: Tích hợp thanh toán **VNPay / PayOS** qua Webhook, tự động gạch nợ hoá đơn theo thời gian thực (Real-time).

### 3. Tích hợp Trí tuệ Nhân tạo (AI Integration)
*   **AI Meter Reading & OCR**: Gọi API Gemini Vision xử lý ảnh chụp đồng hồ điện/nước, trích xuất chỉ số chính xác và đọc thông tin CCCD khách thuê.
*   **AI Auto-fallback Model**: Cơ chế dự phòng thông minh trên FastAPI, tự động đổi Model AI (`gemini-2.5-flash` ➔ `gemini-2.0-flash`) nếu server Google bị quá tải.
*   **Ticket Priority AI**: Phân tích phàn nàn của cư dân (Text + Image) và tự động dán nhãn mức độ ưu tiên (High/Medium/Low).

### 4. Tối ưu Hiệu năng (Performance Optimization)
*   **Redis Caching**: Sử dụng **Upstash Redis** cache lại các Dashboard Analytics nặng (Doanh thu, Tỉ lệ lấp đầy) trong 12 tiếng, giúp Web Dashboard load tức thời.

---

## 🏗️ Kiến trúc Hệ thống (System Architecture)

```mermaid
graph TD
    A[Flutter Mobile App<br/>(Cư dân)] -->|REST API + Bearer JWT| B(Next.js Core Backend<br/>Hosted on Vercel)
    C[Next.js Web Dashboard<br/>(Chủ trọ / Admin)] -->|Server Actions / API| B
    
    B <-->|PostgreSQL + RLS| D[(Supabase Database)]
    B <-->|Cache & Rate Limit| E[(Upstash Redis)]
    B -->|Webhook & Cronjob| F[Upstash QStash]
    F -->|Trigger Reminder| B
    
    B -->|Upload & Scan| G[FastAPI AI Microservice<br/>Hosted on Render]
    G <-->|Prompt + Image| H[Google Gemini API]
    
    B <-->|Webhooks| I[VNPay / PayOS Gateway]
```

---

## 📸 Giao diện Nổi bật (Screenshots)

> 💡 **Tip cho HR / Tech Lead:** *[Chèn 4-6 ảnh đẹp nhất của dự án vào đây. 2 ảnh Web Dashboard, 2 ảnh màn hình Flutter, 1 ảnh quét AI]*

| Web Dashboard (Next.js) | Mobile App (Flutter) |
|:---:|:---:|
| <img src="link_anh_web_1" width="400"/> | <img src="link_anh_app_1" width="200"/> |
| *Báo cáo doanh thu & Quản lý Toà nhà* | *Giao diện thanh toán & Hoá đơn Cư dân* |
| <img src="link_anh_web_2" width="400"/> | <img src="link_anh_app_2" width="200"/> |
| *Quản lý Sự cố (Tickets) với nhãn AI* | *AI Quét CCCD & Đồng hồ điện* |

---

## 🛠️ Cài đặt & Triển khai (Installation & Deployment)

Vui lòng tham khảo tài liệu hướng dẫn chi tiết tại từng Repository:
*   [Setup Core Backend & Web (BE_SMARTRENT) ➔](./link-be)
*   [Setup Mobile App (FLUTTER_MOBILE) ➔](./link-flutter)
*   [Setup AI Service (AI_smartrent) ➔](./link-ai)

---
<div align="center">
  <p>Được thiết kế và phát triển bởi <b>Trần Đình Tài</b></p>
  <p>
    <a href="mailto:email-cua-ban@gmail.com">dinhtai1999t@gmail.com</a> • 
    <a href="https://linkedin.com/in/link-cua-ban">LinkedIn</a>
  </p>
</div>
