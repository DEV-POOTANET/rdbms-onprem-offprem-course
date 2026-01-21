# Lab 02: C# Windows Forms Layout

## รายวิชา

On-Premise and Off-Premise Relational Database Management

---


## ขั้นตอนที่ 1: สร้างโปรเจกต์ Windows Forms

1. เปิด Visual Studio
2. เลือก **Create a new project**
3. เลือก **Windows Forms App (.NET Framework)**
<<<<<<< HEAD

<img src="images/createPJ.png" width="600">
    
4. ตั้งชื่อโปรเจกต์
=======
   
    <img src="images/createPJ.png" width="600">
    
5. ตั้งชื่อโปรเจกต์
>>>>>>> db2557064f5c72908d6a3fab14c61d0d337c7822

   ```text
   HRWinFormApp
   ```
6. กด Create

---

## ขั้นตอนที่ 2: โครงสร้างฟอร์ม (Main Form Layout)

### ฟอร์มหลัก (Form1)

กำหนดคุณสมบัติ

* Name: `FrmMain`
* Text: `HR Management System`
* StartPosition: `CenterScreen`
* Size: `900 x 600`

<img src="images/Form1.png" width="600">

---

## ขั้นตอนที่ 3: Layout ด้วย Panel

<img src="images/pan.png" width="600">

### Panel หลัก main


* Name: `panMain`
* เลือก `Dock in parent container`

<img src="images/panmain.png" width="600">
---

### Panel ด้านซ้าย (Menu)


* Name: `panMenu`
* จัดตำแหน่งตามรูป

<img src="images/panmenu.png" width="600">

เพิ่มปุ่มเมนู และสี

* Button: `btnMeuEmp` → Text: Employees
* Button: `btnMeuDep` → Text: Departments
* Button: `btnMeuJob` → Text: Jobs

<img src="images/btmen.png" width="600">
---

### Panel เนื้อหา (Content)


* Name: `panContent`
* จัดตำแหน่งตามรูป

<img src="images/pancon.png" width="600">
---

### Panel เนื้อหาย่อย (Sub Content)

* Sub Content คือเนื้อหาย่อยๆ ที่อยู่ใน Panel ของ ตัวเอง และวางอยู่ บน Panel Content โดยจะมีเนื่อหาได้มากกว่า 1 Panel ใน Panel Content 
* ให้เพิ่ม 3 Panel
    - Name: `panEmp`
    - Name: `panDep`
    - Name: `panJob`

    <img src="images/subpan.png" width="600">
    
* ใส่ label ให้ Panel panEmp โดยต้อง เลือก Panal ขึ้นมาก่อน

    <img src="images/panemp1.png" width="600">

    <img src="images/lblems.png" width="600">


* ถ้าต้องการจะย่อให้เล็กลง ให้ทำตามภาพ

    <img src="images/undock.png" width="600">

ทำต่อให้ครบทุก panel
---

## ขั้นตอนที่ 4: เขียนโปรแกรมจัดการ Panel
* ปิดการแสดงผลเมื่อเริ่มโปรแกรม

    <img src="images/01.png" width="600">

* เมื่อกดปุ่มให้แสดงผล เมนู ตามที่กด

    <img src="images/02.png" width="600">
---

## ขั้นตอนที่ 5 การเรีบก Form มาแสดง ใน panel

สร้าง Form ใหม่ 
* Form: `FRMJOB` 

<img src="images/nf.png" width="600">

* เลือก Form(windowsform)

<img src="images/FRMJOB.png" width="600">

* เช็คขนาดของ panel panContent

<img src="images/pans.png" width="600">

* ปรับขนาดของ Form FRMJOB ให้เท่ากับ panContent
* เพิ่ม label ใน Form FRMJOB

<img src="images/ex1.png" width="600">

เพิ่มปุ่มใน form1 ชื่อ `btnjobfrm`

<img src="images/btj.png" width="600">


## ขั้นตอนที่ 6: เขียนโปรแกรมจัดการ Form

* เขียนโปรแกรมจัดการปุ่ม ให้เปิด form

<img src="images/opcf.png" width="600">
<img src="images/btjop.png" width="600">

* ปรับ code เพิ่ม เพื่อให้ การจัดการ panel ยังใช้งานได้

<img src="images/edtsp.png" width="600">

## ขั้นตอนที่ 7: Clean Code ให้อ่านง่าย
แก้ไขตามภาพ
<img src="images/cc1.png" width="600">
<img src="images/cc02.png" width="600">
