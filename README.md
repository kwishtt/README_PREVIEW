# 💕 MGL Dating Match - Hệ thống hẹn hò thông minh trên Discord

---

## 🌟 Giới thiệu

**MGL Dating Match** là hệ thống hẹn hò hiện đại giúp bạn kết nối với những người phù hợp trong server Discord! Với giao diện thân thiện và các tính năng thông minh, bạn có thể dễ dàng tìm kiếm bạn bè mới, khám phá những mối quan hệ thú vị và xây dựng cộng đồng sôi động.

### ✨ Những tính năng nổi bật

- 🎯 **Khám phá thông minh**: Xem hồ sơ ngẫu nhiên với bộ lọc theo giới tính
- 🎮 **Điều khiển dễ dàng**: Sử dụng nút bấm để duyệt hồ sơ, quay lại hoặc tiến tới
- 💌 **Kết nối tức thì**: Gửi tin nhắn làm quen trực tiếp qua DM
- 🎨 **Hồ sơ cá nhân**: Tùy chỉnh thông tin cá nhân với ảnh, trạng thái, tuổi, vị trí
- 🏆 **Bảng xếp hạng**: Top những người được quan tâm nhiều nhất
- 🏅 **Hệ thống huy hiệu**: Nhận huy hiệu dựa trên hoạt động

---

## 🚀 Cách sử dụng

### Bước 1: Kiểm tra quyền truy cập

Bạn cần có **role Dating** để sử dụng hệ thống này. Liên hệ admin nếu chưa có role.

### Bước 2: Tạo hồ sơ cá nhân

Sử dụng lệnh `mdatingprofile` để thiết lập thông tin về bản thân.

### Bước 3: Bắt đầu khám phá

Dùng lệnh `mdating` để bắt đầu xem hồ sơ của những người khác!

---

## 📋 Hướng dẫn chi tiết các lệnh

### 🎯 `mdating [bộ_lọc]` - Khám phá hồ sơ

**Mô tả:** Xem hồ sơ ngẫu nhiên của các thành viên trong server

**Cách sử dụng:**

```text
mdating          → Xem tất cả mọi người
mdating nam      → Chỉ xem nam giới  
mdating nữ       → Chỉ xem nữ giới
mdating male     → Chỉ xem nam giới (tiếng Anh)
mdating female   → Chỉ xem nữ giới (tiếng Anh)
```

**Ví dụ thực tế:**

- `mdating` - Khám phá ngẫu nhiên tất cả mọi người
- `mdating nữ` - Chỉ muốn xem hồ sơ của các bạn nữ
- `mdating nam` - Chỉ quan tâm đến các anh chàng

**Khi sử dụng lệnh, bạn sẽ thấy:**

- 🖼️ **Ảnh đại diện** và thông tin cơ bản
- 👤 **Tên hiển thị** với emoji giới tính
- 🎂 **Tuổi** (nếu đã cập nhật)
- 📍 **Vị trí** (nếu đã cập nhật)
- 💭 **Trạng thái/giới thiệu** cá nhân
- 🏅 **Huy hiệu** (nếu có)

**Các nút tương tác:**

- ⬅️ **Quay lại**: Xem lại hồ sơ trước đó
- ➡️ **Người tiếp theo**: Khám phá hồ sơ mới
- 💌 **Nhắn tin làm quen**: Gửi thông báo đến người đó
- 🔍 **Lọc giới tính**: Thay đổi bộ lọc nhanh

---

### 👤 `mdatingprofile` - Quản lý hồ sơ cá nhân

**Mô tả:** Xem và chỉnh sửa thông tin hồ sơ dating của bạn

**Cách sử dụng:**

```text
mdatingprofile              → Xem hồ sơ của bạn
mdatingprofile @người_nào   → Xem hồ sơ của người khác
```

**Ví dụ:**

- `mdatingprofile` - Xem hồ sơ của chính mình
- `mdatingprofile @Minh123` - Xem hồ sơ của Minh123

**Các nút chỉnh sửa (chỉ hiện khi xem hồ sơ của mình):**

