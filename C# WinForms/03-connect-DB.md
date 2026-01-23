# Lab 03: C# Windows Forms Connect database

## รายวิชา

On-Premise and Off-Premise Relational Database Management

---


## ขั้นตอนที่ 1: ติดตั้ง NuGet Package

ติดตั้ง ชื่อแพ็กเกจ:` MySql.Data`

<img src="images/ng.png" width="600">
<img src="images/mysqlng.png" width="600">

หรือ ติดตังผ่าน Package Manager Console

```shell
Install-Package MySql.Data
```

---

## เขียน ไฟล์ connect database 

สร้างไฟล์ใหม่เป็น class ชื่อ `DatabaseHelper.cs`
เพิ่มตามภาพ ในไฟล์ App.config

<img src="images/appcn.png" width="600">

เขียน code ใน ไฟล์ `DatabaseHelper.cs`

<img src="images/dbcon2.png" width="600">

เพิ่มปุ่ม ใน form1 สำหรับการทดสอบการเชื่อมต่อ
เขียน code ให้กับปุ่ม

<img src="images/btntest.png" width="600">

Run โปรแกรมทดสอบ ลองกดปุ่ม

<img src="images/testcon.png" width="600">