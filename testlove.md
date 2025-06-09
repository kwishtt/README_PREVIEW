# 💖 Tài Liệu Kiểm Thử Hệ Thống Tình Yêu MGL Bot

## 📋 Tổng Quan

Tài liệu này cung cấp hướng dẫn kiểm thử chi tiết cho toàn bộ hệ thống tình yêu của MGL Bot, bao gồm 10 module chính:

1. **Main.py** - Hệ thống trợ giúp và điều hướng
2. **Dating.py** - Hệ thống hẹn hò cơ bản
3. **Dating_Match.py** - Hệ thống ghép đôi thông minh
4. **Intimacy.py** - Quản lý điểm thân mật và tương tác
5. **Shop.py** - Cửa hàng vật phẩm tình yêu
6. **Family.py** - Hệ thống gia đình và con cái
7. **House.py** - Quản lý nhà cửa
8. **Pet.py** - Hệ thống thú cưng
9. **Love.py** - Tính độ hợp đôi và giải trí
10. **Admin.py** - Lệnh quản trị

## 🎯 Hướng Dẫn Test Cơ Bản

### **Bước 1: Chuẩn Bị Môi Trường Test**

#### **1.1 Thiết Lập Server Discord**
1. **Tạo server Discord test riêng**
   - Tên server: `MGL Bot Testing`
   - Tạo các kênh: `#general`, `#testing`, `#admin`
2. **Invite bot với quyền Administrator**
   - Hoặc custom permissions: `Send Messages`, `Embed Links`, `Attach Files`, `Add Reactions`, `Manage Roles`
3. **Tạo ít nhất 5 account test:**
   - Account A: `Tester-Alpha` (Tester chính)
   - Account B: `Tester-Beta` (Partner test)
   - Account C: `Tester-Gamma` (Người thứ ba)
   - Account D: `Tester-Delta` (Tester female)
   - Account E: `Admin-Test` (Admin account)

#### **1.2 Cấu Hình Database**
1. **Kiểm tra kết nối MongoDB**
   ```bash
   # Test connection
   mongodb://localhost:27017/mgl_bot_test
   ```
2. **Backup database hiện tại**
   ```bash
   mongodump --db mgl_bot --out backup_before_test
   ```
3. **Tạo database test riêng (khuyến nghị)**
   ```javascript
   use mgl_bot_test
   ```

#### **1.3 Thiết Lập Roles và Permissions**
1. **Tạo roles cần thiết:**
   - `@Đang hẹn hò` - Role ID: cần config trong `love_config.py`
   - `@Nữ` - Role ID: cần config
   - `@Nam` - Role ID: cần config
   - `@Admin` - Quyền quản trị
2. **Gán roles cho accounts:**
   - Account A, C: `@Nam`, `@Đang hẹn hò`
   - Account B, D: `@Nữ`, `@Đang hẹn hò`
   - Account E: `@Admin`

### **Bước 2: Test Flow Cơ Bản - Quy Trình Hẹn Hò Hoàn Chỉnh**

#### **2.1 Phase 1: Hệ thống trợ giúp**
```bash
# Kiểm tra menu trợ giúp
Account A → mhelp
# Expect: Embed với 6 nút bấm chính
# Test tất cả nút: "Tìm Một Nửa", "Hẹn Hò", "Gia Đình", "Thú Cưng", "Cửa Hàng", "Giải Trí"
```

#### **2.2 Phase 2: Tạo hồ sơ hẹn hò**
```bash
# Tạo profile dating
Account A → mdatingprofile
# Nhập bio: "Tôi là một người yêu thích âm nhạc"
# Chọn sở thích: Âm nhạc, Du lịch, Ẩm thực
# Upload ảnh: https://example.com/avatar1.jpg

Account B → mdatingprofile  
# Nhập bio khác và sở thích tương tự
```

#### **2.3 Phase 3: Duyệt hồ sơ và tỏ tình**
```bash
# Duyệt hồ sơ
Account A → mdating
# Bấm ❤️ cho hồ sơ của Account B
# Bấm 💌 gửi tin nhắn: "Chào em, anh thấy profile em rất thú vị"

# Tỏ tình trực tiếp
Account A → henho @Account-B
# Expect: Embed tỏ tình gửi tới Account B
```

#### **2.4 Phase 4: Chấp nhận và thành cặp**
```bash
Account B → dongy
# Expect: Thông báo thành cặp đôi thành công
# Cả 2 account đều nhận notification

# Kiểm tra tình trạng
Account A → nguoiyeu
Account B → nguoiyeu
# Expect: Hiển thị thông tin cặp đôi
```

#### **2.5 Phase 5: Xây dựng mối quan hệ**
```bash
# Tặng quà hàng ngày
Account A → tangthanmat
# Expect: +10 điểm thân mật

# Tương tác vật lý
Account A → om @Account-B
Account B → hon @Account-A
Account A → xoadau @Account-B
# Expect: Cộng điểm thân mật tương ứng

# Kiểm tra shop
Account A → mloveshop
# Mua vật phẩm
Account A → ua hoa_hong 3
# React ✅ để xác nhận
# Expect: Trừ xu, thêm vật phẩm vào inventory

# Sử dụng vật phẩm
Account A → dungvatpham hoa_hong
# Expect: +15 điểm thân mật, trừ 1 hoa hồng
```

#### **2.6 Phase 6: Kết hôn và gia đình**
```bash
# Kiểm tra điểm thân mật
# Cần đạt ít nhất 500-1000 điểm để cầu hôn

# Mua nhẫn từ shop
Account A → ua nhan_tinh_nhan 1
# React ✅

# Cầu hôn
Account A → cauhon
Account B → Bấm nút "Đồng ý" 
# Expect: Thành cặp vợ chồng

# Mua nhà
Account A → muanha villa
# Expect: Mua thành công nếu đủ xu

# Sinh con
Account A → sinhcon  
# Expect: Random tạo con với tên, giới tính, tính cách

# Chăm sóc con
Account A → chamsoccon [tên con]
# Expect: Tăng happiness của con, +điểm thân mật
```

#### **2.7 Phase 7: Thú cưng và hoạt động gia đình**
```bash
# Nhận nuôi thú cưng
Account A → muapet dog
# Đặt tên: "Buddy"

# Chăm sóc pet  
Account A → chamsocpet Buddy
# Expect: Tăng happiness pet, +3 điểm thân mật

# Xem thông tin gia đình
Account A → contoi
Account A → petcuatoi
Account A → nhacuatoi
```

### **Bước 3: Kiểm Tra Database Chi Tiết**

#### **3.1 Sử dụng MongoDB Compass**
```javascript
// Kiểm tra couples collection
db.couples.find({})

// Kiểm tra intimacy_points
db.intimacy_points.find({})

// Kiểm tra inventories
db.inventories.find({})

// Kiểm tra dating_profiles
db.dating_profiles.find({})

// Kiểm tra children
db.children.find({})

// Kiểm tra pets  
db.pets.find({})

// Kiểm tra family_homes
db.family_homes.find({})
```

#### **3.2 Verification Queries**
```javascript
// Verify couple relationship
db.couples.findOne({
  $or: [
    {user1: "USER_ID_A", user2: "USER_ID_B"},
    {user1: "USER_ID_B", user2: "USER_ID_A"}
  ]
})

// Check intimacy points
db.intimacy_points.findOne({couple_id: "COUPLE_ID"})

// Verify inventory items
db.inventories.findOne({couple_id: "COUPLE_ID"})
```

