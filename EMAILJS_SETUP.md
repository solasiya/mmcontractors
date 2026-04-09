# Setting up EmailJS for the Contact Form

The contact form logic is now completely set up and ready to securely send emails to your inbox directly from the webpage. However, you will need to replace the placeholders in the codebase with your actual EmailJS credentials. Because your website is statically generated (just HTML/JS), EmailJS is the most robust and simplest way to submit forms without needing an active backend/Node server.

## Overview of what was implemented
- Handled UI states for the "Send Request" button so users know the mail is `Sending...` while they wait in real-time.
- Included error handling to show browser alerts if the mail failed (or credentials aren't set).
- Included the EmailJS module cleanly in the `<head>` of your `contact.html` document.
- Kept the "Success Modal" firing logic robust so it only triggers upon verified delivery.

---

## 1. Create your EmailJS Account
1. Go to [EmailJS.com](https://www.emailjs.com/) and sign up for a free account.
2. Sign in to your dashboard.

## 2. Connect Your Email Service
1. On the left sidebar, click **Email Services**.
2. Click **Add New Service** and select an email provider (e.g. Gmail).
3. Connect your account.
4. Copy the identifier string labeled **Service ID** (it usually looks like `service_xxxxx`).

## 3. Create your Email Template
1. On the left sidebar, click **Email Templates**.
2. Click **Create New Template**.
3. In the template editor, you will tell EmailJS how to format the incoming emails using variables. Our form has 5 inputs, and their specific `name` attributes map to these variables. Copy and paste this exact layout into your template body:

```text
Hello MM Contractors,

You have received a new quote request from the website:

Name / Company: {{name}}
Phone Number: {{phone}}
Email Address: {{email}}
Project Location: {{location}}

Description of Work:
{{message}}
```
4. Save the template.
5. Copy the identifier string labeled **Template ID** (it usually looks like `template_xxxxx`).

## 4. Retrieve your Public Key
1. Go to **Account** -> **API Keys** on the left menu.
2. Copy your **Public Key**.

## 5. Insert Credentials into the Codebase
Now that you have your three credentials, replace the placeholders in your files.

**File 1:** `contact.html` (Around line 18)
```html
    <script type="text/javascript">
        (function(){
            emailjs.init({
                publicKey: "YOUR_PUBLIC_KEY", // Replace this!
            });
        })();
    </script>
```

**File 2:** `main.js` (Around line 45)
```javascript
// Send form using EmailJS
emailjs.sendForm('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', contactForm)
    .then(() => {
        // Success logic
```

Once replaced and explicitly saved, your Contact Form will immediately start routing forms straight to your actual email inbox without needing any extra hosting features!
