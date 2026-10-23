# Triển khai Bí Ẩn London 1888 trên Vercel

## Phạm vi thay đổi

Các thay đổi chỉ bổ sung lớp triển khai: adapter Express thành Vercel Function, cấu hình build Vite, dependency `@vercel/node`, và hướng dẫn triển khai. Các component giao diện, API route hiện có, dữ liệu vụ án và luật chơi không được chủ động thay đổi.

## Triển khai

1. Giải nén và đẩy toàn bộ thư mục dự án lên một repository Git (GitHub/GitLab/Bitbucket).
2. Trong Vercel, chọn **Add New → Project**, import repository đó.
3. Dùng cấu hình mặc định từ `vercel.json`: Build Command `npm run build`, Output Directory `dist`.
4. Trong **Project Settings → Environment Variables**, thêm `GEMINI_API_KEY` nếu muốn sử dụng tính năng sinh vụ án bằng Gemini.
5. Deploy. Sau khi deploy, mở trang chủ và kiểm tra các API như `/api/cases` và `/api/leaderboard`.

## Lưu ý quan trọng về dữ liệu

Backend hiện tại đọc/ghi `data/custom_cases.json` và `data/users.json` trên hệ thống tệp. Vercel Functions chạy trong môi trường serverless với hệ thống tệp không phải nơi lưu dữ liệu bền vững; các thao tác ghi file không thể được coi là lưu trữ lâu dài và dữ liệu trong bộ nhớ có thể trở về mặc định khi function khởi động lại. Để bảo đảm dữ liệu người dùng/vụ án tùy chỉnh tồn tại ổn định, cần một bước riêng chuyển lớp lưu trữ sang dịch vụ bền vững. Bước đó chưa được thực hiện vì yêu cầu hiện tại là không thay đổi chức năng hoặc kiến trúc ứng dụng.

## Chạy cục bộ

```bash
npm install
npm run dev
```

Đặt `GEMINI_API_KEY` trong môi trường nếu cần sử dụng tính năng AI.
