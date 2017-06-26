# Django Style Guide
This guide gives standarad rules to follow while writting code for any major django project, any microservice or any script written in django or python.

## Table of Contents
* [Coding Style](#coding-style)
	* [Indentation](#indentation)
	* [Whitespaces](#whitespaces)
	* [Code Structure](#code-structure)
	* [Naming Convention](#naming-convention)
	* [Imports](#imports)
	* [Module](#module)
	* [Class](#class)
	* [Function](#function)
	* [String](#string)
	* [Statments](#statments)
	* [Comments](#comments)
	* [Exceptions](#exceptions)
* [File](#file)
	* [Format](#format)
* [Django](#django)
	* [General](#general)
	* [Django project Structure](#django-project-structure)
	* [Model](#model)
	* [Template](#template)
	* [APIException](#apiexception)

## Coding Style
### Indentation
* Use **4 spaces as indentation**.
* Maximum **columns/character per line** number must be **120**.
* Maximum parameter in one line must be 3. If parameter exced are more the 3, align then on next line, below the first open delimiter.

Good
```python
def func( param1, param2, param3,
		param4, param5
):
```
Bad
```python
def func(param1, param2, param3, param4, param5):
```
* When objects are seprated by operator use line break after the last leading operator. Maximum number of parameter in one rule also applies here.

Good
```python
z = a + b + c + \
	d + e + f
```
Bad
```python
z = a + b + c + d + e + f
```
* Any root element in a module must be seprated by 2 line break from its previous element.
```python
'''
	This is example module comment
'''
# first line break(/n)
# second line break(/n)
class SomeClass():
	pass
# first line break(/n)
# second line break(/n)
def module_func():
	pass
```
* Sub element in a class must be seprated by 1 line break from its previous element.
```python
class SomeClass():
# one line break(/n)
def func1():
	pass
# one line break(/n)
def func2():
	pass
```
### Whitespaces
* There must me at most 1 white space after (not before) every comma, colon and semi colon:

Good
```python
some_list = [1, 2, 3, 4]
some_dictionary = {
	'key1': 'value1',
	'key2': 'value2',
}
if x == 4: print x, y; x, y = y, x
```
Bad
```python
some_list = [1,2,3,4]
some_dictionary = {
	'key1':'value1',
	'key2':'value2',
}
if x == 4 : print x , y ; x , y = y , x
```
* Always use 2 white spaces one before and one after of every operator (= , + , - , * , **)

Good
```python
	a = 1 + 2
```
Bad
```python
	a=1+2
```
### Code Structure
* Every module (file) must follow the following coding structure in order, (module comment, imports, module variables, module functions, module classes).
```python
'''
	This is an optional moudle level comment describing general purpose of these module 
'''
import os
import sys
from uuid import UUID


__all__ = ['some_func', "SomeClass"]

CONSTANT_1 = "constant value"


def some_func():
	'''
		function level comment describing purpose of function
		Describe parameter accepted
		Describe return value 
	'''
	pass


class SomeClass():
	'''
		Class level comment descibing purpose of class
		Paremter accepted in init
	'''
	pass

```
* Every file must end with a single newline. Don't include multiple newlines at the end of a file.

###  Naming Convention
* All variables and functions names must follow **lower_case_with_underscores** naming convention

Good
```python
total_student_count = 100
``` 

Bad
```python
totalStudentCount = 100
totalstudentcount = 100
total_studentcount = 100
```
* Class name must follow CamelCase.

Good
```python
class SomeClass():
	pass
```
Bad
```python
class some_class():
	pass
class someclass():
	pass
```
* Never use short forms for variable name. Always write variable with sensiable full english word and the name must denote purpose of the varaible.

Good
```python
user_age = 10
response = request.json()
```
Bad
```python
user_a = 10
resp = req.json()
```
### Imports
* Imports should be the first line in a moudle (file) after the optional module comment.
* Each import must be on different line.

Good
```python
import os
import sys
```
Bad
```python
import os, sys
```
* Imports of sub modules/element of a single module can come on same line.
```python
from PIL import Image, ImageColor
```
* Imports from same moudle must be relative and not absolute.

Good
```python
from .views import MyView
```
Bad
```python
from myapp.views import MyView
```
* Wild card import is allowed. If it is needed to import all the elements form the module, the accpeted way is to import the module and then use the module to access each element.

Good
```python
from someapp import serializer

serializer1 = serializer.Serializer1()
serializer2 = serializer.Serializer2()
```
Bad
```python
from someapp import *

serializer1 = Serializer1()
serializer2 = Serializer2()
```
* All imports must follow the following order with one line break in between (Python library, Third party python library, Django, Third party django library, other apps in the project, relative imports of app module).

```python
import os   
import sys  # python libray

import PIL
import geopie  # python third party libray

import django.views
import django.conf.settings  # django import

import rest_framework.views
from rest_framework.response import Response   # django library 1

import allauth
import allauth.User  # django library 2

import somemoduel.utils  # other apps

from .views import myview  # same apps
```
### Module
* All module level variables (global variables) must be place after imports.
* Each module must have a "**\_\_all\_\_**" varaible describing all the public access varaible, method and classes
* Every non public element in the module must begain with **"_"**.
```python
'''
	This Example module show example for all the above rules
'''
import os

__all__ = [
	'public_variable', 'add_something', 'Calculator'
]   # This variable must expose all public variable 

CONSTANT_ABC = "ABC"

public_variable = "public info"
_private_variable = "some secret"  # private variable must began with underscore ("_")

def _util_func():  # private variable must began with underscore ("_")
	pass


def add_something():
	pass


class PrivateClass():  # private class not included in __all__
	pass


class Calculator():
	pass

```

* Every public element in the module must be named accrounding to usage not according to its implemetation.

Good
```python
def get_user_count():
	pass
```
Bad
```python
def sort_activity_and_get_user_count():
	pass
```
### Class
* Class name must follow CamelCase notation eg (SomeClass)
* Non public method of class must begain with underscore "\_".
* Public method of class must follow lower_cases_underscore notation. Naming of methods must indicate usage instead of implementation
```python
class Calculator():
	
	def _check_if_divisble(self, *args, **kwargs):  # private method
		pass

	def is_prime(self, *args, **kwargs):  # public method
		pass
.
```
* If in doubt whethere a method is pulbic or private, always make the method private.
* always use **"self"** as first argument name for instance level methods and **"cls"** for class level methods.

### Function
* Non public method must begain with underscore "_" and public method follow lower_case_underscore case.
* Each method name must indicate its usage instead of implementation.
* Always user **(\*args, \*\*kwargs)** as default parameter for a function, this will make the function future compatible.
* Use a single empty line to break between statements to break up methods into logical paragraphs internally.
```python
def transformorize_car:
	car = manufacture(options)
	t = transformer(robot, disguise)

	car.after_market_mod()
	t.transform(car)
	car.assign_cool_name()

	fleet.add(car)
```

### String
* Always use single quotes for single lined string and tripel quotes for multile level string. Exception for the rule is when a single line string contains single quote in it.
* Use **startswith()** and **endswith()** instead of indexes for searching start or end of string.

Good
```python
	string = "zayastring"
	is_zaya_in_string = string.startswith("zaya")
```
Bad
```python
	string = "zayastring"
	is_zaya_in_string = string[:4] == "zaya"
```
* Use **format()** instead of **%** for formating string.

Good
```python
	url = "{server}/{api}".format(server="https://example.com", "get/users/")
```
Bad
```python
	url = "%s/%s" % ("https://example.com", "get/users/")
```

### Statments
* If condition in single line is not allowed. One liner if condition are allowed in list comprehensions.

Good
```python
if user.is_admin is True:
	user.get_cookie()

admin_list = [ user for user in userlist if user.is_admin is True]
```
Bad
```python
user.get_cookie() if user.is_admin is True
```
* Always use **is** operator while comparing **True**, **False** and **None**

Good
```python
if user.is_admin is True:
	pass
```
Bad
```python
if user.is_admin:
	pass

if user.is_admin == True:
	pass
```
* Never use a boolean condition without compreative operator.

Good
```python
if is_authenticated is True:
	pass
```
Bad
```python
if is_authenticated:
	pass	
```
* **not** operator must come with operator and not before or after the boolean condition

Good
```python
	if user.is_authenticated is not True:
		pass
```
Bad
```python
	if not user.is_authenticated is True:
		pass
```
* Always use **get()** for reading value from a dictionary with default value, instead of direct index.

Good
```python
	username = user.get("username", None)
```
Bad
```python
	username = user.get("username")
	username = user["username"]
```
* Always use **isinstance()** instead of **type()** for type check of variable

Good
```python
	is_list = isinstance(var, list)
```
Bad
```python
	is_list = (type(var) == type(list))
```
* Context manager should be invoke with function and not with variable
Good
```python
with open("file.txt") as file:
	pass
```
Bad
```python
file = open("file.txt")
with file:
	pass
```

### Comments
* Moudle level comment must be multile line and must be the first line in the file.
* Comments should only be english, unless you are 140% persent sure.
* Never use we, i, us in comment. Comments must be a set of instructions and not procedure.
* Whenever code is change make sure to change to code.
* Each class and function must have a block comment below its name describing what the class and function is doing.
* Paragraph inside the block level comment must be seprated by a line.
* Inline comment must come on same line and must be seprated by min 2 spaces, if single line comment exceds max charachter limit in a single convert inline comment to single line comment.

### Exceptions
* Always be specific about exception in catch expression never catch the super class Exception.

Good
```python
try:
	# some statment
catch KeyError, AttributeError:
	# error handling
else:
	# default error handling
```
Bad
```python
try:
	# some statment
catch Exception:
	# error handling
```
* And else clause must always follow the catch clause and default error handling must be implemented

Good
```python
try:
	# some statment
catch keyError, AttributeError:
	# error handling
else:
	# default error handling
```
Bad
```python
try:
	# some statment
catch KeyError, AttributeError:
	# error handling
```
* Always derive new exception form Exception class instead of BaseException
* Derived exception class must have the following naming format "<TypeOfError>Exception".


## File
### Format
* Every file must be saved with **UTF-8** encoding. Use "\\" escapes to specify non-ascii literals.

## Django
### General
* Meta class must always apper last element in the class

Good
```python
class MyModel(models.Model):
	some_filed = models.IntegerField()

	def __str__(self):
		pass

	def custom_function(self):
		pass

	class Meta:
		verbose_name = "mymodles"
```
Bad
```python
class MyModel(models.Model):
	some_filed = models.IntegerField()

	class Meta:
		verbose_name = "mymodles"

	def __str__(self):
		pass

	def custom_function(self):
		pass
```
### Django project Structure
* Each app must be independent and plugable apps with its own functionally.
* Project must contains a settings folder with three settings in it **local.py**, **prod.py**, **staging.py** and a **sample.local.py**. Only sample.local.py must be push to remote repository with no secret keys in it.
* Each independent app in the project must have its own urls.py and all the apps urls must be included inside th 

### Model
* Model fields must also follow standard naming convenction (lowercase_underscore).
* **ChoiceField** must have its indivisual entries defined as class constant varaibles.

Good
```python
class Superhero(models.Model):
	FLY, WALK, TELEPORT = "fly", "walk", "teleport"
	commutation = models.ChoiceField(
				(FLY, "Fly"),
				(WALK, "Walk"),
				(TELEPORT, "Teleport")
			)
```
Bad
```python
class Superhero(models.Model):
	commutation = models.ChoiceField(
			("fly", "Fly"),
			("walk", "Walk"),
			("teleport", "Teleport")
		)
```
* When use any realted field for model always use string to specify the model which is realted to instead of specifing the class.

Good
```python
class MyModel(models.Model):
	user = models.ForeignKey("auth.models.User")
```
Bad
```python
from auth.models import User

class MyModel(models.Model):
	user = models.ForeignKey(User)
```

### Template
* Template varaible must have a leading and trailing whitespaces inside the clury parentheses.

Good
```html
	<h1>Welcome {{ user.username }} </h1>
```
Bad
```html
	<h1>Welcome {{user.username}}</h1>
```

### APIException
* Errors in request must be handel by rest exception or any sub class of rest exception. Never use custom response to indicate error.

Good
```python
from rest_framework import status, views
from rest_framework.exceptions import APIException

class InvalidPrimaryKeyException(APIException):
	'''
		Custom Rest exception to denote invalid primary key error in the Api.
	'''
    status_code = status.HTTP_400_BAD_REQUEST
    default_detail = ('Invalid pk {pk} for model {model}.')
    default_code = 'invalid_pk'

    def __init__(self, pk="", model="", detail=None, code=None):
        if detail is None:
            detail = self.default_detail.format(pk=pk, model=model)
        super(InvalidPrimaryKeyException, self).__init__(detail, code)

class SomeView(views.APIView):
	param_user_id = "user_id"
	
	def get(self, request, *args, **kwargs):
		user_id = request.query_param.get(self.param_user_name, None)
		try:
			user = User.objects.get(id = user_id)
		catch User.DoesNotExist:
			raise InvalidPrimaryKeyException(pk = user_id, model = "User")  # Custom rest exception
```
Bad
```python
from rest_framework import views, status
from rest_framework.response import Response

class SomeView(views.APIView):
	param_user_id = "user_id"

	def get(self, request, *args, **kwargs):
		user_id = request.query_param.get(self.param_user_id, None)
		try:
			user = User.objects.get(id = user_id)
		catch User.DoesNotExist:
			return Respone("Invalid pk " + user_id + " for model User.", status = status.HTTP_400_BAD_REQUEST)  # Bad direct response
```
