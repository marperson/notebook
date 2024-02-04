# Notebook project
My daily notebook, learning and useful sites


## Installation
### Prerequites
* python 3.11
* mkdocs 
* GitHub repo should be public and enable GitHub page
* mkdocs.yml and docs folder should under root folder (after mkdocs new, copy them to root folder and delete newly generated project folder)

### Installaton
```console
python3.11 -m venv venv
source ./venv/bin/activate
pip install --upgrade pip
pip install -r rerquirements
pip install mkdocs
pip install mkdocs-material
```

### Create new project
```console
mkdocs new notebook
cd notebook
```

### Launch

```console
mkdocs serve
```


### Build static file
```console
mkdocs build
mkdocs build -f mkdocs.yml
```