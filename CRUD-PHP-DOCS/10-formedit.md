# 10: แก้ไขข้อมูลสมาชิก 

ไฟล์นี้ใช้สำหรับ **แสดงฟอร์มแก้ไขข้อมูลสมาชิก**
โดยดึงข้อมูลเดิมจากฐานข้อมูลมาแสดงใน input
และส่งข้อมูลไปอัปเดตที่ไฟล์ `update.php`

---

## สร้างไฟล์ formedit.php

1. เปิดโฟลเดอร์โปรเจกต์
2. สร้างไฟล์ชื่อ  formedit.php

3. เขียนโค้ดดังนี้

```php
<?php
session_start();
include "connect.php";

if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

if (!isset($_GET['did'])) {
    header("Location: display.php");
    exit();
}

$id = $_GET['did'];

$sql = "SELECT * FROM student WHERE id = '$id'";
$result = mysqli_query($condb, $sql);

if (!$result) {
    die("เกิดข้อผิดพลาด");
}

$row = mysqli_fetch_assoc($result);
mysqli_close($condb);
?>
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="utf-8">
    <title>แก้ไขข้อมูลสมาชิก</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
    <div class="card mx-auto" style="max-width: 450px;">
        <div class="card-body">

            <h3 class="text-center mb-4">แก้ไขข้อมูลสมาชิก</h3>

            <form method="post" action="update.php">

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
                    <label class="form-label">เปลี่ยนรหัสผ่าน</label>
                    <input type="password" name="pwd"
                           class="form-control"
                           placeholder="กรอกเฉพาะกรณีเปลี่ยน">
                </div>

                <div class="text-center">
                    <input type="hidden" name="hid" value="<?php echo $row['id']; ?>">

                    <button type="submit" class="btn btn-success">
                        ปรับปรุงข้อมูล
                    </button>

                    <button type="reset" class="btn btn-secondary">
                        ล้างข้อมูล
                    </button>
                </div>

            </form>

        </div>
    </div>
</div>

</body>
</html>

```
## สร้างไฟล์ update.php

1. เปิดโฟลเดอร์โปรเจกต์ `crud-php`
2. สร้างไฟล์ใหม่ชื่อ update.php

3. เขียนโค้ดตามตัวอย่างด้านล่าง

```php
<?php
session_start();
include "connect.php";

// เช็ค login
if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

// ตรวจค่าว่าง
if (
    empty($_POST['name']) ||
    empty($_POST['address']) ||
    empty($_POST['user']) ||
    empty($_POST['hid'])
) {
    echo "<script>
            alert('ข้อมูลไม่ครบ');
            history.back();
          </script>";
    exit();
}

$name = $_POST['name'];
$address = $_POST['address'];
$user = $_POST['user'];
$pwd = $_POST['pwd'];
$id = $_POST['hid'];

// ถ้ามีการกรอกรหัสใหม่
if (!empty($pwd)) {

    $pwd_hash = password_hash($pwd, PASSWORD_DEFAULT);

    $sql = "UPDATE student 
            SET name='$name',
                address='$address',
                username='$user',
                password='$pwd_hash'
            WHERE id='$id'";

} else {

    // ไม่เปลี่ยน password
    $sql = "UPDATE student 
            SET name='$name',
                address='$address',
                username='$user'
            WHERE id='$id'";
}

$result = mysqli_query($condb, $sql);

// ตรวจผลลัพธ์
if ($result) {

    // อัปเดตชื่อใน session
    $_SESSION['name'] = $name;

    echo "<script>
            alert('ปรับปรุงข้อมูลเรียบร้อย');
            window.location='menu.php';
          </script>";
} else {
    echo "<script>
            alert('ไม่สามารถปรับปรุงข้อมูลได้');
            history.back();
          </script>";
}

mysqli_close($condb);
?>
