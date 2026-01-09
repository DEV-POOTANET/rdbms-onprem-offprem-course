# 12: แก้ไขข้อมูลส่วนตัว 

ไฟล์นี้ใช้สำหรับ **ให้สมาชิกแก้ไขข้อมูลของตนเอง**
โดยดึง `id` จาก `session` (ไม่ใช้ GET)  
เหมาะสำหรับสอนแนวคิด **สิทธิ์ผู้ใช้ (User can edit only their own data)**

---

## สร้างไฟล์ formeditme.php
1. เปิดโฟลเดอร์โปรเจกต์
2. สร้างไฟล์ชื่อ  formeditme.php

3. เขียนโค้ดดังนี้

```php
<?php
session_start();

if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

include "connect.php";

$i = $_SESSION['sess_id'];

$sql = "SELECT * FROM student WHERE id='$i'";
$result = mysqli_query($condb, $sql);
$row = mysqli_fetch_assoc($result);
mysqli_close($condb);
?>
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="utf-8">
    <title>แก้ไขข้อมูลส่วนตัว</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
    <div class="card mx-auto" style="max-width: 450px;">
        <div class="card-body">

            <h3 class="text-center mb-4">แก้ไขข้อมูลส่วนตัว</h3>

            <form method="post" action="updateme.php">

                <div class="mb-3">
                    <label class="form-label">ชื่อ-สกุล</label>
                    <input type="text" name="name"
                           value="<?php echo $row['name']; ?>"
                           class="form-control" required>
                </div>

                <div class="mb-3">
                    <label class="form-label">ที่อยู่</label>
                    <input type="text" name="address"
                           value="<?php echo $row['address']; ?>"
                           class="form-control" required>
                </div>

                <hr>

                <h5 class="text-center">ข้อมูลระบบ</h5>

                <div class="mb-3">
                    <label class="form-label">Username</label>
                    <input type="text" name="user"
                           value="<?php echo $row['username']; ?>"
                           class="form-control" required>
                </div>

                <div class="mb-3">
                    <label class="form-label">Password ใหม่</label>
                    <input type="password" name="pwd" class="form-control">
                    <small class="text-muted">
                        เว้นว่าง หากไม่ต้องการเปลี่ยนรหัสผ่าน
                    </small>
                </div>

                <div class="d-flex justify-content-between">
                    <button type="submit" class="btn btn-success">
                        ปรับปรุงข้อมูล
                    </button>

                    <button type="reset" class="btn btn-secondary">
                        ลบข้อมูล
                    </button>
                </div>

            </form>

        </div>
    </div>
</div>

</body>
</html>
```
## สร้างไฟล์ updateme.php

1. เปิดโฟลเดอร์โปรเจกต์
2. สร้างไฟล์ชื่อ  updateme.php

3. เขียนโค้ดดังนี้
```php
<?php
session_start();
include "connect.php";

// ต้อง login ก่อน
if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

// รับค่าจากฟอร์ม
$n = $_POST['name'];
$a = $_POST['address'];
$u = $_POST['user'];
$p = $_POST['pwd'];

// ใช้ id จาก session 
$i = $_SESSION['sess_id'];

// ตรวจค่าว่าง (ยกเว้น password)
if (empty($n) || empty($a) || empty($u)) {
    echo "<script>
            alert('กรุณากรอกข้อมูลให้ครบ');
            history.back();
          </script>";
    exit();
}

// ถ้ามีการกรอกรหัสใหม่
if (!empty($p)) {

    // hash password
    $p_hash = password_hash($p, PASSWORD_DEFAULT);

    $sql = "UPDATE student 
            SET name='$n',
                address='$a',
                username='$u',
                password='$p_hash'
            WHERE id='$i'";
} else {

    // ไม่เปลี่ยน password
    $sql = "UPDATE student 
            SET name='$n',
                address='$a',
                username='$u'
            WHERE id='$i'";
}

mysqli_query($condb, $sql);
mysqli_close($condb);

// อัปเดตชื่อใน session
$_SESSION['name'] = $n;

// กลับหน้าหลัก
echo "<script>
        alert('ปรับปรุงข้อมูลเรียบร้อย');
        window.location='menu.php';
      </script>";
?>
