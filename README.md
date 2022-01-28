# Django

Django is an **open-source**, **Python-based** framework for building web applications.

## Coding Style

- [PEP8](https://www.python.org/dev/peps/pep-0008/)
  PEP 8 is the official style guide for Python.
  PEP 8 describes coding conventions such as:
  - “Use 4 spaces per indentation level.”
  - “Separate top-level function and class definitions with two blank lines.”
  - “Method definitions inside a class are separated by a single blank line.”  
    and many more.......
- [flake8](https://pypi.org/project/flake8/)
  - Flake8 is a very useful command-line tool for checking coding style, quality, and logic errors in projects. . This is a better wrapper for linting. It is a wrapper around these tools:
    - PyFlakes
    - pycodestyle
    - Ned Batchelder's McCabe script
- [Black](https://github.com/psf/black)
  - Black is a Python code formatter.
- Imports

  - PEP 8 suggests that imports should be grouped in the following order:

    1. Standard library imports
    2. Related third-party imports
    3. Local application or library-specific imports
       ![Example Imports](https://i.imgur.com/0HOny95.png)

  - The import order in a Django project is:
    1. Standard library imports.
    2. Imports from core Django.
    3. Imports from third-party apps including those unrelated to Django.
    4. Imports from the apps that you created as part of your Django project.
       > The `isort` Python library sorts your imports so we don’t have to.It imports alphabetically and automatically separates our imports into sections and by type.
  - Avoid Using Import \*
  - Use Aliases to Avoid Python Module Collisions
    - `from django.db.models import CharField as ModelCharField`
    - `from django.forms import CharField as FormCharField`
  - [Django own coding styles](https://docs.djangoproject.com/en/3.2/internals/contributing/writing-code/coding-style/)
  - Use Underscores in URL Pattern Names Rather Than Dashes.
    - It is referring to the
      name argument of url() here, not the actual URL typed into the browser.
    - Dashes in actual URLs are fine (e.g. `route='some-thing-cool/'`)

## Django Environment

- Use the Same Database Engine Everywhere.
- Use Pip and (Virtualenv or venv)
- Use Docker
- Use git

## Layout

## Project Layout

1. `django-admin startproject <mysite>` - This is the default setup django-admin provide us. It is good only for learning. As project scales it becomes difficult to manage.
   ![Not so good layout](https://i.imgur.com/bNqRIJB.png)

2. `Modified two tier approach` - We can modify the default setup into two tier approach.
   ![Two-tier approach](https://i.imgur.com/kxx6gaX.png)
   - `Top Level:` **Repository Root** - The `<repository_root>` directory is the absolute root directory of the project. In addition to the `<django_project_root>` and `<configuration_root>`, we also include other critical components like the `README.md`, `docs/` directory, `manage.py`, `.gitignore`, `requirements.txt` files, and other high-level files that are required for deployment and running the project.
   - `Second Level:`**Django Project Root** - The `<django_project_root>/` directory is the root of the actual Django project. Non-configuration Python code files are inside this directory, its subdirectories, or below.  
     If using django-admin startproject, you would run the command from within the repository root. The Django project that it generates would then be the project root.
   - `Second Level:` **Configuration Root** - The `<configuration_root>` directory is where the settings module and base `URLConf (urls.py)`
     are placed. If using django-admin startproject, the configuration root is initially inside of the Django project root. It **`should be moved to the repository root`.**
     ![Overview](https://i.imgur.com/QJOZH2S.png)
     ![Overview](https://i.imgur.com/hPGfGa9.png)
     `icecreamratings_project/` directory, is the `<repository_root>`. Most of the file are common. Some things are worth mentioning `config/` correspond to `<configuration_root>`. `icecreamratings/` correspond to `<django_project_root>` of the project.
3. [CookieCutter](https://github.com/cookiecutter/cookiecutter-django)
   It provides a much cleaned implementation of above approach. Help us to configure docker,celery and cli,linters and much other options.It asks us few basic question like the services we will use using(Docker,CI/CD,celery....) and then it output a production ready django project.
   ![Output](https://i.imgur.com/tNJktDI.png)

## App Design

- When possible keep to single word names like flavors, animals, blog, polls, dreams,estimates,
  and finances.
- the app’s name should be a plural version of the app’s main model, but
  there are many good exceptions to this rule, blog being one of the most common ones.
- Try and keep your apps small. Remember, it’s better to have many small apps than to have
  a few giant apps.

## Setting and requirements

- Using Multiple Settings Files.Instead of having one settings.py file, with this setup you have a settings/ directory containing
  your settings files.
  ![Example](https://i.imgur.com/Lv4SpKf.png)
- Separate Configuration From Code. use environment variables (for secrets,keys)

## App Locations

Regarding app positions. Majorly there are two choices.
We can either create a folder named `apps` inside the project folder and put all apps inside.
![All apps inside a dir](https://i.imgur.com/SVqrcrX.png)
Now the other way is obvious, we can just choose not to put apps inside any dir.
![Apps without any dir](https://i.imgur.com/j4k838A.png)

## Combining everything we get following choices

**Default App**
![Default App](https://i.imgur.com/KuH1d8m.png)
**Apps inside common dir**
![Apps inside common dir](https://i.imgur.com/RBsr5AH.png)
**Apps inside common dir**
![Apps without common dir](https://i.imgur.com/zTh2RRK.png)

Further improvements can be done depending on the team requirement which can be build on the any of above base.

## Naming convention

- As a general rule, the app’s name should be a plural version of the app’s main model, but
  there are many good exceptions to this rule, blog being one of the most common ones.Don’t just consider the app’s main model, though. You should also consider how you want
  your URLs to appear when cho osing a name. If you want your site’s blog to appear at
  <http://www.example.com/weblog/>, then consider naming your app weblog rather than
  blog, posts, or blogposts, even if the main model is Post, to make it easier for you to see
  which app corresponds with which part of the site.

### Template Location

Templates are the third and most important part of Django's **Model View Template** Structure. A template in Django is basically written in HTML, CSS, and Javascript in a .html file.

- Root Level - This is one of the possible configuration we can adopt. In this approach we can put all out template inside the template folder located at **root level** (Project folder)

![Project View](https://i.imgur.com/bDNN6Uc.png)

We can see that we have multiple apps in the feedback project.
profiles
reviews
So the templates these need can be put into the root level template.
It comes with own disadvantages. One of the biggest con is the inability to reused the app. Since every template is mixed in the root template. We can re use any other project.Or if We want to provide a different layout to each component of our webpage.

- App Level - As the name state we can place the template file of the apps in the their respective folders. As we can one example for the review app.

![Project View](https://i.imgur.com/BsLhIzJ.png)

This approach has it own advantages. Since every app is self contained. We can re use this app in other project of our. Like we can copy this profile app to show user profile in any other project we are building.
