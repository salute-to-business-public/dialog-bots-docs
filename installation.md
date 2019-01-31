# Installation

## Python

Firstly, you should download package from GitHub:

```bash
$ git clone https://github.com/dialogs/python-bot-sdk.git
```

Before installation of libraries, you need to check that you have the latest versions of ``pip`` and ``setuptools``:

```bash
pip install --upgrade pip
pip install --upgrade setuptools
```

Next step is to install necessary packages (run this command from `python-bot-sdk` folder):

```bash
$ pip install -r requirements.txt
```

!>If you need to install SDK into restricted domain network where your SSL certificates might be changed by corporate brandmauer,
    you can use ``--trusted-host`` directive like this:  
    ``$ pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt``


That's it! Then you can launch test examples with this:
```bash
$ python main.py
```
### Anaconda

Anaconda installation is the same as for Python, but you also need to ensure that you have
the latest versions of ``pip`` and ``setuptools``. If not, you have to upgrade them:
* run command ``conda config --set ssl_verify no`` to disable SSL checking
(case of restricted domain networks where your SSL certificates
might be changed by corporate brandmauer);
* then open Anaconda Navigator and install ``setuptools``;
* open Anaconda prompt and input ``easy_install pip``.

After this you can install packages in the usual way.

You can also read [this](http://seanlaw.github.io/2015/12/23/fetching-conda-packages-behind-a-firewall/)
about installing packages in Anaconda without SSL.

## Java

Java Bot SDK is available as ``jar``-dependency via Maven.

## JavaScript

Firstly, you should download package from GitHub:

```bash
$ git clone https://github.com/dialogs/js-bot-sdk.git
```

Second step is installing dependencies (run this command from `js-bot-sdk` folder):

```bash
$ npm i install
```

To launch examples run this:

```bash
$ ts-node ./examples/index.ts
```
