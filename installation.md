# Installation

## Python

1. Check your Python version: you should have 3.5 version or later. If you don't, please [install](https://www.python.org/downloads/) the upgrade.

2. Check that you have the latest versions of ``pip`` and ``setuptools``:

```bash
$ pip install --upgrade pip
$ pip install --upgrade setuptools
```
3. Install package by this command:

```bash
$ pip install dialog_bot_sdk
```

And that's it!

!>If you need to install SDK into restricted domain network where your SSL certificates might be changed by corporate firewall,
    you should follow these steps:<br>
   $ git clone https://github.com/dialogs/python-bot-sdk.git<br>
   $ pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org -r requirements.txt


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

Java Bot SDK is available as ``jar``-dependency via Maven. How to use the SDK with maven/gradle?

1. Add repository

Gradle:
```
repositories {
    maven { url "http://dialog.bintray.com/maven" }
}
```

2. Add BOT dependency

```
dependencies {
    compile 'im.dlg:bot-sdk:2.0.0'
    compile 'org.slf4j:slf4j-log4j12:1.7.27' //or any other slf4j provider
}
```


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
