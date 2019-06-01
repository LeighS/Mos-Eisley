## Lab 2 -  Building out your Jupyter Notebook
In the following exercises you will build up your Notebook from scratch. Feel free to go explore on your own, copy snippets from other Notebooks, or to skip some parts (although some have dependencies). This is all about getting your hands dirty with Jupyter Notebooks.<br>

My (personal) best learning experience is to start small, with snippets you understand, before cloning Notebooks. The following exercises are meant to do just that.<br><br>

### Connecting your Notebook with the Sentinel workspace
The first thing you probably want to do, is to connect your Notebook with the Sentinel workspace.<br>
Click on your first cell. Notice that you can switch **cell type** in the Cell menu , to either Code, Markdown or Raw NBConvert. The default is code.<br><br>

Copy and paste the following in your cell:

```python
!pip install Kqlmagic --no-cache-dir --upgrade
```
This will install KqlMagic, a library that will run KQL queries against a workspace.<br>
While having the cell selected, hit Ctrl+Enter, this will execute your cell content.

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/install-kqlmagic.png
)<br><br>

Since your Notebook is running in Azure, you will see that KqlMagic is actually already installed, this will not the case in a docker instance running locally.

:bulb: *Ctrl+Enter will execute the cell content, while typing "O" will clear the cell output*






