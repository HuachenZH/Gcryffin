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


To install or remove components at your current SDK version [491.0.0], run:
  $ gcloud components install COMPONENT_ID
  $ gcloud components remove COMPONENT_ID

To update your SDK installation to the latest version [491.0.0], run:
  $ gcloud components update




## what i skipped
- manage credentials myself with python (https://ai.google.dev/gemini-api/docs/oauth#manage-credentials)




to_resume:
get started fine tuning:  
- follow the github notebook: https://github.com/google/generative-ai-docs/blob/main/site/en/gemini-api/docs/model-tuning/python.ipynb
- it the info is not sufficient, go read semantic retrieval

