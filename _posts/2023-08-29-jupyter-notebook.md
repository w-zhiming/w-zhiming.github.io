# Jupyter notebook install

## 安裝Jupyter
`pip3 install jupyter`

## 安裝java support

- Download ijava.zip from  https://github.com/SpencerPark/IJava/releases
- Extract  ijava.zip
- install by `python install.py`

## skill
-  shift + enter, run
-  A, B, (D,D) for insert before/after/delete line.


## set root dir
```
jupyter notebook --generate-config
vim .jupyter/jupyter_notebook_config.py

c.ServerApp.notebook_dir = '/Users/Bill_1/study/my-jupyter'
```