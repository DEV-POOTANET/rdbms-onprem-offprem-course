# 11: แก้ไขรูปโปรไฟล์ 

ไฟล์นี้ใช้สำหรับ **อัปโหลดและเปลี่ยนรูปโปรไฟล์ของสมาชิก**
โดยจำกัดชนิดไฟล์เป็น JPG และ PNG  
และส่งไฟล์ไปประมวลผลที่ `updateimg.php`

---

## สร้างไฟล์ editimages.php
1. เปิดโฟลเดอร์โปรเจกต์
2. สร้างไฟล์ชื่อ  editimages.php

3. เขียนโค้ดดังนี้

```php
<?php
session_start();

if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

$im = $_SESSION['sess_id'];
?>
<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="utf-8">
    <title>แก้ไขรูปโปรไฟล์</title>

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

<div class="container mt-5">
    <div class="card mx-auto" style="max-width: 450px;">
        <div class="card-body">

            <h3 class="text-center mb-4">แก้ไขรูปโปรไฟล์</h3>

            <form method="POST" action="updateimg.php" enctype="multipart/form-data">

                <div class="mb-3">
                    <label class="form-label">เลือกรูปโปรไฟล์</label>
                    <input type="file" name="fileimg"
                           class="form-control"
                           accept="image/jpeg,image/png" required>
                </div>

                <div class="text-center mb-3">
                    <small class="text-muted">
                        เฉพาะไฟล์ JPG, PNG เท่านั้น
                    </small>
                </div>

                <div class="d-flex justify-content-between">
                    <button type="submit" class="btn btn-primary">
                        Upload
                    </button>

                    <a href="menu.php" class="btn btn-secondary">
                        กลับ
                    </a>
                </div>

            </form>

        </div>
    </div>
</div>

</body>
</html>
```

## สร้างไฟล์ updateimg.php

1. เปิดโฟลเดอร์โปรเจกต์
2. สร้างไฟล์ชื่อ  updateimg.php

3. เขียนโค้ดดังนี้
```php
<?php
session_start();

// ต้อง login ก่อน
if (!isset($_SESSION['sess_id'])) {
    header("Location: login.html");
    exit();
}

$id = $_SESSION['sess_id']; 

// ตรวจว่ามีไฟล์หรือไม่
if (!empty($_FILES['fileimg']['tmp_name'])) {

    $type = $_FILES['fileimg']['type'];
    $size = $_FILES['fileimg']['size'];

    // อนุญาตเฉพาะ jpg, png
    if ($type != "image/jpeg" && $type != "image/png") {
        echo "<script>
                alert('อนุญาตเฉพาะไฟล์ JPG หรือ PNG');
                history.back();
              </script>";
        exit();
    }

    // จำกัดขนาดไฟล์ไม่เกิน 2MB
    if ($size > 2 * 1024 * 1024) {
        echo "<script>
                alert('ขนาดไฟล์ต้องไม่เกิน 2MB');
                history.back();
              </script>";
        exit();
    }

    // ตั้งชื่อตาม id + นามสกุล
    $ext = ($type == "image/png") ? ".png" : ".jpg";
    $img = $id . $ext;

    // ย้ายไฟล์ 
    move_uploaded_file($_FILES['fileimg']['tmp_name'], "./imgstd/" . $img);

    include "connect.php";
    $sql = "UPDATE student SET images='$img' WHERE id='$id'";
    mysqli_query($condb, $sql);
    mysqli_close($condb);

    echo "<script>
            alert('อัปโหลดรูปเรียบร้อย');
            window.location='menu.php';
          </script>";

} else {
    header("Location: menu.php");
}
?>
