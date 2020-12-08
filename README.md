# Get started quickly with a Reveal.js Presentation

## Usage

Make sure you have the `git-lfs` extension installed as this repo depends on it when Cookiecutter uses it.

Install [Cookiecutter](https://cookiecutter.readthedocs.io/en/latest/index.html) via `pipx`.

```console
$ pipx install cookiecutter
```

Now run it against this repo:

```console
$ cookiecutter https://github.com/calvinhp/cookiecutter-revealjs
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
$ git push -u origin main
```

Enjoy!
