# Django Employment Form App

A Django web application that allows users to submit a job application form. Submissions are saved to a SQLite database via the Django ORM, a confirmation email is sent automatically to the applicant via Gmail, and all submissions can be reviewed through the Django admin interface.

---

## Features

- Job application form with first name, last name, email, availability date, and current occupation
- Form submissions saved to a SQLite database using Django models
- Automated confirmation email sent to the applicant on successful submission
- Flash success message displayed in the browser after submission
- Django admin interface to view and manage all submitted applications
- Environment variables used to keep email credentials secure
- Responsive UI built with Bootstrap 5

---

## Project Structure

```
django_employment_form_APP/
│
├── manage.py                        # Django management entry point
├── .env                             # Email credentials — NOT committed to GitHub
├── .gitignore
├── README.md
│
├── mysite/                          # Project configuration
│   ├── settings.py                  # App settings, email config, database
│   ├── urls.py                      # Root URL routing
│   └── wsgi.py
│
└── job_application/                 # Main app
    ├── models.py                    # Form database model
    ├── forms.py                     # Django form definition
    ├── views.py                     # Route logic, email sending, flash messages
    ├── admin.py                     # Admin interface registration
    ├── urls.py                      # App URL routing
    └── templates/
        └── index.html               # Job application form (Bootstrap 5)
```

---

## Requirements

- Python 3.13+
- Django 6.0.5
- A Gmail account with an [App Password](https://support.google.com/accounts/answer/185833) configured

Install dependencies:

```bash
pip install django python-dotenv
```

---

## Setup

1. Clone the repository:

```bash
git clone https://github.com/PeterTZN/django_employment_form_APP.git
cd django_employment_form_APP
```

2. Create and activate a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate       # macOS/Linux
.venv\Scripts\activate          # Windows
```

3. Install dependencies:

```bash
pip install django python-dotenv
```

4. Create a `.env` file in the project root (same folder as `manage.py`):

```
EMAIL_HOST_USER=your_email@gmail.com
EMAIL_HOST_PASSWORD=your_gmail_app_password
```

> **Important:** Never commit your `.env` file to GitHub. Make sure it is listed in your `.gitignore`.

5. Run database migrations:

```bash
python manage.py migrate
```

6. Create a superuser to access the admin interface:

```bash
python manage.py createsuperuser
```

7. Run the development server:

```bash
python manage.py runserver
```

8. Open your browser and go to `http://127.0.0.1:8000`

---

## Admin Interface

All submitted applications can be viewed and managed via the Django admin panel:

```
http://127.0.0.1:8000/admin
```

Log in with the superuser credentials you created in step 6.

---

## Gmail App Password Setup

This app uses Gmail's SMTP server to send confirmation emails. Google requires an **App Password** rather than your regular account password:

1. Go to your Google Account → Security
2. Enable 2-Step Verification if not already active
3. Go to Security → App Passwords
4. Generate a new App Password for "Mail"
5. Use that 16-character password as `EMAIL_HOST_PASSWORD` in your `.env` file

---

## macOS SSL Fix

If you encounter an `SSLCertVerificationError` on macOS, run this once in your terminal to install the required certificates:

```bash
/Applications/Python\ 3.13/Install\ Certificates.command
```

---

## How It Works

### `views.py`

| Method | Description |
|---|---|
| `GET /` | Renders a blank application form |
| `POST /` | Validates form, saves to database, sends confirmation email, flashes success message |

### `models.py`

Stores each submission with fields: `first_name`, `last_name`, `email`, `date`, `occupation`.

### `settings.py`

Configures Django, SQLite database, and Gmail SMTP email backend. Credentials are loaded securely from `.env`.

---

## .gitignore

Make sure your `.gitignore` includes the following:

```
.env
__pycache__/
.venv/
*.pyc
db.sqlite3
```

---

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| `SSLCertVerificationError` | macOS missing Python SSL certs | Run `Install Certificates.command` — see macOS SSL Fix above |
| Email not sending | Gmail App Password not configured | Follow the Gmail App Password steps above |
| `SMTPAuthenticationError` | Wrong password in `.env` | Double-check your App Password |
| Form not rendering | Form not passed to template context | Ensure `{"form": form}` is in the `render()` call in `views.py` |
| Admin page empty | Model not registered | Check `admin.py` has `admin.site.register(Form)` |

---

## Built With

- [Django](https://www.djangoproject.com/) — web framework
- [SQLite](https://www.sqlite.org/) — database (via Django ORM)
- [python-dotenv](https://pypi.org/project/python-dotenv/) — environment variable management
- [Bootstrap 5](https://getbootstrap.com/) — frontend styling
- [Gmail SMTP](https://support.google.com/mail/answer/7126229) — email delivery

---

## License

MIT License

Copyright (c) 2026 Peter Thomson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

---

## Disclaimer

This project is intended for educational and demonstration purposes only. It is
not intended for use in a production environment without appropriate security
hardening, including but not limited to: replacing the development secret key,
using a production-grade WSGI server, and securing all credentials. The author
accepts no responsibility for any misuse or damage arising from the use of this
software.

---

*Author: Peter Thomson*
*GitHub: [PeterTZN](https://github.com/PeterTZN)*
*Last updated: 22/05/2026*