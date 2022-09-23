Setup Notes
==============

### For VSCode operation:
- Fork repository on GitHub
- Start VS Code
- Make sure the following VS Code Extensions are installed
    - Python
    - optionally:
        - Git History
        - Jupyter - Jupyter notebook support
- Clone fork to local repo (Sht-Cmd-P, Git Clone)
- Set python/conda working environment to `hht`
    - In terminal (assuming Anaconda Miniconda is installed, which is true if VSCode Extension for Python is installed)
        - `% conda --version` to check Conda installed
    - Make sure your current working directory is the local project dir
        - `% ls`
        - or the terminal prompt should be something like
            - `(base) paulleiby@Paul-and-Libbys-MacBook-Pro hilbert-huang-transform %`
    - Create the new conda environment `hht` recommended by the repo yaml file in `env` directory 
        - `% conda env create -f ./env/hht.yml`
    - If needed, see more info on [Getting Started with conda environments](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html)
    - If you get the error message: "Solving environment: failed ... ResolvePackageNotFound"
    - Try the fix from [How to fix `ResolvePackageNotFound` error when creating Conda environment?(]https://stackoverflow.com/questions/58219956/)how-to-fix-resolvepackagenotfound-error-when-creating-conda-environment
    - CONDA_RESTORE_FREE_CHANNEL=1 conda env create -f ./env/hht.yml
    - Pro-Tip: Env-specific Settings re conda channel access
        - If you have a particular env that you always want to have access to the free channel but you don't want to set this option globally, you can instead set the configuration option only for the environment.

        ```sh
        conda activate my_env
        conda config --env --set restore_free_channel true

#### Option of Building the environment manually (yaml approach can fail)
- Warning: Take care to do this in a terminal outside of VSCode. It seemed the VSCode terminal may be influenced by/referencing the python interpreter from elsewhere than the Conda environment, e.g. from the Command Palette. 
    - Following seems to work best in a clean terminal launched from outside VSCode
    - o.w., I was getting stuck with the terminal referencing the wrong python (the 2.7 version installed with Mac OSX), and wrong pip
- create named environment
    - `conda create --name hht_pl python=3.9.7`  # specify python interpreter version at this point?
    - `conda activate hht_pl`
- Install necessary packages
    - `conda install numpy pandas matplotlib scipy ipykernel seaborn pytables`
        - if forget ipykernel above for ipython/jupyter notebooks: 'conda install -n hht_pl ipykernel --update-deps --force-reinstall'
    - `conda install scikit-image`
    - `conda install -c anaconda scikit-learn` # need to specify source channel
    - `conda install pywavelets` # while `conda install pywt` fails
      - Check that pip is accessible from python installed in current environment with `which pip`
        - should be `/Users/paulleiby/opt/anaconda3/envs/hht_pl/bin/pip`
    - `pip install PyEMD` # `conda install PyEMD` installs different package pyemd
        - docs on this package https://pyemd.readthedocs.io/en/latest/intro.html
        - The easiest way is to install `EMD-signal` from the PyPi, for example using
        
            ```
            $ pip install EMD-signal
            ```
        - Once the package is installed it should be accessible in your Python as `PyEMD`, e.g.
            ```
            from PyEMD import EMD
            ```


#### Fine Points (Ugh)
- ? "first always have conda install python=3.x.y in your conda environment such that subsequent pip installs go through conda installed pip?"
- ? "Use `pip` installed with `conda`, e.g. `~/anaconda/bin/pip`. Use it to install packages into a conda environment"
    - From <https://stackoverflow.com/questions/18640305/how-do-i-keep-track-of-pip-installed-packages-in-an-anaconda-conda-environment>
