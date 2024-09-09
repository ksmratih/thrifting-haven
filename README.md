# :handbag: Thrifting Haven :womans_clothes:

## PWS application:
(http://kusuma-ratih-thriftinghaven.pbp.cs.ui.ac.id/)

## :memo: How to implement the checklist

1. Create a new Django Project
In order to create a new Django Project we have to:
Create a new directory named `thrifting-haven` and open the command prompt inside the new directory.
Create a virtual environment by running the command below
```
python -m venv env
```
Then activate the virtual environment with the following command, indicated with (env) on the terminal input line.
```
env\Scripts\activate
```
Afterwards, we set up dependencies in the same directory.
Create a `requirements.txt` file and add the following dependencies
```
django
gunicorn
whitenoise
psycopg2-binary
requests
urllib3
```
We install the dependencies by running the following command
```
pip install -r requirements.txt
```
Finally, we create a Django project named thrifting_haven by running the following command
```
django-admin startproject thrifting_haven .
```
Lastly, we need to configure the project and run the server.
To deploy we add the following to `ALLOWED_HOSTS` in `settings.py`:
```
ALLOWED_HOSTS = ["localhost", "127.0.0.1"]
```
Ensure `manage.py` is in the terminal’s active directory, then start the server with:
```
python manage.py runserver
```
Once opening http://localhost:8000/ on your web browser shows a rocket animation, then you stop the server by pressing `CTRL+C` and deactivate the virtual environment with the command
```
deactivate
```

2. Create an application with the name main in the project




## The diagram that contains the request client to a Django-based web application and the response it gives, and explain the relationship between urls.py, views.py, models.py, and the html file.


## :outbox_tray: The use of git in software development 

Git is essential in software development for managing code versions and enabling collaboration. It allows multiple developers to work on different parts of a project simultaneously by using branches, which can later be merged into the main codebase. Git also tracks changes, providing a history of modifications that makes it easy to revert to previous versions if needed. It also integrates with platforms like GitHub or GitLab, facilitating code reviews and ensuring code quality. 

## :chart_with_upwards_trend: Why Django is used as the starting point for learning software development

Django is a popular choice for beginners because it’s simple, easy to understand, and comes with many built-in tools that make web development easier. Since it’s based on Python, which is known for its clear and straightforward syntax, it's great for learning. Django helps you focus on building your project without worrying too much about complex details, like handling databases or user logins. It also teaches good practices in organizing code, making it a solid foundation for anyone starting in software development.

## :bulb: Why the Django model is called an ORM

Django’s model is called an ORM (Object-Relational Mapper) because it helps you work with databases using Python code instead of writing SQL queries. It turns Python classes into database tables and class attributes into table columns. This makes it easier to manage the database, letting you add, update, or delete data using Python without needing to learn SQL.

