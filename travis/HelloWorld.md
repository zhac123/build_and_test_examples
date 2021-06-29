"Hello World" with Travis CI
============================

Here, we will set up a first Travis CI job, based around a simple "hello world" example, to get you up and running with Travis CI.

Sign in to GitHub
-----------------

If you do not already have an account, then visit [GitHub](https://github.com) and create a free account.

If you already have an account, then visit [GitHub](https://github.com) and sign in.

In the following text, replace `USERNAME` with your GitHub user name.

Create a new repository on GitHub
---------------------------------

Visit `https://github.com/USERNAME`.

Click **Repositories** tab.

Click **New**.

Enter Repository name: `travis-lab`

Click **Create repository**.

Clone your fork locally
-----------------------

Within a terminal window, clone your forked repository:

```console
$ git clone https://USERNAME@github.com/<USERNAME>/travis-lab
$ cd travis-lab
```

Create a "hello world" program
------------------------------

Create a short Python script, `hello.py`, in your repository, with the content:

```python
print("Hello world!")
````

Run it:

```console
$ python hello.py
Hello world!
```

Add and commit this file to your repository and push the changes to GitHub:

```console
$ git add hello.py
$ git commit -m "Added Python hello world script" .
$ git push origin master
```

Visit https://github.com/USERNAME/travis-lab and check that the repository now contains `hello.py`.

Sign in to Travis CI
--------------------

Once you have an account on GitHub, you can use this to sign in to Travis CI, so go to Travis CI, https://travis-ci.com/.

Click on Sign in with GitHub.

Select a Free plan:

* When logged in, click on your avatar/photo on the top-right of the Travis CI page and select **Settings**.
* Click the **Plan** tab.
* Under Free, click **Select plan**.
* Click **Select plan**.

Enable your repository on Travis CI
-----------------------------------

Now, you need to tell Travis CI to check for changes in your repository, so click on your avatar/photo on the top-right of the Travis CI page and select **Settings**.

This will take you to a page, https://travis-ci.com/account/repositories, which shows a list of your GitHub repositories that Travis CI knows about.

If you see the text "GitHub Apps Integration" with an **Activate** button, then:

* Click **Activate**.
* Click **Only select repositories**.
* Click the **Select repositories** drop-down list.
* Select 'USERNAME/travis-lab'.
* Click **Approve & Install**.
* When prompted, enter your GitHub password.

In future you can add additional repositories to Travis CI by returning to https://travis-ci.com/account/repositories and clicking **Manage repositories on GitHub**.

Create a `.travis.yml` job file
-------------------------------

Travis CI looks for a file called `.travis.yml` in a Git repository. This file tells Travis CI how to build and test your software. In addition, this file can be used to specify any dependencies you need installed before building or testing your software. So, let's add one.

Create `.travis.yml` with the content:

```yaml
language: python

python:

  - "3.6"

script: 

  - python hello.py
```

This says we want Travis CI to set up a Python 3.6 environment, then run our `hello.py` script.

Add and commit this file to your repository and push the changes to GitHub:

```console
$ git add .travis.yml
$ git commit -m "Added Travis CI job file" .
$ git push origin master
```

Visit https://github.com/USERNAME/travis-lab and check that the repository now contains `.travis.yml`.

Explore the Travis CI job information
-------------------------------------

Visit https://travis-ci.com/github/USERNAME. You should shortly see a job called `travis-lab`. Jobs are named after the corresponding repositories.

Click on `travis-lab`.

This will take you to a page, https://travis-ci.com/github/USERNAME/travis-lab, which shows information about the run of your Travis CI job.

The job should be coloured green and with a check/tick icon which means that the job succeeded.

Information on your Git repository, including the commit ID and branch is also displayed i.e. the commit that triggered the job to run.

Under the **Current** tab you should see the Travis CI output from running your job. Most of the content is Travis CI-specific configuration, relating to how it configures its environment to build and test your code. Scroll to the bottom and you'll see what Travis CI does after it clones your repository:

```
$ git clone --depth=50 --branch=master https://github.com/USERNAME/travis-lab.git mikej888/travis-lab
$ source ~/virtualenv/python3.6/bin/activate
$ python --version
Python 3.6.7
$ pip --version
pip 20.1.1 from /home/travis/virtualenv/python3.6.7/lib/python3.6/site-packages/pip (python 3.6)
Pip version 20.3 introduces changes to the dependency resolver that may affect your software.
We advise you to consider testing the upcoming changes, which may be introduced in a future Travis CI build image update.
See https://pip.pypa.io/en/latest/user_guide/#changes-to-the-pip-dependency-resolver-in-20-2-2020 for more information.
Could not locate requirements.txt. Override the install: key in your .travis.yml to install dependencies.
```

Certain lines are hidden, usually those concerned with setting up the environment for the job. Hidden lines are denoted by an arrow to the left of the line number. Click on these arrows to see the hidden lines.

At the very bottom, is the content of most interest, Travis CI's execution of our script:

```
$ python hello.py
Hello world!
The command "python hello.py" exited with 0.
Done. Your build exited with 0.
```

If a job completes with an exit code of 0 then the job is coloured green and with a check/tick icon, which means that the job succeeded.

If it completes with a non-zero exit code then the job is coloured red and with an X icon, which means that the job failed e.g. either the build failed or the tests failed.

Jobs still running are coloured yellow.

Add a `README.md` file with a build status icon
-----------------------------------------------

Each job has an associated status icon e.g. https://travis-ci.com/USERNAME/travis-lab.svg?branch=master. This can be embedded into a `README.md` file in a Git repository, so the current status of the build is always shown when viewing the Git repository via GitHub's web interface.

Create a `README.md` file e.g.:

```
# README for travis-lab

[![Build status](https://travis-ci.com/USERNAME/travis-lab.svg?master)](https://travis-ci.com/USERNAME)
```

This is MarkDown syntax and specifies a hyperlink to https://travis-ci.com/USERNAME that is rendered as an SVG image, whose source is at https://travis-ci.com/USERNAME/travis-lab.svg?master.  

Add `README.md` to your repository, commit it and push it.

As you have committed a change to your repository, this will trigger a new run of your job on Travis CI. On the page https://travis-ci.com/github/USERNAME/travis-lab, click **Current**. You may see your build in progress.

Visit https://github.com/USERNAME/travis-lab and look for your icon in your `README.md` file. This feature exploits the fact that GitHub's web interface renders MarkDown-formatted files as HTML.

Change your code
----------------

Make changes to your `hello.py` Python script then commit your changes and push them to GitHub. Watch how Travis CI regularly triggers new jobs.

Create a Python file with some functions, and an associated test file with some unit tests. Update the `script` section of `.travis.yml` to run the tests using `pytest`.
