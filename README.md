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

## GitHub setup
* repo must be public
* go to setting -> pages, "Deploy from branch", "gh-pages", root folder
* docs and mkdocs.yml are at root foler level, or use mkdocs serve -f $path_to_mkdocs_yml
* Build https://squidfunk.github.io/mkdocs-material/publishing-your-site/#with-github-actions-material-for-mkdocs 
  * build with github actions, create a new workflow to watch push 
  ```yaml
    name: ci 
    on:
      push:
        branches:
          - master 
          - main
    permissions:
      contents: write
    jobs:
      deploy:
        runs-on: ubuntu-latest
        steps:
          - uses: actions/checkout@v4
          - name: Configure Git Credentials
            run: |
              git config user.name github-actions[bot]
              git config user.email 41898282+github-actions[bot]@users.noreply.github.com
          - uses: actions/setup-python@v5
            with:
              python-version: 3.x
          - run: echo "cache_id=$(date --utc '+%V')" >> $GITHUB_ENV 
          - uses: actions/cache@v4
            with:
              key: mkdocs-material-${{ env.cache_id }}
              path: .cache
              restore-keys: |
                mkdocs-material-
          - run: pip install mkdocs-material 
          - run: mkdocs gh-deploy --force
  ```
  
    simple yaml:
    ```yaml
    name: Build and deploy mkdocs
    on:
      push:
        branches:
          - main
    permissions:
      contents: write
    jobs:
      deploy:
        name: Deploy docs
        runs-on: ubuntu-latest
        steps:
          - name: install tree
            run: sudo apt-get install -y tree
          - name: Checkout main
            uses: actions/checkout@v4
    
          - name: Setup Python
            uses: actions/setup-python@v5
            with:
              python-version: 3.x
    #      - run: pip install mkdocs
          - run: pip install mkdocs-material  #will install mkdocs as well
    #      - run: pwd
    #      - run: ls -al
    #      - run: ls -al ./docs
    #      - working-directory: ./docs
    #        run: mkdocs gh-deploy --force
          - run: |
              pwd
              tree .
              mkdocs gh-deploy --force --verbose
              tree .
    ```
  * Build manually, fetch and switch to "gh-pages" branch, then use below command to generate all file, commit to "gh-pages" branch
  ```console
  mkdocs gh-deploy --force
  ```
  
* Note:
    - github action will have another workflow, no need to run it manually, use above github workflow or manual process