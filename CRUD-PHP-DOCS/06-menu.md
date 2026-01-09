# 06: หน้าเมนูหลักหลังเข้าสู่ระบบ

เอกสารนี้เป็นขั้นตอนหลังจากผู้ใช้เข้าสู่ระบบสำเร็จ  
ใช้สำหรับแสดงหน้าเมนูหลัก โดยตรวจสอบ session และดึงข้อมูลผู้ใช้จากฐานข้อมูลมาแสดง

---

## สร้างไฟล์หน้าเมนูหลัก

1. เปิดโฟลเดอร์โปรเจกต์ `crud-php`
2. สร้างไฟล์ชื่อ menu.php

3. เขียนโค้ดดังนี้

```php
<?php
session_start();
include "connect.php";

if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

$id = $_SESSION['sess_id'];

$sql = "SELECT * FROM student WHERE id = '$id'";
$result = mysqli_query($condb, $sql);

if (!$result) {
    die("เกิดข้อผิดพลาด");
}

$row = mysqli_fetch_assoc($result);
?>
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="utf-8">
    <title>เมนูหลัก</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
    <div class="card mx-auto" style="max-width: 500px;">
        <div class="card-body text-center">

            <h3 class="mb-3">
                ยินดีต้อนรับคุณ <br>
                <?php echo $_SESSION['name']; ?>
            </h3>

            <img src="imgstd/<?php echo $row['images']; ?>" 
                 class="img-thumbnail mb-4" 
                 width="200">

            <div class="d-grid gap-2 mb-3">
                <a href="display.php" class="btn btn-primary">
                    แสดงข้อมูลทั้งหมด
                </a>

                <a href="formeditme.php" 
                   class="btn btn-warning">
                    แก้ไขข้อมูลส่วนตัว
                </a>

                <a href="editimages.php" 
                   class="btn btn-info">
                    แก้ไขรูป Profile
                </a>
            </div>

            <a href="logout.php" class="btn btn-danger">
                ออกจากระบบ
            </a>

        </div>
    </div>
</div>

</body>
</html>
    