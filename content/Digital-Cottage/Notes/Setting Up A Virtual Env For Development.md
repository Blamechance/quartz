

Virtual environments are good practice when developing projects as they provide enhanced: 
- isolation
- reproducability 
- portability
- security
- and efficiency. 
---
# Installation: 
To set up a virtual environment, you can follow these steps:

## Step 1: Install Virtual Environment.
My pick of choice is generally `venv`, but there's also `pipenv` and `virutalenv` -- though,  `venv` is generally the recommended option as it's included in the native Python library as of `Python 3.3`. 
Make sure you have the virtual environment package installed. If you're using Python, you can install it using **`pip`** by running the following command in your system's command prompt or terminal:

```
pip install virtualenv
```

## Step 2: Open VSCode.
Open Visual Studio Code (VSCode) on your system.

## Step 3: Open Terminal in VSCode:
You can do this by going to View > Terminal or by using the keyboard shortcut Ctrl+` (Backtick).

## Step 4: Create a Virtual Environment In the terminal:
Navigate to the directory where you want to create your virtual environment. 
Next, create a virtual environment by running the following command:

For Windows:

```
python -m venv env
```

For macOS/Linux:

```
python3 -m venv env
```

This will create a virtual environment named "env" in the current directory.

## Step 5: Activate the Virtual Environment
Activate the virtual environment by running the appropriate command based on your operating system:

For Windows:

```
env\\Scripts\\activate
```

For macOS/Linux:

```bash
source venv/bin/activate
```

```
source venv/bin/activate
or 
source venv/scripts/activate
```

You will notice that the virtual environment name "env" appears in the terminal prompt, indicating that the virtual environment is now active.

## Step 6: Start Using the Virtual Environment:
Make sure you install any dependencies and modules you use in your project **only when the virtual environment is active**. 

All installations will then be self-contained in that environment, allowed tidy bundling of dependencies, independent of the global server/OS configuration. 

Have it activated whenever you're working on the project! 


## Step 7: Deactivate the Virtual Environment:
When you're done working in the virtual environment, you can deactivate it by running the following command:

```
deactivate
```

This will return your terminal to the default system environment/shell. 

**Remember to always activate the virtual environment before working on your project to ensure that you are using the correct dependencies and configurations for that specific project.**


# Reproducing Environment On Other Systems:
This 
On the local environment where your app works with all it's dependencies, run the following at the root directory:
```sh
pip freeze > requirements.txt
```
This creates a file listing all the modules installed, as well as their versions. 

To reliably set up those dependencies in other environments, first `clone` or have your project files wherever you want it to be. 
While in the directory with the `requirements.txt` file, install and activate the virtual environment, before running:
```sh
pip install -r requirements.txt
```
This will install all listed dependencies in the new environment. 

---
### Resources
- https://www.geeksforgeeks.org/how-to-create-requirements-txt-file-in-python/


