# Herokuin

#### A project template for Django 1.6.2 with production settings to easily deploy on Heroku with statics on S3 made for Prowl.

#### Pre-requisites

- A Heroku account, and [Foreman](https://www.theforeman.org) installed
- Git
- [virtualenv](https://pypi.python.org/pypi/virtualenv)
- An AWS account that supports S3 & Route 53


#### 1. Create the Prowl working environment

```
    $ mkdir hellodjango && cd hellodjango
    $ virtualenv venv --distribute
    $ source venv/bin/activate
```

#### 2. Install Django along with South (if you haven't done so already)

```
    $ pip install django && south 
```

#### 3. Create the new project using a template

```
    $ django-admin.py startproject --template=https://github.com/Montana/herokuin.git --extension=py,rst,html hellodjango .
```

#### 4. Install additional dependencies for development (not for production)

```
    $ pip install -r requirements/local.txt
```

#### 5. Deploy to Heroku

```
    $ heroku create
    $ git push heroku master
```

#### 6. Set Heroku environment

```
    $ heroku config:set DJANGO_SETTINGS_MODULE=hellodjango.settings.production
    $ heroku config:set SECRET_KEY=my_random_secret_key
    $ heroku config:set AWS_STORAGE_BUCKET_NAME=my_application_bucket
    $ heroku config:set AWS_ACCESS_KEY_ID=my_key_id
    $ heroku config:set AWS_SECRET_ACCESS_KEY=my_secret_key
    $ heroku ps:scale web=1
    $ heroku run python hellodjango/manage.py collectstatic
```

#### 7. Finally
```
    $ heroku open
```

