# About the Flesch-Kincaid Grade Level API

This is a very simple REST API that accepts a piece of text from the user and returns 
the Flesch-Kincaid (F-K) grade level of the text. The user enters the text in the box 
provided by the web application and clicks on the **Submit text** button to receive the 
F-K grade level. It consists of only one endpoint and one POST method, it constitutes 
a Python3 Flask application with HTML renderings and was written in Ubuntu Linux 18.04.

The API is based on a working example found in the book **Python Machine Learning**, 
by Sebastian Raschka, in Chapter 9 **Embedding a Machine Learning Model into a Web Application**. 
It is currently hosted on [PythonAnywhere](http://kosgian82.pythonanywhere.com), 
but it can be also downloaded through this repository and be run locally. Raschka's example 
is about creating a web application of a binary classifier for movie reviews and I have used 
parts of the code for creating this application in a similar fashion.

I have also tried to adhere my Python code to PEP8 standards as much as possible, such as 
separate lines for each import, imports ordered alphabetically, two empty lines between 
functions' or classes' declarations, no more than 100 characters per line etc.


## Installation

This README.md assumes that the user has Python3 installed on their machine. To install 
Python3 from scratch, follow the reccommended online instructions on 
[Python installation](https://realpython.com/installing-python/) 
or any other online resource you may find useful.

Other libraries needed to run this API (preferably within a virtual environment):

* Python3 Flask

```
$ pip3 install flask
```
* py-readability-metrics

```
$ pip3 install py-readability-metrics
$ python3 -m nltk.downloader punkt
```
* The WTForms library

```
$ pip3 install wtforms
```

To clone this repository, run the following command on Git Bash or on a Linux terminal from 
inside the directory you want this repository to be cloned:

```
$ git clone git@github.com:KosGian82/flesch-kincaid-grade-level-api.git
```

If done correctly, the directory tree should look like this:

```
~/flesch-kincaid-grade-level-api$ tree
.
├── flask_app.py
├── README.md
├── static
│   └── style.css
└── templates
    ├── _formhelpers.html
    ├── results.html
    └── text_readability.html

2 directories, 6 files
```
* `flask_app.py` is the main Python code that includes the Flask application of the API, 
as well as the readability metrics function for calculating F-K. 

* `static` contains just a very simple Cascading Style Sheets (file) `style.css`for modifying 
the look and displays of the HTML documents if we want to. 

* `templates` contains `_formhelpers.html`, a generic macro based on Jinja2 templating engine 
for rendering text fields in HTML files, `text_readability.html`, the starting page of the 
API and `results.html`, which displays the results after clicking on the **Submit text** button, 
i.e. the text entered by the user and the F-K grade level.


## Running the API locally

To run the API on your local machine, start Python from a command prompt on Windows, 
or a terminal in Linux or Mac, and from the top level directory of the repository run:

```
$ python3 flask_app.py
```

The output of the command should look like this

```
 * Serving Flask app "flask_app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

Copy and paste `http://127.0.0.1:5000/`on your web browser, or right-click on the URL. 
Then, enter a piece of text (100 words or longer) in the box provided by the web page and 
finally, click on **Submit text** button. The `/results` page should display the text you 
entered and the F-K grade level of the text (or an error message if your text was shorter 
than 100 words).


## Deploying the API to a public server

I have already deployed this API to **PythonAnywhere** web hosting service and can be 
accessed from [here](http://kosgian82.pythonanywhere.com). I followed Raschka's example 
in the same chapter, where he suggests this hosting service, as it allows free accounts 
with limited use and the process is fairly simple for beginners.

Here are some rather detailed instructions:

1. Go to *https://www.pyhtonanywhere.com*
2. Create a beginner account from the *Pricing & signup* link on the top-right corner
3. Access the control panel of your account through the *Dashboard* 
4. Click on the  *Web* tab and then *Add a new web app*
5. Follow the wizard for creating a Flask web application
6. Click on the *Files* tab and upload the repository files under `/home/<username>/mysite/`
7. On the *Web* tab click on *Reload <username>.pythonanywhere.com*
8. If all done correctly, the API should be up and running at `<username>.pythonanywhere.com`

This is just a general set of instructions. In practice, some debugging might be needed, like 
I had to do for this API, or even installations of some prerequisite libraries on the web interface. 
In any case, consult your error logs for more information.

## Improving the API

As mentioned from the very beginning, this is a very basic API with very limited use. 
There are several ways to imrpove and expand it:

* First of all, it is open to anyone, which makes it unsafe if it is meant to be used 
for more important tasks. A more secure RESTful API would require a user to submit 
their authentication information with every request they send, by using something like 
the *Flask-HTTPAuth* Flask extension. Such an authentication request should be stateless, 
according to RESTful architectures, and the API should  not save the user's data generated 
in one session for use in another session with the same or another user.

* The API could possibly benefit from more RESTful features, such as: 
1. Enabling transfer of data via *JSON* if possible
2. Use of common error HTTP codes for not found, forbidden, bad request etc.
3. Sending requests with `curl`
4. Use of versioning in the URL to allow development on newer versions whilst still running older ones
5. Use of caching so that we do not have to query for data all the time
6. Use of nouns in endpoints instead of verbs and consistent paths of endpoints

* At the moment, the API supports only one method POST, for requests to create new resources, 
however it does not store any information. A more complete API would probably have a 
database too, such as *SQLite*, where users would be able to retrieve data with a GET 
method, update with PUT, or remove data with DELETE methods. For example, some *SQLite* 
database would be able to store all the pieces of text someone posts with F-K scores and 
other readability statistics if we wished.

* The F-K calculation function is a light-weight method inside the `flask_app.py` file. 
Heavier applications, such as a fully end-to-end trained machine learning model would 
probably run on some web application in serialised form and the API would be designed 
to deserialise such a model appropriately. Libraries, like Python's Pickle could be 
used for such purposes.

## References

This has been my first ever web application and I had to use some resources to learn 
about Flask and readability metrics on Python, HTML rendering and REST APIs, 
either by using paradigms or borrowing code:

* [Best practices for REST API design](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)

* [Designing a RESTful API with Python and Flask](https://blog.miguelgrinberg.com/post/designing-a-restful-api-with-python-and-flask)

* [Python Machine Learning](https://www.goodreads.com/book/show/25545994-python-machine-learning), 
by Sebastian Raschka, pp. 251 - 276

* [py-readability-metrics](https://py-readability-metrics.readthedocs.io/en/latest/)

* [Understanding And Using REST APIs](https://www.smashingmagazine.com/2018/01/understanding-using-rest-api/)
