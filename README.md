<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>โปรไฟล์ของฉัน</title>
  <style>
    body {
      font-family: sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      background-color: #f0f2f5;
    }
    #profile {
      text-align: center;
      background-color: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }
    img {
      border-radius: 50%;
      width: 100px;
      height: 100px;
    }
    h2 {
      margin: 10px 0;
    }
    p {
      color: #666;
    }
    button {
      background-color: #00B900;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 15px;
    }
  </style>
</head>
<body>
  <div id="profile">
    <img id="pictureUrl" src="https://via.placeholder.com/100" alt="Profile Picture">
    <h2 id="displayName">กำลังโหลด...</h2>
    <p id="userId">กรุณารอสักครู่</p>
    <button id="closeButton">ปิด</button>
  </div>

  <script src="https://static.line-scdn.net/liff/edge/2/sdk.js"></script>
  <script>
    async function main() {
      // 1. เริ่มต้น LIFF
      await liff.init({ liffId: "2007267285-0Ro3ZRYE" });

      // 2. ตรวจสอบว่าล็อกอินหรือยัง
      if (!liff.isLoggedIn()) {
        liff.login();
      } else {
        // 3. ดึงข้อมูลโปรไฟล์
        const profile = await liff.getProfile();

        // 4. นำข้อมูลไปแสดงผล
        document.getElementById("pictureUrl").src = profile.pictureUrl;
        document.getElementById("displayName").textContent = profile.displayName;
        document.getElementById("userId").textContent = "User ID: " + profile.userId;
      }

      // 5. ตั้งค่าปุ่มปิด
      document.getElementById("closeButton").addEventListener('click', () => {
        liff.closeWindow();
      });
    }
    main();
  </script>
</body>
</html>
