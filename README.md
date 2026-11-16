# JavaScript Practicals

A collection of 11 simple JavaScript practical programs. Each practical includes its aim, ready-to-copy code, and expected output.

## How to use

1. Open the practical you want to run.
2. Copy the code under the required filename (usually `index.html`).
3. Save the code in a folder on your computer.
4. Open `index.html` in a web browser.
5. For Practical 1, save the second code block as `script.js` in the same folder as `index.html`.
6. Practical 10 requires an internet connection for the JSON data and jQuery library.

## Index

- [Practical 1](#practical-1)
- [Practical 2](#practical-2)
- [Practical 3](#practical-3)
- [Practical 4](#practical-4)
- [Practical 5](#practical-5)
- [Practical 6](#practical-6)
- [Practical 7](#practical-7)
- [Practical 8](#practical-8)
- [Practical 9](#practical-9)
- [Practical 10](#practical-10)
- [Practical 11](#practical-11)

---

## Practical 1

**Aim:** Demonstrate inline, internal, and external JavaScript; use console methods; create a webpage showing user info and a welcome message.

### `index.html`

```html
<!DOCTYPE html>
<html>
<head>
<title>User Information</title>
</head>
<body>
<h2 id="welcome"></h2>
<p id="info"></p>
<!-- Inline JavaScript -->
<button onclick="alert('Hello!')">Click Me</button>
<!-- Internal JavaScript -->
<script>
let name = "Rahul";
let age = 20;
let course = "BCA";
document.getElementById("info").innerHTML =
"Name: " + name + "<br>Age: " + age + "<br>Course: " + course;
console.log("User information");
console.log(name, age, course);
console.warn("This is a warning");
</script>
<!-- External JavaScript -->
<script src="script.js"></script>
</body>
</html>
```

### `script.js`

```javascript
document.getElementById("welcome").innerText = "Welcome, Rahul!";
console.log("External JavaScript loaded");
```

**Output:** Click the button to see an alert. The webpage displays the welcome message, name, age and course. Console messages appear in the browser console.


---

## Practical 2

**Aim:** Use var, let, const, and demonstrate basic features like template literals and destructuring; build a billing calculator with user input.

### `index.html`

```html
<!DOCTYPE html>
<html>
<body>
<h2>Billing Calculator</h2>
Item: <input id="item"><br><br>
Price: <input id="price" type="number"><br><br>
Quantity: <input id="qty" type="number"><br><br>
<button onclick="calculate()">Calculate Bill</button>
<p id="result"></p>
<script>
var shop = "My Store";
let discount = 10;
const GST = 18;
function calculate() {
let item = document.getElementById("item").value;
let price = Number(document.getElementById("price").value);
let qty = Number(document.getElementById("qty").value);
if (item === "" || price <= 0 || qty <= 0) {
alert("Enter valid details");
return;
}
// Object and destructuring
let bill = { item, price, qty };
let { item: name, price: p, qty: q } = bill;
let total = p * q;
let discountAmount = total * discount / 100;
let gstAmount = (total - discountAmount) * GST / 100;
let finalAmount = total - discountAmount + gstAmount;
// Template literal
document.getElementById("result").innerHTML =
`${shop}<br>Item: ${name}<br>Total: Rs. ${total}
<br>Discount: Rs. ${discountAmount}
<br>GST: Rs. ${gstAmount}
<br>Final Amount: Rs. ${finalAmount}`;
}
</script>
</body>
</html>
```

**Output:** Enter an item, price and quantity, then click Calculate Bill. For Pen, price 50 and quantity 4, the final amount is Rs. 212.40.


---

## Practical 3

**Aim:** Implement control structures and form validation; create a grading system based on user-entered marks.

### `index.html`

```html
<!DOCTYPE html>
<html>
<body>
<h2>Student Grading System</h2>
Name: <input id="name"><br><br>
Maths: <input id="m1" type="number"><br><br>
Science: <input id="m2" type="number"><br><br>
English: <input id="m3" type="number"><br><br>
<button onclick="getGrade()">Get Grade</button>
<p id="result"></p>
<script>
function getGrade() {
let name = document.getElementById("name").value;
let a = document.getElementById("m1").value;
let b = document.getElementById("m2").value;
let c = document.getElementById("m3").value;
if (name === "" || a === "" || b === "" || c === "") {
alert("Please fill all fields");
return;
}
let marks = [Number(a), Number(b), Number(c)];
let total = 0;
for (let i = 0; i < marks.length; i++) {
if (marks[i] < 0 || marks[i] > 100) {
alert("Marks must be from 0 to 100");
return;
}
total = total + marks[i];
}
let percent = total / 3;
let grade;
if (percent >= 90) {
grade = "A+";
} else if (percent >= 75) {
grade = "A";
} else if (percent >= 60) {
grade = "B";
} else if (percent >= 40) {
grade = "C";
} else {
grade = "Fail";
}
let remark;
switch (grade) {
case "Fail":
remark = "Better luck next time";
break;
default:
remark = "Congratulations!";
}
document.getElementById("result").innerHTML =
name + "<br>Total: " + total +
"<br>Percentage: " + percent.toFixed(2) +
"%<br>Grade: " + grade + "<br>" + remark;
}
</script>
</body>
</html>
```

**Output:** Enter the student's name and marks in all three subjects. The total, percentage, grade and remark are displayed.


---

## Practical 4

**Aim:** Use function types, scope, and closures; apply try-catch; build a palindrome checker.

### `index.html`

```html
<!DOCTYPE html>
<html>
<head>
<title>Experiment 4</title>
<style>
body {
    font-family: Arial;
    background: #eef2ff;
    text-align: center;
    padding: 30px;
}
.box {
    background: white;
    padding: 25px;
    margin: auto;
    width: 350px;
    border-radius: 10px;
}
input, button {
    padding: 10px;
    margin: 8px;
}
button {
    background: blue;
    color: white;
    border: none;
    cursor: pointer;
}
</style>
</head>
<body>
<div class="box">
<h2>Palindrome Checker</h2>
<input type="text" id="word" placeholder="Enter a word">
<br>
<button onclick="checkPalindrome()">Check</button>
<h3 id="result"></h3>
<script>
// Palindrome using try-catch
function checkPalindrome() {
    try {
        let str = document.getElementById("word").value.toLowerCase();

        if (str === "")
            throw "Please enter a word";

        let reverse = str.split("").reverse().join("");

        if (str === reverse)
            document.getElementById("result").innerHTML = "Palindrome";
        else
            document.getElementById("result").innerHTML = "Not Palindrome";
    }
    catch(error) {
        document.getElementById("result").innerHTML = error;
    }
}
</script>
</body>
</html>
```

**Output:** Enter 'madam' to get Palindrome. Enter 'hello' to get Not a Palindrome. Empty input displays an error message.


---

## Practical 5

**Aim:** Apply array methods and object handling; create a cart total calculator with discount logic.

### `index.html`

```html
<!DOCTYPE html>
<html>
<body>
<h2>Shopping Cart</h2>
Item: <input id="name">
Price: <input id="price" type="number">
Quantity: <input id="qty" type="number">
<button onclick="addItem()">Add Item</button>
<ul id="list"></ul>
<p id="total"></p>
<script>
let cart = [];
function addItem() {
let name = document.getElementById("name").value;
let price = Number(document.getElementById("price").value);
let qty = Number(document.getElementById("qty").value);
if (name === "" || price <= 0 || qty <= 0) {
alert("Enter valid item details");
return;
}
let item = { name: name, price: price, qty: qty };
cart.push(item);
showCart();
}
function showCart() {
let list = "";
// map() displays cart items
cart.map(function(item) {
list += "<li>" + item.name + " - Rs. " +
item.price + " x " + item.qty + "</li>";
});
document.getElementById("list").innerHTML = list;
// reduce() calculates total
let total = cart.reduce(function(sum, item) {
return sum + item.price * item.qty;
}, 0);
let discount = 0;
if (total > 1000) {
discount = total * 10 / 100;
} else if (total > 500) {
discount = total * 5 / 100;
}
document.getElementById("total").innerHTML =
"Total: Rs. " + total +
"<br>Discount: Rs. " + discount +
"<br>To Pay: Rs. " + (total - discount);
}
</script>
</body>
</html>
```

**Output:** Add items to the cart. A 5% discount is given when the total is above Rs. 500 and a 10% discount when it is above Rs. 1000.


---

## Practical 6

**Aim:** Use string functions and regex for email validation, data extraction, and text analysis.

### `index.html`

```html
<!DOCTYPE html>
<html>
<body>
<h2>Email Validation</h2>
<input id="email" placeholder="Enter email">
<button onclick="checkEmail()">Check Email</button>
<p id="emailResult"></p>
<h2>Text Analysis</h2>
<textarea id="text" rows="5" cols="45">Contact info@abc.com. Call 9876543210.</textarea><br>
<button onclick="analyse()">Analyse Text</button>
<p id="result"></p>
<script>
function checkEmail() {
let email = document.getElementById("email").value;
let pattern = /^[a-zA-Z0-9._]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,}$/;
if (pattern.test(email)) {
document.getElementById("emailResult").innerText = "Valid Email";
} else {
document.getElementById("emailResult").innerText = "Invalid Email";
}
}
function analyse() {
let text = document.getElementById("text").value;
let characters = text.length;
let words = text.trim().split(/\s+/).length;
let upper = text.toUpperCase();
let emails = text.match(/[a-zA-Z0-9._]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,}/g);
let phones = text.match(/\d{10}/g);
let vowels = text.match(/[aeiou]/gi);
document.getElementById("result").innerHTML =
"Characters: " + characters +
"<br>Words: " + words +
"<br>Vowels: " + (vowels ? vowels.length : 0) +
"<br>Emails: " + (emails || "None") +
"<br>Phone numbers: " + (phones || "None") +
"<br>Uppercase: " + upper;
}
</script>
</body>
</html>
```

**Output:** A valid email displays Valid Email. Text analysis displays the character count, word count, vowels, extracted email addresses, phone numbers and uppercase text.


---

## Practical 7

**Aim:** Perform DOM traversal and updates; develop a to-do list app with add, edit, and delete features.

### `index.html`

```html
<!DOCTYPE html>
<html>
<body>
<h2>To-Do List</h2>
<input id="task" placeholder="Enter a task">
<button onclick="addTask()">Add</button>
<ul id="list"></ul>
<script>
function addTask() {
let input = document.getElementById("task");
if (input.value.trim() === "") {
alert("Enter a task");
return;
}
let li = document.createElement("li");
li.innerHTML = input.value +
" <button onclick='editTask(this)'>Edit</button>" +
" <button onclick='deleteTask(this)'>Delete</button>";
document.getElementById("list").appendChild(li);
input.value = "";
// DOM traversal
console.log(li.parentElement);
console.log(li.children);
}
function editTask(button) {
let li = button.parentElement;
let newTask = prompt("Enter new task:");
if (newTask !== null && newTask.trim() !== "") {
li.firstChild.textContent = newTask + " ";
}
}
function deleteTask(button) {
button.parentElement.remove();
}
</script>
</body>
</html>
```

**Output:** Tasks can be added to the list, edited using the Edit button and removed using the Delete button.


---

## Practical 8

**Aim:** Access and validate form fields using events; design a gym admission form with live input checks.

### `index.html`

```html
<!DOCTYPE html>
<html>
<body>
<h2>Gym Admission Form</h2>
<form id="gymForm">
Name: <input id="name"><br><br>
Age: <input id="age" type="number"><br><br>
Phone: <input id="phone"><br><br>
Email: <input id="email"><br><br>
Plan:
<select id="plan">
<option>Monthly</option>
<option>Quarterly</option>
<option>Yearly</option>
</select><br><br>
<button type="submit">Join Gym</button>
</form>
<p id="result"></p>
<script>
document.getElementById("gymForm").addEventListener("submit", function(event) {
event.preventDefault();
let name = document.getElementById("name").value;
let age = Number(document.getElementById("age").value);
let phone = document.getElementById("phone").value;
let email = document.getElementById("email").value;
let plan = document.getElementById("plan").value;
let phonePattern = /^\d{10}$/;
let emailPattern = /^[a-zA-Z0-9._]+@[a-zA-Z0-9]+\.[a-zA-Z]{2,}$/;
if (name.length < 3) {
alert("Name must have at least 3 letters");
} else if (age < 15 || age > 60) {
alert("Age must be between 15 and 60");
} else if (!phonePattern.test(phone)) {
alert("Enter a 10 digit phone number");
} else if (!emailPattern.test(email)) {
alert("Enter a valid email");
} else {
document.getElementById("result").innerText =
"Admission successful! Plan: " + plan;
}
});
</script>
</body>
</html>
```

**Output:** Enter valid details in the form. Incorrect details show an alert. Correct details display Admission successful with the selected plan.


---

## Practical 9

**Aim:** Implement localStorage and sessionStorage to save user preferences like theme settings.

### `index.html`

```html
<!DOCTYPE html>
<html>
<body id="page">
<h2>Theme Settings</h2>
<button onclick="setTheme('light')">Light Theme</button>
<button onclick="setTheme('dark')">Dark Theme</button>
<button onclick="resetTheme()">Reset</button>
<br><br>
Name: <input id="name">
<button onclick="saveName()">Save Name</button>
<p id="result"></p>
<script>
function setTheme(theme) {
localStorage.setItem("theme", theme);
applyTheme();
}
function applyTheme() {
let theme = localStorage.getItem("theme");
let page = document.getElementById("page");
if (theme === "dark") {
page.style.background = "black";
page.style.color = "white";
} else {
page.style.background = "white";
page.style.color = "black";
}
}
function resetTheme() {
localStorage.removeItem("theme");
applyTheme();
}
function saveName() {
let name = document.getElementById("name").value;
sessionStorage.setItem("username", name);
showName();
}
function showName() {
let name = sessionStorage.getItem("username");
if (name) {
document.getElementById("result").innerText = "Hello " + name;
}
}
// Load saved settings
applyTheme();
showName();
</script>
</body>
</html>
```

**Output:** The selected theme remains saved after refreshing the page using localStorage. The name is saved for the current browser tab using sessionStorage.


---

## Practical 10

**Aim:** Load and display JSON data using fetch() and jQuery $.getJSON(); render results dynamically in a table.

### `index.html`

```html
<!DOCTYPE html>
<html>
<head>
<title>JSON Data</title>
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
<h2>Load JSON Data</h2>
<button onclick="loadFetch()">Load using fetch()</button>
<button onclick="loadJQuery()">Load using jQuery</button>
<table border="1" cellpadding="6">
<tr>
<th>ID</th><th>Name</th><th>Email</th><th>City</th>
</tr>
<tbody id="tableBody"></tbody>
</table>
<script>
let url = "https://jsonplaceholder.typicode.com/users";
// Using fetch()
function loadFetch() {
fetch(url)
.then(response => response.json())
.then(data => showData(data))
.catch(error => alert("Unable to load data"));
}
// Using jQuery
function loadJQuery() {
$.getJSON(url, function(data) {
showData(data);
});
}
function showData(users) {
let rows = "";
for (let i = 0; i < users.length; i++) {
rows += "<tr>" +
"<td>" + users[i].id + "</td>" +
"<td>" + users[i].name + "</td>" +
"<td>" + users[i].email + "</td>" +
"<td>" + users[i].address.city + "</td>" +
"</tr>";
}
document.getElementById("tableBody").innerHTML = rows;
}
</script>
</body>
</html>
```

**Output:** Click either button to load JSON data. A table displays the user ID, name, email and city. An internet connection is required.


---

## Practical 11

**Aim:** Use JavaScript timers (setTimeout(), setInterval()).

### `index.html`

```html
<!DOCTYPE html>
<html>
<body>
<h2>JavaScript Timers</h2>
<p id="message"></p>
<h2 id="clock"></h2>
<h2 id="count">10</h2>
<button onclick="startTimer()">Start Countdown</button>
<button onclick="stopTimer()">Stop</button>
<script>
// setTimeout runs once after 3 seconds
setTimeout(function() {
document.getElementById("message").innerText =
"Message displayed after 3 seconds";
}, 3000);
// setInterval updates the clock every second
setInterval(function() {
document.getElementById("clock").innerText =
new Date().toLocaleTimeString();
}, 1000);
let timer;
let seconds = 10;
function startTimer() {
clearInterval(timer);
seconds = 10;
document.getElementById("count").innerText = seconds;
timer = setInterval(function() {
seconds--;
document.getElementById("count").innerText = seconds;
if (seconds === 0) {
clearInterval(timer);
alert("Time is up!");
}
}, 1000);
}
function stopTimer() {
clearInterval(timer);
}
</script>
</body>
</html>
```

**Output:** A message appears after 3 seconds. A digital clock updates every second. The countdown starts from 10 and displays Time is up when it reaches zero.