- 📝 **Trạng thái**: Viết giới thiệu về bản thân (tối đa 200 ký tự)
- 🖼️ **Ảnh**: Thêm URL ảnh đại diện (jpg, png, gif, webp)
- 🎂 **Tuổi**: Cập nhật tuổi (13-100)
- 📍 **Địa điểm**: Thêm vị trí hiện tại
- 🗑️ **Xóa hồ sơ**: Xóa hoàn toàn thông tin (cần xác nhận)

**Lời khuyên khi tạo hồ sơ:**

- ✅ Viết trạng thái thú vị, tích cực
- ✅ Sử dụng ảnh rõ ràng, đẹp
- ✅ Cung cấp thông tin chân thực
- ❌ Không spam hoặc viết nội dung tiêu cực

---

### 🏆 `mtop` - Bảng xếp hạng

**Mô tả:** Xem top 10 người được quan tâm nhiều nhất trong tuần

**Cách sử dụng:**

```text
mtop        → Xem bảng xếp hạng tuần này
```

**Cách tính điểm:**

- Mỗi lần được ai đó nhấn nút 💌 "Nhắn tin làm quen" = +1 điểm
- Chỉ tính trong 7 ngày gần nhất
- Cập nhật theo thời gian thực

**Ý nghĩa của bảng xếp hạng:**

- 🥇🥈🥉 **Top 3**: Những người thu hút nhất
- 📊 **Khuyến khích**: Tạo động lực cập nhật hồ sơ đẹp hơn
- 🎯 **Cạnh tranh lành mạnh**: Khích lệ tương tác tích cực

---

## 🏅 Hệ thống huy hiệu thông minh

Dựa trên hoạt động của bạn, hệ thống sẽ tự động trao các huy hiệu đặc biệt:

| Huy hiệu | Điều kiện | Ý nghĩa |
|----------|-----------|---------|
| 💬 **Người trò chuyện nhiều nhất** | Gửi ≥ 20 lời làm quen trong 30 ngày | Bạn là người kết nối tích cực, thích làm quen |
| 🔥 **Gây chú ý nhất** | Nhận ≥ 50 lượt xem trong 30 ngày | Hồ sơ của bạn rất thu hút mọi người |
| 🧊 **FA lâu nhất** | Không nhận tin nhắn nào >30 ngày | Hãy cập nhật hồ sơ đẹp hơn nhé! |

**Cách kiếm huy hiệu:**

- **Tích cực kết nối**: Thường xuyên sử dụng tính năng nhắn tin làm quen
- **Hồ sơ chất lượng**: Ảnh đẹp, mô tả thú vị sẽ thu hút nhiều lượt xem
- **Tương tác**: Càng nhiều người quan tâm, càng dễ có huy hiệu

---

## ⚙️ Thiết lập và yêu cầu

### 📋 Yêu cầu role

Để sử dụng hệ thống dating, bạn cần có:

- **🎯 Role Dating**: `1312415405645496353`
  - Role này cho phép bạn tham gia vào hệ thống dating
  - Liên hệ admin để được cấp role

- **♀️ Role xác định giới tính**: `1312124176479420506`
  - Người có role này được xác định là nữ
  - Những người không có role này được xác định là nam
  - Dùng để lọc khi tìm kiếm

### 🎮 Prefix lệnh

Bot sử dụng prefix **`m`** cho tất cả các lệnh:

```bash
mdating          # Khám phá hồ sơ
mdatingprofile   # Quản lý hồ sơ
mtop            # Xem bảng xếp hạng
```

---

## 💡 Mẹo sử dụng hiệu quả

### 🎯 Để có hồ sơ thu hút

**✅ Nên làm:**

- Viết trạng thái vui vẻ, tích cực (ví dụ: "Thích đọc sách và du lịch ✈️")
- Sử dụng ảnh rõ nét, dễ nhìn
- Cập nhật đầy đủ thông tin (tuổi, vị trí)
- Thể hiện tính cách, sở thích

**❌ Tránh:**

- Viết tiêu cực hoặc khiếm nhã
- Dùng ảnh mờ, không phù hợp
- Để trống quá nhiều thông tin
- Spam hoặc quảng cáo

