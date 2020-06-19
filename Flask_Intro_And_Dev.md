# Flask Development

## Before Start

 As I am writing this in markdown file, there's no color asscociated with the words. 

 I would be using ⚠️WARNING⚠️, 🔴IMPORTANT❗🔴 or 🔥NEW🔥 to add color to the tutorial.


### Author: Andy Wu

Special Thanks to Peng Xiao, Stackoverflow, etc.

## What is Flask?

Flask is a micro framework. 

Django: web framework, loads of work

Even though Django is “more powerful” than Django, there are still many extensions for Flask to work things out.


## Hello World Deployment, routing, and port

### Basic Deployment

Deploy with virtualenv

Steps:

```
mkdir myproject
cd myproject
python3 -m venv venv


```

### Hello World Deployment

Code for hello world:

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```

### 

An easy example code:
```
'''
Andy's Example template for Flask 1.0.0.
Covers short examples and basic stuff. For really quick references.
For SQL interactions, please look at the other pages.
Content interaction:
1. Basic Flask Templates
2. Setting up directories, hierarchy and stuff
3. Setting up useful pages
'''

'''
1.
The key is really easy: Just Set up the basic templates.
The templates can be listed below:

from flask import Flask
app = Flask(__name__)

@app.route('/')  #🔴IMPORTANT❗🔴 the route here specifies the directory.
def hello_world(): #🔴IMPORTANT❗🔴 the hello world here specifies the function called when you access the directory.
    return 'Hello, World!'
'''

# We have to import flask from Flask to have flask. For requests, import flask form requests.
from flask import Flask, request, render_template

#Just initialize the thing like this. Remember there are several(two)
app = Flask(__name__)

#Specifies the route of the content.
@app.route('/')
#What the route would run afterwards
#Special: This page contains something that is rendered.
def welcome():
    return render_template("index.html")


#Similar stuff: for referencing
@app.route('/apps')
def welcome_root():
    return 'Hello World'

@app.route('/requests',methods=['GET'])
def welcome_get_post():
    if request.method == 'POST':
        return "You've used a POST request!"
    else:
        return "I reckon you've probably using a GET request!"

#For opening ports. You probably don't want to use the same port every time.
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5001)
else:
    app.run()
```

## Flask Folder  Hierachy

Flask folders have a specific hierachy system (which is required if you want to make your website optimal).
Here is the actual folder hierachy system:

1) For HTML files, put them in /project/template

2) For CSS files, put them in /project/static

## On Templates

### Intro to Templates

For example, you have the following thing in HTML:

```
<h1>Hello, {{ name.username }}</h1>
```

Then, we try to put the following in the app.py file:

```
from flask import Flask
from flask import render_template   

app = Flask(__name__)

@app.route('/')
def hello():
    name = {'username': 'root'}
    return render_template('index.html', name=name, title='flask')

if __name__ == "__main__"
    app.run(host='0,0,0,0')
```

This would yield the value of name.username.

### if and for in Templates

We can also use if and for in templates.

For if, here is an example:

```
{% if title %}
<title>welcome to {{title}}</title>
{% else %}
<title>welcome to python</title>
```

and we make some changes in the function below @app.route:
```
return render_template('index.html',name=name,   title='flask')
```
If we keep the "title='flask', the title would be welcome to flask.

However, if we simply remove thou "title='flask'", the title would be welcome to python.

We can also construct for loops in Templates.

Here is an example:

```
<table border="1">
    <thead>
        <tr>
            <th>Name</th>
            <th>Age</th>
        </tr>
    </thead>
    <tbody>
    {% for row in rows %}
    <tr>
        <td>{{row.name}}</td>
        <td>{{row.age}}</td>
    </tr>
    {% endfor %}
    </tbody>
</table>
```

With this, we can put something inside the app.py file:

```
rows = [{'name': 'Python', 'age':27},{'name': 'Python', 'age': 27}]
```
Which would create a neat row to display stuff.

### Template Inheritance

Template Inheritance helps us in keeping features relevant and not redundant.

Similarly, you have to do this:

```
{ % extends "base.html" % }
```

(This should be added in the children HTML file.)

```
{% block content %} {% endblock %}
```

(This should be added in the parent HTML file.)

## Flask and Forms


