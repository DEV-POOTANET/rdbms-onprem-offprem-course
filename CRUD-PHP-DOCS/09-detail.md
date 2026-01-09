# 09: แสดงรายละเอียดสมาชิก 

ไฟล์นี้ใช้สำหรับ **แสดงข้อมูลรายละเอียดของสมาชิก 1 คน**
โดยเรียกดูจากหน้า `display.php` ผ่านการส่งค่า `id` มาทาง URL

---

## สร้างไฟล์ detail.php

1. เปิดโฟลเดอร์โปรเจกต์
2. สร้างไฟล์ชื่อ  detail.php

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
    <title>รายละเอียดสมาชิก</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
    <div class="card mx-auto" style="max-width: 400px;">
        <div class="card-body">

            <h3 class="text-center mb-4">รายละเอียดสมาชิก</h3>

            <table class="table table-bordered">
                <tr>
                    <th>ชื่อ-สกุล</th>
                    <td><?php echo $row['name']; ?></td>
                </tr>

                <tr>
                    <th>ที่อยู่</th>
                    <td><?php echo $row['address']; ?></td>
                </tr>

                <tr class="table-secondary text-center">
                    <th colspan="2">ข้อมูลระบบ</th>
                </tr>

                <tr>
                    <th>Username</th>
                    <td><?php echo $row['username']; ?></td>
                </tr>

                <tr>
                    <th>Password</th>
                    <td>********</td>
                </tr>
            </table>

            <div class="text-center">
                <a href="display.php" class="btn btn-secondary">
                    กลับหน้าแสดงข้อมูล
                </a>
            </div>

        </div>
    </div>
</div>

</body>
</html>
