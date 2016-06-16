---
layout: post
title: "Flask Cheatsheet"
comments: true
description: "Cheatsheet for Flask"
keywords: "python, flask, cheatsheet"
---

### Installation

    $ pip install Flask

### Hello World
    # myapp.py
    from flask import Flask
    app = Flask(__name__)

    @app.route(‘/’)
    def hello_world():
        return ‘Hello World’
    if __name__ == ‘__main__’:
        app.run(debug=True)

### URL Routing

    @app.route(‘/foo/<name>/<int:age>’)
    def view(name, age):
        return ‘%s is %d years old’ % (
            name, age
        )  

### Template Rendering

    from flask import render_template

    return render_template(
        ‘foo.html’,
        var1=value1, var2=value2, ...
        )

### Flask for Django users

| Action | Django | Flask |
|---|---|---|
| Retrieve query params (“GET data”) | request.GET request.GET[‘name’] | request.args request.args[‘name’] |
| Retrieve form params (“POST data”) | request.POST request.POST[‘first_name’] | request.form request.form[‘name’] |
| Checking request type | request.method | request.method |
| Retrieve cookie value | request.COOKIES | request.cookies |
| Set a cookie | response.set_cookie(key, value, ...) | response.set_cookie(key, value, ...) |
| Sessions | request.session[‘foo’] | session[‘foo’] |
|Access settings | from django.conf import settings settings.my_name| app.config app.config[‘my_name’]|

### Useful functionality

| From flask import.. | This is a... | usage |
|---|---|---|
| Flask | Flask application object | app = Flask(__name__) |
| request | Thread-local request object | request.args[‘test’] request.form[‘name’] |
| session | Thread-local session object | session[‘name’] = ‘value’ |
| url_for | Builds URLs based on route names | url_for(‘blog’, id=45, slug=‘hi’) |
| redirect | Generates a redirect response | return redirect(‘/hello’) |

### Basic App Layout
Commands:

    mkdir templates
    mkdir static

    touch templates/index.html
    touch static/base.css
    touch my_app.py

Structure:

    my_app.py
    static/
        logo.png
        base.css
    templates/
        blog_post.html
        index.html

###  Package App Layout

Commands:

    mkdir ~/my_app
    mkdir ~/my_app/templates
    mkdir ~/my_app/static  

    cd my_app
    touch __init__.py
    touch application.py
    touch models.py
    touch static/base.css
    touch templates/index.html

Structure:

    my_app/
        __init__.py
        application.py
        models.py
        static/
            logo.png
            base.css
        templates/
            blog_post.html
            index.html

### Large applications structure
[Link](https://www.digitalocean.com/community/tutorials/how-to-structure-large-flask-applications)

Commands:

    mkdir ~/LargeApp
    mkdir ~/LargeApp/app
    mkdir ~/LargeApp/app/templates
    mkdir ~/LargeApp/app/static  

    cd ~/LargeApp
    virtualenv env
    touch ~/LargeApp/run.py
    touch ~/LargeApp/config.py
    touch ~/LargeApp/app/__init__.py

Structure:

    ~/LargeApp
        |-- run.py
        |-- config.py
        |__ /env             # Virtual Environment
        |__ /app             # Our Application Module
             |-- __init__.py
             |-- /module_one
                 |-- __init__.py
                 |-- controllers.py
                 |-- models.py                
             |__ /templates
                 |__ /module_one
                     |-- hello.html
             |__ /static
             |__ ..
             |__ .
        |__ ..
        |__ .

### More Info

* [http://flask.pocoo.org](http://flask.pocoo.org) (main site & docs)
* [http://flask.pocoo.org/docs/quickstart](http://flask.pocoo.org/docs/quickstart)
* [http://github.com/mitsuhiko/flask](http://github.com/mitsuhiko/flask)

* Links to Flask Modules guide: Click [here](https://github.com/akul08/flask-guide/)
