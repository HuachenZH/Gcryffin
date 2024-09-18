# "cheatsheet"
Technically, it's just a list of commands that i've used.  

list accounts:  $ gcloud auth list  


## Get started
- List all projects:  
  ```shell
  $ gcloud config list project
  ```

- Set currently active project:  
  ```shell
  $ gcloud config set project PROJECT_ID
  ```
  Then a message says: "WARNING: Your active project does not match the quota project in your local Application Default Credentials file. This might result in unexpected quota issues.
  To update your Application Default Credentials quota project, use the `gcloud auth application-default set-quota-project` command."
  
  - Then i set the quota project by using:  
    ```shell
    $ gcloud auth application-default set-quota-project gcryffin-prototype
    ```
    - A prompt appears, saying API is enabled on my project, would i like to enable y/N ?  
    - i type "y" and it seems that API is enabled, credential is savec to file ~/.config/gcloud/application_default_credentials.json
      - i took a look inside the json, there are keys like "client_id", "client_secret", "quota_project_id", "refresh_token"


----------------------------------

# $ pip install google-generativeai

show available models:  
```python
print('Available base models:', [m.name for m in genai.list_models()])
```



