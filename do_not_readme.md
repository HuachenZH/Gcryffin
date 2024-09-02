# Gcryffin
In construction

## Prepare environment - virtual env
We use pyenv.  
Official repo of pyenv: [github](https://github.com/pyenv/pyenv-virtualenv).  
Summarize:
1. `cd` to project directory
2. Set Python version for the directory:
    ```shell
    $ pyenv local 3.12.5
    ```
3. Create virtual environment:
    ```shell
    $ pyenv virtualenv 3.12.5 Gcryffin
    ```
    The good practice is to give the virtual env the same name as the project directory. You can also name it differently.
4. (Optional) You can check if the virtual environment is created successfully by:
    ```shell
    $ pyenv virtualenvs
    ```
    Normally it shoud give:
    ```
    3.12.5/envs/Gcryffin (created from /home/{user}/.pyenv/versions/3.12.5)
    Gcryffin (created from /home/{user}/.pyenv/versions/3.12.5)
    ```
    Each virtual environment has two entries. The shorter one is a symlink.
5. Activate versions:
    ```shell
    $ pyenv local Gcryffin
    ```
    In this `pyenv command`, instead of specifying version, we specify an environment.  
6. Automatically activate/deactivate virtual environment:  
  If pyenv-virtualenv is properly installed, the virtual environment is automatically activated or deactivated when you enter or leave the project directory.
7. (Optional) If you want to delete the virtual environment:
    ```shell
    $ pyenv uninstall Gcryffin
    ```