### **Bước 4: Test Negative Cases - Kiểm Thử Trường Hợp Lỗi**

#### **4.1 Dating System Errors**
```bash
# Test tự tỏ tình
Account A → henho @Account-A  
# Expect: Error "Không thể tỏ tình với chính mình"

# Test tỏ tình người đã có người yêu
Account C → henho @Account-A
# Expect: Error "Người này đã có người yêu"

# Test chấp nhận khi không có lời mời
Account C → dongy
# Expect: Error "Không có lời mời hẹn hò nào"

# Test cooldown
Account A → henho @Account-C (ngay sau khi tỏ tình thành công)
# Expect: Error cooldown 1 giờ
```

#### **4.2 Shop System Errors**
```bash
# Test mua khi không đủ xu
Account A → ua qua_dac_biet 100
# Expect: Error "Không đủ xu"

# Test mua vật phẩm không tồn tại
Account A → ua fake_item 1
# Expect: Error "Vật phẩm không tồn tại"

# Test sử dụng vật phẩm khi không có
Account A → dungvatpham expensive_item
# Expect: Error "Không có vật phẩm này"
```

#### **4.3 Intimacy System Errors**
```bash
# Test tặng quà khi đã tặng trong ngày
Account A → tangthanmat
Account A → tangthanmat (lần 2 trong ngày)
# Expect: Error cooldown

# Test cầu hôn khi chưa đủ điểm
# (Reset điểm thân mật về 0 bằng admin command)
Account A → cauhon
# Expect: Error "Cần ít nhất X điểm thân mật"

# Test tương tác vật lý khi chưa có người yêu
Account C → om @Account-D
# Expect: Error "Bạn chưa có người yêu"
```

#### **4.4 Family System Errors**
```bash
# Test sinh con khi chưa kết hôn
Account C → sinhcon
# Expect: Error "Phải kết hôn trước"

# Test chăm sóc con không tồn tại
Account A → chamsoccon FakeChild
# Expect: Error "Không tìm thấy con"
```

### **Bước 5: Performance Testing - Kiểm Thử Hiệu Suất**

#### **5.1 Stress Testing**
```bash
# Test spam commands
Account A → mhelp (x50 lần liên tục)
# Monitor: Response time, memory usage, error rate

# Test concurrent operations
# 3 accounts cùng lúc:
Account A → mdating
Account B → mloveshop  
Account C → mhelp
# Monitor: Database locks, response time
```

#### **5.2 Database Load Testing**
```bash
# Tạo nhiều couples (script automation)
# Test với 100+ couples trong database
# Verify: dscd command performance
# Query optimization check
```

### **Bước 6: Automated Testing Script**

#### **6.1 Basic Test Script (Python)**
```python
# test_love_system.py
import discord
import asyncio
import time

class LoveSystemTest:
    def __init__(self, bot_token, test_server_id):
        self.client = discord.Client()
        self.server_id = test_server_id
        
    async def run_basic_flow(self):
        """Run complete love system test flow"""
        # Test help system
        await self.test_help_system()
        
        # Test dating flow
        await self.test_dating_flow()
        
        # Test shop system
        await self.test_shop_system()
        
        # Generate report
        self.generate_report()
        
    async def test_help_system(self):
        """Test mhelp command and navigation"""
        pass
        
    # More test methods...
```

### **Bước 7: Test Report Generation**

#### **7.1 Test Results Template**
```markdown
# MGL Bot Love System Test Report

## Test Summary
- **Ngày test:** [DATE]
- **Tester:** [NAME]  
- **Môi trường:** [TEST/PROD]
- **Database:** [DB_NAME]

## Test Results
### ✅ Passed Tests: X/Y
### ❌ Failed Tests: Z

## Failed Test Details
- TC-D-001: [Error description]
- TC-S-005: [Error description]

## Performance Metrics
- Average response time: Xms
- Database query time: Yms
- Memory usage: Z MB

## Recommendations
1. [Issue 1 and fix recommendation]
2. [Issue 2 and fix recommendation]
```

---

## 🔧 I. MAIN.PY - HỆ THỐNG TRỢ GIÚP

### **Lệnh được định nghĩa:**
- `mhelp` - Hiển thị menu trợ giúp chính

### **Thành phần giao diện:**
- `LoveHelpView` - Giao diện chính với các nút điều hướng

### **Các trường hợp kiểm thử:**

#### 1.1 Lệnh `mhelp`
| Mã Test | Mô Tả | Đầu Vào | Kết Quả Mong Đợi | Kiểm Tra MongoDB | Trường Hợp Đặc Biệt |
|---------|-------|---------|------------------|-------------------|-------------------|
| TC-M-001 | Hiển thị menu trợ giúp | `mhelp` | Embed với tiêu đề "Hệ Thống Tình Yêu MGL" và 6 nút bấm | Không có | Không có |
| TC-M-002 | Xử lý timeout | Chờ 180 giây không tương tác | Các nút bị vô hiệu hóa, hiện thông báo hết thời gian | Không có | Trễ mạng |

#### 1.2 Tương tác với các nút bấm
| Mã Test | Nút Bấm | Tiêu Đề Embed Mong Đợi | Nội Dung Mong Đợi |
|---------|---------|-------------------------|-------------------|
| TC-M-003 | "Tìm Một Nửa" | "🔥 Tìm Một Nửa" | Các lệnh mdating, mdatingprofile, mtoptt |
| TC-M-004 | "Hẹn Hò" | "💕 Hẹn Hò" | Các lệnh mhenho, mdongy, mtuchoi, mchiatay |
| TC-M-005 | "Gia Đình" | "👨‍👩‍👧‍👦 Gia Đình" | Các lệnh msinhcon, mcontoi, mdattenten |
| TC-M-006 | "Thú Cưng" | "🐾 Thú Cưng" | Các lệnh mmuapet, mdattenpet, mpetcuatoi |
| TC-M-007 | "Cửa Hàng" | "🏪 Cửa Hàng & Tài Sản" | Các lệnh mloveshop, mbuylove, mtuido |
| TC-M-008 | "Giải Trí" | "🎮 Giải Trí" | Các lệnh mlove, mship, mmatch |
| TC-M-009 | "Trang Chủ" | Quay về menu chính | Embed gốc với 6 nút bấm |

#### 1.3 Kiểm soát quyền truy cập
| Mã Test | Điều Kiện | Hành Vi Mong Đợi |
|---------|-----------|------------------|
| TC-M-010 | Người dùng khác bấm nút | Tương tác thất bại với thông báo lỗi |
| TC-M-011 | Người dùng gốc bấm nút | Tương tác thành công |

### **🧪 Hướng Dẫn Test Chi Tiết:**

#### **Test Cơ Bản:**
1. **Gõ `mhelp`** → Kiểm tra hiển thị đúng embed
2. **Bấm từng nút** → Xem có chuyển sang đúng trang không
3. **Chờ 3 phút** → Kiểm tra timeout có hoạt động
4. **Để người khác bấm nút** → Xem có chặn được không

#### **Test Nâng Cao:**
1. **Spam nhiều `mhelp`** → Kiểm tra có lag không
2. **Bấm nút liên tục** → Test rate limiting
3. **Xóa tin nhắn giữa chừng** → Xem bot có crash không

