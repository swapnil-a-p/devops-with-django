# DevOps With Django

A small Django to-do application used as a deployment and DevOps practice project.

This repository is intentionally simple. The goal is not product complexity; it is to use a familiar Python web app as a base for environment setup, deployment experimentation, and infrastructure workflow practice.

## What It Includes

- Django 4.x application
- basic CRUD-style to-do workflow
- server-rendered templates
- SQLite-backed local development setup
- static asset handling

## Tech Stack

- Python
- Django
- SQLite
- HTML / CSS

## Project Structure

- `manage.py` — Django management entrypoint
- `todoApp/` — project configuration and root URLs
- `todos/` — application models, views, templates, and routes
- `staticfiles/` — static assets

## Local Setup

1. Create and activate a virtual environment.

```bash
python -m venv .venv
source .venv/bin/activate
```

2. Install dependencies.

```bash
pip install -r requirements.txt
```

3. Run migrations.

```bash
python manage.py migrate
```

4. Start the development server.

```bash
python manage.py runserver
```

5. Open the app locally at:

```text
http://127.0.0.1:8000/todos
```

## Why This Repo Exists

This project was used as a lightweight Django base for practicing deployment-oriented workflows such as:

- environment bootstrapping
- app packaging
- static file handling
- branch-based deployment experimentation
- infrastructure and hosting practice around a Python web app

## Notes

This is an older practice project, not an actively developed product. It is best viewed as a compact Django deployment sandbox rather than a production-grade application.
