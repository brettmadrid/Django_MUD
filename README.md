# Django_MUD

## Install to Django

1. heroku login
2. pipenv install gunicorn - The webserver for Heroku to use instead of the defualt Django one
3. pipenv install psycopg2-binary - PostgreSQL client binaries
4. pipenv install dj-database-url - enables parameterizeing database to allow to use SQLite locally and Heroku to use Postgres
5. pipenv install whitenoise - optimizes use of static files if present
6. pipenv shell - to start the virtual environments
7. pip3 freeze > requirements.txt - This creates a requirements.txt file which is required if using the virtualenv (pipenv shell created a virtualenv)
8. Create an .env file if not already created with the following:

ALLOWED_HOSTS=localhost,127.0.0.1
DEBUG=True
SECRET_KEY=<secrec key val>
DATABASE_URL="sqlite:///db.sqlite3"

\*\* Note- These values should later be copied into the config variable in Heroku settings console and DEBUG=False and the DATABASE_URL the url of postgres

9. pipenv install django - if it is not already installed.
10. add 'from decouple import config' to settings.py - allows to make reference to env file
11. add 'import dj_database_url' to settings.py. Allows for env use of database
12. pipenv install python-decouple
13. Change ALLOWED_HOSTS in the settings.py to: ALLOWED_HOSTS =
14. Add to the DATABASES section of settings.py the following:

    DATABASES['default'] = dj_database_url.config(conn_max_age=600)
    DATABASES['default'] = dj_database_url.config(default='postgres//...')
    DATABASES['default'] = dj_database_url.parse('postgres//...', conn_max_age=600)

15. Create a Procfile and put in it the following:

web: gunicorn <projectName>.wsgi --log-file -

16. Edit settings.py and add WhiteNoise to the MIDDLEWARE_CLASSES just below SecurityMiddleware

'whitenoise.middleware.WhiteNoiseMiddleware'

17. add static settings to settings.py

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

18. In the Heroku CLI type: 'heroku create <your app>' - Creates app on Heroku
19. In the Heroku CLI type: 'heroku addons:create heroku-postgresql:hobby-dev' - makes a Heroku postgres database and sets the environment variable
20. Set Heroku config variables:

ALLOWED_HOSTS=.herokuapp.com
DEBUG=False
SECRET_KEY=<secret key from env file>
