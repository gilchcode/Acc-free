<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hệ Thống Vượt Link Nhận Tài Liệu</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: #ffffff;
            padding: 35px 40px;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 550px;
        }

        .view {
            display: none;
        }

        .view.active {
            display: block;
        }

        .center {
            text-align: center;
        }

        .icon {
            font-size: 50px;
            color: #4c51bf;
            margin-bottom: 15px;
        }

        h1 {
            color: #2d3748;
            font-size: 24px;
            margin-bottom: 10px;
        }

        p {
            color: #718096;
            font-size: 15px;
            margin-bottom: 25px;
            line-height: 1.5;
        }

        .step-box {
            background: #f7fafc;
            border: 2px dashed #cbd5e0;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 25px;
            text-align: left;
        }

        .step-title {
            font-weight: 600;
            color: #2d3748;
            margin-bottom: 8px;
            font-size: 16px;
        }

        .doc-title {
            font-size: 18px;
            font-weight: 600;
            color: #2b6cb0;
            margin-bottom: 8px;
        }

        .btn {
            display: inline-block;
            background: #4c51bf;
            color: white;
            padding: 12px 24px;
            font-size: 16px;
            font-weight: 600;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            text-decoration: none;
            transition: background 0.3s ease, transform 0.2s ease;
            width: 100%;
            margin-bottom: 12px;
            text-align: center;
        }

        .btn:hover {
            background: #434190;
            transform: translateY(-2px);
        }

        .btn-success {
            background: #48bb78;
        }
        .btn-success:hover {
            background: #38a169;
        }

        .btn-secondary {
            background: #e2e8f0;
            color: #4a5568;
        }

        .btn-secondary:hover {
            background: #cbd5e0;
        }

        .admin-link {
            margin-top: 15px;
            font-size: 13px;
            text-align: center;
        }

        .admin-link a {
            color: #a0aec0;
            text-decoration: none;
        }

        .admin-link a:hover {
            color: #4c51bf;
        }

        /* Form & Admin Styling */
        .form-group {
            margin-bottom: 15px;
            text-align: left;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
            color: #4a5568;
            font-size: 14px;
        }

        .form-group input {
            width: 100%;
            padding: 10px 14px;
            border: 1px solid #cbd5e0;
            border-radius: 8px;
            font-size: 14px;
        }

        .form-group input:focus {
            outline: none;
            border-color: #4c51bf;
        }

        .admin-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .table-responsive {
            max-height: 200px;
            overflow-y: auto;
            margin-bottom: 20px;
            border: 1px solid #e2e8f0;
            border-radius: 8px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            text-align: left;
            font-size: 13px;
        }

        th, td {
            padding: 8px 10px;
            border-bottom: 1px solid #e2e8f0;
        }

        th {
            background: #f7fafc;
            color: #4a5568;
            position: sticky;
            top: 0;
        }

        .action-btns button {
            padding: 4px 8px;
            font-size: 11px;
            margin-right: 4px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        .btn-edit { background: #d69e2e; color: white; }
        .btn-delete { background: #e53e3e; color: white; }
        
        .error-msg {
            color: #e53e3e;
            font-size: 13px;
            margin-bottom: 10px;
            text-align: center;
        }
    </style>
</head>
<body>

    <div class="container">

        <!-- 1. GIAO DIỆN TRANG CHỦ (YÊU CẦU VƯỢT LINK) -->
        <div id="bypassView" class="view active center">
            <div class="icon">🔒</div>
            <h1>Yêu Cầu Vượt Link</h1>
            <p>Để nhận tài liệu ngẫu nhiên miễn phí, vui lòng hoàn thành bước vượt link bên dưới để mở khóa hệ thống.</p>

            <div class="step-box center">
                <div class="step-title" style="color: #4c51bf; margin-bottom: 5px;">HƯỚNG DẪN</div>
                <p style="font-size: 14px; margin-bottom: 0;">1. Bấm nút <b>"Đi Đến Link Vượt"</b>.<br>2. Hoàn thành vượt link ở trang đích.<br>3. Quay lại đây để nhận tài liệu ngẫu nhiên!</p>
            </div>

            <button class="btn" onclick="openBypassLink()">🔗 Đi Đến Link Vượt Ngay</button>
            <button class="btn btn-success" id="btnUnlock" style="display:none;" onclick="showRandomDoc()">🎉 Đã Vượt Link Xong - Nhận Tài Liệu</button>
            
            <div class="admin-link">
                <a href="#" onclick="switchView('loginView')">🔐 Đăng nhập Quản trị viên</a>
            </div>
        </div>

        <!-- 2. GIAO DIỆN NHẬN TÀI LIỆU NGẪU NHIÊN (SAU KHI VƯỢT LINK THÀNH CÔNG) -->
        <div id="successView" class="view center">
            <div class="icon">🎁</div>
            <h1>Vượt Link Thành Công!</h1>
            <p>Cảm ơn bạn đã hoàn thành thử thách. Dưới đây là tài liệu ngẫu nhiên dành riêng cho bạn:</p>

            <div class="step-box">
                <div class="doc-title" id="docTitle">Đang tải tài liệu...</div>
                <p id="docDesc" style="margin-bottom: 0; color: #718096; font-size: 14px;"></p>
            </div>

            <a id="docLink" href="#" target="_blank" class="btn btn-success">📥 Mở / Tải Tài Liệu Ngay</a>
            <button class="btn btn-secondary" onclick="showRandomDoc()">🎲 Bốc Thêm Tài Liệu Khác</button>
            <button class="btn btn-secondary" style="background:#fff; color:#718096; border:1px solid #cbd5e0;" onclick="switchView('bypassView')">🔄 Quay Lại Trang Vượt Link</button>
        </div>

        <!-- 3. GIAO DIỆN ĐĂNG NHẬP -->
        <div id="loginView" class="view">
            <div class="center">
                <h1>Đăng Nhập Quản Trị</h1>
                <p>Nhập thông tin tài khoản admin của bạn</p>
            </div>
            
            <div id="loginError" class="error-msg"></div>

            <div class="form-group">
                <label>Tài khoản</label>
                <input type="text" id="username" placeholder="Nhập tài khoản">
            </div>
            <div class="form-group">
                <label>Mật khẩu</label>
                <input type="password" id="password" placeholder="Nhập mật khẩu">
            </div>

            <button class="btn" onclick="handleLogin()">Đăng Nhập</button>
            <button class="btn btn-secondary" onclick="switchView('bypassView')">Quay Lại Trang Chủ</button>
        </div>

        <!-- 4. GIAO DIỆN BẢNG ĐIỀU KHIỂN QUẢN TRỊ (ADMIN PANEL) -->
        <div id="adminView" class="view">
            <div class="admin-header">
                <h2>Quản Trị Hệ Thống</h2>
                <button class="btn btn-secondary" style="width: auto; padding: 6px 12px; margin: 0;" onclick="switchView('bypassView')">Đăng Xuất</button>
            </div>

            <!-- Cài đặt Link Vượt -->
            <div class="form-group" style="background: #f7fafc; padding: 12px; border-radius: 8px; border: 1px solid #e2e8f0;">
                <label style="color: #2b6cb0;">🔗 Cài Đặt Link Vượt (Link Rút Gọn)</label>
                <div style="display: flex; gap: 8px;">
                    <input type="url" id="inputBypassUrl" placeholder="https://link-rut-gon-cua-ban.com">
                    <button class="btn" style="width: auto; margin:0; padding: 0 15px;" onclick="saveBypassUrl()">Lưu Link</button>
                </div>
            </div>

            <label style="display: block; margin-bottom: 5px; font-weight: 600; color: #4a5568; font-size: 14px;">Danh Sách Tài Liệu Ngẫu Nhiên</label>
            <div class="table-responsive">
                <table id="docTable">
                    <thead>
                        <tr>
                            <th>Tiêu đề / Mô tả</th>
                            <th>Thao tác</th>
                        </tr>
                    </thead>
                    <tbody id="docTableBody">
                        <!-- Render bằng JS -->
                    </tbody>
                </table>
            </div>

            <form id="docForm" onsubmit="saveDocument(event)">
                <input type="hidden" id="editIndex" value="-1">
                <div class="form-group">
                    <label id="formLabelTitle">Thêm Tài Liệu Mới</label>
                    <input type="text" id="inputTitle" placeholder="Tên tài liệu..." required>
                </div>
                <div class="form-group">
                    <input type="text" id="inputDesc" placeholder="Mô tả ngắn về tài liệu..." required>
                </div>
                <div class="form-group">
                    <input type="url" id="inputUrl" placeholder="Đường dẫn tài liệu (Google Drive, v.v.)..." required>
                </div>

                <button type="submit" class="btn" id="saveBtnText">Thêm Tài Liệu</button>
            </form>
        </div>

    </div>

    <script>
        // Cấu hình tài khoản Quản trị viên mới
        const ADMIN_USER = "vudepzaii";
        const ADMIN_PASS = "Vudepz@i2910";

        // Mặc định Link Vượt (Link Rút Gọn) ban đầu
        const DEFAULT_BYPASS_LINK = "https://example.com/link-vượt-của-bạn";

        // Mặc định danh sách tài liệu khởi tạo
        const defaultDocuments = [
            {
                title: "Tài liệu Lập trình Web Nâng cao",
                desc: "Hướng dẫn xây dựng ứng dụng Fullstack từ cơ bản đến nâng cao.",
                url: "https://example.com/tai-lieu-1"
            },
            {
                title: "Bộ Script Game FPS Unity",
                desc: "Mã nguồn mẫu tối ưu hóa hệ thống bắn súng.",
                url: "https://example.com/tai-lieu-2"
            },
            {
                title: "Tổng hợp Đề thi và Lời giải Toán học",
                desc: "Tài liệu ôn tập chuyên sâu các dạng toán trọng tâm.",
                url: "https://example.com/tai-lieu-3"
            }
        ];

        // Lấy dữ liệu từ LocalStorage
        function getDocuments() {
            let docs = localStorage.getItem('site_documents');
            return docs ? JSON.parse(docs) : defaultDocuments;
        }

        function saveDocumentsToStorage(docs) {
            localStorage.setItem('site_documents', JSON.stringify(docs));
        }

        function getBypassLink() {
            return localStorage.getItem('site_bypass_link') || DEFAULT_BYPASS_LINK;
        }

        // Chuyển đổi giao diện
        function switchView(viewId) {
            document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
            document.getElementById(viewId).classList.add('active');
            
            if (viewId === 'bypassView') {
                // Reset trạng thái nút khi về trang chủ
                document.getElementById('btnUnlock').style.display = 'none';
            } else if (viewId === 'adminView') {
                renderAdminTable();
                resetForm();
                document.getElementById('inputBypassUrl').value = getBypassLink();
            }
        }

        // --- Luồng Vượt Link của Người Dùng ---
        function openBypassLink() {
            const targetLink = getBypassLink();
            // Mở link rút gọn trong tab mới
            window.open(targetLink, '_blank');
            
            // Hiển thị nút "Đã Vượt Link Xong" để người dùng bấm vào nhận tài liệu
            setTimeout(() => {
                document.getElementById('btnUnlock').style.display = 'inline-block';
            }, 1500); // Hiện sau 1.5 giây để họ kịp bấm sang tab vượt link
        }

        function showRandomDoc() {
            const documents = getDocuments();
            if (documents.length === 0) {
                alert("Hiện tại chưa có tài liệu nào trong hệ thống!");
                return;
            }
            
            // Chọn ngẫu nhiên một tài liệu
            const randomIndex = Math.floor(Math.random() * documents.length);
            const selectedDoc = documents[randomIndex];

            document.getElementById("docTitle").innerText = selectedDoc.title;
            document.getElementById("docDesc").innerText = selectedDoc.desc;
            document.getElementById("docLink").href = selectedDoc.url;

            switchView('successView');
        }

        // --- Đăng Nhập ---
        function handleLogin() {
            const user = document.getElementById("username").value.trim();
            const pass = document.getElementById("password").value.trim();
            const errorEl = document.getElementById("loginError");

            if (user === ADMIN_USER && pass === ADMIN_PASS) {
                errorEl.innerText = "";
                document.getElementById("username").value = "";
                document.getElementById("password").value = "";
                switchView('adminView');
            } else {
                errorEl.innerText = "Sai tài khoản hoặc mật khẩu!";
            }
        }

        // --- Quản Trị (Admin Panel) ---
        function saveBypassUrl() {
            const newUrl = document.getElementById('inputBypassUrl').value.trim();
            if (!newUrl) {
                alert("Vui lòng nhập đường dẫn hợp lệ!");
                return;
            }
            localStorage.setItem('site_bypass_link', newUrl);
            alert("Đã lưu Link Vượt thành công!");
        }

        function renderAdminTable() {
            const documents = getDocuments();
            const tbody = document.getElementById("docTableBody");
            tbody.innerHTML = "";

            documents.forEach((doc, index) => {
                const tr = document.createElement("tr");
                tr.innerHTML = `
                    <td><strong>${doc.title}</strong><br><small style="color:#718096">${doc.desc}</small></td>
                    <td class="action-btns" style="white-space: nowrap;">
                        <button class="btn-edit" onclick="editDoc(${index})">Sửa</button>
                        <button class="btn-delete" onclick="deleteDoc(${index})">Xóa</button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function saveDocument(event) {
            event.preventDefault();
            const index = parseInt(document.getElementById("editIndex").value);
            const title = document.getElementById("inputTitle").value.trim();
            const desc = document.getElementById("inputDesc").value.trim();
            const url = document.getElementById("inputUrl").value.trim();

            let documents = getDocuments();

            if (index === -1) {
                documents.push({ title, desc, url });
            } else {
                documents[index] = { title, desc, url };
            }

            saveDocumentsToStorage(documents);
            renderAdminTable();
            resetForm();
            alert("Lưu tài liệu thành công!");
        }

        function editDoc(index) {
            const documents = getDocuments();
            const doc = documents[index];

            document.getElementById("editIndex").value = index;
            document.getElementById("inputTitle").value = doc.title;
            document.getElementById("inputDesc").value = doc.desc;
            document.getElementById("inputUrl").value = doc.url;

            document.getElementById("formLabelTitle").innerText = "Chỉnh Sửa Tài Liệu";
            document.getElementById("saveBtnText").innerText = "Cập Nhật Tài Liệu";
        }

        function deleteDoc(index) {
            if (confirm("Bạn có chắc chắn muốn xóa tài liệu này không?")) {
                let documents = getDocuments();
                documents.splice(index, 1);
                saveDocumentsToStorage(documents);
                renderAdminTable();
                resetForm();
            }
        }

        function resetForm() {
            document.getElementById("editIndex").value = -1;
            document.getElementById("inputTitle").value = "";
            document.getElementById("inputDesc").value = "";
            document.getElementById("inputUrl").value = "";
            document.getElementById("formLabelTitle").innerText = "Thêm Tài Liệu Mới";
            document.getElementById("saveBtnText").innerText = "Thêm Tài Liệu";
        }
    </script>
</body>
</html>