---

## 💕 II. DATING.PY - HẸN HÒ CƠ BẢN

### **Lệnh được định nghĩa:**
- `henho/date` - Gửi lời mời hẹn hò
- `dongy/accept` - Chấp nhận lời mời
- `tuchoi/reject` - Từ chối lời mời  
- `chiatay/breakup` - Chia tay người yêu
- `nguoiyeu/ny` - Kiểm tra tình trạng mối quan hệ
- `dscd/couples` - Danh sách các cặp đôi

### **Các trường hợp kiểm thử:**

#### 2.1 Lệnh `henho/date`
| Mã Test | Điều Kiện Tiền Đề | Đầu Vào | Kết Quả Mong Đợi | Thay Đổi MongoDB | Trường Hợp Đặc Biệt |
|---------|-------------------|---------|------------------|-------------------|-------------------|
| TC-D-001 | Người dùng chưa có người yêu | `henho @user2` | Embed tỏ tình gửi cho user2 | Thêm vào date_requests | @user2 offline |
| TC-D-002 | Người dùng đã có người yêu | `henho @user3` | Lỗi "đã có người yêu" | Không thay đổi | Không có |
| TC-D-003 | Tỏ tình chính mình | `henho @self` | Lỗi "không thể tỏ tình chính mình" | Không thay đổi | Không có |
| TC-D-004 | Đối tượng đã có người yêu | `henho @taken_user` | Lỗi "người đó đã có người yêu" | Không thay đổi | Không có |
| TC-D-005 | Cooldown đang hoạt động | Gọi lệnh trong vòng 1 giờ | Lỗi cooldown | Không thay đổi | Đúng lúc kết thúc cooldown |

#### 2.2 Lệnh `dongy/accept`
| Mã Test | Điều Kiện Tiền Đề | Đầu Vào | Kết Quả Mong Đợi | Thay Đổi MongoDB | Trường Hợp Đặc Biệt |
|---------|-------------------|---------|------------------|-------------------|-------------------|
| TC-D-006 | Có lời mời đang chờ | `dongy` | Thành công, thành cặp đôi | Thêm vào couples, xóa date_requests | Nhiều lời mời cùng lúc |
| TC-D-007 | Không có lời mời nào | `dongy` | Lỗi "không có lời mời" | Không thay đổi | Không có |
| TC-D-008 | Đã có người yêu | `dongy` | Lỗi "đã có người yêu" | Không thay đổi | Không có |

#### 2.3 Lệnh `tuchoi/reject`  
| Mã Test | Điều Kiện Tiền Đề | Đầu Vào | Kết Quả Mong Đợi | Thay Đổi MongoDB | Trường Hợp Đặc Biệt |
|---------|-------------------|---------|------------------|-------------------|-------------------|
| TC-D-009 | Có lời mời đang chờ | `tuchoi` | Thông báo thành công | Xóa date_request cụ thể | Không có |
| TC-D-010 | Không có lời mời nào | `tuchoi` | Lỗi "không có lời mời" | Không thay đổi | Không có |

#### 2.4 Lệnh `chiatay/breakup`
| Mã Test | Điều Kiện Tiền Đề | Đầu Vào | Kết Quả Mong Đợi | Thay Đổi MongoDB | Trường Hợp Đặc Biệt |
|---------|-------------------|---------|------------------|-------------------|-------------------|
| TC-D-011 | Đang có người yêu | `chiatay` → React 💔 | Thành công, xóa mối quan hệ | Xóa khỏi couples | Partner offline |
| TC-D-012 | Không có người yêu | `chiatay` | Lỗi "chưa có người yêu" | Không thay đổi | Không có |
| TC-D-013 | React ❌ thay vì 💔 | `chiatay` → React ❌ | Hủy thao tác | Không thay đổi | Không có |
| TC-D-014 | Timeout (60 giây) | `chiatay` → chờ | Thông báo hết thời gian | Không thay đổi | Không có |
| TC-D-015 | Cooldown 7 ngày | Thử trong vòng 7 ngày | Lỗi cooldown | Không thay đổi | Đúng lúc 7 ngày |

#### 2.5 Lệnh `nguoiyeu/ny`
| Mã Test | Điều Kiện | Đầu Vào | Kết Quả Mong Đợi | Trường Hợp Đặc Biệt |
|---------|-----------|---------|------------------|-------------------|
| TC-D-016 | Người dùng có người yêu | `nguoiyeu` | Embed với thông tin cặp đôi | Partner rời server |
| TC-D-017 | Người dùng chưa có người yêu | `nguoiyeu` | Thông báo lỗi | Không có |
| TC-D-018 | Kiểm tra người khác | `nguoiyeu @user2` | Thông tin cặp đôi của user2 | User2 không có partner |

#### 2.6 Lệnh `dscd/couples`
| Mã Test | Điều Kiện | Kết Quả Mong Đợi | Trường Hợp Đặc Biệt |
|---------|-----------|------------------|-------------------|
| TC-D-019 | Server có cặp đôi | Danh sách phân trang các cặp đôi | >10 cặp đôi |
| TC-D-020 | Server không có cặp đôi | "Không có cặp đôi nào" | Không có |
| TC-D-021 | Một số cặp đôi không hợp lệ | Chỉ hiển thị cặp đôi hợp lệ | User bị xóa |

### **🧪 Hướng Dẫn Test Chi Tiết:**

#### **Chuẩn Bị:**
1. **Tạo 3 account test:** A, B, C
2. **Đảm bảo tất cả đều chưa có người yêu**
3. **Reset cooldown nếu cần:** Admin dùng lệnh reset

#### **Test Flow Cơ Bản:**
```
1. A: henho @B          → Kiểm tra B nhận được lời tỏ tình
2. B: dongy             → Kiểm tra A+B thành cặp đôi
3. A: nguoiyeu          → Xem thông tin cặp đôi
4. A: dscd              → Kiểm tra xuất hiện trong danh sách
5. A: chiatay → React💔 → Kiểm tra chia tay thành công
```

#### **Test Negative Cases:**
```
1. A: henho @A          → Lỗi tự tỏ tình
2. C: henho @A          → Lỗi A đã có người yêu (nếu A+B đang yêu)
3. A: henho @B (lần 2)  → Lỗi cooldown 1 giờ
4. A: dongy (không có lời mời) → Lỗi không có lời mời
```

#### **Test Database:**
- **Kiểm tra MongoDB collection `couples`** có record với user1/user2
- **Kiểm tra collection `date_requests`** được tạo và xóa đúng
- **Verify relationship integrity** giữa các collections

---

## 🔍 III. DATING_MATCH.PY - GHÉP ĐÔI THÔNG MINH

### **Lệnh được định nghĩa:**
- `mdating` - Duyệt hồ sơ hẹn hò
- `mdatingprofile` - Quản lý hồ sơ cá nhân
- `mtoptt` - Bảng xếp hạng hệ thống hẹn hò

### **Các trường hợp kiểm thử:**

