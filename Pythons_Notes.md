# Python notes

## Create a virtual envirorment

To create a virtual environment, go to your project’s directory and run venv. If you are using Python 2, replace venv with virtualenv in the below commands.

On macOS and Linux:

`python3 -m venv env`

## Activating a virtual environment

`source env/bin/activate`

## Leaving the virtual environment

`deactivate`


## Setup requirements

You can use pipreqs to automatically generate a requirements.txt file based on the import statements that the Python script(s) contain. 
To use pipreqs, assuming that you are in the directory where example.py is located:

`pip3 install pipreqs`

`pipreqs .`

It will generate the following requirements.txt file:

> requests==2.23.0
> 
> beautifulsoup4==4.9.1

which you can install with:

`pip3 install -r requirements.txt`

## Freezing dependencies

Pip can export a list of all installed packages and their versions using the freeze command:

`python3 -m pip freeze`


