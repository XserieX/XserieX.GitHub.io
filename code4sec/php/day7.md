sleep()
===================

![](../images/sleep.png)

 **sleep()** คือ การสั่งให้หยุดการรันโปรแกรมไว้ก่อน

 **รูปแบบการใช้งาน**

    sleep ( int $seconds ) : int

ใน php มีฟังก์ชันทำให้หยุดการทำงานระยะหนึ่งหรือทำให้ล่าช้า หลายฟังก์ชัน 
เช่น usleep() ฟังก์ชันการดำเนินงานล่าช้าในรูปแบบหน่วยไมโครวินาที หรือ 
ฟังก์ชัน set_time_limit()  ใช้ในการจำกัดเวลาการ Run Script  
และฟังก์ชันที่เราจะพูดถึงในบทความนี้ครับ sleep() ฟังก์ชั่นหลับ คือสั่งให้หยุด
การรันโปรแกรมไว้ก่อน เป็นเวลาตามที่ต้องการ หลังจากนั้น จึงค่อยทำการรันต่อไป 
หรือหมายถึงฟังก์ชันความล่าช้าในการดำเนินการของสคริปต์ปัจจุบันเป็นเวลาหลายวินาที  
ฟังก์ชันนี้จะคืนค่าเป็น 0 ถ้าทำงานสำเร็จ และคืนค่าเป็น false ในกรณีที่เเกิดการผิดพลาดขึ้นมาครับ 

แต่ถ้าหากโทรถูกขัดจังหวะโดยสัญญาณฟังก์ชันจะส่งกลับค่าไม่ใช่ศูนย์ บนแพลตฟอร์มของ 
Windows ค่านี้จะเป็น 192 มันหมายถึงค่าของค่าคงที่ของ Windows API WAIT_IO_COMPLETION 
บนแพลตฟอร์มอื่น ๆ , ค่าตอบแทนเป็นจำนวนวินาทีที่เหลืออยู่ในความล่าช้า 

***ตัวอย่าง***

    <?php
        echo date('h:i:s') . "<br>";
        sleep(10);
        echo date('h:i:s') . "<br>";
    ?>

***ผลลัพธ์***

    02:17:39
    02:17:49

จะเห็นว่าเมื่อรันโค้ดนี้ หลังจากที่ echo date('h:i:s') 04:48:28 เสร็จแล้ว
โปรแกรมจะทำงานฟังก์ชัน sleep(10) ซึ่งจะหยุดสักระยะเวลาประมาณ 10 วินาที 
แล้วค่อย echo date('h:i:s')  04:48:38 ในเวลาต่อมา  ฟังก์ชันนี้ไม่ซับซ้อน
ซึ่งเข้าใจง่าย คือถ้าต้องให้โปรแกรมทำ delay กี่วินาที ก็กำหนดไปแค่นั้นเองครับ 
เราสามารถนำไปประยุกต์กับโปรเจ็คเราได้ เช่น ถ้าต้องการหยุดทำสักระยะหนึ่ง ก็ใช้ฟังก์ชันนี้ 
เป็นต้น นอกจากนั้นแล้ว  ยังมีหลายฟังก์ชัน ที่ทำงานคล้ายๆกัน
เช่น usleep () - การดำเนินการล่าช้าในหน่วยไมโครวินาที  
time_nanosleep () - ล่าช้าไปหลายวินาทีและนาโนวินาที 
time_sleep_until () - ทำให้สคริปต์พักจนกระทั่งถึงเวลาที่ระบุ 

***ตัวอย่าง***

    <?php
        sleep(10);
        session_start();
        $serverName = "localhost";
        $userName = "root";
        $userPassword = "123456789";
        $dbName = "XserieX";
     
        $objCon = mysqli_connect($serverName,$userName,$userPassword,$dbName);
     
        $strSQL = "SELECT * FROM member WHERE Username = '".mysqli_real_escape_string($objCon,$_POST['txtUsername'])."' 
        and Password = '".mysqli_real_escape_string($objCon,$_POST['txtPassword'])."'";
        $objQuery = mysqli_query($objCon,$strSQL);
        $objResult = mysqli_fetch_array($objQuery,MYSQLI_ASSOC);
        if(!$objResult)
        {
            echo "Username and Password Incorrect!";
        }
        else
        {
                $_SESSION["UserID"] = $objResult["UserID"];
                $_SESSION["Status"] = $objResult["Status"];
     
                session_write_close();
            
                if($objResult["Status"] == "ADMIN")
                {
                    header("location:admin_page.php");
                }
                else
                {
                    header("location:user_page.php");
                }
        }
        mysqli_close($objCon);
    ?>

จากโค้ดด้านบนจะเห็นได้ว่าจะทำการหน่วงเวลาใรการ login ไว้ 10 วินาที
เพื่อป้องกันการ brute force โดยเราอาจจะตั้งค่าเวลาแบบ random ก็ได้
เพื่อไม่ให้สามารถเดาได้ว่า หน่วงไว้กี่วีนาที

***อ้างอิง***
- <https://mindphp.com/%E0%B8%84%E0%B8%B9%E0%B9%88%E0%B8%A1%E0%B8%B7%E0%B8%AD/63-%E0%B8%9F%E0%B8%B1%E0%B8%87%E0%B8%81%E0%B9%8C%E0%B8%8A%E0%B8%B1%E0%B9%88%E0%B8%99-php/552-sleep().html#:~:text=%E0%B9%83%E0%B8%99%20php%20%E0%B8%A1%E0%B8%B5%E0%B8%9F%E0%B8%B1%E0%B8%87%E0%B8%81%E0%B9%8C%E0%B8%8A%E0%B8%B1%E0%B8%99%E0%B8%97%E0%B8%B3%E0%B9%83%E0%B8%AB%E0%B9%89,%E0%B9%80%E0%B8%9B%E0%B9%87%E0%B8%99%E0%B9%80%E0%B8%A7%E0%B8%A5%E0%B8%B2%E0%B8%95%E0%B8%B2%E0%B8%A1%E0%B8%97%E0%B8%B5%E0%B9%88%E0%B8%95%E0%B9%89%E0%B8%AD%E0%B8%87%E0%B8%81%E0%B8%B2%E0%B8%A3>