#### 3.1 Lệnh `mdating`
| Mã Test | Điều Kiện Tiền Đề | Đầu Vào | Kết Quả Mong Đợi | Kiểm Tra MongoDB | Trường Hợp Đặc Biệt |
|---------|-------------------|---------|------------------|-------------------|-------------------|
| TC-DM-001 | User có role dating | `mdating` | Thẻ hồ sơ với các nút bấm | Thêm vào view_history | Không có hồ sơ nào |
| TC-DM-002 | Lọc theo giới tính | `mdating nam` | Chỉ hiện hồ sơ nam | Áp dụng bộ lọc giới tính | Không có hồ sơ nam |
| TC-DM-003 | Lọc theo giới tính | `mdating nữ` | Chỉ hiện hồ sơ nữ | Áp dụng bộ lọc giới tính | Không có hồ sơ nữ |
| TC-DM-004 | Không có role dating | `mdating` | Thông báo lỗi | Không thay đổi | Không có |
| TC-DM-005 | Đã có người yêu | `mdating` | Lỗi "đã có người yêu" | Không thay đổi | Không có |

#### 3.2 Tương tác với hồ sơ hẹn hò
| Mã Test | Nút Được Bấm | Hành Động Mong Đợi | Thay Đổi MongoDB | Trường Hợp Đặc Biệt |
|---------|--------------|---------------------|-------------------|-------------------|
| TC-DM-006 | ❤️ (Thích) | Gửi thông báo like | Ghi log tương tác, cập nhật stats | Đối tượng tắt DM |
| TC-DM-007 | ❌ (Bỏ qua) | Hiển thị hồ sơ tiếp theo | Thêm vào view_history | Hết hồ sơ |
| TC-DM-008 | 💌 (Nhắn tin) | Modal nhập tin nhắn | Ghi log tương tác | Tin nhắn quá dài |
| TC-DM-009 | ⏹️ (Dừng) | Kết thúc phiên duyệt | Cập nhật thống kê phiên | Không có |

#### 3.3 Lệnh `mdatingprofile`
| Mã Test | Điều Kiện | Đầu Vào | Kết Quả Mong Đợi | Thay Đổi MongoDB | Trường Hợp Đặc Biệt |
|---------|-----------|---------|------------------|-------------------|-------------------|
| TC-DM-010 | Lần đầu thiết lập | `mdatingprofile` | Quy trình tạo hồ sơ | Thêm hồ sơ mới | Không có |
| TC-DM-011 | Đã có hồ sơ | `mdatingprofile` | Hồ sơ hiện tại với nút chỉnh sửa | Không thay đổi | Không có |
| TC-DM-012 | Xem hồ sơ người khác | `mdatingprofile @user` | Hồ sơ công khai của user | Thêm vào view_history | Hồ sơ riêng tư |
| TC-DM-013 | Chỉnh sửa bio | Bấm nút bio → modal | Xác nhận cập nhật bio | Cập nhật profile.bio | Bio quá dài (>500 ký tự) |
| TC-DM-014 | Chỉnh sửa sở thích | Bấm nút sở thích | Chọn sở thích | Cập nhật profile.interests | Đạt giới hạn sở thích |
| TC-DM-015 | Upload ảnh | Gửi URL ảnh | Xác thực và cập nhật ảnh | Cập nhật profile.photos | URL không hợp lệ |

#### 3.4 Lệnh `mtoptt`
| Mã Test | Danh Mục | Kết Quả Mong Đợi | Trường Hợp Đặc Biệt |
|---------|----------|------------------|-------------------|
| TC-DM-016 | Người được yêu thích nhất | Top 10 theo lượt like | Không ai có like |
| TC-DM-017 | Hoạt động nhiều nhất | Top 10 theo lượt xem hồ sơ | Không có hoạt động |
| TC-DM-018 | Hồ sơ hot | Xu hướng tháng hiện tại | Tháng mới, không có dữ liệu |

### **🧪 Hướng Dẫn Test Chi Tiết:**

#### **Chuẩn Bị:**
1. **Tạo role "Đang hẹn hò"** với ID trong config
2. **Tạo role "Nữ"** với ID trong config  
3. **Gán role cho các account test**
4. **Tạo ít nhất 5 hồ sơ mẫu**

#### **Test Profile Creation:**
```
1. A: mdatingprofile     → Lần đầu, tạo hồ sơ
2. Nhập bio, chọn sở thích, upload ảnh
3. A: mdatingprofile     → Lần 2, xem hồ sơ đã tạo
4. Test edit bio/interests/photos
```

#### **Test Dating Flow:**
```
1. A: mdating           → Bắt đầu duyệt hồ sơ
2. Bấm ❤️ một vài hồ sơ → Kiểm tra notification
3. Bấm 💌 gửi tin nhắn  → Kiểm tra modal
4. Bấm ❌ bỏ qua       → Kiểm tra hồ sơ tiếp theo
5. A: mdating (lần 2)   → Không thấy hồ sơ đã xem
```

#### **Test Filters:**
```
1. A: mdating nam       → Chỉ thấy profile nam
2. A: mdating nữ        → Chỉ thấy profile nữ
3. A: mdating all       → Thấy tất cả profile
```

#### **Test Rankings:**
```
1. Tạo nhiều tương tác like/view
2. A: mtoptt            → Kiểm tra ranking đúng
3. Verify database stats match displayed results
```

---

## 💝 IV. INTIMACY.PY - THÂN MẬT & TƯƠNG TÁC

### **Commands được định nghĩa:**
- `tangthanmat/mlovegift/mdailygift` - Tặng quà hàng ngày
- `dungvatpham/museitem/mtangqua` - Sử dụng vật phẩm
- `cauhon/mpropose` - Cầu hôn
- `om/mhug` - Ôm
- `hon/mkiss` - Hôn
- `xoadau/mpat` - Xoa đầu

### **Test Cases:**

#### 4.1 Command `tangthanmat` (Daily Gift)
| Test Case | Điều Kiện Tiền Đề | Expected Output | Points Added | MongoDB Changes | Edge Cases |
|-----------|-------------------|-----------------|--------------|-----------------|------------|
| TC-I-001 | Có người yêu, chưa dùng today | Success message | +10 | Update intimacy_points | Exactly at midnight |
| TC-I-002 | Chưa có người yêu | Error message | 0 | No changes | None |
| TC-I-003 | Đã dùng trong ngày | Cooldown error | 0 | No changes | Exactly at cooldown end |
| TC-I-004 | Partner offline | Success + DM fail | +10 | Update intimacy_points | None |

#### 4.2 Command `dungvatpham` (Use Item)
| Test Case | Điều Kiện Tiền Đề | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------------------|-------|-----------------|-----------------|------------|
| TC-I-005 | Có item trong inventory | `dungvatpham hoa_hong` | Item used, points added | Decrease item count, increase points | Item count = 0 |
| TC-I-006 | Không có item | `dungvatpham expensive_item` | Error "không có vật phẩm" | No changes | None |
| TC-I-007 | Invalid item name | `dungvatpham fake_item` | Error "vật phẩm không tồn tại" | No changes | None |
| TC-I-008 | No parameter | `dungvatpham` | Usage help message | No changes | None |
| TC-I-009 | Chưa có người yêu | `dungvatpham hoa_hong` | Error message | No changes | None |

#### 4.3 Command `cauhon` (Propose)
| Test Case | Điều Kiện Tiền Đề | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------------------|-----------------|-----------------|------------|
| TC-I-010 | Đủ điểm + có nhẫn | Proposal embed with buttons | Consume ring if accepted | Partner offline |
| TC-I-011 | Chưa đủ điểm thân mật | Error "cần X điểm" | No changes | Exactly at required points |
| TC-I-012 | Không có nhẫn | Error "cần nhẫn" | No changes | None |
| TC-I-013 | Chưa có người yêu | Error message | No changes | None |
| TC-I-014 | Đã kết hôn | Error "đã kết hôn" | No changes | None |
| TC-I-015 | Accept proposal | Success, married status | Insert into married_couples, remove ring | None |
| TC-I-016 | Reject proposal | Reject message | No changes | None |
| TC-I-017 | Proposal timeout | Timeout message | No changes | None |

