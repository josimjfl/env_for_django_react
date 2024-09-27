
# Creat .env file for Django and React 
## JFL_CRM `.env` Setup Guide
### By JFL IT Lab
#### Author: Josim Uddin as josimjfl@gmail.com
This guide will help you configure environment variables for both the **backend (Django)** and **frontend (React)** parts of the JFL_CRM project. This will ensure sensitive data like API keys and URLs are securely managed and not hardcoded into the codebase.

## 1. Django (Backend) Setup

For Django, we use the `python-decouple` package to manage environment variables.

### Steps:

1. **Install `python-decouple`**:
   ```bash
   pip install python-decouple
   ```

2. **Create a `.env` file** at the root of your Django project (where `manage.py` is located):
   ```env
   DEBUG=True
   SECRET_KEY=your-secret-key-here
   DATABASE_URL=postgres://user:password@localhost:5432/mydb
   ALLOWED_HOSTS=localhost,127.0.0.1
   ```

3. **Edit `settings.py`** to use the environment variables:
   
   ```python
   from decouple import config
   import os

   # Load settings from .env
   SECRET_KEY = config('SECRET_KEY')
   DEBUG = config('DEBUG', default=False, cast=bool)
   ALLOWED_HOSTS = config('ALLOWED_HOSTS', default='').split(',')

   # Database Configuration
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.postgresql',
           'NAME': config('DATABASE_URL'),
       }
   }
   ```

4. **Ensure `.env` is in `.gitignore`**:
   Add the following line to `.gitignore` to prevent `.env` from being pushed to version control:
   ```
   .env
   ```

### Example `.env` for Django:

```env
DEBUG=False
SECRET_KEY=super-secret-key
DATABASE_URL=postgres://dbuser:dbpassword@127.0.0.1:5432/mydatabase
ALLOWED_HOSTS=localhost,127.0.0.1,myapp.com
```

---

## 2. React (Frontend) Setup

For React, environment variables are prefixed with `REACT_APP_` to be accessible in the app.

### Steps:

1. **Create a `.env` file** in the root of the React app (same directory as `package.json`):
   ```env
   REACT_APP_API_BASE_URL=http://127.0.0.1:8000/api/
   REACT_APP_ENVIRONMENT=development
   ```

2. **Access environment variables in your React code**:
   ```javascript
   const apiUrl = process.env.REACT_APP_API_BASE_URL;
   console.log('API Base URL:', apiUrl);
   ```

3. **Add `.env` to `.gitignore`**:
   ```bash
   echo ".env" >> .gitignore
   ```

### Example `.env` for React:

```env
REACT_APP_API_BASE_URL=http://127.0.0.1:8000/api/
REACT_APP_GOOGLE_MAPS_API_KEY=your-google-maps-api-key
REACT_APP_ENVIRONMENT=production
```

---

## 3. Combine Django and React Environment Variables

In **JFL_CRM**, the backend `.env` will handle configurations such as the secret key, database settings, and allowed hosts, while the frontend `.env` will handle things like the base API URL and third-party services (e.g., Google Maps).

Make sure you manage both `.env` files separately and ensure they are both listed in `.gitignore` to avoid leaking sensitive information.

---

## Summary of `.env` Setup

- **Django (Backend)**: 
  - Handles secret keys, database credentials, and allowed hosts.
- **React (Frontend)**:
  - Manages the base API URL, third-party APIs, and environment-specific settings.

Be sure to handle environment variables securely in both parts of the project.

---


IF Error, Please update this
##### Below solution for Uncaught ReferenceError: process is not defined:

    if you are using CRA (create react app), use '''process.env.'''
    if you are using ViteJS, use '''import.meta.env.'''

Read more here about how to import env process in Vite: https://vitejs.dev/guide/env-and-mode.html

Examples:

CRA: ```process.env.API_BASE_URL```

Vite: ```import.meta.env.VITE_API_BASE_URL```

Please Follow jflitlab
