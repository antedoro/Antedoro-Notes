# Python notes

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
