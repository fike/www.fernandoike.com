+++
title = "Flask tutorial with migrations"
date = 2020-12-11T16:03:40-03:00
draft = true
description = "Why create a repo based Flask original tutorial..."
categories = ["python", "docker", "flask"]
tags = ["python", "docker", "flask"]
+++
Note: This text is a draft, and needs a lot of improvements.

[Flask project](https://flask.palletsprojects.com) has a really [good tutorial](https://flask.palletsprojects.com/en/1.1.x/tutorial/) to follow and study, I followed almost at all there. If you have time to follow step by step, I recommend to use the Flask tutorial from documentation, because they explain how to use [Blueprints](https://flask.palletsprojects.com/en/1.1.x/tutorial/views/), how to create and [test](https://flask.palletsprojects.com/en/1.1.x/tutorial/tests/) features.

I followed this tutorial, finally, to use Flask better. As an exercise for me, I thought to implement a new attribute to a user, change the database to [PostgreSQL](https://postgresql.org), and create unit tests.

## Change database

Beyond changing the database engine, I thought too was good to implement migrations like Django ORM and migrations.
Flask has an extension for SQLAlchemy called [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) and
for migrations using [Alembic](https://alembic.sqlalchemy.org/en/latest/) called
[Flask-Migrate](https://github.com/miguelgrinberg/Flask-Migrate).

To change from SQLite to PostgreSQL, need to change db_url variable to use PostgreSQL connection URI in the "*flaskr/\__init\__.py*" file.

```python
[...]

    if db_url is None:
        # URI PostgreSQL 
        db_url = "postgresql://flaskr:flaskr_pass@localhost:5432/flaskr"

[...]
```

The original tutorial code use the **Click** Flask feature to create tables in the database, as this repo use Flask-Migrate we can comment **init-db** code command in the [same file](https://github.com/fike/flask-tutorial/blob/master/flaskr/__init__.py).

```python (flask/__init__.py)
[...]

# @click.command("init-db")
# @with_appcontext
# def init_db_command():
# """Clear existing data and create new tables."""
# init_db()
# click.echo("Initialized the database.")

[...]
```

## Adding a new profile field

Add profile attribute in the User model editing *flaskr/auth/models.py*:

```python
[...]

class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True, nullable=False)
    _password = db.Column("password", db.String, nullable=False)
    profile = db.Column(db.Text, nullable=False) // Profile attribute

[...]
```

In the view needs to add a profile in the endpoint */register* to receive profile data from the form.
Add a conditional check for a profile is null, return to the user that profile description is required,
add profile together with username and password to storage in the database.

```Python
@bp.route("/register", methods=("GET", "POST"))
def register():
[...]
    if request.method == "POST":
        username = request.form["username"]
        password = request.form["password"]
        profile = request.form["profile"] # add profile variable to receive data profile
        error = None

        if not username:
            error = "Username is required."
        elif not password:
            error = "Password is required."
        elif not profile: # Check if profile field is null 
            error = "Profile is required." # Return that it's required.
        elif db.session.query(
            User.query.filter_by(username=username).exists()
        ).scalar():
            error = f"User {username} is already registered."

        if error is None:
            # the name is available, create the user and go to the login page
            db.session.add(User(username=username, password=password, profile=profile)) # Added profile in database session
            db.session.commit()
            return redirect(url_for("auth.login"))

        flash(error)

    return render_template("auth/register.html")

[...]
```

Good, now create a route to edit the profile. At the moment, just edit the username and profile description, I think in the feature I'll implement to change the password to explore Flask security features. 😉

```Python
[...]

@bp.route("/<int:id>/profile", methods=("GET", "POST"))
@login_required
def profile(id):
    """Update a user profile"""
    user = get_profile(id)

    if request.method == "POST":
        username = request.form["username"] 
        profile = request.form["profile"] # Adding a profile field in the form.
        error = None

        if not username:
            error = "Username is required"

        if not profile:
            error = "Profile is required" # Adding profile check is null

        if error is not None:
            flash(error)
        else:
            user.username = username
            user.profile = profile
            db.session.commit()
            return redirect(url_for("blog.index"))
    
    return render_template("auth/profile.html", user=user)

[...]

```

After created functions profile needs to change register.html to add the profile field in the Jinja2 file, *templates/auth/register.html*.

```HTML
{% extends 'base.html' %}

{% block header %}
  <h1>{% block title %}Register{% endblock %}</h1>
{% endblock %}

{% block content %}
  <form method="post">
    <label for="username">Username</label>
    <input name="username" id="username" required>
    <label for="profile">Profile Description</label>
    <input name="profile" id="profile" required> 
    <label for="password">Password</label>
    <input type="password" name="password" id="password" required>
    <input type="submit" value="Register">
  </form>
{% endblock %}
```

The original tutorial doesn't have the user profile page, needs to create the profile page and save it in the *templates/auth/profile.html* to edit.

```html
{% extends 'base.html' %}

{% block header %}
  <h1>{% block title %}Profile{% endblock %}</h1>
{% endblock %}

{% block content %}
  <form method="post">
    <label for="username">Username</label>
    <input name="username" id="username" value="{{ request.form['username'] or user['username'] }}" required>
    <label for="profile">Profile</label>
    <textarea name="profile" id="profile">{{ request.form['profile'] or user['profile'] }}</textarea>
    <input type="submit" value="Save">
  </form>
{% endblock %}
```

And the last code change, to add a link to the profile on the homepage when logged. For to do this, change a line in the *templates/base.html*.

From

```html
<li><span>{{ g.user['username'] }}</span>

```

To

```html
li><a href="{{ url_for('auth.profile', id=g.user['id']) }}">{{ g.user['username'] }}</a>

```


# Testing


Now it's time to write tests!!! 

I know, I know... I should create tests before the code using TDD. I'll do it in the next project. 😊

There are two tests in the *tests/test_auth.py* need to adapt to the support profile field on the register page. 

The test_register must support to filled form with profile data:

```python

def test_register(client, app):
    # test that viewing the page renders without template errors
    assert client.get("/auth/register").status_code == 200

    # test that successful registration redirects to the login page
    response = client.post(
        "/auth/register", data={"username": "a", "password": "a", "profile": "a user profile"}) # Profile data to filled the form
    assert "http://localhost/auth/login" == response.headers["Location"]

    # test that the user was inserted into the database
    with app.app_context():
        assert User.query.filter_by(username="a").first() is not None
```

The test_register_validate_input must support:

* When the profile is empty and return that it's required
* Add profile data in the test case when a user was registered before

```python

@pytest.mark.parametrize(
    ("username", "password", "profile", "message"),
    (
        ("", "", "", b"Username is required."),
        ("a", "", "", b"Password is required."),
        ("a", "a", "", b"Profile is required."), # Added 
        ("test", "test", "test user profile", b"already registered"),
        ("other", "test1", "other user profile", b"already registered"),
    ),
)
def test_register_validate_input(client, username, password, profile, message):
    response = client.post(
        "/auth/register", data={"username": username, "password": password, "profile": profile}
    )
    assert message in response.data

```

This test checks if each user can change its profile and can't change the profile of another user.

```python


def test_profile_update(client, auth, app):
    auth.login()
    assert client.get("/auth/1/profile").status_code == 200
    client.post("/auth/1/profile", data={"username": "a", "profile": "b"})

    with app.app_context():
        assert User.query.get(1).profile == "b"

```

# Improve developer experience


To add SQLAlchemy and Alembic, the flaskr tutorial becomes a little bit more complex to start and add new features. I tried to simplify the developer experience to implement a make file and containers using a few shell commands.


```bash
# start database
make up-db

# create tables
make migrate
```

To generate migrations and apply them in the database.

```bash
# update migrations
make gen-migrate

# apply migrations
make migrate

```

To clean containers generated.

```bash
make clean
```


## How to use my repo

If you just want to test, clone my repo and create a python virtual environment

```bash
# clone repo
git clone https://github.com/fike/flask-tutorial

# create the virtual environment
cd flask-tutorial
python3 -m venv venv

# activate the virtual environment
source venv/bin/activate

```

