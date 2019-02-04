# Installation

## Python

1. Clone package from GitHub:

```bash
$ git clone https://github.com/dialogs/python-bot-sdk.git
```

2. Check that you have the latest versions of ``pip`` and ``setuptools``:

```bash
pip install --upgrade pip
pip install --upgrade setuptools
```

3. Install required packages (run this command from `python-bot-sdk` folder):

```bash
$ pip install -r requirements.txt
```

!>If you need to install SDK into restricted domain network where your SSL certificates might be changed by corporate firewall,
    you can use ``--trusted-host`` directive like this:  
    ``$ pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt``


That's it! Launch examples with this:
```bash
$ python main.py
```
### Anaconda

Anaconda installation is the same as for Python, however you also need to ensure that you have
the latest versions of ``pip`` and ``setuptools``. If not, you have to upgrade them:
* run command ``conda config --set ssl_verify no`` to disable SSL checking
(case of restricted domain networks where your SSL certificates
might be changed by corporate firewall);
* then open Anaconda Navigator and install ``setuptools``;
* open Anaconda prompt and input ``easy_install pip``.

After this you can install packages in the usual way.

You can read more about installing packages in Anaconda without
SSL [here](http://seanlaw.github.io/2015/12/23/fetching-conda-packages-behind-a-firewall/).

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
