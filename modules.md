##Modules

A module file contains all the information needed to configure the shell for and application. Once a module package is initialized, the environment can be modified using module-specific commands. You can use modules to gain accesss to software or to use different versions of packages.

To see what modules are available to use on Colonial One, use the command `module avail`

`module list`
will tell you what modules and versions you currently have loaded.

`module load module_name/version` 
loads a module. If you do not list a version number, the most recent version will automatically be loaded.

`module unload module_name`
unloads the named module, and reverts settings back to OS defaults.