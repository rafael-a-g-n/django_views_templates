# 📚 Django Online Course Platform

A modern, full-featured online course management system built with Django 4.2. This project demonstrates Django's powerful views, templates, and ORM capabilities through a practical e-learning platform.

![Django](https://img.shields.io/badge/Django-4.2.17-green.svg)
![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

## 🌟 Features

- **Course Management**: Browse and enroll in popular online courses
- **User Enrollment System**: Track student enrollments with different course modes (Audit, Honor, Beta)
- **Instructor & Learner Profiles**: Comprehensive user management with roles
- **Lesson Organization**: Structured course content with ordered lessons
- **Media Support**: Course images and static file handling
- **Admin Interface**: Powerful Django admin panel for content management
- **Responsive Design**: Modern CSS styling for optimal viewing experience

## 📋 Table of Contents

- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Models](#-models)
- [Views & URLs](#-views--urls)
- [Templates](#-templates)
- [Admin Panel](#-admin-panel)
- [API Endpoints](#-api-endpoints)
- [Development](#-development)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

## 🔧 Prerequisites

- Python 3.8 or higher
- pip (Python package installer)
- Virtual environment (recommended)
- SQLite3 (included with Python)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd django_views&templates
```

### 2. Create Virtual Environment

**Windows (PowerShell):**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**Linux/Mac:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Apply Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Create Superuser

```bash
python manage.py createsuperuser
```

Follow the prompts to create an admin account.

### 6. Collect Static Files

```bash
python manage.py collectstatic --noinput
```

### 7. Run Development Server

```bash
python manage.py runserver
```

Visit `http://127.0.0.1:8000/onlinecourse/` to view the application.

## ⚙️ Configuration

### Environment Variables

For production, set the following environment variables:

```bash
SECRET_KEY=your-secret-key-here
DEBUG=False
ALLOWED_HOSTS=your-domain.com,www.your-domain.com
```

### Database Configuration

The project uses SQLite by default. To use PostgreSQL or MySQL, update `DATABASES` in `myproject/settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'your_db_name',
        'USER': 'your_db_user',
        'PASSWORD': 'your_db_password',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```

## 📖 Usage

### Accessing the Application

- **Home Page**: `http://127.0.0.1:8000/onlinecourse/`
- **Admin Panel**: `http://127.0.0.1:8000/admin/`
- **Course Details**: `http://127.0.0.1:8000/onlinecourse/course/<course_id>/`

### Adding Courses

1. Log in to the admin panel at `/admin/`
2. Navigate to **Courses** → **Add Course**
3. Fill in course details:
   - Course name
   - Description
   - Upload course image
   - Select instructors
   - Add lessons inline
4. Click **Save**

### Enrolling in Courses

1. Browse available courses on the home page
2. Click the **Enroll** button on any course
3. View enrolled course details and lessons

## 📁 Project Structure

```
django_views&templates/
├── manage.py                 # Django management script
├── requirements.txt          # Python dependencies
├── runtime.txt              # Python version specification
├── db.sqlite3               # SQLite database
│
├── myproject/               # Main project directory
│   ├── __init__.py
│   ├── settings.py          # Project settings
│   ├── urls.py              # Root URL configuration
│   ├── wsgi.py              # WSGI configuration
│   └── asgi.py              # ASGI configuration
│
├── onlinecourse/            # Main application
│   ├── __init__.py
│   ├── admin.py             # Admin interface configuration
│   ├── apps.py              # App configuration
│   ├── models.py            # Database models
│   ├── views.py             # View functions
│   ├── urls.py              # App URL patterns
│   ├── tests.py             # Unit tests
│   │
│   ├── migrations/          # Database migrations
│   │   ├── __init__.py
│   │   └── 0001_initial.py
│   │
│   ├── templates/           # HTML templates
│   │   └── onlinecourse/
│   │       ├── course_list.html
│   │       └── course_detail.html
│   │
│   └── static/              # Static files (CSS, JS, images)
│       └── onlinecourse/
│           └── course.css
│
└── static/                  # Collected static files
    ├── admin/               # Django admin static files
    └── media/               # User-uploaded media
        └── course_images/   # Course images
```

## 🗄️ Models

### Course
- **Fields**: name, image, description, pub_date, total_enrollment
- **Relationships**: ManyToMany with Instructor and User (through Enrollment)

### Lesson
- **Fields**: title, order, content
- **Relationships**: ForeignKey to Course

### Instructor
- **Fields**: user (ForeignKey), full_time, total_learners
- **Relationships**: ForeignKey to User model

### Learner
- **Fields**: user (ForeignKey), occupation, social_link
- **Occupation Choices**: Student, Developer, Data Scientist, Database Admin

### Enrollment
- **Fields**: user, course, date_enrolled, mode, rating
- **Mode Choices**: Audit, Honor, BETA

## 🌐 Views & URLs

### Available Views

| View | URL Pattern | Description |
|------|-------------|-------------|
| `popular_course_list` | `/onlinecourse/` | Lists top 10 courses by enrollment |
| `course_details` | `/onlinecourse/course/<id>/` | Shows course details and lessons |
| `enroll` | `/onlinecourse/course/<id>/enroll/` | Handles course enrollment (POST) |

### URL Configuration

```python
# Root URLs (myproject/urls.py)
/admin/                     # Django admin interface
/onlinecourse/              # Online course application

# App URLs (onlinecourse/urls.py)
''                          # Course list
'course/<int:course_id>/'   # Course details
'course/<int:course_id>/enroll/'  # Enrollment endpoint
```

## 🎨 Templates

### course_list.html
Displays a list of popular courses with:
- Course images
- Course name and description
- Enrollment count
- Enroll button
- Responsive grid layout

### course_detail.html
Shows detailed course information:
- Course name and description
- List of lessons (ordered)
- Lesson content

## 🔐 Admin Panel

The Django admin interface provides:

- **Course Management**: Create, edit, and delete courses with inline lesson editing
- **Lesson Management**: Manage course lessons with title, order, and content
- **User Management**: Manage instructors and learners
- **Enrollment Tracking**: View and manage student enrollments
- **Search & Filters**: Search courses by name/description, filter by publication date

### Admin Features

```python
# Course Admin
- Inline lesson editing (5 extra forms)
- List display: name, publication date
- Search: name, description
- Filter: publication date

# Lesson Admin
- List display: title
```

## 📡 API Endpoints

### GET Endpoints

- `GET /onlinecourse/` - Retrieve list of popular courses
- `GET /onlinecourse/course/<course_id>/` - Retrieve course details

### POST Endpoints

- `POST /onlinecourse/course/<course_id>/enroll/` - Enroll in a course

## 🛠️ Development

### Running Tests

```bash
python manage.py test onlinecourse
```

### Creating New Migrations

```bash
python manage.py makemigrations onlinecourse
python manage.py migrate
```

### Loading Sample Data

Create a fixture file or use the Django shell:

```bash
python manage.py shell
```

```python
from onlinecourse.models import Course, Instructor, Lesson
from django.contrib.auth.models import User

# Create sample data
user = User.objects.create_user('instructor1', 'email@example.com', 'password')
instructor = Instructor.objects.create(user=user, full_time=True, total_learners=0)
course = Course.objects.create(
    name='Python Basics',
    description='Learn Python programming from scratch',
    total_enrollment=0
)
course.instructors.add(instructor)
```

### Code Style

This project follows PEP 8 guidelines. To check code style:

```bash
pip install flake8
flake8 onlinecourse/
```

## 🚢 Deployment

### Production Checklist

- [ ] Set `DEBUG = False` in settings.py
- [ ] Configure `ALLOWED_HOSTS` with your domain
- [ ] Change `SECRET_KEY` to a secure random value
- [ ] Use environment variables for sensitive data
- [ ] Configure production database (PostgreSQL recommended)
- [ ] Set up static file serving (WhiteNoise or CDN)
- [ ] Configure email backend for notifications
- [ ] Enable HTTPS/SSL certificates
- [ ] Set up logging and monitoring
- [ ] Configure backup strategy

### Deployment with Gunicorn

```bash
gunicorn myproject.wsgi:application --bind 0.0.0.0:8000
```

### Docker Deployment (Optional)

Create a `Dockerfile`:

```dockerfile
FROM python:3.8
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
RUN python manage.py collectstatic --noinput
CMD ["gunicorn", "myproject.wsgi:application", "--bind", "0.0.0.0:8000"]
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Write clear, documented code
- Add unit tests for new features
- Update documentation as needed
- Follow Django best practices
- Use meaningful commit messages

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- Built as part of the IBM Django course on Coursera
- Django Software Foundation for the excellent framework
- Community contributors and testers

## 📧 Contact

For questions or support, please open an issue on GitHub.

---

## 📚 Additional Resources

- [Django Documentation](https://docs.djangoproject.com/)
- [Django Tutorial](https://docs.djangoproject.com/en/4.2/intro/tutorial01/)
- [Django Best Practices](https://django-best-practices.readthedocs.io/)
- [Python Virtual Environments](https://docs.python.org/3/tutorial/venv.html)

---

**Happy Learning! 🎓**

