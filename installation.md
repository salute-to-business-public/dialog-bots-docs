# Installation

## Python installation

Firstly, you should download package from GitHub:

```bash
$ git clone https://github.com/dialogs/python-bot-sdk.git
```

Next step is to install python packages (run this command from `python-bot-sdk` folder):

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

## Java installation

Java Bot SDK is available as ``jar``-dependency via Maven.

## JavaScript installation

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
