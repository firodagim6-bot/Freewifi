
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Online Work Registration</title>

<style>
* {
  box-sizing: border-box;
}
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #edf2f7;
  color: #222;
}
header {
  background: #102c50;
  color: white;
  text-align: center;
  padding: 25px 10px;
}
.container {
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
}
.card {
  background: white;
  padding: 20px;
  margin-bottom: 18px;
  border-radius: 12px;
  box-shadow: 0 3px 12px #0001;
}
h2 {
  color: #102c50;
}
input, textarea, button {
  width: 100%;
  padding: 13px;
  margin: 9px 0;
  border: 1px solid #ccc;
  border-radius: 7px;
}
button {
  background: #087b47;
  color: white;
  border: none;
  font-weight: bold;
}
button:hover {
  background: #065d36;
}
.payment {
  background: #e6f7ed;
  padding: 15px;
  border-radius: 8px;
}
.small {
  font-size: 13px;
  color: #666;
}
.hidden {
  display: none;
}
footer {
  text-align: center;
  padding: 20px;
  color: #666;
}
</style>
</head>

<body>

<header>
<h1>ONLINE WORK</h1>
<p>Registration and Work Information</p>
</header>

<div class="container">

<div class="card">
<h2>Welcome</h2>
<p>Welcome to our online work registration website.</p>
<p>Read the work description and payment terms
before registering.</p>
</div>

<div class="card">
<h2>Work Information</h2>
<p>Work description: To be announced clearly by the
website administrator.</p>
<p>Payment terms: No income or job is guaranteed
until the work and conditions are explained.</p>
</div>

<div class="card">
<h2>Registration</h2>

<form id="registerForm">

<input type="text" id="name"
placeholder="Full Name" required>

<input type="tel" id="phone"
placeholder="Phone Number" required>

<input type="email" id="email"
placeholder="Email (optional)">

<label>Upload payment receipt (optional):</label>
<input type="file" id="receipt"
accept="image/*">

<label>
<input type="checkbox" id="agree"
style="width:auto" required>
I have read and understood the terms.
</label>

<button type="submit">Submit Registration</button>

</form>

<p id="result"></p>
</div>

<div class="card">
<h2>Payment Information</h2>

<div class="payment">
<h3>Registration fee: 300 ETB</h3>
<p>Receiver: Efrem</p>
<p>Telebirr: 0987130401</p>
</div>

<p class="small">
Only pay after the actual work, fee purpose,
refund conditions and terms have been explained.
</p>
</div>

<div class="card">
<h2>ID Verification</h2>
<p>Identity verification must be voluntary and
handled through a secure verification service.</p>

<p class="small">
Do not upload sensitive identity documents
to this demonstration website.
</p>
</div>

<div class="card">
<h2>Admin Login</h2>

<input type="password" id="adminPassword"
placeholder="Admin Password">

<button onclick="adminLogin()">Login</button>

<div id="adminPanel" class="hidden">
<h3>Registration Records</h3>
<div id="records"></div>
</div>
</div>

</div>

<footer>
<p>Online Work Registration System</p>
</footer>

<script>

let registrations = [];

document.getElementById("registerForm")
.addEventListener("submit", function(e) {

e.preventDefault();

let person = {
name: document.getElementById("name").value,
phone: document.getElementById("phone").value,
email: document.getElementById("email").value,
date: new Date().toLocaleString()
};

registrations.push(person);

document.getElementById("result").innerHTML =
"Registration received in this demo. " +
"Your payment has NOT been verified.";

this.reset();

});

function adminLogin() {

let password =
document.getElementById("adminPassword").value;

// Demo password only. Replace with secure server authentication.
if(password === "CHANGE_THIS_PASSWORD") {

document.getElementById("adminPanel")
.classList.remove("hidden");

let output = "";

registrations.forEach(function(person, index) {

output += `
<div class="payment">
<p>Name: ${escapeHTML(person.name)}</p>
<p>Phone: ${escapeHTML(person.phone)}</p>
<p>Email: ${escapeHTML(person.email)}</p>
<p>Date: ${escapeHTML(person.date)}</p>
</div>
`;

});

document.getElementById("records").innerHTML =
output || "No registrations yet.";

} else {

alert("Incorrect password!");

}

}

function escapeHTML(value) {
return String(value).replace(/[&<>"']/g, function(c) {
return {
"&":"&amp;",
"<":"&lt;",
">":"&gt;",
'"':"&quot;",
"'":"&#39;"
}[c];
});
}

</script>

</body>
</html>
