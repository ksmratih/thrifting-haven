# :handbag::scarf: Thrifting Haven :boot::coat:

## :link: PWS application:
http://kusuma-ratih-thriftinghaven.pbp.cs.ui.ac.id/


<details>
<Summary><b>Assignment 2</b></summary>


## [ASSIGNMENT 2](https://pbp-fasilkom-ui.github.io/ganjil-2025/en/assignments/individual/assignment-2)

## :memo: How to implement the checklist

### :ballot_box_with_check: Create a new Django Project
In order to create a new Django Project we have to:
+ Create a new directory named `thrifting-haven` and open the command prompt inside the new directory.
+ Create a virtual environment by running the command below
```
python -m venv env
```
+ Then activate the virtual environment with the following command, indicated with (env) on the terminal input line.
```
env\Scripts\activate
```
Afterwards, we set up dependencies in the same directory.
+ Create a `requirements.txt` file and add the following dependencies
```
django
gunicorn
whitenoise
psycopg2-binary
requests
urllib3
```
+ We install the dependencies by running the following command
```
pip install -r requirements.txt
```
Finally, we create a Django project named thrifting_haven by running the following command
```
django-admin startproject thrifting_haven .
```
Lastly, we need to configure the project and run the server.
+ To deploy we add the following to `ALLOWED_HOSTS` in `settings.py`:
```
ALLOWED_HOSTS = ["localhost", "127.0.0.1"]
```
+ Ensure `manage.py` is in the terminal’s active directory, then start the server with:
```
python manage.py runserver
```

### :ballot_box_with_check: Create an application with the name `main` in the project

Create a new application called `main` inside the `thrifting-haven` project by running the following command
```
python manage.py startapp main
```
To go into the next step, we make sure that the `settings.py` file inside `thrifting_haven` project directory has 'main' added to the `INSTALL_APPS` variable as shown below
```
INSTALLED_APPS = [
    ...,
    'main'
]
```

### :ballot_box_with_check: Perform routing in the project so that the application main can run
In order to configure the URL routing for the 'main' application we need to:
+ Create a `urls.py` file in the `main` directory with the following contents:
```
from django.urls import path
from main.views import show_main

app_name = 'main'

urlpatterns = [
    path('', show_main, name='show_main'),
]
```

### :ballot_box_with_check: Create a model in the application `main` with the name `Product` 
The following needs to be put into `models.py` in order to have the following attributes:
+ `name` as the name of the item with type CharField.
+ `price` as the price of the item with type IntegerField.
+ `description` as the description of the item with type TextField.
```
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.IntegerField()
    description = models.TextField()
    condition = models.CharField(max_length=100)
```

### :ballot_box_with_check: Create a function in `views.py` to return to an HTML template that displays the name of the application and your name and class
The code declares the show_main function, which accepts a request parameter. We hereby add a function that will handle HTTP requests and return the appropriate view such as the following:
```
from django.shortcuts import render

def show_main(request):
    context = {
        'application_name' : 'thrifting-haven',
        'class': 'PBD',
        'name': 'Kusuma Ratih Hanindyani'
    }

    return render(request, "main.html", context)
```

### :ballot_box_with_check: Create a routing in `urls.py` for the application `main` to map the function created in `views.py`
To add a URL route in the project's urls.py to connect it to the main view we need to open the `urls.py` file inside of the `thrifting_haven` project directory, not the one inside the `main` directory.

+ Import the include function from django.urls.
```
...
from django.urls import path, include
```

+ Add the following URL route to direct to the main view within the urlpatterns variable.
```
urlpatterns = [
    ...
    path('', include('main.urls')),
    ...
]
```

### :ballot_box_with_check: Perform deployment to PWS so that it can be accessed by others via the Internet
In order to deploy to PWS at https://pbp.cs.ui.ac.id we have to:
+ create a new project labeled as `thriftinghaven`
+ on the `settings.py` file of the Django project, add the PWS deployment URL to the ALLOWED_HOSTS field such as shown below
```
ALLOWED_HOSTS = ["localhost", "127.0.0.1","kusuma-ratih-thriftinghaven.pbp.cs.ui.ac.id"]
```
+ Do a git `add`, `commit`, and `push` for deployment to the PWS.