#### 4.4 Physical Interaction Commands
| Command | Cooldown | Points Added | Test Cases |
|---------|----------|--------------|------------|
| `om/mhug` | 1 hour | +5 | TC-I-018 to TC-I-021 |
| `hon/mkiss` | 2 hours | +8 | TC-I-022 to TC-I-025 |
| `xoadau/mpat` | 30 minutes | +3 | TC-I-026 to TC-I-029 |

#### Common Physical Interaction Test Cases:
| Test Case | Điều Kiện | Expected Output | Points | Edge Cases |
|-----------|-----------|-----------------|--------|------------|
| TC-I-018+ | Có người yêu, no cooldown | Success message with gif | As specified | Partner left server |
| TC-I-019+ | Chưa có người yêu | Error message | 0 | None |
| TC-I-020+ | Cooldown active | Cooldown error with time | 0 | Exactly at cooldown end |
| TC-I-021+ | At max intimacy points | Success but no points added | 0 | None |

---

## 🛍️ V. SHOP.PY - CỬA HÀNG TÌNH YÊU

### **Commands được định nghĩa:**
- `cuahang/loveshop/shoptinhyeu` - Xem cửa hàng
- `ua/lovebuy/cuahangmua` - Mua vật phẩm
- `inventory_love` (implied) - Xem túi đồ

### **Available Items:**
| Item ID | Name | Price | Intimacy Points | Description |
|---------|------|-------|-----------------|-------------|
| hoa_hong | 🌹 Hoa hồng | 50 | +15 | Hoa hồng tươi thắm |
| socola | 🍫 Socola | 30 | +10 | Hộp socola ngọt ngào |
| thu_tinh_cam | 💌 Thư tình cảm | 60 | +20 | Lá thư đầy tình cảm |
| nhan_tinh_nhan | 💍 Nhẫn tình nhân | 150 | +50 | Nhẫn tượng trưng tình yêu |
| nuoc_hoa | 🧴 Nước hoa | 40 | +12 | Nước hoa thơm ngát |
| qua_dac_biet | 🎁 Quà đặc biệt | 300 | +100 | Món quà bí mật |

### **Test Cases:**

#### 5.1 Command `cuahang`
| Test Case | Điều Kiện | Expected Output | Edge Cases |
|-----------|-----------|-----------------|------------|
| TC-S-001 | Normal access | Embed với all items + prices | None |
| TC-S-002 | Discount active | Items show ~~old~~ **new** price | Discount expired during view |
| TC-S-003 | No discount | Regular prices | None |

#### 5.2 Command `ua` (Buy Items)
| Test Case | Điều Kiện Tiền Đề | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------------------|-------|-----------------|-----------------|------------|
| TC-S-004 | Enough money + has partner | `ua hoa_hong 2` | Confirmation embed | Pending purchase | None |
| TC-S-005 | Not enough money | `ua qua_dac_biet 10` | Error "không đủ xu" | No changes | Exactly enough money |
| TC-S-006 | No partner | `ua hoa_hong` | Error "cần có người yêu" | No changes | None |
| TC-S-007 | Invalid item | `ua fake_item` | Error "vật phẩm không tồn tại" | No changes | None |
| TC-S-008 | Quantity too high | `ua hoa_hong 100` | Error "tối đa X vật phẩm" | No changes | At max quantity |
| TC-S-009 | Inventory full | Buy when inventory = MAX | Error "túi đồ đầy" | No changes | Exactly at limit |
| TC-S-010 | Confirm purchase (✅) | React ✅ | Success, items added | Deduct money, add items | None |
| TC-S-011 | Cancel purchase (❌) | React ❌ | "Đã hủy giao dịch" | No changes | None |
| TC-S-012 | Purchase timeout | Wait 60s | "Đã hết thời gian" | No changes | None |

#### 5.3 Inventory Management
| Test Case | Scenario | Expected Behavior | MongoDB Check |
|-----------|----------|-------------------|---------------|
| TC-S-013 | Check couple inventory | Show all items with quantities | Query by couple_id |
| TC-S-014 | Empty inventory | "Túi đồ trống" message | No inventory doc |
| TC-S-015 | Item count accuracy | Correct quantities displayed | Verify item counts |

#### 5.4 Discount System
| Test Case | Scenario | Expected Behavior | Edge Cases |
|-----------|----------|-------------------|------------|
| TC-S-016 | Admin set discount | All prices reduced | Discount during purchase |
| TC-S-017 | Discount expires | Prices return to normal | Mid-purchase expiry |
| TC-S-018 | No active discount | Regular pricing | None |

---

## 👨‍👩‍👧‍👦 VI. FAMILY.PY - GIA ĐÌNH

### **Commands được định nghĩa:**
- `sinhcon/havechild` - Sinh con (30 days cooldown)
- `contoi/mychildren` - Xem thông tin con
- `dattenten/renamechild` - Đổi tên con
- `chamsoccon/careforchild` - Chăm sóc con
- `thongkecon/childstats` - Thống kê con cái

### **Test Cases:**

#### 6.1 Command `sinhcon`
| Test Case | Điều Kiện Tiền Đề | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------------------|-----------------|-----------------|------------|
| TC-F-001 | Đã kết hôn + đủ điểm | Random child created | Insert into children | At exact intimacy requirement |
| TC-F-002 | Chưa kết hôn | Error "phải kết hôn trước" | No changes | None |
| TC-F-003 | Chưa đủ điểm thân mật | Error with current/required points | No changes | None |
| TC-F-004 | Đã có MAX children | Error "đã có đủ con" | No changes | At exactly MAX children |
| TC-F-005 | Cooldown active | Cooldown error | No changes | Exactly at 30 days |
| TC-F-006 | Partner offline | Success với notification fail | Insert child | None |

#### 6.2 Child Generation System
| Test Case | Expected Behavior | Verification |
|-----------|-------------------|--------------|
| TC-F-007 | Random gender (boy/girl) | 50/50 distribution over time |
| TC-F-008 | Random name from lists | Names from predefined arrays |
| TC-F-009 | Random personality trait | Trait from predefined list |
| TC-F-010 | Unique child ID | No duplicate IDs |

#### 6.3 Command `contoi`
| Test Case | Điều Kiện | Expected Output | Edge Cases |
|-----------|-----------|-----------------|------------|
| TC-F-011 | Has children | List of children with details | None |
| TC-F-012 | No children | "Chưa có con" message | None |
| TC-F-013 | View other's children | Other user's children (if public) | Private family |

#### 6.4 Command `dattenten`
| Test Case | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------|-----------------|-----------------|------------|
| TC-F-014 | `dattenten OldName NewName` | Success message | Update child.name | Name too long |
| TC-F-015 | Invalid old name | Error "không tìm thấy con" | No changes | Similar names |
| TC-F-016 | Inappropriate new name | Error or filter | No changes | Profanity filter |

