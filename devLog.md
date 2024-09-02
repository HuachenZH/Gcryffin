# devLog

## info
- gemini vs vertex ai:
  - gemini: is the LLM
  - vertex ai: is the platform to interact and fine tune gemini
- official doc (this is an overview of procedures): [fine tuning gemini with api](https://ai.google.dev/gemini-api/docs/model-tuning)
  - when you are ready to start: [Fine-tuning tutorial](https://ai.google.dev/gemini-api/docs/model-tuning/tutorial?lang=python)
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





## Obstables
- while preparing virtualenv, `pyenv virtualenv 3.12.5 Gcryffin`, it gives: "pyenv: no installed versions match the prefix `-q'".  
  However it seems that the virtualenv is still created.  



to_resume:
- setup oauth: https://ai.google.dev/gemini-api/docs/oauth