## :ballot_box_with_check: Create a `README.md` that contains a link to the PWS application that has been deployed
To create a README.md, simply open the used IDE (VS code) and add a `README.md` file to the project directory `thrifting-haven`.

## :bar_chart: Diagram that contains the request client to a Django-based web application and the response it gives, explaining the relationship between `urls.py`, `views.py`, `models.py`, and the `html` file
![diagram](diagram.png)
+ The user's request will first be processed and then forwarded to the appropriate view.
+ The view will then read/write data from the Model and use a Template to display and return the response to the user.

## :outbox_tray: The use of `git` in software development 

Git is essential in software development for managing code versions and enabling collaboration. It allows multiple developers to work on different parts of a project simultaneously by using branches, which can later be merged into the main codebase. Git also tracks changes, providing a history of modifications that makes it easy to revert to previous versions if needed. It also integrates with platforms like GitHub or GitLab, facilitating code reviews and ensuring code quality. 

## :chart_with_upwards_trend: Why Django is used as the starting point for learning software development

Django is a popular choice for beginners because it’s simple, easy to understand, and comes with many built-in tools that make web development easier. Since it’s based on Python, which is known for its clear and straightforward syntax, it's great for learning. Django helps you focus on building your project without worrying too much about complex details, like handling databases or user logins. It also teaches good practices in organizing code, making it a solid foundation for anyone starting in software development.

## :bulb: Why the Django model is called an ORM

Django’s model is called an ORM (Object-Relational Mapper) because it helps you work with databases using Python code instead of writing SQL queries. It turns Python classes into database tables and class attributes into table columns. This makes it easier to manage the database, letting you add, update, or delete data using Python without needing to learn SQL.

</details>

<details>
<Summary><b>Assignment 3</b></summary>


## [ASSIGNMENT 3](https://pbp-fasilkom-ui.github.io/ganjil-2025/en/assignments/individual/assignment-3)

### :ballot_box_with_check: Creating a form input to add a model

In order to reduce the possibility of redundancy of code we create a skeleton that acts as a base for views.
+ Create a directory `templates` in the `main` directory and create a new HTML file named `base.html`. 
+ In the `settings.py` file of the `thrifting_haven` directory you add the following to the `TEMPLATES` variable 
```
'DIRS': [BASE_DIR / 'templates'],
```

+ Create a new file in the `main` directory with the name `forms.py` so that it can receive Product datas
```
from django.forms import ModelForm
from main.models import Product

class ThriftEntryForm(ModelForm):
    class Meta:
        model = Product
        fields = ["name", "price", "description", "condition"]
```
+ Change the Primary Key From Integer to UUID by adding the following to the `main` subdirectory
```
import uuid  # add this line at the very top
...
class MoodEntry(models.Model):
    id = models.UUIDField(primary_key=True, default=uuid.uuid4, editable=False)  # add this line
...
```
+ Open the `views.py` file in the `main` directory and add `from django.shortcuts import render, redirect` at the top of the file
+ Create a new function to add new products
```
def create_product(request):
    form = ThriftEntryForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        form.save()
        return redirect('main:show_main')

    context = {'form': form}
    return render(request, "create_product.html", context)
```
+ Create a HTML template to display the form and add it to `urls.py` in the `main` directory
```
urlpatterns = [
    path('', show_main, name='show_main'),
    path('create-product', create_product, name='create_product'),
]
```

### :ballot_box_with_check: Add 4 views to view the added objects in XML, JSON, XML by ID, and JSON by ID formats

To access the XML and JSON data from the forms directly we insert the following functions into `views.py`
```
def show_xml(request):
    data = Product.objects.all()
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

def show_json(request):
    data = Product.objects.all()
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")

def show_xml_by_id(request, id):
    data = Product.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

def show_json_by_id(request, id):
    data = Product.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
```

