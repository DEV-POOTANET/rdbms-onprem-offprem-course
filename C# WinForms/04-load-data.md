# Lab 02: C# Windows Forms Loda data from DB

## รายวิชา

On-Premise and Off-Premise Relational Database Management

---


## ขั้นตอนที่ 1: สร้าง folder Models เพื่อเก็บไฟล์ Models

* สร้าง folder Models
* สร้าง class Job

<img src="images/cj.png" width="600">

## ขั้นตอนที่ 2: สร้าง folder Data สำหรับเก็บเารื่องการจัดการกับข้อมูล

* สร้าง folder Data

* ย้าย  ไฟล์ `DatabaseHelper.cs` มาเก็บใน folder Data

* สร้าง folder Repositories ใน `Data`
* สร้าง interface  ชื่อ `IJobRepository`

<img src="images/ij.png" width="600">


* สร้าง class ชื่อ `JobRepository` 

<img src="images/crj.png" width="600">

## ขั้นตอนที่ 2: ใช้ dataGridView ในการแสดงข้อมูล
* เพิ่ม dataGridView ใน form job

<img src="images/fdgv.png" width="600">

* เอาข้อมูลมาแสดงใน dataGridView

<img src="images/cdgv.png" width="600">

* ผลการทำงาน dataGridView

<img src="images/res.png" width="600">

* การปรับแต่ง dataGridView

<img src="images/dgvcust.png" width="600">


<img src="images/res2.png" width="600">