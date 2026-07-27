# Event Tracking — Tổng hợp tính năng

> Module thuộc **CRM** trong Twendee Work ERP. File nguồn: [event-tracking.html](event-tracking.html), được nhúng vào shell ERP qua iframe tại view `events` trong [erp.html](erp.html).
>
> **Mục tiêu:** Lập kế hoạch sự kiện → phân công người tham dự → quản lý ngân sách → thu thập lead → khởi chạy chiến dịch follow-up. Tất cả kết nối liền mạch với các module CRM, Accounting/Finance khác.

---

## 1. Cấu trúc màn hình

Màn gồm **2 màn con** chuyển đổi qua lại (SPA, không reload):

| Màn | Mô tả |
|-----|-------|
| **List screen** | Danh sách tất cả sự kiện dạng card + KPI + bộ lọc |
| **Detail screen** | Chi tiết 1 sự kiện, chia 4 section với sticky pill-nav + scrollspy |

Khi nhúng trong ERP (`?embed=1`), topbar và language toggle riêng của màn sẽ tự ẩn để dùng chung chrome của shell.

---

## 2. Màn danh sách (List)

### 2.1. KPI tổng quan (4 thẻ)
- **Total events** — tổng số sự kiện + số sắp diễn ra (upcoming) trong năm.
- **Team assigned** — số nhân sự (unique) được phân công trên tất cả sự kiện.
- **Budget allocated** — tổng ngân sách đã phân bổ (planned + committed).
- **Leads captured** — tổng số lead thu được → pipeline mới.

### 2.2. Bộ lọc & tìm kiếm (Toolbar)
- **Category chips**: lọc nhanh theo danh mục (All + các danh mục có dữ liệu), kèm số đếm và chấm màu nhận diện.
- **Search box**: tìm theo tên sự kiện hoặc địa điểm (lọc real-time khi gõ).

### 2.3. Event cards (lưới responsive)
Mỗi card hiển thị:
- Banner màu theo danh mục + tên danh mục + **status badge** (Planning / Live / Completed).
- Tên sự kiện, khoảng thời gian, địa điểm, số lead đã thu.
- Cụm **avatar** người tham dự (hiển thị tối đa 4, dư ra hiện `+N`).
- Tổng ngân sách đã phân bổ.
- Click vào card → mở màn chi tiết.

### 2.4. Hành động cấp trang
- **Export** — xuất lịch sự kiện ra file `.ics` (mô phỏng bằng toast).
- **Create Event** — mở drawer tạo sự kiện mới.

---

## 3. Màn chi tiết (Detail)

Sticky pill-nav 4 mục với scrollspy tự highlight khi cuộn; kèm 2 hành động luôn hiển thị:
- **Edit** — sửa thông tin sự kiện.
- **Save as Campaign** — lưu toàn bộ lead của sự kiện thành chiến dịch follow-up.

### 3.1. Overview
- **Event details**: danh mục, trạng thái, ngày bắt đầu/kết thúc, địa điểm, chủ sự kiện (owner), mục tiêu/mô tả.
- **Budget health**: đã chi / tổng kế hoạch, thanh progress đổi màu cảnh báo (bình thường → `warn` >85% → `danger` >100%), % đã phân bổ và số còn lại.
- **Team on this event**: danh sách nhân sự tham dự dạng badge có avatar.

### 3.2. Attendees (Người tham dự)
- Bảng: người + vai trò + trạng thái (Confirmed) + hành động xóa.
- **Assign people**: drawer chọn nhiều nhân sự từ TEAM (có ô tìm kiếm, chọn/bỏ chọn), lưu lại.
- Xóa từng người trực tiếp trên bảng.

### 3.3. Budget Planning (Kế hoạch ngân sách)
- **4 KPI**: Planned budget · Allocated (kèm % kế hoạch) · Pending accounting · Paid.
- **Bảng line item**: tên khoản chi, vendor, danh mục, số tiền, trạng thái (**Planned / Requested / Paid**).
- **Add item**: drawer thêm khoản chi (tên, danh mục, số tiền ước tính, vendor).
- **Payment request → Accounting**:
  - Nút gửi trên từng khoản `planned`, hoặc **Request all planned** để gửi hàng loạt.
  - Drawer payment: liệt kê khoản chi, tính **Subtotal + VAT 10% + Total**, chọn payee, ngày cần, **approver** (Finance Manager / CFO / Accounting Lead), ghi chú.
  - Gửi → khoản chi chuyển sang `requested`, định tuyến qua module **Finance/Accounting** để duyệt.
- **Flow timeline 3 bước**: Lập kế hoạch → Gửi request Accounting → Được duyệt & thanh toán (trạng thái từng bước cập nhật theo dữ liệu thực tế).

### 3.4. Lead Capture (Thu thập lead)
- **Bảng lead**: contact (tên + chức danh), công ty + email, mức độ quan tâm (**🔥 Hot / 🌤 Warm / ❄️ Cold**), người phụ trách.
- **Capture lead**: drawer nhập contact (tên, chức danh, công ty, email, phone, interest level, assign to, ghi chú). Có nút **Save & add another** để nhập liên tiếp.
- Mỗi lead được tạo thành **Lead trong CRM**, gắn tag nguồn = sự kiện này.
- **Create activity**: tạo task follow-up cho lead → CRM Activity.
- Xóa lead trực tiếp trên bảng.

---

## 4. Chiến dịch follow-up (Save as Campaign)

- Gom toàn bộ lead của sự kiện thành **audience** cho một chiến dịch nurture.
- Chọn tên chiến dịch, **loại** (Email sequence / Call cadence / Newsletter / Multi-touch), ngày bắt đầu, owner.
- Xem trước danh sách lead sẽ được đưa vào audience.
- Lưu → chiến dịch được tạo, gắn với sự kiện.

---

## 5. Tạo / Sửa sự kiện (Create / Edit Event)

Drawer form dùng chung cho tạo mới và chỉnh sửa:
- Tên sự kiện (bắt buộc), **danh mục** (radio grid có màu).
- Ngày bắt đầu / kết thúc, địa điểm/venue.
- Event owner, **planned budget** (USD).
- Mục tiêu / mô tả (tùy chọn).

**Danh mục sự kiện:** Conference · Trade Show · Workshop · Webinar · Networking · Product Launch (mỗi loại một màu nhận diện).

---

## 6. Liên kết với các module khác trong ERP

| Từ Event Tracking | Đến module |
|-------------------|-----------|
| Payment request | **Finance / Accounting** (duyệt & thanh toán) |
| Lead capture | **CRM Leads** (gắn nguồn = sự kiện) |
| Create activity | **CRM Activity** (task follow-up) |
| Save as Campaign | **Lead Generation Campaign** (nurture audience) |

---

## 7. Chi tiết kỹ thuật (prototype)

- **Stack**: HTML tĩnh + CSS thuần + vanilla JS, không dependency ngoài (chỉ Google Fonts). Dữ liệu là mock in-memory (`EVENTS`, `TEAM`, `CATEGORIES`) — mọi thay đổi mất khi reload.
- **Design system**: theme Cerulean ERP (primary `#007BA7`), dùng chung design tokens với các màn ERP khác.
- **UI patterns**: drawer/panel trượt phải + overlay, toast notifications, sticky pill-nav + scrollspy (IntersectionObserver), badge trạng thái, progress bar cảnh báo.
- **Responsive**: grid tự co, breakpoint tại 900/820/640/520px.
- **Language toggle**: VI/EN (mới ở mức cosmetic, chưa dịch nội dung).