### :ballot_box_with_check: Create URL routing for each of the views added

To create URL routing for each of the views added we have to:
+ Open the `urls.py` file in the `main` directory and import the previous functions such as the following
```
from main.views import show_main, create_mood_entry, show_xml, show_json, show_xml_by_id, show_json_by_id
```
+ Add the URL path to the `urlpatterns` variable in the `urls.py` file in the `main` directory to access the functions that were imported such as the following
```
    path('xml/', show_xml, name='show_xml'),
    path('json/', show_json, name='show_json'),
    path('xml/<str:id>/', show_xml_by_id, name='show_xml_by_id'),
    path('json/<str:id>/', show_json_by_id, name='show_json_by_id'),
```

## :mailbox_with_mail: Why we need data delivery in implementing a platform

The main reason data delivery is essential in implementing a platform is to ensure that users receive the information they need quickly and accurately, enabling seamless interaction with the platform. This enhances the user experience by ensuring real-time data access, maintaining data consistency, and supporting essential platform functions like displaying content, processing transactions, and integrating with external systems, all while ensuring performance and security.

## :file_folder: XML or JSON

I prefer JSON over XML because it's simpler and easier to work with. JSON has a compact, readable format that's quicker to write, parse, and debug compared to XML, which can be more complex and harder to read. Since JSON works well with JavaScript and other programming languages, it's perfect for modern web development and APIs where speed and efficiency are important. While XML has extra features like namespaces and schemas, these are often not needed for most applications today, which is why JSON is more popular.

## :clipboard: The functional usage of `is_valid()` method in Django forms and why we need the method in forms

The is_valid() method in Django forms checks whether the data entered is correct and follows the required rules, such as completeness and proper format. If the data is valid, it returns True and stores the cleaned data for further processing. If not, it returns False and provides error messages. This method is crucial to ensure that only valid and safe data is processed, preventing errors and security risks in the application, and providing feedback to users to correct any mistakes before submitting the form.

## :minidisc: Why we need `csrf_token` when creating a form in Django

The `csrf_token` in Django forms is essential to protect against Cross-Site Request Forgery (CSRF) attacks, which occur when a malicious website tricks a user into making unwanted requests to another site where they are authenticated. By using `csrf_token`, Django ensures that form submissions are legitimate and come from the same user who loaded the page. Without it, attackers could exploit this vulnerability by tricking users into performing unintended actions, such as changing account settings or transferring funds, potentially compromising the security of the web application.

## :postbox: Postman Results

### XML
![xml](images/xml.png)

### JSON 
![json](images/json.png)

### XML by ID
![xml by ID](images/xml%20by%20id.png)

### JSON by ID
![json by ID](images/json%20by%20id.png)

</details>

<details>
<Summary><b>Assignment 4</b></summary>


## [ASSIGNMENT 4](https://pbp-fasilkom-ui.github.io/ganjil-2025/en/assignments/individual/assignment-4)


### :ballot_box_with_check: Implement the register, login, and logout functions

