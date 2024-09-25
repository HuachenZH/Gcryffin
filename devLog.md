# devLog

## info
- gemini vs vertex ai:
  - gemini: is the LLM
  - vertex ai: is the platform to interact and fine tune gemini
- official doc (this is an overview of procedures): [fine tuning gemini with api](https://ai.google.dev/gemini-api/docs/model-tuning)
  - when you are ready to start: [Fine-tuning tutorial](https://ai.google.dev/gemini-api/docs/model-tuning/tutorial?lang=python)
  - same as above, but in [github notebook](https://github.com/google/generative-ai-docs/blob/main/site/en/gemini-api/docs/model-tuning/python.ipynb)
- [Get started with semantic retrieval](https://ai.google.dev/gemini-api/docs/semantic_retrieval)
- medium article, [use py swarm to get started with gemini](https://medium.com/@kyeg/get-started-with-gemini-the-all-new-ultra-powerful-model-from-google-7f96c003f7f5)


## Prepare environment
It's been a time i haven't coded. Respawn as newbie. Ah shit, here we go again.  

- upgrade pyenv:  
  Check the readme of pyenv, read the section "Upgrading".  
  As i installed pyenv by git clone, i need to go to the pyenv repo and git pull.  
  (As a reminder, i installed pyenv as ~/.pyenv)  

- show the list of version of python in pyenv: `pyenv install --list`
- install latest stable py release: `pyenv install 3.12.5`

- intiate pyenv virtual env (Cf readme)


## WBS
- getting_started
  - set_up_auth
    - a_google_cloud_project (prerequisite)
    - a_local_installation_of_the_gcloud_CLI (prerequisite)
    - set_up_OAuth_quickstart
  - ...


### WBS - forEach
- a_google_cloud_project, [official doc](https://developers.google.com/workspace/guides/create-project)
  - install the gcould CLI, [doc](https://cloud.google.com/sdk/docs/install#linux)
    - i picked the instructions in "linux" (wsl is not ubuntu, i was wrong)  
      ```shell
      # download archive by curl. You can put it in ~
      $ curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-linux-x86_64.tar.gz
      # "unzip":
      $ tar -xf google-cloud-cli-linux-x86_64.tar.gz
      # install gcloud sdk:
      $ ./google-cloud-sdk/install.sh
      ```
      During the install process, it will prompt two questions.  
      The first prompt is google's data collection, you can put N.  
      The second prompt is to add gcloud CLI to PATH. It's suggested to put y.  
    - first time running: 
      - $ `./google-cloud-sdk/bin/gcloud init`
      - then i need to sign in, wsl cannot open browser so i need to copy paste the url in browser
      - need to use dvt account, google cloud service is enabled
    - update: when i tried to create a gcloud project by CLI, it says "ERROR: (gcloud.projects.create) FAILED_PRECONDITION: Cloud Resource Manager project creation is disabled."
    - created with my own gmail accout:  
      - Project name : Gcryffin-prototype
      - Project number : 660248704793
      - Project ID : gcryffin-prototype

- set_up_OAuth_quickstart
  - official doc: https://ai.google.dev/gemini-api/docs/oauth
  - first you need to enable API.  
    Normally there is a button in the tuto, click it and it opens in your gcloud project.  
  - Create OAuth 2.0 client ID (it's a credential)
  - make the above credential default, cf "Set up application default credentials"


## Obstacles
- while preparing virtualenv, `pyenv virtualenv 3.12.5 Gcryffin`, it gives: "pyenv: no installed versions match the prefix `-q'".  
  However it seems that the virtualenv is still created.  

- gcloud create project obstacle:
  - if i use dvt account, i cannot create project
  - if i my own gamil account, i can create project, but some features will be disabled

- when trying to list tuned models, it says "403 Request had insufficient authentication scopes. [reason: "ACCESS_TOKEN_SCOPE_INSUFFICIENT"


To install or remove components at your current SDK version [491.0.0], run:
  $ gcloud components install COMPONENT_ID
  $ gcloud components remove COMPONENT_ID

To update your SDK installation to the latest version [491.0.0], run:
  $ gcloud components update



## trouble shooting
- API trouble, it returns "inactiveRpcError, timeout of 60 second exceeded.", and also "503 Getting metadata from plugin failed with error: ('invalid_grant: Token has been expired or revoked."
  - __description of trouble__: i ran the simplest code
    ```python
    for i, m in zip(range(5), genai.list_tuned_models()):
        print(m.name)
    ```
    And it gives error each time, saying that timeout exceeded and token expired.  
    However i check in google cloud that the credentials is enabled
  - __root cause__: the credential is enabled at google cloud's side, but in my local, the `client_secret.json` is not converted into usable crendientials.  
    In other words, the ADC is not ok.  
  - __solution__: i found it in the official doc of [oauth](https://ai.google.dev/gemini-api/docs/oauth),  
    I need to run the command in terminal:  
    ```shell 
    $ gcloud auth application-default login \
    --client-id-file=client_secret.json \
    --scopes='https://www.googleapis.com/auth/cloud-platform,https://www.googleapis.com/auth/generative-language.retriever'
    ``` 
    Then it will prompt that the credential is saved to ADC: "/home/huachen/.config/gcloud/application_default_credentials.json"  

    Not sure but maybe you also need to `$ gcloud auth application-default login`

- API trouble, still the same shitty code as above, now it says:  
  ```text
  PermissionDenied: 403 Request had insufficient authentication scopes. [reason: "ACCESS_TOKEN_SCOPE_INSUFFICIENT"
  domain: "googleapis.com"
  metadata {
    key: "service"
    value: "generativelanguage.googleapis.com"
  }
  metadata {
    key: "method"
    value: "google.ai.generativelanguage.v1beta.ModelService.ListTunedModels"
  }
  ]
  ```
  - __root cause__: problem at python code
  - __work around__: in this [github issue](https://github.com/google-gemini/generative-ai-python/issues/8),  
    I found a snippet:  
    ```shell
    curl -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
     -H "X-Goog-User-Project: $(gcloud config get project)" -X GET \
     "https://generativelanguage.googleapis.com/v1beta2/models"
    ```
    I tried it and it works. Then in the official doc, i also found  
    ```shell
    access_token=$(gcloud auth application-default print-access-token)
    project_id=gcryffin-prototype
    curl -X GET https://generativelanguage.googleapis.com/v1/models \
        -H 'Content-Type: application/json' \
        -H "Authorization: Bearer ${access_token}" \
        -H "x-goog-user-project: ${project_id}" | grep '"name"'
    ```
    This also works.  
    Then i found that the problem is at the python code, `genai.list_tuned_models()` does not work, `genai.list_models()` works


## Abbr.
| abbr    |  full name |
| ------- |  --------- |
| ADC |  application default credentail |




## what i skipped
- manage credentials myself with python (https://ai.google.dev/gemini-api/docs/oauth#manage-credentials)




to_resume:
in reiAyanami, try run the chunk "test"