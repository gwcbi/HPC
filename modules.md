## Modules

A module file contains all the information needed to configure the shell for an application. Once a module package is initialized, the environment can be modified using module-specific commands. You can use modules to gain accesss to software or to use different versions of packages.

To see what modules are available to use on Colonial One, use the command `module avail`

`module list`
will tell you what modules and versions you currently have loaded.

`module load module_name/version` 
loads a module. If you do not list a version number, the most recent version will automatically be loaded.

`module unload module_name`
unloads the named module, and reverts settings back to OS defaults.

You can use `source activate env_name` to activate an environment, or a space within a project with specific dependencies and settings that allow you to use a module. Use `source deactivate` to leave the environment.

To search for a module to find if it is available or what versions it is available in, use the comand `module spider modulename`

Sometimes you need to find out the address or other information about a module, so that you can see what is included with it. You can do this using the command `module show module_name`.