In order to implement the Register we need to 
+ Import `UserCreationForm` and `messages` into `views.py` in the main subdirectory
```
from django.contrib.auth.forms import UserCreationForm
from django.contrib import messages
```
+ Add the `register` function
```
def register(request):
    form = UserCreationForm()

    if request.method == "POST":
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            messages.success(request, 'Your account has been successfully created!')
            return redirect('main:login')
    context = {'form':form}
    return render(request, 'register.html', context)
```
+ Create a new HTML file named `register.html`
+ Import the `register` function into `urls.py` and add the URL path to `urlpatterns`
```
from main.views import register
...
 urlpatterns = [
     ...
     path('register/', register, name='register'),
 ]
```
In order to implement a Login Function we need to
+ Import `authenticate`, `login`, and `AuthenticationForm` into `views.py`
```
from django.contrib.auth.forms import UserCreationForm, AuthenticationForm
from django.contrib.auth import authenticate, login
```
+ Add the `login_user` function
```
def login_user(request):
   if request.method == 'POST':
      form = AuthenticationForm(data=request.POST)

      if form.is_valid():
            user = form.get_user()
            login(request, user)
            return redirect('main:show_main')

   else:
      form = AuthenticationForm(request)
   context = {'form': form}
   return render(request, 'login.html', context)
```
+ Create a new HTML file named `login.html`
+ Import the `login_user` function into `urls.py` and add a URL path to `urlpatterns`
```
from main.views import login_user
...
urlpatterns = [
   ...
   path('login/', login_user, name='login'),
]
```
Lastly we need to implement the Logout Function
+ Import `logout` in `views.py`
```
from django.contrib.auth import logout
```
+ Add the `logout_user` function to `views.py`
```
def logout_user(request):
    logout(request)
    return redirect('main:login')
```
+ In the `main.html` file we add the following hyperlink tag
```
<a href="{% url 'main:logout' %}">
  <button>Logout</button>
</a>
```
+ In `urls.py` import the `logout_user` function and finally, we add the URL path to `urlpatterns` such as the following
```
from main.views import logout_user
...
urlpatterns = [
   ...
   path('logout/', logout_user, name='logout'),
]
```
### :ballot_box_with_check: Make two accounts with three dummy data

### account 1
![account 1](images/account%201.png)

### account 2
![account 2](images/account%202.png)

### :ballot_box_with_check: Connect the models `Product` and `User`

In order to connect the models `Product` and `User` in `models.py` you need to:
+ Add the import
```
from django.contrib.auth.models import User
```
+ Modify the `Product` model
```
class Product(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
```
In `views.py`, you need to:
+ Update `create_product`
```
def create_product(request):
    form = ThriftEntryForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        thrift_entry = form.save(commit=False)
        thrift_entry.user = request.user
        thrift_entry.save()
        return redirect('main:show_main')

    context = {'form': form}
    return render(request, "create_product.html", context)
```
+ Update `show_main`
```
def show_main(request):
    thrift_entries = Product.objects.filter(user=request.user)

    context = {
         'name': request.user.username,
         ...
    }
...
```
+ Run the model migration with
```
python manage.py makemigrations
python manage.py migrate
```
+ Add another statement in `settings.py` in the thrifting_haven subdirectory
```
import os
```
+ Change the variable `DEBUG` into the following
```
PRODUCTION = os.getenv("PRODUCTION", False)
DEBUG = not PRODUCTION
```
+ Test by making another account and seeing whether the previous Product entry will not be displayed on the page of the new account.

### :ballot_box_with_check: Display logged in user details and apply cookies like last login

In order to apply cookies and display the logged in user details you need to:
+ In `views.py` import the following
```
import datetime
from django.http import HttpResponseRedirect
from django.urls import reverse
```
+ In the `login_user` function, to track when the user last logged in we replace the code in the `if form.isvalid()` block with the following
```
...
if form.is_valid():
    user = form.get_user()
    login(request, user)
    response = HttpResponseRedirect(reverse("main:show_main"))
    response.set_cookie('last_login', str(datetime.datetime.now()))
    return response
...
```
+ In the `show_main` function, we add the to the `context` variable
```
context = {
    ...
    'last_login': request.COOKIES['last_login'],
}
```
+ Modify the `logout_user` function
```
def logout_user(request):
    logout(request)
    response = HttpResponseRedirect(reverse('main:login'))
    response.delete_cookie('last_login')
    return response
```
+ To display the last login data in `main.html` add the following
```
...
<h5>Last login session: {{ last_login }}</h5>
...
```

## :globe_with_meridians: The difference between `HttpResponseRedirect()` and `redirect()`

The main difference between `HttpResponseRedirect()` and `redirect()` is in their flexibility. `HttpResponseRedirect()` requires a URL as its first argument, meaning you can only redirect to a specific URL. On the other hand, `redirect()` is more versatile as it ultimately returns an `HttpResponseRedirect`, but it allows you to pass in a model, view name, or URL as its argument. This makes `redirect()` more convenient for various use cases.

