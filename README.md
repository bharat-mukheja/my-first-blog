TwentyForSeven
============

A simple and easy-to-understand blogging application.

[What is a blog](https://en.wikipedia.org/wiki/Blog)?

###Features of this application:###

  * Very easy to understand
  * Elegant Looking
  * Minimalistic cluttering
  * Separate drafting and publishing


How to Use
-------------

1. Click on a blog post to read open it in full page
2. Use pallette on top right to create a new blog post or modify an existing while on the post page
3. Use publish button below the post to publish a draft
4. Use the admin panel <ip-address>/admin to log in and make changes to publishing.
>(Note that when you create a blog it is saved as a draft first, and is not visible to a user unless he is logged in. To make it public, publish it, and the steps of modification of blog(including creating a new one) can only be done by a logged in user)


How to setup on server
-------------

    $ git clone https://github.com/bmukheja/my-first-blog.git


Download the source onto a webserver preferably running Apache 2(as it's been tested on the same).


###Create a Database###

    $ python manage.py migrate

Since this is a python based code, you need WSGI to make apache server run it without using Django server.

###Using WSGI

    $ vi /var/www/<wsgi_file_name>_wsgi.py

Paste the following content into the file. You can write your own wsgi code too, but since its just a few lines it would boil down to the same only.

    import os
    import sys

    path = '/home/<your server username>/my-first-blog'  # use your own Server username here
    if path not in sys.path:
    sys.path.append(path)

    os.environ['DJANGO_SETTINGS_MODULE'] = 'mysite.settings'

    from django.core.wsgi import get_wsgi_application
    from django.contrib.staticfiles.handlers import StaticFilesHandler
    application = StaticFilesHandler(get_wsgi_application())

This file's job is to tell the Apache server where our web app lives and what the Django settings file's name is.

The StaticFilesHandler is for dealing with our CSS. This is taken care of automatically for you during local development by the runserver command. We'll find out a bit more about static files later in the tutorial, when we edit the CSS for our site.

Hit Save and then go back to the shell.

Now restart the Apache server, and see if the website is working at the root of the IP address.


###Debugging Tips

* If there is an error of dependencies, go to the location where file 'requirements.txt' is and run the following command -

        pip install -r requirements.txt

* Check mistakes in the WSGI configuration file, specifically check for path errors.
* If not solved, contact me on my email bharat.mukheja@gmail.com
