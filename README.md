# Velora Hotel — Hệ thống Quản lý Khách sạn

Giao diện web quản lý vận hành khách sạn (HTML / CSS / JavaScript thuần, không cần bước build).

## Cấu trúc tệp
- `index.html` — Khung ứng dụng chính, điều hướng sidebar và modal dùng chung.
- `styles.css` — Toàn bộ stylesheet (bảng màu pastel, bố cục responsive, mẫu in báo cáo).
- `app.js` — Dữ liệu khởi tạo (`getDefaultData()`), quản lý `state`, các màn hình: Tổng quan, Loại phòng, Phòng, Bảng giá, Dịch vụ, Khách hàng, Quản trị viên, Báo cáo (Doanh thu tổng, Doanh thu dịch vụ, Tần suất sử dụng phòng).
- `transactions.js` — Phân hệ Giao dịch: Đặt phòng, Phân phòng, Nhận phòng (Check-in), Trả phòng (Check-out), Thanh toán & Hóa đơn.

## Chạy cục bộ hoặc đưa lên GitHub Pages
1. Có thể mở trực tiếp `index.html` hoặc chạy qua bất kỳ static server nào (ví dụ Live Server, `npx serve .`, `python -m http.server 5500`).
2. Đăng nhập mặc định trong giao diện: tài khoản `admin` / mật khẩu `123` (lưu trong mã nguồn demo `app.js`).
3. Để công khai web xem online trên GitHub: vào **Settings → Pages → Build and deployment → Branch: `main` (`/ (root)`) → Save**.

## Hướng dẫn tích hợp dữ liệu / Backend
Hiện toàn bộ dữ liệu ứng dụng được đọc/ghi thông qua `state` và lưu cục bộ trên trình duyệt tại `localStorage` (`STORAGE_KEY = 'velora_hotel_db_v3_pos'`):
- `getDefaultData()` trong `app.js` — cấu trúc dữ liệu mẫu ban đầu.
- `loadState()` trong `app.js` — nơi nạp `state` khi khởi chạy ứng dụng.
- `saveState(newState)` trong `app.js` — điểm lưu trung tâm mỗi khi có thao tác thêm/sửa/cập nhật; có sẵn ghi chú điểm mở rộng để đồng bộ lên API/Database.

### Các bảng / danh sách chính trong `state`
- `hotelInfo`: thông tin khách sạn
- `roomCategories`: hạng phòng (`HP001`…)
- `rooms`: danh sách phòng (`P001`…)
- `amenityGroups`, `amenities`: nhóm tiện ích & tiện ích
- `pricePlans`: bảng giá theo thời gian
- `serviceGroups`, `services`: nhóm danh mục & dịch vụ (`DV001`…)
- `surcharges`, `cancellationPolicies`: phụ thu & chính sách hủy phòng
- `customers`: danh sách khách hàng (`KH001`…)
- `bookings`: đơn đặt phòng (`DP001`…)
- `checkins`: bản ghi nhận/trả phòng thực tế (`LT001`…)
- `invoices`: giao dịch thanh toán / hoàn phí hủy (`HD001`…)
- `bookingHistory`, `pendingHistoryLogs`: lịch sử thay đổi đơn đặt phòng
- `staff`: danh sách nhân sự (`NV-001`…)
