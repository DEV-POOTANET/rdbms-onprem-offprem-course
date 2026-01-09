# 05: เข้าสู่ระบบ (Login)

เอกสารนี้ใช้สำหรับสร้างหน้าเข้าสู่ระบบ  
เพื่อรับค่า Username และ Password จากผู้ใช้

---

## สร้างไฟล์ login.html

1. เปิดโฟลเดอร์โปรเจกต์ `crud-php`
2. สร้างไฟล์ชื่อ  login.html

3. เขียนโค้ดดังนี้

```html
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="utf-8">
    <title>เข้าสู่ระบบ</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
    <div class="card mx-auto" style="max-width: 400px;">
        <div class="card-body">

            <h3 class="text-center mb-4">เข้าสู่ระบบ</h3>

            <form method="post" action="check.php">

                <div class="mb-3">
                    <label class="form-label">Username</label>
                    <input type="text" name="user" class="form-control" required>
                </div>

                <div class="mb-3">
                    <label class="form-label">Password</label>
                    <input type="password" name="pwd" class="form-control" required>
                </div>

                <div class="d-flex justify-content-between">
                    <button type="submit" class="btn btn-primary">เข้าสู่ระบบ</button>
                    <button type="reset" class="btn btn-secondary">ลบข้อมูล</button>
                </div>

                <div class="text-center mt-3">
                    <a href="register.html">สมัครสมาชิกใหม่</a>
                </div>

            </form>

        </div>
    </div>
</div>

</body>
</html>
```

## สร้างไฟล์ check.php


1. สร้างไฟล์ใหม่ชื่อ check.php

2. เขียนโค้ดตามตัวอย่างด้านล่าง

```php
<?php
session_start();
include "connect.php";

// ตรวจว่ามีการส่งค่ามาหรือไม่
if (empty($_POST['user']) || empty($_POST['pwd'])) {
    echo "<script>
            alert('กรุณากรอก Username และ Password');
            history.back();
          </script>";
    exit();
}

$user = $_POST['user'];
$pwd  = $_POST['pwd'];

// ค้นหา username
$sql = "SELECT * FROM student WHERE username = '$user'";
$result = mysqli_query($condb, $sql);

// ตรวจว่าพบ username หรือไม่
if (mysqli_num_rows($result) == 1) {

    $row = mysqli_fetch_assoc($result);

    // ตรวจรหัสผ่าน (สำคัญมาก)
    if (password_verify($pwd, $row['password'])) {

        // เก็บข้อมูลลง session
        $_SESSION['sess_id'] = $row['id'];
        $_SESSION['name']    = $row['name'];

        // ไปหน้าเมนู
        header("Location: menu.php");
        exit();

    } else {
        // password ผิด
        echo "<script>
                alert('รหัสผ่านไม่ถูกต้อง');
                history.back();
              </script>";
    }

} else {
    // ไม่พบ username
    echo "<script>
            alert('ไม่พบ Username นี้');
            history.back();
          </script>";
}

mysqli_close($condb);
?>