#### 6.5 Command `chamsoccon`
| Test Case | Điều Kiện | Expected Output | Points/Benefits | Edge Cases |
|-----------|-----------|-----------------|-----------------|------------|
| TC-F-017 | Valid child, no cooldown | Success + happiness increase | +intimacy with partner | Child at max happiness |
| TC-F-018 | Invalid child name | Error message | No changes | None |
| TC-F-019 | Cooldown active | Cooldown error | No changes | Multiple care attempts |

---

## 🏠 VII. HOUSE.PY - NHÀ CỬA

### **Commands được định nghĩa:**
- `muanha/buyhome` - Mua nhà
- `nhacuatoi/myhome/home` - Xem thông tin nhà
- `bannha/sellhome` - Bán nhà

### **House Types:**
| Type | Name | Price | Max Children | Max Pets | Intimacy Bonus |
|------|------|-------|--------------|----------|----------------|
| apartment | 🏢 Căn hộ | 500 | 2 | 2 | +5 |
| house | 🏡 Nhà phố | 1000 | 3 | 3 | +10 |
| villa | 🏰 Biệt thự | 2000 | 5 | 5 | +15 |
| mansion | 🏰 Dinh thự | 5000 | 10 | 10 | +25 |

### **Test Cases:**

#### 7.1 Command `muanha`
| Test Case | Điều Kiện Tiền Đề | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------------------|-------|-----------------|-----------------|------------|
| TC-H-001 | Married + enough money | `muanha villa` | Purchase confirmation | Insert family_homes | Exactly enough money |
| TC-H-002 | Not married | `muanha house` | Error "phải kết hôn" | No changes | None |
| TC-H-003 | Not enough money | `muanha mansion` | Error "không đủ xu" | No changes | None |
| TC-H-004 | Invalid house type | `muanha castle` | Error + house list | No changes | Typo in house name |
| TC-H-005 | Already own house | `muanha apartment` | Error "đã có nhà" | No changes | None |
| TC-H-006 | No parameter | `muanha` | House types list | No changes | None |

#### 7.2 Command `nhacuatoi`
| Test Case | Điều Kiện | Expected Output | Edge Cases |
|-----------|-----------|-----------------|------------|
| TC-H-007 | Own a house | House details embed | None |
| TC-H-008 | No house | "Chưa có nhà" message | None |
| TC-H-009 | View other's house | Other family's house (if public) | Private house |

#### 7.3 Command `bannha`
| Test Case | Điều Kiện | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-----------|-----------------|-----------------|------------|
| TC-H-010 | Own a house | Confirmation dialog | Pending sale | None |
| TC-H-011 | No house | Error "chưa có nhà" | No changes | None |
| TC-H-012 | Confirm sale | Success + money return | Delete family_homes, add money | Partial refund |
| TC-H-013 | Cancel sale | Cancel message | No changes | None |

#### 7.4 House Benefits
| Test Case | Scenario | Expected Behavior |
|-----------|----------|-------------------|
| TC-H-014 | Intimacy bonus application | Bonus added to interactions |
| TC-H-015 | Child/pet limit enforcement | Limits based on house type |
| TC-H-016 | House upgrade | New limits applied |

---

## 🐾 VIII. PET.PY - THÚ CƯNG

### **Commands được định nghĩa:**
- `muapet/adoptpet` - Mua thú cưng
- `dattenpet/renamepet` - Đổi tên pet
- `petcuatoi/mypets/pets` - Xem thông tin pet
- `chamsocpet/carepet` - Chăm sóc pet (3 times/day)

### **Pet Types:**
| Type | Name | Price | Lifespan | Happiness Decay | Activities |
|------|------|-------|----------|-----------------|------------|
| dog | 🐕 Chó | 200 | 90 days | 5/day | đi dạo, ném bóng, huấn luyện, tắm |
| cat | 🐈 Mèo | 150 | 120 days | 3/day | vuốt ve, chơi đồ chơi, tắm, cho ăn vặt |
| bird | 🐦 Chim | 100 | 60 days | 4/day | cho ăn, dạy nói, làm sạch lồng |
| rabbit | 🐰 Thỏ | 120 | 80 days | 2/day | cho ăn cỏ, chơi đùa, vệ sinh |

### **Test Cases:**

#### 8.1 Command `muapet`
| Test Case | Điều Kiện Tiền Đề | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------------------|-------|-----------------|-----------------|------------|
| TC-P-001 | Has partner + money | `muapet dog` | Pet adoption success | Insert into pets | At pet limit |
| TC-P-002 | No partner | `muapet cat` | Error "cần có người yêu" | No changes | None |
| TC-P-003 | Not enough money | `muapet dog` | Error "không đủ xu" | No changes | Exactly enough money |
| TC-P-004 | Invalid pet type | `muapet dragon` | Error + pet list | No changes | Typo in pet name |
| TC-P-005 | At pet limit | `muapet bird` | Error "đã đủ pet" | No changes | House limit check |
| TC-P-006 | No parameter | `muapet` | Pet types list | No changes | None |

#### 8.2 Command `dattenpet`
| Test Case | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------|-----------------|-----------------|------------|
| TC-P-007 | `dattenpet OldName NewName` | Success message | Update pet.name | Name too long |
| TC-P-008 | Invalid old name | Error "không tìm thấy pet" | No changes | Similar names |
| TC-P-009 | Inappropriate new name | Error or filter | No changes | Profanity filter |

#### 8.3 Command `petcuatoi`
| Test Case | Điều Kiện | Expected Output | Edge Cases |
|-----------|-----------|-----------------|------------|
| TC-P-010 | Has pets | List with happiness, age, etc. | None |
| TC-P-011 | No pets | "Chưa có pet" message | None |
| TC-P-012 | View other's pets | Other user's pets (if public) | Private pets |

#### 8.4 Command `chamsocpet`
| Test Case | Điều Kiện | Input | Expected Output | Points Added | Edge Cases |
|-----------|-----------|-------|-----------------|--------------|------------|
| TC-P-013 | Valid pet, uses < 3 today | `chamsocpet Fluffy` | Success + happiness up | +3 intimacy | Pet at max happiness |
| TC-P-014 | Invalid pet name | `chamsocpet FakePet` | Error message | 0 | None |
| TC-P-015 | Used 3 times today | `chamsocpet Fluffy` | Cooldown error | 0 | Reset at midnight |
| TC-P-016 | Pet very happy | `chamsocpet Fluffy` | Happy pet response | +3 intimacy | None |
| TC-P-017 | Pet sad | `chamsocpet SadPet` | Sad pet response | +3 intimacy | None |

#### 8.5 Pet Lifecycle
| Test Case | Scenario | Expected Behavior |
|-----------|----------|-------------------|
| TC-P-018 | Daily happiness decay | Happiness reduces per pet type |
| TC-P-019 | Pet lifespan expires | Pet dies, removal notification |
| TC-P-020 | Zero happiness | Pet becomes very sad/sick |

---

## 🎮 IX. LOVE.PY - GIẢI TRÍ

### **Commands được định nghĩa:**
- `love/ship/match` - Tính độ hợp đôi

### **Test Cases:**

