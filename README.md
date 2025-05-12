# New Django Web Dev Template (production ready)
Use this template to speed up your Django development and deliver web-development projects as quickly as possible.

### What features does this Django template include?
- Production ready, you can immediately deploy this to Digital Ocean.
- Comes with a landing, about us, blog, and contact page that you can modify.
- Responsive design.
- Contact us form.
- 404 page
- Has blog with Wagtail CMS built-in for editing
- Technical SEO optimization.
- Dynamic Sitemap.xml
- Robots.txt
- Google analytics
- Plausible analytics
- Custom user model.
- Google SMTP email server connections
- Tailwind css 4.0 setup for rapid development

### Table of contents

  - [What features does Django template include?](#what-features-does-django-template-include)
  
- [Local development](#local-development)
  - [Admin superuser](#admin-superuser)
- [Customizing](#customizing)
  - [Adding title, description to page](#adding-title-description-to-page)
- [Deployment:](#deployment)
    - [Create a firebase credential file](#create-a-firebase-credential-file)
    - [Deploying credential file to production](#deploying-credential-file-to-production)
- [Images credits](#images-credits)



## Local development

Follow the below steps for local development setup:

1. Ensure a new repo has been created using this template ('https://github.com/wesordonez/new-web-dev-template')

2. Create a virtual environment for local development

```py
python3 venv -venv
python3 source bin activate
```

3. Install dependencies

```py
pip install -r requirements.txt
```

4. Add a `.env` file inside the `project` folder using the included `.env.dev` file as a guide.

Required env variables are:
- SECRET_KEY
- Development Database Variables (default configuration is for postgres but sqlite would work too)

> **NOTE:** The secret key is generated using the `get_random_secret_key()` function. Copy this into the `.env` file and delete the print statement AFTER the databases and tables have been migrated

5. Create a new database in postgres (PGAdmin 4) with the name used in the env variabl `SQL_NAME`

6. Now in your terminal create database tables using

```
python manage.py migrate
```
Your database should be created and ready to use.

> **IMPORTANT:** This step should not be skipped as it may cause problems in the migration history order requiring a restart.

7. The migrate command should have triggered the `get_random_secret_key()` function outputing a secret key. This should be copied into the `env` file at this time and the printstatement commented out. A new secret key should be created for the production secret when time for deployment. 

8. Now run the website from the terminal using.

```py
python manage.py runserver
```
Your website should be available at: http://localhost:8000/

The Django admin page should be available at: http://localhost:8000/admin/

The Wagtail Dashboard page should be available at http://localhost:8000/cms/

Test the website works and the contact form successfully writes data to the created database.

9. To run Tailwind CSS open a new terminal and run:
```py
npm install tailwindcss@latest
npm install cross-env
npm install postcss-simple-vars
```
Then you should be able to start tailwind which will auto update and watch for changes using this command:
```py
python manage.py tailwind start
```

10. Create admin superuser using the following command in terminal:
```py
python manage.py createsuperuser
```

Follow the prompts and test at: https:localhost:8000/admin/

## Trouble Shooting
**Note:** If you are facing problems starting this program in windows OS, remove logging from project/settings.py

## Customizing

All html, css, js and assets lies inside the templates.
- To modify the landing page, update `home.html`.
- To add link to header and footer or modify head tags, check `base.html`.
- extend `base.html` to have the same footer and header.

### Adding title, description to page
To add title to a page use the following tags
```py
{% block title %}lorem impsum {% endblock title %}
{% block description %}lorem impsum{% endblock description %} #meta description

{% block socialTitle %}{{blog.title}} | {% endblock socialTitle %} # open graph title, for socials
{% block socialDescription %}{{blog.meta_description}}{% endblock socialDescription %} # open graph description, for socials
{% block pageType %}article{% endblock pageType %}
{% block pageImage %}{% endblock pageImage %} # social image
```

To add additional head tags

```py
{% block head_tags %}lorem impsum {% endblock head_tags %}
```
To add scripts at the end of the elements
```
{% block scripts %}
    <script src="{% static "" %}" />
{% endblock scripts %}
```

## Deployment:

Follow Dunosis documentation to deploy to Digital Ocean App Platform using GitHub Actions. 


## Credits
This template was based heavily on the following template by PaulleDemon
- https://github.com/PaulleDemon/Django-website-template

Images are taken from free to use sites such as 
1. unsplash - https://unsplash.com/
2. Pexels - https://www.pexels.com/