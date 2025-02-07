
# Jupyter Notebook Questions

## Question 1
What is the purpose of the following Jupyter Notebook commands? Provide examples where applicable.
1. `%matplotlib inline`
2. `%timeit`
3. `%%writefile`
4. Can you name any other similar examples?
```
1. `%matplotlib inline` makes sure matplotlib plots are displayed inside the notebook.
2. `%timeit` measures the execution time of a single line of code.
3. `%%writefile` writes the entire cell contents to a file, useful for saving scripts or text files directly from a notebook.

Other Jupyter Notebook magic commands are as follows:
i) `%matplotlib notebook` This command enables interactive plots in Jupyter Notebook, instead of static images.
ii) `%%bash` This command facilitates running an entire cell as Bash commands.
iii) `%load` This command enables loading an external Python script into the Notebook.
```

## Question 2
You have installed Jupyter Notebook on your local machine. When you try to start it by running jupyter notebook, you get the following error:

```bash
jupyter: command not found
```

Describe the issue and suggest a potential solution.

```
There are couple of scnerios to consider:
1. Maybe Jupyter is not in the $PATH. I'm a Linux user so would try this command `which jupyter` to check if Jupyter is in my system's path.
2. It could also be that Jupyter is installed but in a different virtual env. So, I need to make sure of that.
```

## Question 3
- What is the purpose of a Jupyter kernel?
- Explain how you can install a new kernel and the location of the kernel configuration file.
```
A Jupyter kernel is a runtime environment that executes code inside a Jupyter Notebook.
It allows users to run different programming languages (such as Python, R, Julia, etc.) inside Jupyter.

To install a new Jupyter kernel run the following command:
python -m ipykernel install --user --name=my_env --display-name "Python (my_env)"

After installation, I can select it in Jupyter Notebook under:
Kernel -> Change Kernel -> Python (my_env)
```

## Question 4
You are working in a Jupyter Notebook and want to execute a bash command directly within a cell. How can you do this?

## Question 5
A colleague asks how to share a Jupyter Notebook as a PDF file to share with a collaborator.

- How can you export a notebook as a PDF file with all markdown information?
- Other than PDF, what other formats can the colleague export the notebook?

The colleague tried to export the notebook as a PDF but reports that he/she is getting the following error: `nbconvert failed: PDF creating failed`.

- What might be the reason for the error? How can you fix this?


## Question 6
You are running a computationally heavy code block in a Jupyter Notebook. After some time, you get notified that the kernel has shutdown.

- What could be causing this issue?
- Suggest ways to prevent this from happening in the future.


## Question 7
Explain the difference between a Jupyter Notebook and JupyterLab. What are the advantages of using JupyterLab over Jupyter Notebook?


## Question 8
You need to install a Jupyter Notebook extension, such as nbextensions, to enhance its functionality.

- How would you install and enable this extension?
- Once installed, how can you access its features?


## Question 9
You are using Jupyter Notebook on a remote server but want to access it through your local machine's browser.

- What steps are required to set up an SSH tunneling for this purpose?


## Question 10
Your colleague is running a Jupyter Notebook server on a remote machine, but they are currently using a token-based URL for accessing it. They would like to set up a password for better usability and security.

- Explain the steps your colleague needs to follow to configure the Jupyter Notebook server to use a password instead of a token.


## Question 11
What is JupyterHub, and how does it differ from a standalone Jupyter Notebook? Provide an example scenario where JupyterHub would be more suitable.


## Question 12
You are tasked with configuring JupyterHub to authenticate users via OAuth with GitHub.

- What additional software or libraries are required to set this up?
- Describe how to configure JupyterHub to use GitHub OAuth for authentication.


## Question 13
JupyterHub needs to integrate with an existing LDAP directory for user authentication.

- What configurations are required to enable LDAP authentication in JupyterHub?
- How can you test the LDAP configuration before deploying it?


## Question 14
You are tasked with securing JupyterHub for public access.

- What steps would you take to secure the server (e.g., SSL/TLS, firewalls)?
- How can you configure JupyterHub to redirect HTTP traffic to HTTPS?


## Question 15
A user wants to install custom libraries in their JupyterHub environment but is unable to do so due to permission errors.

- Why might this happen?
- How would you configure JupyterHub to allow users to install libraries in their own environment without compromising the system?