## :desktop_computer: How the `Product` model is linked with `User`

The `Product` model is linked to the `User` model through a ForeignKey, where each `Product` belongs to a single `User`, but a user can have multiple products. The `on_delete=models.CASCADE` option ensures that if a user is deleted, their associated products are also removed. In the view, when a user creates a product, it's linked to them via `thrift_entries = Product.objects.filter(user=request.user)`Additionally, product entries are filtered by the logged-in user, ensuring users only see their own entries. This setup allows the application to track and display products on a per-user basis.


## :keyboard: The difference between authentication and authorization, what happens when a user logs in

Authentication is the process of verifying a user’s identity by checking their credentials, typically a username and password. When a user logs in, Django verifies these credentials through its built-in authentication system. If the details are correct, Django creates a session, allowing the user to stay logged in as they navigate through the site. Django implements authentication using the User model and authentication backends, with the default being the username-password system, though other methods like OAuth can be integrated.

Authorization determines what an authenticated user is allowed to do within the application. Once a user is logged in, Django uses permissions and groups to manage access control, ensuring users can only access resources or perform actions they’re permitted to. This is handled through checks like request.user.is_authenticated and permission classes for views. Django’s admin system, for example, uses these permissions to control which users can manage specific models or data.


## :cookie: How does Django remember logged-in users? Explain other uses of cookies and whether all cookies are safe to use.

Django remembers logged-in users by storing a session ID in a cookie on the user's browser. This session ID helps Django retrieve the user's session data from the server, allowing them to stay logged in as they navigate the site.

Cookies are also used for purposes like tracking user preferences or analytics, but not all cookies are safe. Sensitive data should never be stored directly in cookies, and security measures like HttpOnly, Secure, and SameSite should be applied to protect against attacks like XSS and CSRF.

</details>

<details>
<Summary><b>Assignment 5</b></summary>


### :ballot_box_with_check: Implement Functions to delete and edit products

In order to add the `edit_product` and `delete_product` functions
+ In `views.py` we add and import
```
from django.shortcuts import .., reverse
from django.http import .., HttpResponseRedirect
...
def edit_product(request, id):
    product = Product.objects.get(pk = id)

    form = ThriftEntryForm(request.POST or None, instance=product)

    if form.is_valid() and request.method == "POST":
        form.save()
        return HttpResponseRedirect(reverse('main:show_main'))

    context = {'form': form}
    return render(request, "edit_product.html", context)

def delete_product(request, id):
    product = Product.objects.get(pk = id)
    product.delete()
    return HttpResponseRedirect(reverse('main:show_main'))
```
+ In `urls.py` we add and import
```
from main.views import edit_product, delete_product
...
urlpatterns = [
    ...
    path('edit-product/<uuid:id>', edit_product, name='edit_product'),
    path('delete/<uuid:id>', delete_product, name='delete_product'),
]
```

### :ballot_box_with_check: Customize the design of the HTML templates that have been created in previous assignments using CSS
In the `base.html` file in `templates` of the root directory insert the following:
```
...
<head>
{% block meta %}
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1">
{% endblock meta %}
<script src="https://cdn.tailwindcss.com">
</script>
</head>
...
```

### :ballot_box_with_check: Customize the product list page to be more attractive and responsive

