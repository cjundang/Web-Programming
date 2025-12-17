# ชั่วโมงที่ 3 : JSON และ Web API

---

## 1. แนวคิดข้อมูลแบบ JSON

### 1.1 ความหมายของ JSON

JSON (JavaScript Object Notation) คือรูปแบบการจัดเก็บและแลกเปลี่ยนข้อมูลที่นิยมใช้ในระบบ Web Application โดยเฉพาะการสื่อสารระหว่าง Client และ Server

คุณสมบัติสำคัญของ JSON

* โครงสร้างอ่านง่าย
* มีรูปแบบใกล้เคียง Object ในภาษาโปรแกรม
* รองรับการแลกเปลี่ยนข้อมูลข้ามระบบ

JSON ไม่ใช่ภาษาโปรแกรม แต่เป็น **รูปแบบข้อมูล (Data Format)**

---

### 1.2 ตัวอย่าง JSON อย่างง่าย

```json
{
  "name": "Alice",
  "age": 16,
  "score": 85
}
```

ข้อมูลถูกจัดเก็บในรูปแบบ **คู่ค่า (key : value)**

---

### 1.3 ความเชื่อมโยงกับ Python

| แนวคิด     | Python              | JSON                  |
| ---------- | ------------------- | --------------------- |
| Dictionary | `{"name": "Alice"}` | `{ "name": "Alice" }` |
| List       | `[1,2,3]`           | `[1,2,3]`             |

นักเรียนที่มีพื้นฐาน Python จะสามารถเข้าใจ JSON ได้ง่าย เนื่องจากมีแนวคิดคล้ายกัน

---

## 2. Object และ Array ใน JavaScript

### 2.1 Object ใน JavaScript

JavaScript ใช้ Object เพื่อเก็บข้อมูลหลายค่าในตัวแปรเดียว

```javascript
let student = {
    name: "Bob",
    age: 15,
    score: 70
};
```

การเข้าถึงข้อมูลใน Object

```javascript
console.log(student.name);
```

---

### 2.2 Array ใน JavaScript

Array ใช้เก็บข้อมูลหลายรายการในรูปแบบลำดับ

```javascript
let scores = [60, 70, 80];
```

---

### 2.3 Array ของ Object

โครงสร้างนี้พบได้บ่อยมากใน Web API

```javascript
let students = [
    { name: "Alice", score: 80 },
    { name: "Bob", score: 65 },
    { name: "Charlie", score: 45 }
];
```

การวนลูปเพื่ออ่านข้อมูล

```javascript
for (let i = 0; i < students.length; i++) {
    console.log(students[i].name);
}
```

---

## 3. การแปลงข้อมูล JSON

### 3.1 แปลง JSON เป็น JavaScript Object

```javascript
let jsonText = '{"name":"Alice","age":16}';
let obj = JSON.parse(jsonText);

console.log(obj.name);
```

ใช้เมื่อรับข้อมูล JSON จาก Server

---

### 3.2 แปลง JavaScript Object เป็น JSON

```javascript
let student = { name: "Bob", age: 15 };
let jsonString = JSON.stringify(student);

console.log(jsonString);
```

ใช้เมื่อส่งข้อมูลจาก Client ไปยัง Server

---

## 4. แนวคิด Web API

### 4.1 Web API คืออะไร

Web API คือบริการที่เปิดให้โปรแกรมอื่นเรียกใช้งานข้อมูลหรือฟังก์ชันผ่านอินเทอร์เน็ต โดยส่วนใหญ่จะส่งข้อมูลในรูปแบบ JSON

แนวคิดการทำงาน

1. Client ส่งคำขอ (Request)
2. Server ประมวลผล
3. Server ส่งข้อมูล JSON กลับมา (Response)

---

### 4.2 ตัวอย่างการใช้งาน Web API

* ดึงรายชื่อผู้ใช้
* ดึงข้อมูลข่าวสาร
* ดึงข้อมูลสภาพอากาศ

> ในชั่วโมงนี้จะใช้ **Public API** เพื่อให้ทดลองได้ทันที

---

## 5. การเรียกใช้ Web API ด้วย fetch()

### 5.1 แนวคิด fetch()

`fetch()` เป็นคำสั่งใน JavaScript ที่ใช้เรียก Web API
ทำงานแบบไม่หยุดการทำงานของหน้าเว็บ (Asynchronous)

โครงสร้างพื้นฐาน

```javascript
fetch(url)
  .then(response => response.json())
  .then(data => {
      console.log(data);
  });
```

---

## 6. กิจกรรมปฏิบัติ : ทดลองอ่านข้อมูล JSON

### ตัวอย่างที่ 1 : อ่านข้อมูลจากตัวแปร JSON

```html
<!DOCTYPE html>
<html>
<head>
    <title>JSON Demo</title>
</head>
<body>

<h3 id="output"></h3>

<script>
    let student = {
        name: "Alice",
        score: 85
    };

    document.getElementById("output").innerHTML =
        student.name + " score = " + student.score;
</script>

</body>
</html>
```

---

## 7. กิจกรรมปฏิบัติ : เรียก Web API และแสดงผลบนหน้าเว็บ

ใช้ Web API ตัวอย่าง
`https://jsonplaceholder.typicode.com/users`

---

### ตัวอย่างโปรแกรมสาธิต

```html
<!DOCTYPE html>
<html>
<head>
    <title>Web API Demo</title>
</head>
<body>

<h3>User List</h3>
<button onclick="loadData()">Load Data</button>

<ul id="list"></ul>

<script>
function loadData() {
    fetch("https://jsonplaceholder.typicode.com/users")
        .then(response => response.json())
        .then(data => {
            let list = document.getElementById("list");
            list.innerHTML = "";

            for (let i = 0; i < data.length; i++) {
                let item = document.createElement("li");
                item.innerHTML = data[i].name;
                list.appendChild(item);
            }
        });
}
</script>

</body>
</html>
```

---

## 8. แนวทางการสาธิตเพิ่มเติมในชั้นเรียน

ให้ผู้เรียนทดลอง:

* เปลี่ยนจากแสดงชื่อ เป็นอีเมล
* แสดงข้อมูลในรูป Table
* แสดงเฉพาะผู้ใช้บางรายการ
* นับจำนวนข้อมูลที่ได้จาก API

---

## 9. สรุปท้ายชั่วโมง

ในชั่วโมงนี้ ผู้เรียนได้เรียนรู้ว่า

* JSON เป็นรูปแบบข้อมูลที่ใช้ใน Web Application
* JavaScript ใช้ Object และ Array แทน JSON ได้โดยตรง
* Web API คือแหล่งข้อมูลจาก Server
* `fetch()` ใช้เรียกข้อมูลจาก Web API
* สามารถแสดงข้อมูลจาก API บนหน้าเว็บได้จริง

