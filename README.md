# HEROKU DEPLOYMENT
### Python Application development to Heroku
#### Requirements
<ol>
<li>Gunicorn</li>
<li>Heroku Account</li>
<li>Heroku Command line Interface</li>

</ol>

## Gather all the Requirements needed

### Install gunicorn

gunicorn is unix based server that will run your application on Heroku

```sh
python3.8 -m  pip install gunicorn
```
### Create a free [Heroku](https://dashboard.heroku.com/) account


### Install the Heroku CLI

For ubuntu/Debian
```
curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
```
For other versions find the [CLI](https://devcenter.heroku.com/articles/heroku-cli)


## List all the python Dependencies

Use this command to list all the dependencies

```
pip freeze
```
Then put all those dependencies in a file called _requirements.txt_

```
pip freeze > requirements.txt

```
*remove the pkg-resources==0.0.0* dependency.

### Create a Procfile

procfile

```
web: gunicorn manage:app
```

### Create a Heroku application

```
heroku login
```
### Create a new application

```
heroku create <name-of-app>
```
*Name your application as per the name of your choice ..make the name associative with your project*

### Adding Configurations

Add our environment variables as configuration variables to our Heroku project.

```
heroku config:set API_KEY=<YOUR API_KEY>

heroku config:set SECRET_KEY=<YOUR SECRET KEY>
```
*Enables you to access the environment configurations in your Heroku application.*

### Deployment

```
git add .

git commit -m "deployment to heroku / any commit message"

git push heroku master

```
# **Deployment of your previous project after integrating Database**

### We need to now configure our Heroku server for deployment
<ol>
<li>

**First we need to set configuration variables for our email username and password.**

</li>

```sh
* heroku config:set MAIL_USERNAME=YOUR EMAIL ADDRESS
* heroku config:set MAIL_PASSWORD=YOUR EMAIL PASSWORD
```
<li>

**Set up Postgres on Heroku.**

</li>

```sh
heroku addons:create heroku-postgresql
```

<li>

**We then need to define this new Database URI inside our config.py**

</li>

* Inside your class ProdConfig(Config):

```
SQLALCHEMY_DATABASE_URI = os.environ.get("DATABASE_URL")
```

<li>

**Updating application for production**

</li>

```
app = create_app('production')
```

<li>

**Update our requirements.txt file to pick the new extensions and modules we have used.**

</li>

```sh
pip freeze > requirements.txt
```
*Remember to remove the pkg-resources==0.0.0 line to prevent throwing an error when deploying.*

<li>

**Define your database schema on our Heroku database.**

</li>

```sh
heroku run python3.8 manage.py db upgrade
```
</ol>



<mark>*<p align = "center"> &copy;2022 Reuben Kipkemboi.</p>*</mark>
    



