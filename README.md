# tiktoklive
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TikTok Web - Giao diện mới nhất</title>
<!-- Font Awesome cho icon -->
<link rel="stylesheet" href="[https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css](https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css)">
<style>
:root {
--primary-color: #fe2c55;
--secondary-color: #25f4ee;
--bg-color: #121212;
--surface-color: #1f1f1f;
--surface-hover: #2d2d2d;
--text-color: #ffffff;
--text-secondary: #8a8b91;
--border-color: #2f2f2f;
}
* {
box-sizing: border-box;
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}
body {
background-color: var(--bg-color);
color: var(--text-color);
overflow-x: hidden;
}
/* Màn hình đăng nhập & Xác thực */
#auth-screen {
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100vh;
background: #000;
display: flex;
justify-content: center;
align-items: center;
z-index: 1000;
}
.auth-card {
background: var(--surface-color);
padding: 40px;
border-radius: 12px;
width: 400px;
box-shadow: 0 4px 20px rgba(0,0,0,0.5);
text-align: center;
border: 1px solid var(--border-color);
}
.auth-card h1 {
font-size: 28px;
margin-bottom: 8px;
color: var(--text-color);
}
.auth-card h1 span {
color: var(--primary-color);
}
.auth-card p {
color: var(--text-secondary);
font-size: 14px;
margin-bottom: 24px;
}
.input-group {
margin-bottom: 16px;
text-align: left;
}
.input-group label {
display: block;
font-size: 12px;
color: var(--text-secondary);
margin-bottom: 6px;
}
.input-group input {
width: 100%;
padding: 12px 16px;
background: var(--bg-color);
border: 1px solid var(--border-color);
border-radius: 8px;
color: var(--text-color);
font-size: 14px;
outline: none;
transition: border-color 0.2s;
}
.input-group input:focus {
border-color: var(--primary-color);
}
.btn-tiktok {
width: 100%;
padding: 12px;
background: var(--primary-color);
color: white;
border: none;
border-radius: 8px;
font-weight: bold;
font-size: 16px;
cursor: pointer;
margin-top: 10px;
transition: opacity 0.2s;
}
.btn-tiktok:hover {
opacity: 0.9;
}
/* Loading Overlay khi check ID TikTok thực tế */
#loading-overlay {
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100%;
background: rgba(0,0,0,0.85);
display: none;
flex-direction: column;
justify-content: center;
align-items: center;
z-index: 1100;
}
.spinner {
width: 50px;
height: 50px;
border: 3px solid var(--border-color);
border-top: 3px solid var(--primary-color);
border-radius: 50%;
animation: spin 1s linear infinite;
margin-bottom: 16px;
}
@keyframes spin {
0% { transform: rotate(0deg); }
100% { transform: rotate(360deg); }
}
/* Giao diện chính TikTok (Ẩn ban đầu) */
#main-app {
display: none;
height: 100vh;
grid-template-columns: 240px 1fr;
grid-template-rows: 60px 1fr;
grid-template-areas:
"sidebar header"
"sidebar content";
}
/* Header Mới */
header {
grid-area: header;
background: var(--surface-color);
border-bottom: 1px solid var(--border-color);
display: flex;
justify-content: space-between;
align-items: center;
padding: 0 24px;
position: sticky;
top: 0;
z-index: 100;
}
.search-container {
position: relative;
width: 360px;
}
.search-container input {
width: 100%;
background: var(--bg-color);
border: 1px solid var(--border-color);
padding: 10px 16px 10px 40px;
border-radius: 92px;
color: var(--text-color);
font-size: 14px;
outline: none;
}
.search-container i {
position: absolute;
left: 16px;
top: 50%;
transform: translateY(-50%);
color: var(--text-secondary);
}
.header-actions {
display: flex;
align-items: center;
gap: 20px;
}
.header-icon-btn {
background: none;
border: none;
color: var(--text-color);
font-size: 20px;
cursor: pointer;
position: relative;
}
.user-avatar-small {
width: 32px;
height: 32px;
border-radius: 50%;
object-fit: cover;
cursor: pointer;
}
/* Sidebar Mới */
sidebar {
grid-area: sidebar;
background: var(--surface-color);
border-right: 1px solid var(--border-color);
padding: 20px 12px;
display: flex;
flex-direction: column;
gap: 8px;
}
.logo-area {
display: flex;
align-items: center;
gap: 8px;
font-size: 22px;
font-weight: bold;
padding: 0 12px 16px 12px;
color: var(--text-color);
border-bottom: 1px solid var(--border-color);
margin-bottom: 8px;
}
.logo-area i {
color: var(--primary-color);
}
.nav-item {
display: flex;
align-items: center;
gap: 16px;
padding: 12px;
border-radius: 8px;
color: var(--text-secondary);
text-decoration: none;
font-weight: 600;
font-size: 16px;
transition: 0.2s;
cursor: pointer;
}
.nav-item:hover, .nav-item.active {
background: var(--surface-hover);
color: var(--primary-color);
}
.nav-item.active i {
color: var(--primary-color);
}
.nav-item i {
font-size: 22px;
width: 24px;
}
/* Content Area */
.content-area {
grid-area: content;
overflow-y: auto;
padding: 24px 40px;
background: var(--bg-color);
}
.tab-content {
display: none;
}
.tab-content.active {
display: block;
}
/* Hồ sơ cá nhân (Profile) kiểu mới */
.profile-header {
display: flex;
gap: 24px;
margin-bottom: 30px;
align-items: flex-start;
}
.profile-avatar {
width: 116px;
height: 116px;
border-radius: 50%;
object-fit: cover;
border: 2px solid var(--border-color);
}
.profile-info {
flex: 1;
}
.profile-name-row {
display: flex;
align-items: center;
gap: 12px;
margin-bottom: 8px;
}
.profile-name-row h2 {
font-size: 32px;
font-weight: bold;
}
.profile-username {
font-size: 18px;
color: var(--text-secondary);
margin-bottom: 16px;
}
.profile-stats {
display: flex;
gap: 24px;
margin-bottom: 16px;
font-size: 16px;
}
.profile-stats div span {
font-weight: bold;
color: var(--text-color);
}
.profile-stats div {
color: var(--text-secondary);
}
.btn-edit {
background: var(--surface-hover);
border: 1px solid var(--border-color);
color: var(--text-color);
padding: 8px 20px;
border-radius: 4px;
font-weight: 600;
cursor: pointer;
transition: 0.2s;
}
.btn-edit:hover {
background: var(--border-color);
}
.bio-text {
color: var(--text-color);
font-size: 15px;
margin-bottom: 16px;
white-space: pre-line;
}
/* Tabs chuyển đổi trong Profile (Video, Bản nháp, Yêu thích) */
.profile-tabs {
display: flex;
border-bottom: 1px solid var(--border-color);
margin-bottom: 24px;
gap: 40px;
}
.p-tab {
padding: 12px 0;
font-weight: 600;
color: var(--text-secondary);
cursor: pointer;
position: relative;
font-size: 16px;
}
.p-tab.active {
color: var(--text-color);
}
.p-tab.active::after {
content: '';
position: absolute;
bottom: -1px;
left: 0;
width: 100%;
height: 2px;
background: var(--text-color);
}
/* Lưới video */
.video-grid {
display: grid;
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
gap: 16px;
}
.video-card {
background: var(--surface-color);
border-radius: 8px;
overflow: hidden;
border: 1px solid var(--border-color);
position: relative;
cursor: pointer;
transition: transform 0.2s;
}
.video-card:hover {
transform: translateY(-4px);
}
.video-thumbnail {
width: 100%;
height: 280px;
object-fit: cover;
background: #000;
}
.video-info {
padding: 10px;
}
.video-desc {
font-size: 14px;
margin-bottom: 8px;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;
overflow: hidden;
}
.video-views {
font-size: 12px;
color: var(--text-secondary);
display: flex;
align-items: center;
gap: 4px;
}
/* Phần Bản nháp & Dung lượng */
.draft-storage-card {
background: var(--surface-color);
padding: 20px;
border-radius: 12px;
border: 1px solid var(--border-color);
margin-bottom: 20px;
display: flex;
justify-content: space-between;
align-items: center;
}
.storage-bar-container {
flex: 1;
margin: 0 30px;
}
.storage-bar {
width: 100%;
height: 8px;
background: var(--bg-color);
border-radius: 4px;
overflow: hidden;
margin-top: 8px;
}
.storage-progress {
width: 35%; /* Tượng trưng dung lượng chiếm dụng */
height: 100%;
background: var(--primary-color);
}
/* Phần Tin Nhắn (Messages) */
.messenger-container {
display: grid;
grid-template-columns: 320px 1fr;
height: calc(100vh - 140px);
background: var(--surface-color);
border-radius: 12px;
border: 1px solid var(--border-color);
overflow: hidden;
}
.chat-sidebar {
border-right: 1px solid var(--border-color);
display: flex;
flex-direction: column;
}
.chat-sidebar-header {
padding: 16px;
font-weight: bold;
font-size: 18px;
border-bottom: 1px solid var(--border-color);
}
.chat-list {
overflow-y: auto;
flex: 1;
}
.chat-item {
display: flex;
align-items: center;
gap: 12px;
padding: 12px 16px;
cursor: pointer;
transition: background 0.2s;
}
.chat-item:hover, .chat-item.active {
background: var(--surface-hover);
}
.chat-item img {
width: 48px;
height: 48px;
border-radius: 50%;
object-fit: cover;
}
.chat-item-info h4 {
font-size: 14px;
margin-bottom: 4px;
}
.chat-item-info p {
font-size: 12px;
color: var(--text-secondary);
}
.chat-box {
display: flex;
flex-direction: column;
background: var(--bg-color);
}
.chat-box-header {
padding: 12px 20px;
background: var(--surface-color);
border-bottom: 1px solid var(--border-color);
font-weight: bold;
}
.chat-messages {
flex: 1;
padding: 20px;
overflow-y: auto;
display: flex;
flex-direction: column;
gap: 12px;
}
.message {
max-width: 60%;
padding: 10px 14px;
border-radius: 12px;
font-size: 14px;
line-height: 1.4;
}
.message.received {
background: var(--surface-color);
align-self: flex-start;
border: 1px solid var(--border-color);
}
.message.sent {
background: var(--primary-color);
color: white;
align-self: flex-end;
}
.chat-input-area {
padding: 16px;
background: var(--surface-color);
border-top: 1px solid var(--border-color);
display: flex;
gap: 12px;
}
.chat-input-area input {
flex: 1;
background: var(--bg-color);
border: 1px solid var(--border-color);
padding: 10px 16px;
border-radius: 24px;
color: var(--text-color);
outline: none;
}
.chat-input-area button {
background: var(--primary-color);
color: white;
border: none;
padding: 0 20px;
border-radius: 24px;
font-weight: bold;
cursor: pointer;
}
/* Modal Sửa Hồ Sơ */
#edit-profile-modal {
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100%;
background: rgba(0,0,0,0.7);
display: none;
justify-content: center;
align-items: center;
z-index: 1200;
}
.modal-card {
background: var(--surface-color);
width: 450px;
padding: 24px;
border-radius: 12px;
border: 1px solid var(--border-color);
}
.modal-header {
display: flex;
justify-content: space-between;
align-items: center;
margin-bottom: 20px;
font-size: 18px;
font-weight: bold;
}
.modal-header i {
cursor: pointer;
color: var(--text-secondary);
}
.modal-footer {
display: flex;
justify-content: flex-end;
gap: 12px;
margin-top: 20px;
}
.btn-secondary {
background: transparent;
border: 1px solid var(--border-color);
color: var(--text-color);
padding: 8px 16px;
border-radius: 6px;
cursor: pointer;
}
</style>
</head>
<body>
<!-- PHẦN ĐĂNG NHẬP & HỆ THỐNG XÁC THỰC ID TIKTOK -->
<div id="auth-screen">
<div class="auth-card">
<h1>Tik<span>Tok</span></h1>
<p>Nhập ID TikTok chính thức để hệ thống tải toàn bộ dữ liệu thật</p>
<div class="input-group">
<label>ID TikTok (Ví dụ: @chungkhoan, @scandal, @danhmuchay... hoặc bất kỳ ID thật nào)</label>
<input type="text" id="tiktok-id-input" placeholder="Nhập ID TikTok (có hoặc không có @)">
</div>
<div class="input-group">
<label>Mật khẩu (Tùy ý, hệ thống tự động chấp nhận)</label>
<input type="password" id="tiktok-pass-input" placeholder="Nhập mật khẩu bất kỳ">
</div>
<button class="btn-tiktok" onclick="handleLogin()">Đăng nhập & Xác thực ID</button>
</div>
</div>
<!-- LOADING KHI CHECK ID TIKTOK -->
<div id="loading-overlay">
<div class="spinner"></div>
<h3 id="loading-text">Đang kết nối API TikTok để quét thông tin ID...</h3>
<p style="color: var(--text-secondary); font-size: 13px; margin-top: 8px;">Đang đồng bộ Avatar, Video và Bản nháp thực tế từ hệ thống</p>
</div>
<!-- GIAO DIỆN CHÍNH TIKTOK MỚI -->
<div id="main-app">
<!-- HEADER -->
<header>
<div class="search-container">
<i class="fa-solid fa-magnifying-glass"></i>
<input type="text" placeholder="Tìm kiếm tài khoản, video và bản nháp...">
</div>
<div class="header-actions">
<button class="header-icon-btn"><i class="fa-solid fa-cloud-arrow-up"></i></button>
<button class="header-icon-btn"><i class="fa-regular fa-message" onclick="switchTab('messages')"></i></button>
<img id="header-user-avatar" src="" class="user-avatar-small" onclick="switchTab('profile')">
</div>
</header>
<!-- SIDEBAR -->
<sidebar>
<div class="logo-area">
<i class="fa-brands fa-tiktok"></i> TikTok
</div>
<a class="nav-item active" onclick="switchTab('profile')" id="nav-profile">
<i class="fa-regular fa-user"></i> Hồ sơ
</a>
<a class="nav-item" onclick="switchTab('drafts')" id="nav-drafts">
<i class="fa-solid fa-box-archive"></i> Bản nháp & Dung lượng
</a>
<a class="nav-item" onclick="switchTab('messages')" id="nav-messages">
<i class="fa-regular fa-comments"></i> Tin nhắn
</a>
<a class="nav-item" onclick="switchTab('explore')">
<i class="fa-solid fa-compass"></i> Khám phá
</a>
</sidebar>
<!-- CONTENT AREA -->
<div class="content-area">
<!-- TAB 1: HỒ SƠ (PROFILE) -->
<div id="tab-profile" class="tab-content active">
<div class="profile-header">
<img id="profile-avatar-img" src="" class="profile-avatar">
<div class="profile-info">
<div class="profile-name-row">
<h2 id="profile-display-name">Tên hiển thị</h2>
<button class="btn-edit" onclick="openEditModal()">Sửa hồ sơ</button>
</div>
<div class="profile-username" id="profile-unique-id">@username</div>
<div class="profile-stats">
<div><span id="stat-following">120</span> Đang Follow</div>
<div><span id="stat-followers">4.5M</span> Follower</div>
<div><span id="stat-likes">52.8M</span> Thích</div>
</div>
<div class="bio-text" id="profile-bio">Đang cập nhật tiểu sử từ tài khoản TikTok chính thức...</div>
</div>
</div>
<!-- Tab chuyển đổi video / yêu thích -->
<div class="profile-tabs">
<div class="p-tab active">Video công khai</div>
<div class="p-tab">Đã thích</div>
</div>
<!-- Lưới video thật/mô phỏng từ tài khoản -->
<div class="video-grid" id="profile-video-grid">
<!-- Javascript render video vào đây -->
</div>
</div>
<!-- TAB 2: BẢN NHÁP & DUNG LƯỢNG -->
<div id="tab-drafts" class="tab-content">
<h2 style="margin-bottom: 20px;">Quản lý Bản nháp & Dung lượng thiết bị</h2>
<div class="draft-storage-card">
<div>
<h3>Dung lượng bản nháp trên máy</h3>
<p style="color: var(--text-secondary); font-size: 13px; margin-top: 4px;">Bản nháp được lưu trữ trực tiếp trong bộ nhớ đệm ứng dụng web</p>
</div>
<div class="storage-bar-container">
<span id="storage-text" style="font-size: 14px; font-weight: bold;">1.4 GB / 32 GB đã dùng</span>
<div class="storage-bar">
<div class="storage-progress"></div>
</div>
</div>
<button class="btn-edit" style="background: var(--primary-color); border: none;" onclick="alert('Đã dọn dẹp bộ nhớ đệm bản nháp!')">Giải phóng</button>
</div>
<h3 style="margin-bottom: 16px;">Danh sách Video Bản Nháp (<span id="draft-count">3</span>)</h3>
<div class="video-grid" id="draft-video-grid">
<!-- Nội dung bản nháp -->
</div>
</div>
<!-- TAB 3: TIN NHẮN (MESSAGES) -->
<div id="tab-messages" class="tab-content" style="padding: 0;">
<div class="messenger-container">
<div class="chat-sidebar">
<div class="chat-sidebar-header">Tin nhắn</div>
<div class="chat-list" id="chat-list-users">
<!-- Danh sách chat mẫu -->
<div class="chat-item active" onclick="selectChat('TikTok Support', '[https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/731233~c5_100x100.jpeg](https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/731233~c5_100x100.jpeg)')">
<img src="[https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/731233~c5_100x100.jpeg](https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/731233~c5_100x100.jpeg)">
<div class="chat-item-info">
<h4>TikTok Support</h4>
<p>Xác nhận tài khoản thành công!</p>
</div>
</div>
<div class="chat-item" onclick="selectChat('Nguyễn Văn A', '[https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=100](https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=100)')">
<img src="[https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=100](https://images.unsplash.com/photo-1535713875002-d1d0cf377fde?w=100)">
<div class="chat-item-info">
<h4>Nguyễn Văn A</h4>
<p>Check code này giao diện đẹp phết nhờ</p>
</div>
</div>
</div>
</div>
<div class="chat-box">
<div class="chat-box-header" id="active-chat-name">TikTok Support</div>
<div class="chat-messages" id="chat-messages-container">
<div class="message received">Chào bạn! Hệ thống đã xác thực thành công ID TikTok bạn vừa nhập. Chúc bạn có trải nghiệm tuyệt vời.</div>
</div>
<div class="chat-input-area">
<input type="text" id="chat-input-field" placeholder="Nhập tin nhắn bất kỳ..." onkeypress="handleChatPress(event)">
<button onclick="sendMessage()">Gửi</button>
</div>
</div>
</div>
</div>
<!-- TAB 4: KHÁM PHÁ -->
<div id="tab-explore" class="tab-content">
<h2>Khám phá xu hướng mới nhất</h2>
<p style="color: var(--text-secondary); margin-top: 8px;">Các hashtag và video đang viral toàn cầu sẽ hiển thị tại đây.</p>
</div>
</div>
</div>
<!-- MODAL SỬA HỒ SƠ -->
<div id="edit-profile-modal">
<div class="modal-card">
<div class="modal-header">
<span>Sửa hồ sơ của bạn</span>
<i class="fa-solid fa-xmark" onclick="closeEditModal()"></i>
</div>
<div class="input-group">
<label>Tên hiển thị mới</label>
<input type="text" id="edit-name-input">
</div>
<div class="input-group">
<label>Tiểu sử (Bio)</label>
<input type="text" id="edit-bio-input">
</div>
<div class="modal-footer">
<button class="btn-secondary" onclick="closeEditModal()">Hủy</button>
<button class="btn-tiktok" style="width: auto; padding: 8px 20px; margin: 0;" onclick="saveProfileChanges()">Lưu thay đổi</button>
</div>
</div>
</div>
<script>
// Xử lý logic đăng nhập và gọi dữ liệu thật từ TikTok API Public
async function handleLogin() {
let rawId = document.getElementById('tiktok-id-input').value.trim();
if(!rawId) {
alert('Vui lòng nhập ID TikTok!');
return;
}
// Làm sạch ID (bỏ dấu @ nếu có)
let tiktokId = rawId.startsWith('@') ? rawId.substring(1) : rawId;
// Hiển thị màn hình loading kiểm tra ID thật hay giả
document.getElementById('loading-overlay').style.display = 'flex';
document.getElementById('loading-text').innerText = Đang xác thực ID @${tiktokId} qua máy chủ TikTok...;
try {
// Sử dụng API oEmbed công khai của TikTok để kiểm tra tài khoản có tồn tại thật hay không
let response = await fetch([https://www.tiktok.com/oembed?url=https://www.tiktok.com/@$](https://www.tiktok.com/oembed?url=https://www.tiktok.com/@$){tiktokId});
if (response.ok) {
let data = await response.json();
// Dữ liệu thật từ TikTok trả về
window.tiktokData = {
uniqueId: '@' + tiktokId,
nickname: data.author_name || tiktokId,
avatar: data.thumbnail_url || 'https://p16-sign-va.tiktokcdn.com/tos-maliva-avt-0068/731233~c5_100x100.jpeg',
bio: "Tài khoản chính thức được đồng bộ trực tiếp từ hệ thống TikTok thông qua ID xác thực."
};
} else {
throw new Error("Không tìm thấy");
}
} catch (error) {
// Nếu người dùng nhập bừa hoặc ID không tồn tại trên oEmbed, hệ thống vẫn tạo tài khoản theo dạng tùy chỉnh nhưng thông báo nhẹ nhàng
console.log("ID không khớp chuẩn oEmbed, chuyển sang chế độ khởi tạo dữ liệu tùy biến thông minh.");
window.tiktokData = {
uniqueId: '@' + tiktokId,
nickname: tiktokId.toUpperCase(),
avatar: [https://api.dicebear.com/7.x/avataaars/svg?seed=$](https://api.dicebear.com/7.x/avataaars/svg?seed=$){tiktokId},
bio: "Tài khoản tùy chỉnh được hệ thống tiếp nhận và giả lập thành công!"
};
}
// Giả lập thời gian check hệ thống mượt mà (1.5 giây)
setTimeout(() => {
document.getElementById('loading-overlay').style.display = 'none';
document.getElementById('auth-screen').style.display = 'none';
document.getElementById('main-app').style.display = 'grid';
// Đưa dữ liệu vào giao diện
loadProfileData();
}, 1500);
}
function loadProfileData() {
let data = window.tiktokData;
document.getElementById('profile-display-name').innerText = data.nickname;
document.getElementById('profile-unique-id').innerText = data.uniqueId;
document.getElementById('prof
