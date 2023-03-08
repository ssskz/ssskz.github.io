---
title: Jupyter Notebook On Linux
commentable: true
Edit: 2023-3-8
mathjax: true
mermaid: true
tags: linux  python
categories: Operating-System
description: Open the Jupyter Notebook on the remote server using a local browser.
---
Lately I've been running a lot of code for neural networks, so I always use .ipynb files. However, since running on the local machine often out of memory. So I decided to use the academy's Linux servers

But it took me a lot to access the server's Jupyter Notebook on my local browser. So I summarized my experience and shared it with you.

# Prerequisite Preparation

Assuming that you already have Jupyter Notebook installed on your Linux server.

# Configure Jupyter Notebook

## Generate Jupyter Notebook configuration file

```markdown
jupyter notebook --generate-config
```

If you've used this command before, or created a configuration file yourself, the command line may ask you if you want to overwrite an existing file. 

If you want to override, just select Override.

## Edit Jupyter Notebook configuration file

The command line will tell you the path to the config file, for example:

```markdown
/home/username/.jupyter/jupyter_notebook_config.py
```

This file contains various configuration information of Jupyter, but by default it is commented out. So we're going to set up a few of them.

You can open and modify the file through vim:

```markdown
vim /home/username/.jupyter/jupyter_notebook_config.py
```

### Start with password-related settings

Add a line at the end of the above config file and save before exit:

```markdown
c.NotebookApp.allow_password_change=False
```

Then enter on the command line:

```markdown
jupyter notebook password
```