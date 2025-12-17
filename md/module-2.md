
# ชั่วโมงที่ 2 : JavaScript Syntax และ DOM

## 1. บทบาทของ JavaScript ในเว็บ

JavaScript เป็นภาษาโปรแกรมที่ทำงานบนฝั่งผู้ใช้ (Client-side) ภายในเว็บเบราว์เซอร์ มีหน้าที่หลักในการควบคุมพฤติกรรมของหน้าเว็บ ทำให้เว็บเพจสามารถโต้ตอบกับผู้ใช้ได้

หากไม่มี JavaScript หน้าเว็บจะทำหน้าที่เพียงแสดงข้อมูลแบบคงที่ แต่เมื่อมี JavaScript จะสามารถ

* ตรวจสอบข้อมูลที่ผู้ใช้กรอก
* ตอบสนองต่อการกดปุ่มหรือการเปลี่ยนค่า
* ปรับเปลี่ยนเนื้อหาบนหน้าเว็บแบบทันที

**ตัวอย่างแนวคิด**
ปุ่ม “Submit” เมื่อถูกกดแล้วสามารถแสดงข้อความ หรือคำนวณผลลัพธ์โดยไม่ต้องโหลดหน้าเว็บใหม่


## 2. JavaScript Syntax พื้นฐาน

### 2.1 ตัวแปร (Variables)

JavaScript ใช้คำสั่ง `let` หรือ `const` ในการประกาศตัวแปร

```javascript
let name = "Alice";
let score = 85;
```

เปรียบเทียบกับ Python

| แนวคิด | Python           | JavaScript            |
| ------ | ---------------- | --------------------- |
| ตัวแปร | `name = "Alice"` | `let name = "Alice";` |

### 2.2 เงื่อนไข (Conditional Statement)

```javascript
let score = 45;

if (score >= 50) {
    console.log("Pass");
} else {
    console.log("Fail");
}
```

แนวคิดเหมือนกับ Python ต่างกันที่รูปแบบไวยากรณ์


### 2.3 Loop

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

ใช้สำหรับทำงานซ้ำ ๆ เช่น การแสดงข้อมูลหลายรายการ


### 2.4 Function

```javascript
function add(a, b) {
    return a + b;
}
```

ฟังก์ชันช่วยจัดกลุ่มคำสั่ง ทำให้โค้ดอ่านง่ายและนำกลับมาใช้ซ้ำได้


## 3. ความเชื่อมโยงกับ Python

JavaScript และ Python มีแนวคิดพื้นฐานเหมือนกัน เช่น

* ตัวแปร
* เงื่อนไข
* Loop
* Function

แตกต่างกันที่

* JavaScript ใช้ `{}` แทนการย่อหน้า
* JavaScript ทำงานหลักบนเว็บเบราว์เซอร์

การเข้าใจ Python มาก่อนจะช่วยให้เรียน JavaScript ได้ง่ายขึ้น


## 4. DOM (Document Object Model)

### 4.1 แนวคิดของ DOM

DOM คือโครงสร้างที่แทน HTML ในรูปแบบวัตถุ (Object)
JavaScript ใช้ DOM เพื่อเข้าถึงและแก้ไขเนื้อหาของหน้าเว็บ

กล่าวได้ว่า
**DOM คือสะพานเชื่อมระหว่าง JavaScript กับ HTML**

### 4.2 การเข้าถึง Element

```javascript
document.getElementById("title");
```

คำสั่งนี้ใช้เลือก HTML element ที่มี `id="title"`


### 4.3 การอ่านและแก้ไขค่า

```javascript
document.getElementById("title").innerHTML = "New Title";
```

สามารถใช้ JavaScript เปลี่ยนข้อความบนหน้าเว็บได้ทันที

## 5. Event Handling

### 5.1 แนวคิด Event

Event คือเหตุการณ์ที่เกิดจากการกระทำของผู้ใช้ เช่น

* การคลิกปุ่ม
* การเปลี่ยนค่าข้อมูล
* การพิมพ์ข้อความ

### 5.2 onclick

```html
<button onclick="showMessage()">Click Me</button>
```

```javascript
function showMessage() {
    alert("Hello JavaScript");
}
```

เมื่อผู้ใช้คลิกปุ่ม จะเรียกฟังก์ชันที่กำหนดไว้


### 5.3 onchange

```html
<input type="number" id="score" onchange="checkScore()">
<p id="result"></p>
```

```javascript
function checkScore() {
    let score = document.getElementById("score").value;

    if (score >= 50) {
        document.getElementById("result").innerHTML = "Pass";
    } else {
        document.getElementById("result").innerHTML = "Fail";
    }
}
```


## 6. กิจกรรมปฏิบัติ : ควบคุมปุ่มและฟอร์มด้วย JavaScript

### ตัวอย่างกิจกรรมสาธิต

```html
<!DOCTYPE html>
<html>
<head>
    <title>JavaScript DOM Demo</title>
</head>
<body>

<h3 id="title">Student Information</h3>

<input type="text" id="name" placeholder="Enter your name">
<button onclick="showName()">Show</button>

<p id="output"></p>

<script>
    function showName() {
        let name = document.getElementById("name").value;
        document.getElementById("output").innerHTML =
            "Hello " + name;
    }
</script>

</body>
</html>
```


## 7. แนวทางการฝึกเพิ่มเติมในชั้นเรียน

ให้ผู้เรียนทดลอง:

* เปลี่ยนข้อความแสดงผล
* เพิ่มเงื่อนไขตรวจสอบข้อมูล
* เปลี่ยนสีข้อความด้วย JavaScript
* เพิ่ม input ใหม่และควบคุมผ่าน DOM

## 8. สรุปท้ายชั่วโมง

ในชั่วโมงนี้ ผู้เรียนได้เรียนรู้ว่า

* JavaScript ทำให้เว็บโต้ตอบกับผู้ใช้ได้
* Syntax ของ JavaScript มีแนวคิดคล้าย Python
* DOM ใช้เชื่อม JavaScript กับ HTML
* Event Handling เป็นหัวใจของ Web Application

ความรู้ในชั่วโมงนี้เป็นพื้นฐานสำคัญสำหรับการทำงานกับ JSON, Web API และ Backend ในชั่วโมงถัดไป
