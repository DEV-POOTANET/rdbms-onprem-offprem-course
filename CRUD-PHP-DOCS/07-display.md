# 07: แสดงข้อมูลทั้งหมด 

เอกสารนี้ใช้สำหรับแสดงข้อมูลผู้ใช้ทั้งหมดจากตาราง `student`  
โดยต้องผ่านการเข้าสู่ระบบก่อนจึงจะสามารถเข้าถึงได้

---

## สร้างไฟล์ display.php

1. เปิดโฟลเดอร์โปรเจกต์ `crud-php`
2. สร้างไฟล์ชื่อ  display.php

3. เขียนโค้ดดังนี้

```php
<?php
session_start();
include "connect.php";

if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

$sql = "SELECT * FROM student";
$result = mysqli_query($condb, $sql);

if (!$result) {
    die("เกิดข้อผิดพลาดในการดึงข้อมูล");
}

$num = mysqli_num_rows($result);
?>
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="utf-8">
    <title>แสดงข้อมูลทั้งหมด</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-4">

    <div class="text-center mb-3">
        แสดงข้อมูลทั้งหมด <strong><?php echo $num; ?></strong> คน |
        <a href="menu.php">กลับหน้าหลัก</a>
    </div>

    <table class="table table-bordered table-striped table-hover text-center">
        <thead class="table-dark">
            <tr>
                <th>ที่</th>
                <th>ชื่อ-สกุล</th>
                <th>ที่อยู่</th>
                <th>Username</th>
                <th>รายละเอียด</th>
                <th>แก้ไข</th>
                <th>ลบ</th>
            </tr>
        </thead>

        <tbody>
        <?php
        $n = 1;
        while ($row = mysqli_fetch_assoc($result)) {
        ?>
            <tr>
                <td><?php echo $n++; ?></td>
                <td class="text-start"><?php echo $row['name']; ?></td>
                <td class="text-start"><?php echo $row['address']; ?></td>
                <td><?php echo $row['username']; ?></td>
                <td>
                    <a href="detail.php?did=<?php echo $row['id']; ?>" class="btn btn-info btn-sm">
                        รายละเอียด
                    </a>
                </td>
                <td>
                    <a href="formedit.php?did=<?php echo $row['id']; ?>" class="btn btn-warning btn-sm">
                        แก้ไข
                    </a>
                </td>
                <td>
                    <a href="deleteuser.php?did=<?php echo $row['id']; ?>"
                       class="btn btn-danger btn-sm"
                       onclick="return confirm('คุณต้องการลบใช่หรือไม่')">
                        ลบ
                    </a>
                </td>
            </tr>
        <?php
        }
        mysqli_close($condb);
        ?>
        </tbody>
    </table>

</div>

</body>
</html>