### 🎪 Để kết nối hiệu quả

**💌 Khi nhắn tin làm quen:**

- Đọc kỹ hồ sơ trước khi nhắn tin
- Chỉ nhắn với những người thực sự quan tâm
- Tôn trọng khi người khác không phản hồi

**🔍 Khi khám phá:**

- Sử dụng bộ lọc phù hợp với sở thích
- Tận dụng nút "Quay lại" để xem lại người thú vị
- Kiên nhẫn - tình bạn đẹp cần thời gian

---

## 🚨 Lưu ý quan trọng

### ⚡ Hạn chế hệ thống

- **👤 Không hiển thị bản thân**: Bot sẽ không bao giờ hiển thị hồ sơ của chính bạn
- **🔄 Không lặp lại**: Mỗi người chỉ xuất hiện 1 lần trong 24h để tránh spam
- **📱 Vấn đề DM**: Nếu người khác tắt tin nhắn riêng tư, bạn sẽ nhận thông báo lỗi
- **🛡️ Tuổi an toàn**: Chỉ chấp nhận tuổi từ 13-100 để đảm bảo an toàn cộng đồng

### 🎨 Về ảnh đại diện

- **Ưu tiên**: Ảnh URL bạn thêm → Avatar Discord mặc định
- **Định dạng hỗ trợ**: JPG, PNG, GIF, WEBP
- **Kiểm tra tự động**: Hệ thống sẽ kiểm tra URL có hợp lệ không

### 🔒 Quyền riêng tư

- **Thông tin cá nhân**: Chỉ hiển thị những gì bạn chọn chia sẻ
- **Lịch sử xem**: Người khác không thể biết bạn đã xem hồ sơ họ
- **Xóa dữ liệu**: Bạn có thể xóa hoàn toàn hồ sơ bất cứ lúc nào

---

## 🛠️ Khắc phục sự cố

### ❓ Các vấn đề thường gặp

#### 🔴 "Không có quyền truy cập"

- ✅ Kiểm tra đã có role Dating chưa
- ✅ Liên hệ admin để được cấp quyền

### 🔴 "Không tìm thấy ai"

- ✅ Đợi vài giờ để cache làm mới
- ✅ Thử thay đổi bộ lọc giới tính
- ✅ Thời điểm khác có thể có nhiều người online hơn

### 🔴 "Không thể gửi tin nhắn"

- ✅ Người đó đã tắt DM, không phải lỗi của bạn
- ✅ Thử với người khác

### 🔴 "URL ảnh không hợp lệ"

- ✅ Kiểm tra link có mở được không
- ✅ Đảm bảo là link trực tiếp đến file ảnh
- ✅ Thử tải ảnh lên Discord rồi copy link

### 🆘 Hỗ trợ

Nếu vẫn gặp vấn đề:

1. **📝 Ghi lại lỗi**: Screenshot hoặc copy thông báo lỗi
2. **👥 Hỏi cộng đồng**: Nhiều người có thể đã gặp vấn đề tương tự
3. **🔧 Liên hệ admin**: Để được hỗ trợ trực tiếp
4. **⏳ Thử lại sau**: Đôi khi là vấn đề tạm thời

---

## 🎉 Kết luận

**MGL Dating Match** không chỉ là công cụ hẹn hò mà còn là cầu nối giúp xây dựng cộng đồng gắn kết. Hãy sử dụng một cách tích cực, tôn trọng lẫn nhau và tận hưởng những kết nối mới!

### 🌟 Chúc bạn

- 💕 Tìm được những người bạn thú vị
- 🎊 Có những cuộc trò chuyện vui vẻ
- 🏆 Đạt được huy hiệu đẹp
- 🌈 Xây dựng mối quan hệ bền vững

---

**📱 Phiên bản:** 1.0  
**👨‍💻 Phát triển bởi:** MGL Bot Development Team  
**🌐 Website:** discord.gg/mgl

- *Cảm ơn bạn đã đồng hành cùng MGL Dating Match! 💕*
