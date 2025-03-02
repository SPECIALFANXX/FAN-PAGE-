<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fan Club Website</title>
  <style>
    /* Global Styles */
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .container {
      background-color: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      width: 400px;
      text-align: center;
    }
    h1, h2 {
      color: #333;
      margin-bottom: 20px;
    }
    p {
      color: #555;
      font-size: 18px;
      line-height: 1.6;
      margin-bottom: 20px;
    }
    input, select, button {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }
    button {
      background-color: #28a745;
      color: #fff;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #218838;
    }
    .error-message {
      color: red;
      margin-top: 10px;
      display: none;
    }
    ul {
      list-style-type: none;
      padding: 0;
    }
    ul li {
      font-size: 18px;
      color: #555;
      margin: 10px 0;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    ul li::before {
      content: "❤‍🔥";
      margin-right: 10px;
    }
  </style>
</head>
<body>
  <!-- Signup Page -->
  <div id="signupPage" class="container">
    <h2>Create an Account</h2>
    <form id="signupForm">
      <input type="text" placeholder="Full Name" required>
      <input type="email" placeholder="Email Address" required>
      <input type="password" placeholder="Password" required>
      <input type="password" placeholder="Confirm Password" required>
      <button type="submit">Sign Up</button>
    </form>
    <p>Already have an account? <a href="#" onclick="showPage('loginPage')">Log in here</a></p>
  </div>

  <!-- Login Page -->
  <div id="loginPage" class="container" style="display: none;">
    <h2>Log In</h2>
    <form id="loginForm">
      <input type="email" placeholder="Email Address" required>
      <input type="password" placeholder="Password" required>
      <button type="submit">Log In</button>
    </form>
    <p>Don’t have an account? <a href="#" onclick="showPage('signupPage')">Sign up here</a></p>
    <p class="error-message" id="loginError">Invalid Credentials</p>
  </div>

  <!-- Welcome Page -->
  <div id="welcomePage" class="container" style="display: none;">
    <h1>Welcome to My Fan Club!</h1>
    <p>
      Hello there! We're thrilled to have you as part of our amazing fan club. 
      Here, you'll find exclusive content, behind-the-scenes updates, and a 
      community of passionate fans just like you. Whether you're here for the 
      latest news, exciting events, or just to connect with fellow enthusiasts, 
      you're in the right place. Let's make this journey unforgettable together!
    </p>
    <button onclick="showPage('formPage')">Next</button>
    <button onclick="logout()">Log Out</button>
  </div>

  <!-- Form Page -->
  <div id="formPage" class="container" style="display: none;">
    <h2>Please Fill in Your Information</h2>
    <form id="infoForm">
      <input type="text" placeholder="Full Name" required>
      <input type="text" placeholder="Address" required>
      <input type="date" placeholder="Date of Birth" required>
      <input type="tel" placeholder="Phone Number" required>
      <select required>
        <option value="">Select Country</option>
        <option value="USA">United States</option>
        <option value="Canada">Canada</option>
        <option value="UK">United Kingdom</option>
      </select>
      <input type="text" placeholder="State" required>
      <input type="text" placeholder="City" required>
      <input type="text" placeholder="Zip Code" required>
      <button type="submit">Submit</button>
    </form>
  </div>

  <!-- Benefit Page -->
  <div id="benefitPage" class="container" style="display: none;">
    <h1>❤‍🔥 What My Super Fans Get:</h1>
    <ul>
      <li>📍 Daily New Content</li>
      <li>💋 Instant Access** to over 100+ sexy pics & nude videos upon subscription</li>
      <li>📍 B/G & Solo Content (PPV available)</li>
      <li>📌 Panties for Sale</li>
      <li>📍 Twerk Videos</li>
      <li>🥰 Unlimited Chat</li>
      <li>❣ Masturbation Video</li>
    </ul>
    <button onclick="showPage('amountPage')">Next</button>
    <button onclick="showPage('welcomePage')">Back to Welcome Page</button>
  </div>

  <!-- Amount Page -->
  <div id="amountPage" class="container" style="display: none;">
    <h1>Exclusive Access</h1>
    <p>
      For just <strong>$150.00</strong>, you’ll get exclusive access to all my hottest content, babe! 
      You’ll receive sexy and nude content daily, and I promise you’ll love it.
    </p>
    <label>
      <input type="checkbox" id="agreeCheckbox"> Click on this box if you agree to the payment amount.
    </label>
    <button id="proceedButton" disabled>Proceed to Payment</button>
    <button onclick="showPage('accessPage')">Next</button>
  </div>

  <!-- Access Page -->
  <div id="accessPage" class="container" style="display: none;">
    <h1>Access Page</h1>
    <p>Input your info to start enjoying all my naughty content!</p>
    <form id="accessForm">
      <input type="text" id="fanId" placeholder="Fan ID" required>
      <input type="text" id="fanCode" placeholder="Fan Code" required>
      <button type="submit">Submit</button>
    </form>
    <p class="error-message" id="accessError">Invalid Fan ID or Fan Code</p>
  </div>

  <script>
    // Simulated signup and login data
    let signupData = { email: "", password: "" };
    let isLoggedIn = false;

    // Show specific page and hide others
    function showPage(pageId) {
      const pages = ["signupPage", "loginPage", "welcomePage", "formPage", "benefitPage", "amountPage", "accessPage"];
      pages.forEach((page) => {
        document.getElementById(page).style.display = page === pageId ? "block" : "none";
      });
    }

    // Signup functionality
    document.getElementById("signupForm").addEventListener("submit", function (event) {
      event.preventDefault();
      const email = document.querySelector("#signupForm input[type='email']").value;
      const password = document.querySelector("#signupForm input[type='password']").value;
      signupData = { email, password };
      localStorage.setItem("signupData", JSON.stringify(signupData));
      alert("Signup successful! Please log in.");
      showPage("loginPage");
    });

    // Login functionality
    document.getElementById("loginForm").addEventListener("submit", function (event) {
      event.preventDefault();
      const email = document.querySelector("#loginForm input[type='email']").value;
      const password = document.querySelector("#loginForm input[type='password']").value;
      if (email === signupData.email && password === signupData.password) {
        isLoggedIn = true;
        localStorage.setItem("isLoggedIn", true);
        showPage("welcomePage");
      } else {
        document.getElementById("loginError").style.display = "block";
      }
    });

    // Logout functionality
    function logout() {
      isLoggedIn = false;
      localStorage.removeItem("isLoggedIn");
      showPage("loginPage");
    }

    // Form Page: Prevent form submission and handle data
    document.getElementById("infoForm").addEventListener("submit", function (event) {
      event.preventDefault(); // Prevent the form from submitting and reloading the page

      // Collect form data (for demonstration purposes)
      const formData = {
        fullName: document.querySelector("#infoForm input[type='text']").value,
        address: document.querySelector("#infoForm input[type='text']").value,
        dob: document.querySelector("#infoForm input[type='date']").value,
        phone: document.querySelector("#infoForm input[type='tel']").value,
        country: document.querySelector("#infoForm select").value,
        state: document.querySelector("#infoForm input[type='text']").value,
        city: document.querySelector("#infoForm input[type='text']").value,
        zipCode: document.querySelector("#infoForm input[type='text']").value,
      };

      // Log the form data to the console (for demonstration purposes)
      console.log("Form Data Submitted:", formData);

      // Optionally, you can save the form data to localStorage or send it to a server
      localStorage.setItem("formData", JSON.stringify(formData));

      // Navigate to the next page (Benefit Page)
      showPage("benefitPage");
    });

    // Amount Page: Enable/disable Proceed button
    document.getElementById("agreeCheckbox").addEventListener("change", function () {
      document.getElementById("proceedButton").disabled = !this.checked;
    });

    // Access Page: Validate Fan ID and Fan Code
    document.getElementById("accessForm").addEventListener("submit", function (event) {
      event.preventDefault();
      const fanId = document.getElementById("fanId").value;
      const fanCode = document.getElementById("fanCode").value;
      if (fanId === "THEWORLD" && fanCode === "XVX660X1") {
        alert("Access granted! Enjoy your content.");
      } else {
        document.getElementById("accessError").style.display = "block";
      }
    });

    // Check login status on page load
    if (localStorage.getItem("isLoggedIn")) {
      showPage("welcomePage");
    } else {
      showPage("signupPage");
    }
  </script>
</body>
</html>
