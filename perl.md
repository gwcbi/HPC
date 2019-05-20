# Setting up a local perl library

### _Q: How do I install perl modules when I don't have root access?_
### _A: Set up a local perl library!_

In order to install perl modules on C1, you will need to create a local perl library.
In this example we will create our local library in a hidden directory within your home directory.

## 1. Create a new hidden directory, `.perl`

```bash
cd $HOME
mkdir .perl
```

## 2. Install the `cpanm` package manager and the `local::lib` package.

#### (Adapted from [this stack exchange answer](https://stackoverflow.com/a/2980715))

```bash
wget -O- http://cpanmin.us | perl - -l $HOME/.perl5 App::cpanminus local::lib
```

This what what the commands do:

`wget -O- http://cpanmin.us` fetches the latest version of `cpanm` and prints it to `STDOUT` which 
is then piped to `perl - -l $HOME/.perl5 App::cpanminus local::lib`.
The first `-` tells `perl` to expect the program to come in on `STDIN`, 
this makes `perl` run the version of `cpanm` we just downloaded. `perl` passes the rest of the arguments 
to `cpanm`. The `-l $HOME/.perl5` argument tells cpanm where to install Perl modules, 
and the other two arguments are two modules to install. [`App::cpanmins`](https://metacpan.org/pod/App::cpanminus)
is the package that installs `cpanm`.
[`local::lib`](https://metacpan.org/pod/local::lib) is a helper module that manages the 
environment variables needed to run modules in local directory.

## 3. Set environment variables using `local::lib`

```bash
eval $(perl -I $HOME/.perl5/lib/perl5 -Mlocal::lib=$HOME/.perl5)
```

## 4. Add commands to `.bashrc`

This enables the local perl library every time you login:

```bash
echo 'eval $(perl -I $HOME/.perl5/lib/perl5 -Mlocal::lib=$HOME/.perl5)' >> .bashrc
echo 'export MANPATH=$HOME/.perl5/man:$MANPATH' >> .bashrc
```

## 5. Install additional perl packages

Perl packages can now be installed using `cpanm Module::Name`. 
For example, run the following command to install `Log4perl`:

```bash
cpanm Log::Log4perl
```
