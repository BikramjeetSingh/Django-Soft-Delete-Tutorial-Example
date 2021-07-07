
Complete source code for the example in my article on [implementing soft deletion in Django](https://dev.to/bikramjeetsingh/soft-deletes-in-django-a9j).

# Setup

1. Clone repository
2. (Optional but recommended) Create a virtual environment, `python -m venv venv`, and activate it, `source venv/bin/activate`
3. Install requirements, `pip install -r requirements.txt`
4. Create database and run migrations: `python manage.py migrate`
5. Run the Django shell: `python manage.py shell`

# Try Out the Soft Deletion Pattern

Import the relevant models:

```python
from django.contrib.auth.models import User
from tutorialapp.models import Note
```

Create a user:

```python
john = User.objects.create_user('john', 'lennon@thebeatles.com', 'johnpassword')
```

Create a couple of notes:

```python
my_note = Note.objects.create(user=john, title="Strawberry Fields", content="Strawberry Fields Forever")
another_note = Note.objects.create(user=john, title="Here Comes The Sun", content="It's All Right")
```

Soft delete them:

```python
my_note.soft_delete()
```

And restore them:

```python
my_note.restore()
```

Fetch undeleted notes:

```python
Note.objects.all()
```

Fetch all notes, included those that have been soft deleted:

```python
Note.all_objects.all()
```

Fetch undeleted notes belonging to a user, using Django's reverse relationships:

```python
john.notes.all()
```