I modified the `main.html` file to look like the following:
```
{% extends 'base.html' %}
{% load static %}

{% block meta %}
<title>Thrifting Haven</title>
{% endblock meta %}
{% block content %}
{% include 'navbar.html' %}
<div class="overflow-x-hidden px-4 md:px-8 pb-8 pt-24 min-h-screen bg-yellow-950 flex flex-col"
     style="background-image: url('{% static 'image/background6.jpg' %}'); background-size: cover; background-position: center; background-repeat: no-repeat;">

  <div class="p-2 mb-6 relative">
    <div class="relative grid grid-cols-1 z-30 md:grid-cols-3 gap-8">

      {% include "card_info.html" with title='Name' value=name %}
      {% include "card_info.html" with title='Class' value=class %}
    </div>
</div>
    <div class="px-3 mb-4">
      <div class="flex rounded-md items-center bg-sky-950 py-2 px-4 w-fit">
        <h1 class="text-white text-center">Last Login: {{last_login}}</h1>
      </div>
    </div>
    <div class="flex justify-end mb-6">
        <a href="{% url 'main:create_product' %}" class="bg-sky-950 hover:bg-sky-700 text-white font-bold py-2 px-4 rounded-lg transition duration-300 ease-in-out transform hover:-translate-y-1 hover:scale-105">
            Add New Product Entry
        </a>
    </div>
    
    {% if not thrift_entries %}
    <div class="flex flex-col items-center justify-center min-h-[24rem] p-6">
        <img src="{% static 'image/very-sad.png' %}" alt="Sad face" class="w-32 h-32 mb-4"/>
        <p class="text-center text-gray-600 mt-4">There are no products in Thrifting Haven.</p>
    </div>
    {% else %}
    <div class="columns-1 sm:columns-2 lg:columns-3 gap-6 space-y-6 w-full">
        {% for thrift_entry in thrift_entries %}
            {% include 'card_product.html' with thrift_entry=thrift_entry %}
        {% endfor %}
    </div>
    {% endif %}
</div>
{% endblock content %}
```
### :ballot_box_with_check: The product list page will display details of each product using cards, for each product card, create two buttons to edit and delete the product on that card
In `card_product.html` I insert the following:
```
<div class="relative break-inside-avoid">
    <!-- Floating items on top -->
    <div class="absolute top-2 z-10 left-1/2 -translate-x-1/2 flex items-center -space-x-2">
        <div class="w-[3rem] h-8 bg-gray-200 rounded-md opacity-80 -rotate-90"></div>
        <div class="w-[3rem] h-8 bg-gray-200 rounded-md opacity-80 -rotate-90"></div>
    </div>
    
    <!-- Main Product Card -->
    <div class="relative top-5 bg-blue-100 shadow-md rounded-lg mb-6 break-inside-avoid flex flex-col border-2 border-blue-300 transform rotate-1 hover:rotate-0 transition-transform duration-300">
        <div class="bg-blue-200 text-gray-800 p-4 rounded-t-lg border-b-2 border-blue-300">
            <h3 class="font-bold text-xl mb-2">{{ thrift_entry.name }}</h3>
            <p class="text-gray-600">{{ thrift_entry.description }}</p>
        </div>
        
        <!-- Product Details -->
        <div class="p-4">
            <p class="font-semibold text-lg mb-2">Condition</p>
            <p class="text-gray-700 mb-2">
                <span class="bg-[linear-gradient(to_bottom,transparent_0%,transparent_calc(100%_-_1px),#CDC1FF_calc(100%_-_1px))] bg-[length:100%_1.5rem] pb-1">{{ thrift_entry.condition }}</span>
            </p>

            <!-- Price Section with Actual Price and Dollar Sign -->
            <div class="mt-4">
                <p class="text-gray-700 font-semibold mb-2">Price</p>
                <div class="relative pt-1">
                    <div class="flex mb-2 items-center justify-between">
                        <div>
                            <!-- Display actual price with dollar sign -->
                            <span class="text-xl font-semibold inline-block py-1 px-2 uppercase rounded-full text-green-600 bg-green-200">
                                ${{ thrift_entry.price }}
                            </span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Action Buttons: Edit and Delete -->
    <div class="absolute top-0 -right-4 flex space-x-1">
        <!-- Edit Button -->
        <a href="{% url 'main:edit_product' thrift_entry.pk %}" class="bg-yellow-500 hover:bg-yellow-600 text-white rounded-full p-2 transition duration-300 shadow-md">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-9 w-9" viewBox="0 0 20 20" fill="currentColor">
                <path d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zM11.379 5.793L3 14.172V17h2.828l8.38-8.379-2.83-2.828z" />
            </svg>
        </a>
        <!-- Delete Button -->
        <a href="{% url 'main:delete_product' thrift_entry.pk %}" class="bg-red-500 hover:bg-red-600 text-white rounded-full p-2 transition duration-300 shadow-md">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-9 w-9" viewBox="0 0 20 20" fill="currentColor">
                <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
            </svg>
        </a>
    </div>
</div>
```

