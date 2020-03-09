## Neurodesign: Optimal experimental designs for task fMRI

This file contains the description of the source files accompanying the manuscript published in Journal of Statistical Software (JSS).

### `code.py`

This file contains the source code to generate the examples and figures in the paper.

### `code-section-6.py`

This file contains the source code to perform the simulation study presented in section 6 of the paper.

### `neurodesign.zip`

This file contains the source code for the python package.  The current version is 0.2.0.  

##### Web links to specific version:

The [Github](https://github.com/neuropower/neurodesign/releases/tag/0.2.0) repository contains the source code available for collaboration and version control.

The [Read The Docs](https://readthedocs.org/projects/neurodesign/) link shows the documentation, generated with sphinx from the source code.

The code is distributed through [pypi](https://pypi.python.org/pypi/neurodesign/0.2.1) for easy installation.

##### Description of directory

- `docs/`

    This folder contains the source code to generate the documentation through sphinx.  Most of the functions/documentation is annotated in the source code and generated with sphinx' autodoc.

- `examples/`

    This folder contains 3 different scripts to use the package to evaluate designs or generate designs with the genetic algorithm.
    The files `JSS_example.py` contains the source code to generate the examples and figures in the paper.
    This is identical to the file in the main folder.

- `source/`

    Following a classical folder structure, this folder contains the source code for the package.  More details:
    - `src/media/`: This folder contains the logo used on reports.
    - `src/generate.py`: This library contains functions to generate sequences of stimuli/ITI's.
    - `src/neurodesign.py`: This library contains classes `design`, `experiment` and `population` to compute and optimise design efficiencies.
    - `src/msequence.py`: The library contains code to generate m-sequences.
    - `src/report.py`: The code in this library can be used to generate reports shown in the manuscript.
    - `CHANGES.md`: Changes per release
    - `setup.py`: installation file

    More details about each function can be found in the documentations online (or in docs).

### `neuropower.zip`

While the name, that we chose with only one application in mind, can be somewhat misleading, this is the source code for the full neuropowertools suite, consisting of neuropower and neurodesign.  Neuropower is an application for sample size calculations, and has not been reviewed as part of the JSS publication.  However, for a full replicability of the application, the source code for neuropower is also included.

The current  release is 0.2.0.

##### Web links to specific version:

The [Github](https://github.com/neuropower/neuropower-web/releases/tag/0.2.0) repository contains the source code available for collaboration and version control.

##### Description of directory

The are the most important folders:
- `apps`: This directory contains the main code for the web application.
- `apps/designtoolbox`: The main code for the GUI of neurodesign can be found here.  The GET/POST statements are accepted in `apps/designtoolbox/views.py`.

The other folders are directories used for the front-end created with django.  The files follow a logical structure in line with most django applications.

##### To reproduce the application

---
#### **Note: The following text is almost identical to the readme from [the NeuroVault github page](https://github.com/NeuroVault/NeuroVault) as our deployment is based on the neurovault architecture. Please see their page for more information/options.**
---

###### Installing dependencies
1. Fork the main repository (https://github.com/neuropower/neuropower-web)
2. Clone your fork to your computer: `git clone https://github.com/<your_username>/neuropower`
  3. *Warning: if you are using OS X you have to clone the repository to a subfolder in your home folder - `/Users/<your_username>/...` - otherwise docker-machine will not be able to mount code directories and may fail silently.*
3. Install docker >= 1.10 (If you are using OS X you'll also need [docker-machine](https://docs.docker.com/machine/install-machine/) and VirtualBox)
4. Install docker-compose >= 1.6
  5. If you are using OS X and homebrew steps 3 and 4 can be achieved by: `brew update && brew install docker docker-machine docker-compose`
6. Make sure your docker daemon is running and environment variables are configured (on OS X: `docker-machine create --driver virtualbox nv && docker-machine start nv && eval "$(docker-machine env nv)"`)

###### Pull the docker image

```
docker pull neuropower/neuropower
```
The docker image will be pulled from docker hub and made available on your local machine.


###### Webhook passwords

The application uses Django for deployment.  To use the application to its full extent, you need to set an environment variable **DJANGO_KEY**.  A key can be generated [here](http://www.miniwebtool.com/django-secret-key-generator/). Furthermore, an environment variable neets to be set for an opbeat account (**OPBEAT_ORG**, **OPBEAT_TOKEN** and **OPBEAT_APP_ID**), which is a logger as well as for mailgun (**MAILGUN_KEY**), which is an application to send and receive e-mails.  Accounts are free.


###### Running the server
```
docker-compose up -d
```
The webpage will be available at 127.0.0.1 (unless you are using docker-machine - then run `docker-machine ip nv` to figure out which IP address you need to use; remember that your enviroment variables need to be properly configured by running `eval "$(docker-machine env nv)"`).

You can also run the server in non detached mode (shows all the logs in realtime).
```
docker-compose up
```
###### Stopping the server
```
docker-compose stop
```
