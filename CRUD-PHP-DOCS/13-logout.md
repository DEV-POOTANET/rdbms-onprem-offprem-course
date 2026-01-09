# 13: ออกจากระบบ (logout.php)

ไฟล์นี้ใช้สำหรับ **ออกจากระบบ (Logout)**
โดยการลบข้อมูล session ทั้งหมด แล้วพาผู้ใช้กลับไปหน้า Login

---

## สร้างไฟล์ logout.php
1. เปิดโฟลเดอร์โปรเจกต์
2. สร้างไฟล์ชื่อ  logout.php

3. เขียนโค้ดดังนี้

```php
<?php
session_start();

// ลบข้อมูล session ทั้งหมด
session_unset();

// ทำลาย session
session_destroy();

// กลับไปหน้า login
header("Location: login.html");
exit();
?>
