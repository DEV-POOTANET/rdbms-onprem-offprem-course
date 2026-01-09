# 08: ลบข้อมูลผู้ใช้ 

เอกสารนี้ใช้สำหรับลบข้อมูลผู้ใช้จากตาราง `student`  
โดยสามารถลบได้เฉพาะกรณีที่ผู้ใช้เข้าสู่ระบบแล้วเท่านั้น

---

## สร้างไฟล์ deleteuser.php

1. เปิดโฟลเดอร์โปรเจกต์ `crud-php`
2. สร้างไฟล์ชื่อ deleteuser.php

3. เขียนโค้ดดังนี้

```php
<?php
session_start();
include "connect.php";

// เช็คว่า login แล้วหรือยัง
if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

// ตรวจว่ามีการส่ง id มาหรือไม่
if (!isset($_GET['did'])) {
    header("Location: display.php");
    exit();
}

$id = $_GET['did']; 

// ลบข้อมูล
$sql = "DELETE FROM student WHERE id = '$id'";
$result = mysqli_query($condb, $sql);

// ตรวจผลลัพธ์
if ($result) {
    echo "<script>
            alert('ลบข้อมูลเรียบร้อย');
            window.location='display.php';
          </script>";
} else {
    echo "<script>
            alert('ไม่สามารถลบข้อมูลได้');
            history.back();
          </script>";
}

mysqli_close($condb);
?>
