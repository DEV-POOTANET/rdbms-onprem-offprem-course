# 03: สร้างไฟล์เชื่อมต่อฐานข้อมูล (connect.php)

เอกสารนี้ใช้สำหรับสร้างไฟล์เชื่อมต่อฐานข้อมูล MySQL ด้วยภาษา PHP เพื่อใช้ในระบบ CRUD

---

## สร้างไฟล์ connect.php

1. เปิดโปรเจกต์ `crud-php` ใน **Visual Studio Code**
2. สร้างไฟล์ใหม่ชื่อ connect.php

3. เขียนโค้ดตามตัวอย่างด้านล่าง

```php
<?php
// แสดง error เฉพาะตอนพัฒนา
error_reporting(E_ALL);
ini_set('display_errors', 1);

// ตั้งค่า timezone
date_default_timezone_set('Asia/Bangkok');

// ข้อมูลเชื่อมต่อฐานข้อมูล
$db_host = "localhost";
$db_user = "root";
$db_pass = "";
$db_name = "dbstd";

// เชื่อมต่อฐานข้อมูล
$condb = mysqli_connect($db_host, $db_user, $db_pass, $db_name);

// ตรวจสอบการเชื่อมต่อ
if (!$condb) {
 die("เชื่อมต่อฐานข้อมูลไม่สำเร็จ");
}

// ตั้งค่า charset (ป้องกันปัญหาภาษา)
mysqli_set_charset($condb, "utf8mb4");
?>

```
ทอดสอบ http://localhost/crud-php/connect.php จะต้องไม่มี error