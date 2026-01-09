# 04: สร้างฟอร์มสมัครสมาชิก (register.html)

เอกสารนี้ใช้สำหรับสร้างหน้าแบบฟอร์มสมัครสมาชิกด้วยภาษา HTML และ Bootstrap  
เพื่อส่งข้อมูลไปบันทึกในฐานข้อมูลด้วยไฟล์ PHP ในขั้นตอนถัดไป

---

## สร้างไฟล์ register.html

1. เปิดโฟลเดอร์โปรเจกต์ `crud-php` ใน **Visual Studio Code**
2. สร้างไฟล์ใหม่ชื่อ register.html

3. เขียนโค้ดตามตัวอย่างด้านล่าง

```html
<!DOCTYPE html>
<html lang="th">
<head>
 <meta charset="utf-8">
 <title>สมัครสมาชิก</title>

 <!-- Bootstrap CSS (CDN) -->
 <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
 <div class="card mx-auto" style="max-width: 400px;">
     <div class="card-body">

         <h3 class="text-center mb-4">สมัครสมาชิก</h3>

         <form method="post" action="save.php">

             <div class="mb-3">
                 <label class="form-label">ชื่อ-สกุล</label>
                 <input type="text" name="name" class="form-control" required>
             </div>

             <div class="mb-3">
                 <label class="form-label">ที่อยู่</label>
                 <input type="text" name="address" class="form-control" required>
             </div>

             <hr>

             <h5 class="text-center">ข้อมูลระบบ</h5>

             <div class="mb-3">
                 <label class="form-label">Username</label>
                 <input type="text" name="user" class="form-control" required>
             </div>

             <div class="mb-3">
                 <label class="form-label">Password</label>
                 <input type="password" name="pwd" class="form-control" required>
             </div>

             <div class="d-flex justify-content-between">
                 <button type="submit" class="btn btn-primary">สมัครสมาชิก</button>
                 <button type="reset" class="btn btn-secondary">ลบข้อมูล</button>
             </div>

         </form>

     </div>
 </div>
</div>

</body>
</html>
```

ทดสอบการทำงาน

เปิดเว็บเบราว์เซอร์ เข้าไปที่ http://localhost/crud-php/register.html


## สร้างไฟล์ save.php

1. เปิดโฟลเดอร์โปรเจกต์ `crud-php`
2. สร้างไฟล์ใหม่ชื่อ save.php

3. เขียนโค้ดตามตัวอย่างด้านล่าง

```php
<?php
include "connect.php";

// ตรวจสอบว่ากรอกข้อมูลครบหรือไม่
if (
    empty($_POST['name']) ||
    empty($_POST['address']) ||
    empty($_POST['user']) ||
    empty($_POST['pwd'])
) {
    echo "<script>
            alert('กรุณากรอกข้อมูลให้ครบ');
            history.back();
          </script>";
    exit();
}

// รับค่าจากฟอร์ม
$name = $_POST['name'];
$address = $_POST['address'];
$user = $_POST['user'];
$pwd = $_POST['pwd'];

// เข้ารหัสรหัสผ่าน (สำคัญมาก)
$pwd_hash = password_hash($pwd, PASSWORD_DEFAULT);

// คำสั่ง SQL
$sql = "INSERT INTO student (name, address, username, password)
        VALUES ('$name', '$address', '$user', '$pwd_hash')";

// สั่งบันทึกข้อมูล
$result = mysqli_query($condb, $sql);

// ตรวจสอบผลลัพธ์
if ($result) {
    echo "<script>
            alert('สมัครสมาชิกเรียบร้อย');
            window.location='login.html';
          </script>";
} else {
    echo "<script>
            alert('เกิดข้อผิดพลาด');
            history.back();
          </script>";
}

mysqli_close($condb);
?>
