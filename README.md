# django-docker-compose


## How to install

-  sudo docker-compose run web django-admin startproject projectname .
-  ls -l
-  sudo chown -R $USER:$USER .
-  ls -l
-  nano .env
```
DEBUG=True
DB_NAME=
DB_HOST=
DB_USER=
DB_PASSWORD=
DB_PORT=
```
-  add environment in the settings.py file
```
import environ

env = environ.Env(
    # set casting, default value
    DB_NAME=(str, 'dbname'),
    DB_HOST=(str, 'dbhost'),
    DB_USER=(str, 'dbuser'),
    DB_PASSWORD=(str, 'dbpass'),
    DB_PORT=(str, 'port'),
    DEBUG=(bool, True)
)

# reading .env file
base = environ.Path(__file__) - 2 # two folders back (/a/b/ - 2 = /)
environ.Env.read_env(env_file=base('.env')) # reading .env file
```
-  set up mysql db in the settings.py file
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': env('DB_NAME'),
        'HOST': env('DB_HOST'),
        'USER': env('DB_USER'),
        'PASSWORD': env('DB_PASSWORD'),
        'PORT': env('DB_PORT'),
        'OPTIONS': {
            'sql_mode': 'traditional',
        }
    }
}
```
-  set up postgres db in the settings.py file
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': env('DB_NAME'),
        'USER': env('DB_USER'),
        'PASSWORD': env('DB_PASSWORD'),
        'HOST': env('DB_HOST'),
        'PORT': env('DB_PORT'),
    }
}
```
-  change debug value in the settings.py file
```
DEBUG = env('DEBUG')
```
-  set up cors configuration in the settings.py file
```
MIDDLEWARE = [
    ...
    'corsheaders.middleware.CorsMiddleware',
    'django.middleware.common.CommonMiddleware',
    ...
]

CORS_ORIGIN_ALLOW_ALL = True
```
-  allowed host
```
ALLOWED_HOSTS = ['*']
```
- docker-compose up -d