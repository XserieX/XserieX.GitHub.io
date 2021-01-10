Prepare
===================

![](../images/001.jpg)

 **Prepare** คือ ฟังก์ชันที่ใช้ในการหลบเลี่ยง สตริงที่ใช้กับ mysql query ช่วยป้องกันการทำ SQL Injection
 โดยการทำ SQL injection ใช้หลักการอาศัยช่องโหว่ของ string กำหนดค่าให้ parameter แล้วแทนค่า ให้กับ เงื่อนไขนั้นอีกที 

 **รูปแบบการใช้งาน**

    mysqli_prepare ( mysqli $link , string $query ) : mysqli_stmt

ในการ bind parameter จะใช้คำสั่ง
$stmt->bind_param('s', $strCustomerID); 
ในค่าแรกที่กำหนดจะเป็น string type ประกอบด้วย 
- i (Interger) จำนวนเต็ม
- d (double) เลขทศนิยม
- s (string) ข้อความ
- b (Blob / Binary Large OBject ) ข้อมูล Binary

***โค้ดปกติที่ใช้กันทั่วไป NON-Prepare*** 

    $strCustomerID = $_GET['id']; 
    $conn = mysqli_connect($serverName,$userName,$userPassword,$dbName);
    $sql = "SELECT * FROM customer WHERE CustomerID = '$strCustomerID'";
    $query = mysqli_query($conn,$sql);

เมื่อเราใส่ URL http://localhost/job/test.php?id=C001

***ผลลัพธ์***

    C001
    Win Weerachai
    win.weerachai@thaicreate.com
    TH
    1000000
    600000

***ทำการ SQL Injection***

http://localhost/job/test.php?id=C001'+or+'1'='1&Submit=Submit#
http://localhost/job/test.php?id=C001'+or+'1'+=+'1

***ผลลัพธ์***

    C001
    Win Weerachai
    win.weerachai@thaicreate.com
    TH
    1000000
    600000

    C002
    John Smith
    john.smith@thaicreate.com
    UK
    2000000
    800000

    C003
    Jame Born
    jame.born@thaicreate.com
    US
    3000000
    600000

    C004
    Chalee Angel
    chalee.angel@thaicreate.com
    US
    4000000
    100000

***โค้ดที่ใช้ Prepare***

    $strCustomerID = $_GET['id'];
    $conn = new mysqli($serverName,$userName,$userPassword,$dbName);
    $sql = "SELECT * FROM customer WHERE CustomerID = ? ";
    $stmt = $conn->prepare($sql);
    $stmt->bind_param('s', $strCustomerID); 
    $stmt ->execute();
    $result = $stmt->get_result();

เมื่อเราใส่ http://localhost/job/?id=C001

***ผลลัพธ์***

    C001
    Win Weerachai
    win.weerachai@thaicreate.com
    TH
    1000000
    600000

***ทำการ SQL Injection***

    http://localhost/job/?id=C001'+or+'1'='1&Submit=Submit#
    http://localhost/job/?id=C001'+or+'1'+=+'1

***ผลลัพธ์***
จะไม่มีข้อมูลใดๆออกมา
 
***อ้างอิง***
- <https://www.ninenik.com/content.php?arti_id=927>
- <https://www.php.net/manual/en/mysqli.prepare.php>
