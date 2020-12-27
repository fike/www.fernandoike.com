+++
title = "Testing with Flask send cookie with value correctly"
date = 2020-12-26T10:46:46-03:00
draft = true
description = "It's an example how to test if Flask server set cookie in the HTTP response."
categories = ["flask", "pytest", "python"]
tags = ["flask", "pytest", "python"]
+++
I have used [Flask tutorial code](https://flask.palletsprojects.com/en/1.1.x/tutorial/) to improve my programming skills, I changed a few things that of it as part of my learning path. The repo with Flask tutorial modified is [here](https://github.com/fike/flask-tutorial).

I implemented in the profile page an option to choose what's the color of the top banner for all pages when a user is logged. After a user logged, Flask will create a cookie with the color banner if browser users don't have it, read it and write response HTML in which the color banner in the user profile was saved.

It seems like the picture below:

![Flask image with the banner color different than site](/images/flask_banner.png)

I thought that copy/paste here the Flask tutorial is bad, because I'll have to explain more than I planned about changes of original code. So, I created another repo on Github that have a Flask project more simple. Basically, when receiving an HTTP Request from a browser, Flask will response it a random background color as part of text like the screenshot below:

![Flask project image with a random background color](/images/flask_cookie_2.png)

I whished to test if the cookie is created correctly, but I tried to use as few as possible external libraries and methods of Flask and Python. This means that don't use Python [requests](https://github.com/psf/requests), for example. I think there is a way to extract cookies using only [FlaskClient](https://flask.palletsprojects.com/en/1.1.x/api/#flask.testing.FlaskClient), but I didn't find it (I guest I didn't understand how to do that). I used regex to extract value from the cookie, although could be used a list comprehension, it's an elegant solution. 😉

Below is Flask app.py code, up to date code can found [here](https://github.com/fike/flask-pytest-cookie).

{{< gist fike 900141281182ce06441dc4b7a7d1f714 "app.py" >}}

This code creates a new cookie session called **color**, the value is written base on a random color list. If a color cookie exists, Flask reads the color cookie and writes a "span class" based CSS file.

{{< gist fike 900141281182ce06441dc4b7a7d1f714 "style.css" >}}

The test catches the Set-Cookie header and parses the color cookie value compare to the color list supported.

{{< gist fike 900141281182ce06441dc4b7a7d1f714 "test_app.py" >}}

Do you have a better way to test a cookie value using FlaskClient? Please, write in the comments.

Ouch, I almost forgot to mention an important thing. My Flask tutorial version implemented the cookie creation after the a user do the site logon, you can find the respective test [here](https://github.com/fike/flask-tutorial/blob/master/tests/test_auth.py#L107).
