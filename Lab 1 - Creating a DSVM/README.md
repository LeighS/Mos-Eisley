## Lab 1 -  Create a Data Science Virtual Machine (DSVM)
Every Jupyter Notebook needs to be hosted, either locally, or in Azure. In Azure you can use a shared service, or host your notebooks on your own VM.<br>
In this lab - for better performance - you are going to create a DSVM.<br><br>

1. Navigate to the Azure portal and create a new Data Science VM for Linux (Ubuntu), with any instance details of your liking:<br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/create-dsvm.png
)<br><br>
This image contains JupyterHub and opens the required ports upon creation.
While the VM is being deployed, proceed to the next lab.


## Lab 2- Create your first Jupyter Notebook
1.	Navigate to https://notebooks.azure.com/ and login with your Corp credentials
2.	Click on My Projects and click on **New Project** and create your first project with any name:

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/create-project.png
)<br><br>

Now that you have created a project, let's add a Notebook.<br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/create-notebook.png
)<br><br>

## Lab 3 - Start your Notebook
Verify that your DSVM has deployed successfully and is up & running.<br>

Your NSG should contain a JupyterHub allow rule for TCP 8000.<br><br>

1. Start your new Notebook and select the **Direct Compute** option.
2. Configure the settings in the screen below based on your DSVM settings:
![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/configure-dsvm.png
)<br><br>

*Note:*<br>
If you are getting a message "Kernel not found", select Python 3.6 - AzureML:
![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/python3.6-kernel.png
)<br><br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/notebook-running.png
)<br><br>

**Your Jupyter Project and Notebook has been created and your notebook is up & running.<br>
Proceed to the next lab, where the fun starts!**