#### 9.1 Command `love/ship/match`
| Test Case | Input | Expected Output | Algorithm | Edge Cases |
|-----------|-------|-----------------|-----------|------------|
| TC-L-001 | `love User1 User2` | Match % with romantic comment | Name-based calculation | Same name |
| TC-L-002 | `love` (no args) | Default "MGL" vs "Mẫu Giáo Lớn" | Default names | None |
| TC-L-003 | `love @user` (one arg) | User vs "Mẫu Giáo Lớn" | Mention handling | User offline |
| TC-L-004 | Very high match (90%+) | "Vĩnh cửu" tier comment | Score >= 90 | None |
| TC-L-005 | High match (80-89%) | "Setlove" tier comment | 80 <= Score < 90 | None |
| TC-L-006 | Good match (60-79%) | "Mơ về nhà" tier comment | 60 <= Score < 80 | None |
| TC-L-007 | Medium match (40-59%) | "Có duyên" tier comment | 40 <= Score < 60 | None |
| TC-L-008 | Low match (20-39%) | "Xa lạ" tier comment | 20 <= Score < 40 | None |
| TC-L-009 | Very low (0-19%) | "Không duyên" tier comment | Score < 20 | None |
| TC-L-010 | Cooldown active | Cooldown error (15s) | Rate limit | Exactly at 15s |

#### 9.2 Love Image Generation
| Test Case | Scenario | Expected Output | Edge Cases |
|-----------|----------|-----------------|------------|
| TC-L-011 | Successful image creation | Love image with names + % | Image generation fails |
| TC-L-012 | Image cache hit | Faster response time | Cache miss |
| TC-L-013 | Long names | Proper text fitting | Name overflow |

---

## ⚙️ X. ADMIN.PY - LỆNH QUẢN TRỊ

### **Commands được định nghĩa:**
- `lovedbclear` - Xóa database (Admin only)
- `quatang/qua_tang` - Tặng vật phẩm (Admin only)
- `setintimacy` - Set điểm thân mật (Admin only)
- `forcebreakup` - Ép chia tay (Admin only)

### **Test Cases:**

#### 10.1 Command `lovedbclear`
| Test Case | Điều Kiện | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-----------|-------|-----------------|-----------------|------------|
| TC-A-001 | Admin permissions | `lovedbclear couples` | Confirmation dialog | Pending clear | None |
| TC-A-002 | No admin perms | `lovedbclear` | Permission error | No changes | None |
| TC-A-003 | Invalid target | `lovedbclear invalid` | Error + valid options | No changes | None |
| TC-A-004 | Confirm clear | React ✅ | Success message | Clear specified collection | None |
| TC-A-005 | Cancel clear | React ❌ | Cancel message | No changes | None |

#### 10.2 Command `quatang`
| Test Case | Điều Kiện | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-----------|-------|-----------------|-----------------|------------|
| TC-A-006 | Admin + valid item | `quatang @user hoa_hong 5` | Success message | Add items to inventory | User has no couple |
| TC-A-007 | No admin perms | `quatang @user item` | Permission error | No changes | None |
| TC-A-008 | Invalid item | `quatang @user fake_item` | Error message | No changes | None |
| TC-A-009 | Invalid quantity | `quatang @user hoa_hong -1` | Error message | No changes | Zero quantity |

#### 10.3 Command `setintimacy`
| Test Case | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------|-----------------|-----------------|------------|
| TC-A-010 | `setintimacy @user1 @user2 500` | Success message | Update intimacy points | Users not a couple |
| TC-A-011 | Invalid amount | `setintimacy @u1 @u2 -100` | Error message | No changes | Over max limit |
| TC-A-012 | Same user twice | `setintimacy @user @user 100` | Error message | No changes | None |

#### 10.4 Command `forcebreakup`
| Test Case | Input | Expected Output | MongoDB Changes | Edge Cases |
|-----------|-------|-----------------|-----------------|------------|
| TC-A-013 | `forcebreakup @user` | Success message | Delete couple record | User has no partner |
| TC-A-014 | User not in relationship | `forcebreakup @single_user` | Error message | No changes | None |

---

## 🔧 TROUBLESHOOTING & FAQ

### **❗ Các Lỗi Thường Gặp Và Cách Xử Lý**

#### **Lỗi Database**
| Lỗi | Nguyên Nhân | Cách Khắc Phục |
|-----|-------------|----------------|
| `pymongo.errors.ServerSelectionTimeoutError` | Không kết nối được MongoDB | Kiểm tra MongoDB service, connection string |
| `Collection not found` | Database collection chưa được tạo | Chạy bot lần đầu để tạo collections |
| `Duplicate key error` | Trùng lặp dữ liệu | Xóa document trùng lặp hoặc reset collection |
| `Document too large` | Document vượt quá 16MB | Tối ưu hóa dữ liệu, chia nhỏ document |

#### **Lỗi Commands**
| Lỗi | Nguyên Nhân | Cách Khắc Phục |
|-----|-------------|----------------|
| `Command not found` | Module chưa được load | Restart bot, kiểm tra import |
| `Missing permissions` | Bot thiếu quyền | Cấp quyền cần thiết cho bot |
| `User not found` | User ID không hợp lệ | Kiểm tra user còn trong server |
| `Channel not accessible` | Bot không truy cập được channel | Kiểm tra permissions, channel visibility |

#### **Lỗi Cooldown**
| Lỗi | Mô Tả | Thời Gian Cooldown |
|-----|-------|-------------------|
| `henho cooldown` | Tỏ tình quá nhanh | 1 giờ |
| `chiatay cooldown` | Chia tay quá nhanh | 7 ngày |
| `tangthanmat cooldown` | Tặng quà trong ngày | Reset lúc 0h |
| `Physical interaction cooldown` | Tương tác vật lý | 30 phút - 2 giờ |

### **🔍 Debug Commands cho Developers**

#### **MongoDB Debug Queries**
```javascript
// Kiểm tra couples không hợp lệ
db.couples.find({
  $or: [
    {user1: {$exists: false}},
    {user2: {$exists: false}},
    {user1: null},
    {user2: null}
  ]
})

// Tìm intimacy points âm
db.intimacy_points.find({points: {$lt: 0}})

// Kiểm tra inventory items không hợp lệ
db.inventories.find({
  $or: [
    {"items.quantity": {$lt: 0}},
    {"items.item_id": null}
  ]
})

// Tìm children không có parents
db.children.find({
  $or: [
    {parent1: {$exists: false}},
    {parent2: {$exists: false}}
  ]
})
```

#### **Admin Debug Commands** (thêm vào admin.py nếu cần)
```python
# Lệnh debug để reset toàn bộ dữ liệu user
@commands.command(name="resetuser")
@commands.has_permissions(administrator=True)
async def reset_user_data(self, ctx, user: discord.Member):
    """Reset toàn bộ dữ liệu love system của user"""
    # Implementation: Xóa khỏi tất cả collections
    
# Lệnh kiểm tra tính toàn vẹn dữ liệu
@commands.command(name="checkintegrity")
@commands.has_permissions(administrator=True)  
async def check_data_integrity(self, ctx):
    """Kiểm tra tính toàn vẹn dữ liệu trong database"""
    # Implementation: Verify referential integrity
```

### **📝 FAQ - Câu Hỏi Thường Gặp**

#### **Q1: Tại sao lệnh `henho` không hoạt động?**
**A:** Kiểm tra:
- User có đang ở trong server không?
- Bot có quyền send messages không?
- User đã có người yêu chưa?
- Có đang trong thời gian cooldown không?

