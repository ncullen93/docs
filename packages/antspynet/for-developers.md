# Welcome to ants.dev

### Note: this is a private repo for documentation and sharing private keys / dev tools

The ants.dev website is an online platform for medical imaging analysis using the ANTs ecosystem.

## What is ants.dev?

The ants.dev platform is meant to be three things:

- a cloud-based solution for medical imaging analysis using ANTs that can optionally be self-hosted
- a centralized location for documentation and tutorials of the ANTsX ecosystem of packages
- a discovery platform for deep learning-based medical imaging models similar to Huggingface.co

## What are the goals of ants.dev?

The goals of ants.dev are the following:

- to make medical imaging analysis (and ANTs specifically) more accessible to non-developers
- to make it easier to track, store, and compare medical image analysis results
- to provide compute (and storage) for medical images to those who need it
- to make it easier to discover and compare deep learning models for medical imaging

## Development architecture

The website consists of three independent parts all in separate repos:

- frontend: contains JS (react) code to control the app user interface
- backend (NOTE: not yet in use): contains Python (django-rest-framework) code for app api / database
- engine: contains Python (FastAPI) code that runs ANTsPy code

### Quickstart running locally

Steps to get the application running locally:

- Clone all the repos

```
mkdir ants.dev
cd ants.dev
git clone https://github.com/antsx/backend.git
git clone https://github.com/antsx/frontend.git
git clone https://github.com/antsx/engine.git
```

- Start up the engine

```
cd engine
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload --port 5050
```

- Start up the backend (NOTE: not yet in use)

To start the back-end, you need to set the DJANGO_SECRET_KEY in the .env file in the main directory. So,
first create the .env file in the outermost backend/ directory and add:
`export DJANGO_SECRET_KEY="___ key here ___"`

```
cd backend
source .env
pip install -r requirements.txt
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

- Start the frontend

```
cd frontend
npm run dev
```

This should automatically launch the application in the broswer. If it doesn't, then
navigate to the localhost specified in the terminal. Now, you should be able to use the
application as normal. This will use the local database, however, which will be empty
the first time you use the application.

### frontend

The frontend is built using React and Javascript. Auth is done using firebase.

Key packages:

- tailwindcss for styling
- next-ui for ui components
- react-router-dom for routes
- firebase for auth

To run locally from main directory:

```
npm run dev
```

### backend

The backend is built using Python and Django-Rest-Framework. The backend is only the database
for the application and does not run any kind of analysis code. It stores information like
the user profile, etc.

To run locally from main directory:

```
source .env
python manage.py runserver
```

### engine

The engine is built using Python and FastAPI. The engine is where actual ANTs code runs and
where all real analysis happens.

Key packages:

- ants (install: pip install antspyx)
- pins (used to store and share data/models/other python objects: https://rstudio.github.io/pins-python/)

To run locally from main directory:

```
uvicorn main:app --reload --port 5050
```

## Frequently Asked Questions

- What are the key functionalities of the app?

  Users can run ANTs functions on their images. The intermediate and end results of any analysis can be saved in the app
  and will therefore persist across user sessions. Results can be visualized and compared via figures as well as via tables.
  This app therefore provides an interactive user interface to the ANTs ecosystem.

- Why would people want to use the app?

  Users of the app gain access to all ANTs functions in a more intuitive interface without the need to write any code. Additionally,
  the app can help manage results and images themselves. People may also want to use the app if they do not readily have access to
  appropriate computing resources.

- How do users store images and how do they share them with the app?

  Via user's own S3 bucket: Users store images in their own AWS S3 buckets and share read-only access with
  the app via the appropriate credentials. The app can see what images exist in the bucket and can download
  the images from the bucket in order to run ANTs functions on them via the engine. However, the
  app cannot add images to or delete images from the bucket.

  Via ANTs' S3 bucket: Alternatively, users can store images in our S3 buckets for a fee. In this way,
  users can upload images directly via the app and can also manage their images via the app.

- Where does the engine (i.e., ANTs functions) run?

  The engine runs on its own heroku server. Each task is launched via a non-blocking FastAPI call so
  that one user's actions do not block another's.
