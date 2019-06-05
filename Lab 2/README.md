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

Since your Notebook is running in Azure, you will see that KqlMagic is actually already installed, this will not the case in a docker instance running locally. But it's a good practice to make sure you have the lastest version running.

:bulb: *Ctrl+Enter will execute the cell content, while typing "O" will clear the cell output*

#### Configure your workspace settings and connect
To connect to your Sentinel workspace, we need to provide your workspace settings. This can be configured through a Jupyter configuration file (recommended) or in the Notebook itself. For now we will configure it in the Notebook.<br>

:triangular_flag_on_post: *Your homework: figure out how you can get your workspace configuration settings from a config file*

1. Insert a new cell and add the following content:
```python
# Workspace connection variables
path = %env PATH
tenant_id = '<Your TenantId>'
subscription_id = '<Your SubscriptionId>'
resource_group = '<Your ResourceGroup>'
workspace_id = '<Your WorkspaceId>'
workspace_name = '<Your WorkspaceName>'
print('We are going to use the following Log Analytics Workspace: {}'.format(workspace_name))
```
2. Run the cell
3. Insert another cell and add the following:
```python
# Reload KqlMagic and connect to the workspace (requires )
%reload_ext Kqlmagic
%kql loganalytics://code;workspace=workspace_id;tenant=tenant_id;alias="<Your WorkspaceName>"
```
4. Run the cell<br><br>
:bulb: If you see an star in brackets like this **[*]** it means that the cell content is being executed 

5. Make sure you pay attention to the cell output and login into Azure:

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/login-workspace.png
)<br><br>

After a succesful Azure login, you are ready to run your first KQL query using a Jupyter Notebook!<br><br>
*Note: ignore any Javascript errors*

### Running a KQL query
**1. Insert a new cell, add the following and execute the cell:**
```python
%kql SecurityAlert | summarize count() by ProductName
```
<br>
This would output something like this:

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/kql-query1.png
)<br><br>


:bulb: *Notice the following above*:<br>
***%kql** means that you are going to pass a KQL query on a single line. Using a double %% sign, means that you are going to use multi lines like the example in the following step*<br><br>

### Matching VM addresses with TOR and C2 addresses
In this exercise you will leverage ServiceMap Kusto data, which has outbound IP addresses.<br>
You will match these addresses with TOR and C2 data to hunt for IOC's.

#### Kusto query
Execute the following to get the ServiceMap addresses:
```python
%%kql
VMConnection
| where Direction == 'outbound'
| limit 20
```
Put the output in a dataframe:
```python
connections = _.to_dataframe()
```

Since you probably don't have a much, we are going to cheat a little bit and insert a row with a demo IP address:
```python
connections2 = pd.DataFrame({'DestinationIp': ['82.118.242.113'], 'Computer': ['ContosoDc']})
connections=connections.append(connections2)
connections
```
<br>

:grey_exclamation: **Make sure you see the inserted row!**

### Tor list retrieval
Now you are going to retrieve an external TOR list.<br>
First import the panda library:
```python
import pandas as pd
```

Now get the TOR list:
```python
torlist = pd.read_csv('https://www.dan.me.uk/torlist',header=0,names=["DestinationIp"])
```
Let's check if we got the TOR list allright:
```python
# Check if we have a solid Torlist, show only 5 rows
torlist.sample(5)
```
Now, you are going to check if we have a match (you should):
```python
# Check if we find a match (you should since we inserted a demo row)
connections.merge(torlist, on="DestinationIp")
```
You should see something like this:<br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/torlist.png
)<br><br>






