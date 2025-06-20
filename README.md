# Vikramkumar-project2
You're asking how to find bugs effectively and like a pro! That's a great goal, whether you're a developer, a tester, or just someone who wants to improve the quality of software. Here's a breakdown of how to approach bug finding with a professional mindset: 
coding:
1. User Authentication & Session Management:

○ Secure Password Hashing: Passwords are never stored in plain text.

werkzeug.security.generate_password_hash uses strong, one-way hashing with

salting by default. check_password_hash verifies the password.

○ Session Management: Flask's session object is used to store user login status. It's

cryptographically signed using app.config['SECRET_KEY'], preventing tampering.

○ Logout Functionality: Properly terminates the user's session.

2. Input Validation and Sanitization (Flask-WTF):

○ Flask-WTF: This extension integrates WTForms, providing a robust way to define

and validate web forms.

○ DataRequired: Ensures fields are not empty.

○ Length: Enforces minimum and maximum lengths for inputs (e.g., username,

password).

○ EqualTo: Used for "confirm password" fields to ensure they match.

○ HTML Escaping (Jinja2): Flask's templating engine (Jinja2) automatically escapes

all data rendered in templates by default. This is crucial for preventing Cross-Site

Scripting (XSS) attacks, where malicious scripts could be injected into your pages.

By escaping, user-supplied data is treated as text, not executable code.

3. Cross-Site Request Forgery (CSRF) Protection:

○ Flask-WTF's CSRFProtect: Automatically generates and validates CSRF tokens

for all forms.

○ {{ form.csrf_token }} in the HTML template renders a hidden input field containing

the unique token. Flask-WTF then verifies this token on form submission. This

prevents attackers from tricking users into performing unwanted actions on your

site.

4. Error Handling:

○ Custom 404 (Not Found) and 500 (Internal Server Error) pages are provided. This

is a security best practice as it prevents your application from revealing sensitive
<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width,

initial-scale=1.0">

<title>Register</title>

<link rel="stylesheet" href="{{ url_for('static',

filename='style.css') }}">

</head>

<body>

<div class="container">

<h2>Register</h2>

{% with messages = get_flashed_messages(with_categories=true)

%}

{% if messages %}

<ul class="flashes">

{% for category, message in messages %}

<li class="{{ category }}">{{ message }}</li>

{% endfor %}

</ul>

{% endif %}

{% endwith %}

<form method="POST">

{{ form.csrf_token }}

<div>

{{ form.username.label }}<br>

{{ form.username(size=32) }}

{% if form.username.errors %}

<ul class="errors">

{% for error in form.username.errors %}

<li>{{ error }}</li>

{% endfor %}

</ul>

{% endif %}

</div>

<div>

{{ form.password.label }}<br>

{{ form.password(size=32) }}

{% if form.password.errors %}

<ul class="errors">
{% for error in form.password.errors %}

<li>{{ error }}</li>

{% endfor %}

</ul>

{% endif %}

</div>

<div>

{{ form.confirm_password.label }}<br>

{{ form.confirm_password(size=32) }}

{% if form.confirm_password.errors %}

<ul class="errors">

{% for error in form.confirm_password.errors

%}

<li>{{ error }}</li>

{% endfor %}

</ul>

{% endif %}

</div>

<div>

{{ form.submit() }}

</div>

</form>

<p>Already have an account? <a href="{{ url_for('login')

}}">Login here</a></p>

</div>

</body>

</html>

