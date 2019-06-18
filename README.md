# Get started quickly with a Reveal.js Presentation

## Usage

Create a `virutalenv` and install [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/index.html).

```console
(cookiecutter) $ pip install cookiecutter
```

Now run it against this repo:

```console
(cookiecutter) $ cookiecutter https://github.com/calvinhp/cookiecutter-revealjs
```

You will be prompted for some information about your presentation and it will create a new folder filled with a Reveal.js project ready for you to build.

Check out your presentation:

```console
$ cd my_awesome_presentation
$ ls
```

Once you create your own presentation, you can create a git repo and push it there:

```console
$ git init
$ git add .
$ git commit -m "first awesome commit"
$ git remote add origin git@github.com:calvinhp/my_awesome_presentation.git
$ git push -u origin master
```

Enjoy!
