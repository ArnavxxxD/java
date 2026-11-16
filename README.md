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
<head>
<title>Experiment 5</title>
<style>
body {
    font-family: Arial;
    background: #f0fdf4;
    text-align: center;
    padding: 30px;
}
.box {
    background: white;
    padding: 25px;
    width: 350px;
    margin: auto;
    border-radius: 10px;
}
input, button {
    padding: 10px;
    margin: 8px;
}
button {
    background: green;
    color: white;
    border: none;
}
#result {
    background: #dcfce7;
    padding: 12px;
}
</style>
</head>
<body>

<div class="box">
<h2>Shopping Cart Calculator</h2>

<input type="text" id="name" placeholder="Product Name">
<input type="number" id="price" placeholder="Product Price">
<br>

<button onclick="addItem()">Add Product</button>

<h3>Cart Items</h3>
<p id="items"></p>
<h3 id="result"></h3>
</div>

<script>
let cart = [];

function addItem() {
    let name = document.getElementById("name").value;
    let price = Number(document.getElementById("price").value);

    if (name === "" || price <= 0) {
        alert("Enter valid product details");
        return;
    }

    // Object inside array
    let product = {name: name, price: price};
    cart.push(product);

    displayCart();

    document.getElementById("name").value = "";
    document.getElementById("price").value = "";
}

function displayCart() {

    // Using map()
    let items = cart.map(p => p.name + " - ₹" + p.price);

    document.getElementById("items").innerHTML =
        items.join("<br>");

    // Using reduce()
    let total = cart.reduce((sum, p) => sum + p.price, 0);

    let discount = total >= 1000 ? total * 0.10 : 0;

    let finalAmount = total - discount;

    document.getElementById("result").innerHTML =
        "Total: ₹" + total +
        "<br>Discount: ₹" + discount +
        "<br>Final Amount: ₹" + finalAmount;
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
<head>
<title>Experiment 6</title>
<style>
body {
    font-family: Arial;
    background: #fff7ed;
    text-align: center;
    padding: 30px;
}
.box {
    background: white;
    width: 380px;
    margin: auto;
    padding: 25px;
    border-radius: 10px;
}
input, textarea, button {
    padding: 10px;
    margin: 8px;
    width: 85%;
}
button {
    background: orange;
    color: white;
    border: none;
}
</style>
</head>
<body>

<div class="box">
<h2>String & Regex Operations</h2>

<input id="email" placeholder="Enter Email">
<button onclick="validateEmail()">Validate Email</button>

<textarea id="text" placeholder="Enter some text"></textarea>
<button onclick="analyzeText()">Analyze Text</button>

<p id="result"></p>
</div>

<script>
// Email validation using Regex
function validateEmail() {
    let email = document.getElementById("email").value;

    let pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

    if (pattern.test(email))
        alert("Valid Email");
    else
        alert("Invalid Email");
}

// String functions and data extraction
function analyzeText() {
    let str = document.getElementById("text").value;

    let words = str.trim() ? str.trim().split(/\s+/).length : 0;

    let numbers = str.match(/\d+/g) || [];

    document.getElementById("result").innerHTML =
        "Length: " + str.length +
        "<br>Uppercase: " + str.toUpperCase() +
        "<br>Lowercase: " + str.toLowerCase() +
        "<br>Words: " + words +
        "<br>Numbers: " + numbers.join(", ");
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
<head>
<title>Experiment 7</title>
<style>
body {
    font-family: Arial;
    background: #f5f3ff;
    text-align: center;
    padding: 30px;
}
.box {
    background: white;
    width: 380px;
    margin: auto;
    padding: 25px;
    border-radius: 10px;
}
input, button {
    padding: 10px;
    margin: 5px;
}
button {
    background: purple;
    color: white;
    border: none;
    cursor: pointer;
}
li {
    padding: 10px;
    text-align: left;
    margin: 8px;
    background: #eee;
}
</style>
</head>
<body>

<div class="box">
<h2>My To-Do List</h2>

<input id="task" placeholder="Enter a task">
<button onclick="addTask()">Add</button>

<ul id="list"></ul>
</div>

<script>
function addTask() {
    let value = document.getElementById("task").value;

    if (value.trim() === "") {
        alert("Enter a task");
        return;
    }

    // Create new element
    let li = document.createElement("li");

    let span = document.createElement("span");
    span.textContent = value;

    // Edit button
    let edit = document.createElement("button");
    edit.textContent = "Edit";
    edit.onclick = function() {
        let newTask = prompt("Edit task", span.textContent);
        if (newTask && newTask.trim() !== "")
            span.textContent = newTask;
    };

    // Delete button
    let del = document.createElement("button");
    del.textContent = "Delete";
    del.onclick = function() {
        li.remove();
    };

    li.appendChild(span);
    li.appendChild(edit);
    li.appendChild(del);

    document.getElementById("list").appendChild(li);

    document.getElementById("task").value = "";
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
<head>
    <title>Experiment 8</title>

    <style>
        body {
            font-family: Arial;
            background: #eff6ff;
            text-align: center;
            padding: 30px;
        }

        form {
            background: white;
            width: 350px;
            margin: auto;
            padding: 25px;
            border-radius: 10px;
        }

        input, select, button {
            width: 90%;
            padding: 10px;
            margin: 8px;
        }

        button {
            background: blue;
            color: white;
            border: none;
        }

        #msg {
            color: red;
        }
    </style>
</head>

<body>

<form onsubmit="return validateForm()">

    <h2>Gym Admission Form</h2>

    <input type="text" id="name" placeholder="Full Name" required>

    <input type="number" id="age" placeholder="Age" required>

    <input type="text" id="phone" placeholder="Phone Number" required>

    <input type="email" id="email" placeholder="Email Address" required>

    <select id="plan" required>
        <option value="">Select Plan</option>
        <option>Monthly</option>
        <option>Yearly</option>
    </select>

    <p id="msg"></p>

    <button type="submit">Submit</button>

</form>

<script>

// Live age validation
document.getElementById("age").addEventListener("input", function() {
    let age = Number(this.value);

    document.getElementById("msg").innerHTML =
        age >= 18 ? "Eligible for admission" : "Minimum age is 18";
});

// Form validation
function validateForm() {

    let name = document.getElementById("name").value;
    let age = Number(document.getElementById("age").value);
    let phone = document.getElementById("phone").value;
    let email = document.getElementById("email").value;
    let plan = document.getElementById("plan").value;

    let emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;

    if (name.trim() === "" || age < 18 ||
        !/^\d{10}$/.test(phone) ||
        !emailPattern.test(email) || plan === "") {

        alert("Please enter valid details");
        return false;
    }

    alert("Gym Admission Successful!");
    return false;
}

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
