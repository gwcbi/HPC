# Creating and using environments using conda

If you are working on a project that needs specific versions of python or other softwares, it may be useful for you to make and use a virtual environment. Conda allows you to make virtual environments where specific versions of packages and their dependencies can be stored, so instead of loading a lot of different modules with different versions, you can activate an environment where all of a package's specific required dependencies are stored.

To make or use an environment using conda, first load miniconda:
`module load miniconda3`

You can make sure that conda is installed an running on your system by typing: `conda --version`

Note: if you are using miniconda, especially CBI's version of miniconda3, you should not have any modules loaded prior to loading miniconda3 or load additional modules while you have miniconda3 loaded. Doing so can cause big problems. You must open a different terminal window and load other modules there.

After installing conda, you need to create channels. It's important to add them in this order so that conda-forge is the highest priority.
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

Now that you have conda loaded, you can create your environment. You do this by using the command `conda create -n name_of_environment name_of_package`. For example, if I want to create an environment called humann2 with the metaphlan2 package installed, I would use the command:
`conda create -n humann2 metaphlan2`

Once the package is installed with all of its dependencies, you can then use:
`conda activate humann2` to use your environment. From there, you can run commands with the correct package versions.

Once your environment has been activated, you can see the packages that are in the environment using `conda list`

`conda info --envs` shows all your enivronments available

`conda deactivate` will deactivate the current environment

To check if they have a recipe or program, see the [bioconda recipe index](https://bioconda.github.io/conda-recipe_index.html).

For more information on using conda, see the [conda documents](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
