Session_regenerate_id
===================

![](../images/cookie.jpg)

 **Session_regenerate_id** คือ เซสชันหรือการจัดการเซสชันเป็นวิธีการทำให้ข้อมูลพร้อมใช้งานในหน้าต่างๆ
 ของเว็บแอปพลิเคชัน ฟังก์ชันsession_regenerate_id() สร้างรหัสเซสชันใหม่และอัปเดตรหัสปัจจุบันด้วยรหัสที่สร้างขึ้นใหม่
 ช่วยในการป้องกันการโดนสวมสิทธ์ การเอาเซสชันไปใช้ได้

 **รูปแบบการใช้งาน**

    session_regenerate_id([$delete_old_session]);

ส่งคืนค่า
สิ่งนี้จะส่งคืนค่าบูลีนซึ่งเป็น TRUE ในกรณีที่สำเร็จเป็น FALSE

***ตัวอย่างการนำไปใช้*** 

    <html>   
        <head>
            <title>Setting up a PHP session</title>
        </head>   
        <body>
        <?php  
            session_id("my-id");
            session_start();   
            print("Id: ".session_id());
            session_regenerate_id();
            echo "<br>";
            print("New Session Id: ".session_id());         
        ?>
        </body>   
    </html>

เมื่อเรียกใช้ไฟล์ html ด้านบนมันจะแสดงข้อความต่อไปนี้

***ผลลัพธ์***

    Id: my-id
    New Session Id: sm6tplqv1e2dhchnv75d7i3bic

***ตัวอย่างการนำไปใช้ 2***

    <html>
    <body>
          <?php
            $id = session_create_id(); 
            session_id($id);
            print("\n"."Id: ".$id);
            session_start();  
            session_regenerate_id();
            echo "<br>";
            print("New Session Id: ".session_id());     
        ?>
    </body>
    </html>

สิ่งนี้จะให้ผลลัพธ์ดังต่อไปนี้

***ผลลัพธ์***

    Id: r30p6i4cnu0qs683lsu8bchv5u
    New Session Id: jj24l3eumtps2nudqa0gm843qr

***ตัวอย่างการนำไปใช้ 3***

    <html>   
        <head>
            <title>Setting up a PHP session</title>
        </head>   
        <body>
        <?php  
            session_id("my-id");
            session_start();   
            print("Id: ".session_id());
            session_regenerate_id(TRUE);
            echo "<br>";
            print("New Session Id: ".session_id());         
        ?>
        </body>   
    </html>

เมื่อเรียกใช้ไฟล์ html ด้านบนมันจะแสดงข้อความต่อไปนี้

***ผลลัพธ์***

    Id: my-id
    New Session Id: k5dli3nl4lf6vogu156r4qb0l1

***อ้างอิง***
- <https://www.tutorialspoint.com/php/php_function_session_regenerate_id.htm>
- <https://www.php.net/manual/en/function.session-regenerate-id.php>