#### **Q2: Điểm thân mật không tăng khi sử dụng vật phẩm?**
**A:** Kiểm tra:
- Có đang ở trạng thái có người yêu không?
- Vật phẩm có tồn tại trong inventory không?
- Database connection có ổn định không?

#### **Q3: Không thể mua vật phẩm từ shop?**
**A:** Kiểm tra:
- Có đủ xu không?
- Có người yêu chưa?
- Inventory có đầy không?
- Item ID có đúng không?

#### **Q4: Lệnh admin không hoạt động?**
**A:** Kiểm tra:
- User có role admin không?
- Bot có quyền administrator không? 
- Command syntax có đúng không?

#### **Q5: Profile hẹn hò không hiển thị?**
**A:** Kiểm tra:
- Có role "Đang hẹn hò" không?
- Profile đã được tạo chưa?
- Bio và ảnh có hợp lệ không?

### **🚨 Emergency Procedures - Quy Trình Khẩn Cấp**

#### **Database Corruption**
```bash
# 1. Stop bot immediately
pm2 stop mgl-bot

# 2. Backup current database
mongodump --db mgl_bot --out emergency_backup_$(date +%Y%m%d_%H%M%S)

# 3. Restore from last known good backup
mongorestore --db mgl_bot --drop backup_folder/

# 4. Restart bot
pm2 start mgl-bot
```

#### **Mass Data Loss**
```bash
# 1. Check backup availability
ls -la backups/ | head -10

# 2. Restore specific collections
mongorestore --db mgl_bot --collection couples backup/couples.bson

# 3. Verify data integrity
node scripts/verify_database.js

# 4. Notify users if needed
```

#### **Performance Issues**
```bash
# 1. Check MongoDB performance
db.currentOp()
db.stats()

# 2. Check bot memory usage
pm2 monit

# 3. Restart if necessary
pm2 restart mgl-bot

# 4. Check logs
pm2 logs mgl-bot --lines 100
```

### **📈 Performance Monitoring**

#### **Key Metrics to Monitor**
- **Response Time:** < 2 seconds average
- **Database Queries:** < 100ms average
- **Memory Usage:** < 500MB
- **Error Rate:** < 1%
- **Active Couples:** Growth trend
- **Daily Active Users:** Engagement metrics

#### **MongoDB Performance Optimization**
```javascript
// Thêm indexes quan trọng
db.couples.createIndex({user1: 1, user2: 1})
db.couples.createIndex({server_id: 1})
db.intimacy_points.createIndex({couple_id: 1})
db.inventories.createIndex({couple_id: 1})
db.dating_profiles.createIndex({user_id: 1})
db.dating_profiles.createIndex({server_id: 1})
```

---

*📝 Tài liệu được tạo tự động từ phân tích source code - Cập nhật: Tháng 6, 2025*

---

## ⚡ QUICK TEST COMMANDS - LỆNH TEST NHANH

### **🚀 Test Nhanh 5 Phút - Kiểm Tra Cơ Bản**
```bash
# 1. Test help system (30 giây)
mhelp → Bấm tất cả nút → Kiểm tra navigation

# 2. Test dating flow (2 phút)  
henho @partner → đợi partner dongy → nguoiyeu

# 3. Test shop (1 phút)
mloveshop → ua hoa_hong 1 → react ✅ → dungvatpham hoa_hong

# 4. Test intimacy (1 phút)
tangthanmat → om @partner → hon @partner

# 5. Quick verification (30 giây)
dscd → kiểm tra couple xuất hiện trong list
```

### **⚡ Test Nhanh Từng Module**

#### **🔧 MAIN.PY - 30 giây**
```bash
mhelp                    # Expect: Menu với 6 nút
→ Bấm "Hẹn Hò"          # Expect: Embed lệnh hẹn hò  
→ Bấm "Cửa Hàng"        # Expect: Embed lệnh shop
→ Bấm "Trang Chủ"       # Expect: Quay về menu chính
```

#### **💕 DATING.PY - 1 phút**
```bash
henho @user             # Expect: Embed tỏ tình
(Partner) dongy         # Expect: Thành cặp đôi
nguoiyeu               # Expect: Thông tin couple
dscd                   # Expect: Xuất hiện trong danh sách
```

#### **🔍 DATING_MATCH.PY - 2 phút**  
```bash
mdatingprofile         # Tạo/xem profile
mdating               # Duyệt hồ sơ, bấm ❤️/❌
mtoptt               # Xem rankings
```

#### **💝 INTIMACY.PY - 1 phút**
```bash
tangthanmat           # Expect: +10 điểm
om @partner           # Expect: +5 điểm, cooldown 1h
hon @partner          # Expect: +8 điểm, cooldown 2h
```

#### **🛍️ SHOP.PY - 1 phút**
```bash
mloveshop             # Xem catalog
ua hoa_hong 2         # Mua 2 hoa hồng
→ React ✅            # Confirm purchase
dungvatpham hoa_hong  # Sử dụng 1 hoa hồng
```

#### **👨‍👩‍👧‍👦 FAMILY.PY - 30 giây** (cần kết hôn trước)
```bash
sinhcon               # Sinh con (cần đủ điểm)
contoi                # Xem thông tin con
chamsoccon [tên]      # Chăm sóc con
```

#### **🏠 HOUSE.PY - 30 giây** (cần kết hôn trước)
```bash
muanha villa          # Mua nhà (cần đủ xu)
nhacuatoi            # Xem thông tin nhà
```

#### **🐾 PET.PY - 30 giây**
```bash
muapet dog            # Nhận nuôi chó
petcuatoi            # Xem thông tin pet
chamsocpet [tên]     # Chăm sóc pet
```

#### **🎮 LOVE.PY - 15 giây**
```bash
love User1 User2      # Tính độ hợp đôi
mlove                 # Love với "Mẫu Giáo Lớn"
```

#### **⚙️ ADMIN.PY - 30 giây** (cần quyền admin)
```bash
setintimacy @u1 @u2 1000    # Set điểm thân mật
quatang @user hoa_hong 5    # Tặng vật phẩm
forcebreakup @user          # Ép chia tay
```

### **📊 Quick Verification Checklist**

#### **✅ Database Quick Check**
```javascript
// MongoDB quick queries
db.couples.count()                    // Số cặp đôi
db.intimacy_points.count()           // Số record điểm thân mật  
db.inventories.count()               // Số inventory
db.dating_profiles.count()           // Số profile hẹn hò
```

#### **✅ Common Error Patterns**
```bash
# Test các lỗi phổ biến
henho @self              # → Error: Tự tỏ tình
dongy (no request)       # → Error: Không có lời mời
tangthanmat (2nd time)   # → Error: Cooldown
ua fake_item             # → Error: Vật phẩm không tồn tại
```

### **🎯 Priority Testing Order**

#### **P0 - Critical (Test đầu tiên):**
1. `mhelp` - Menu hoạt động
2. `henho` → `dongy` - Dating flow
3. `mloveshop` → `ua` - Shop functions
4. `tangthanmat` - Daily gift
5. Admin commands working

#### **P1 - High (Test tiếp theo):**
1. Dating profile system
2. Physical interactions
3. Marriage system
4. Family features  
5. House system

#### **P2 - Medium (Test khi có thời gian):**
1. Pet system
2. Love calculation
3. Rankings
4. Advanced features

#### **P3 - Low (Enhancement):**
1. UI improvements
2. Additional commands
3. Extended customization
4. Performance optimizations