### :ballot_box_with_check: Create a navigation bar (navbar) for the features in the application that is responsive to different device sizes
In the root directory, in`templates` insert the `navbar.html` as the following:
```
<nav class="bg-sky-950 shadow-lg fixed top-0 left-0 z-40 w-screen">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">
        <div class="flex items-center">
          <h1 class="text-2xl font-bold text-center text-white">Thrifting Haven</h1>
        </div>
        <div class="hidden md:flex items-center">
          {% if user.is_authenticated %}
            <span class="text-gray-300 mr-4">Welcome, {{ user.username }}</span>
            <a href="{% url 'main:logout' %}" class="text-center bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded transition duration-300">
              Logout
            </a>
          {% else %}
            <a href="{% url 'main:login' %}" class="text-center bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded transition duration-300 mr-2">
              Login
            </a>
            <a href="{% url 'main:register' %}" class="text-center bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded transition duration-300">
              Register
            </a>
          {% endif %}
        </div>
        <div class="md:hidden flex items-center">
          <button class="mobile-menu-button">
            <svg class="w-6 h-6 text-white" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
              <path d="M4 6h16M4 12h16M4 18h16"></path>
            </svg>
          </button>
        </div>
      </div>
    </div>
    <!-- Mobile menu -->
    <div class="mobile-menu hidden md:hidden  px-4 w-full md:max-w-full">
      <div class="pt-2 pb-3 space-y-1 mx-auto">
        {% if user.is_authenticated %}
          <span class="block text-gray-300 px-3 py-2">Welcome, {{ user.username }}</span>
          <a href="{% url 'main:logout' %}" class="block text-center bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded transition duration-300">
            Logout
          </a>
        {% else %}
          <a href="{% url 'main:login' %}" class="block text-center bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded transition duration-300 mb-2">
            Login
          </a>
          <a href="{% url 'main:register' %}" class="block text-center bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded transition duration-300">
            Register
          </a>
        {% endif %}
      </div>
    </div>
    <script>
      const btn = document.querySelector("button.mobile-menu-button");
      const menu = document.querySelector(".mobile-menu");
    
      btn.addEventListener("click", () => {
        menu.classList.toggle("hidden");
      });
    </script>
  </nav>
  ```

## :arrows_clockwise: The priority order of these CSS selectors if there are multiple CSS selectors for an HTML element

In CSS, the priority order of selectors is based on specificity. Inline styles have the highest precedence, followed by ID selectors, then class, attribute, and pseudo-class selectors, and finally, type selectors. If selectors have the same specificity, the last one in the CSS file takes precedence, overriding earlier rules.

## :twisted_rightwards_arrows: Why responsive design becomes an important concept in web application development

Responsive design is crucial in web development as it ensures websites adapt to various screen sizes and devices, providing a better user experience. Applications like YouTube and Airbnb effectively use responsive design, making their sites user-friendly on mobile and desktop. In contrast, the AREN website lacks responsiveness, leading to poor usability on mobile devices.

## :signal_strength: The differences between margin, border, and padding, and how to implement these three things

In CSS, margin, border, and padding are different properties that define the spacing and structure around an element. Margin creates space outside the element's border, separating it from other elements. Border is the outline around the element's content, while padding adds space inside the border, between the content and the border.

## :vibration_mode: The concepts of flex box and grid layout along with their uses

Flexbox and grid layout are two powerful CSS layout systems. Flexbox is a one-dimensional layout tool used for aligning items in rows or columns, making it ideal for smaller layouts. Grid layout, on the other hand, is a two-dimensional system that enables the arrangement of items in rows and columns, making it more suited for complex layouts like web pages with multiple sections or areas.


</details>