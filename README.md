<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Công ty Âu Thị - Quản lý & Bảo trì Hệ thống Điện mặt trời</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    let sites = [
      { name: 'Huy Hưng', company: 'Công ty Huy Hưng', owner: 'Nguyễn Văn A', device: '', schedule: '', log: '', errors: '' },
      { name: 'Quang điện Quê Hương', company: 'CT Quê Hương', owner: 'Trần Văn B', device: '', schedule: '', log: '', errors: '' },
      { name: 'Năng lượng Phúc Điền', company: 'CT Phúc Điền', owner: 'Lê Văn C', device: '', schedule: '', log: '', errors: '' },
      { name: 'Anh Dũng Phú Gia', company: 'CT Phú Gia', owner: 'Phạm Văn D', device: '', schedule: '', log: '', errors: '' },
      { name: 'Năng lượng Sơn Hải', company: 'CT Sơn Hải', owner: 'Đỗ Văn E', device: '', schedule: '', log: '', errors: '' },
      { name: 'Solar Đinh Lăng', company: 'CT Đinh Lăng', owner: 'Ngô Văn F', device: '', schedule: '', log: '', errors: '' },
      { name: 'Năng lượng AD', company: 'CT AD', owner: 'Bùi Văn G', device: '', schedule: '', log: '', errors: '' },
      { name: 'Quang Mikha', company: 'CT Mikha', owner: 'Đinh Văn H', device: '', schedule: '', log: '', errors: '' },
      { name: 'Sơn Hải Solar', company: 'CT Sơn Hải Solar', owner: 'Trương Văn I', device: '', schedule: '', log: '', errors: '' },
      { name: 'Năng lượng Quốc Cường', company: 'CT Quốc Cường', owner: 'Phan Văn K', device: '', schedule: '', log: '', errors: '' },
      { name: 'Khánh Tùng', company: 'CT Khánh Tùng', owner: 'Vũ Văn L', device: '', schedule: '', log: '', errors: '' },
      { name: 'Quang Minh', company: 'CT Quang Minh', owner: 'Hoàng Văn M', device: '', schedule: '', log: '', errors: '' }
    ];

    function filterSites() {
      const filter = document.getElementById('siteFilter').value.toLowerCase();
      const list = document.getElementById('siteList');
      list.innerHTML = '';
      sites.forEach((site, index) => {
        if (site.name.toLowerCase().includes(filter)) {
          const div = document.createElement('div');
          div.className = 'p-2 border rounded shadow bg-white mb-2';
          div.innerHTML = `
            <div class="flex justify-between items-center">
              <input type='text' class='text-lg font-semibold border-b focus:outline-none' value='${site.name}' onchange='updateSiteName(${index}, this.value)'>
              <button class='bg-blue-600 text-white px-3 py-1 rounded' onclick='openSiteDetail(${index})'>Xem chi tiết</button>
            </div>
            <div class='text-sm text-gray-600 mt-1'>🏢 ${site.company} | 👤 ${site.owner}</div>`;
          list.appendChild(div);
        }
      });
    }

    function updateSiteName(index, newName) {
      sites[index].name = newName;
      filterSites();
    }

    function addNewSite() {
      const name = prompt("Nhập tên site:");
      const company = prompt("Nhập tên công ty chủ quản:");
      const owner = prompt("Nhập tên chủ đầu tư:");
      if (name && company && owner) {
        sites.push({ name: name.trim(), company: company.trim(), owner: owner.trim(), device: '', schedule: '', log: '', errors: '' });
        filterSites();
        alert("🆕 Site đã được thêm. Bấm 'Xem chi tiết' để nhập thông tin chi tiết về thiết bị và bảo trì.");
      }
    }

    function openSiteDetail(index) {
      const site = sites[index];
      const popup = window.open('', '_blank', 'width=800,height=600');
      popup.document.write(`<!DOCTYPE html><html lang='vi'><head><meta charset='UTF-8'><title>Chi tiết Site</title>
        <style>
          body { font-family: sans-serif; padding: 20px; }
          .btn { background: #1d4ed8; color: white; padding: 10px 16px; border: none; border-radius: 4px; cursor: pointer; margin: 10px 5px; display: inline-block; }
          .btn:hover { background-color: #2563eb; }
          .form { margin: 10px 0; }
          .form input, .form textarea { width: 100%; padding: 8px; margin: 4px 0; border: 1px solid #ccc; border-radius: 4px; }
          label { font-weight: bold; }
        </style>
        <script>
          function saveSiteData() {
            const device = document.getElementById('device').value;
            const schedule = document.getElementById('schedule').value;
            const log = document.getElementById('log').value;
            const errors = document.getElementById('errors').value;
            window.opener.sites[${index}].device = device;
            window.opener.sites[${index}].schedule = schedule;
            window.opener.sites[${index}].log = log;
            window.opener.sites[${index}].errors = errors;
            alert("✅ Dữ liệu đã được lưu tạm thời trong bộ nhớ trình duyệt!");
          }
        </script>
        </head><body>
        <h2>📌 Site: ${site.name}</h2>
        <p>🏢 <b>Công ty:</b> ${site.company}</p>
        <p>👤 <b>Chủ đầu tư:</b> ${site.owner}</p>

        <h3 class="section-title">📋 Nhập chi tiết:</h3>

        <div class="form">
          <label>📦 Danh sách thiết bị:</label>
          <textarea id="device" rows="4">${site.device || ''}</textarea>
        </div>

        <div class="form">
          <label>🗓️ Lịch bảo trì định kỳ:</label>
          <textarea id="schedule" rows="3">${site.schedule || ''}</textarea>
        </div>

        <div class="form">
          <label>🛠️ Nhật ký bảo trì:</label>
          <textarea id="log" rows="3">${site.log || ''}</textarea>
        </div>

        <div class="form">
          <label>❗ Check mã lỗi thường gặp:</label>
          <textarea id="errors" rows="2">${site.errors || ''}</textarea>
        </div>

        <button onclick='saveSiteData()' class='btn'>💾 Lưu</button>
        <button onclick='window.close()' class='btn' style='background:#dc2626;'>Đóng</button>
      </body></html>`);
      popup.document.close();
    }
  </script>
</head>
<body class="bg-gray-100 p-6">
  <div class="max-w-4xl mx-auto">
    <h1 class="text-2xl font-bold mb-4">Công ty Âu Thị - Quản lý & Bảo trì Hệ thống Điện mặt trời</h1>

    <label class="block mb-2 font-semibold">🔍 Lọc theo tên site:</label>
    <input id="siteFilter" oninput="filterSites()" class="w-full p-2 border rounded mb-4" placeholder="Nhập tên site...">

    <button onclick="addNewSite()" class="mb-4 px-4 py-2 bg-green-600 text-white rounded">➕ Thêm site mới</button>

    <div id="siteList" class="space-y-2"></div>
  </div>

  <script>
    window.onload = filterSites;
  </script>
</body>
</html>
