## Git and github
Git is a version control system. It tracks changes in sets of files for working in collaborative environments and allows you to go back to previous states. Github is the web-based service. 

You can make a free account [here](https://github.com/join?source=header-home), and make changes to files from your web browser, but for best results and maximum efficiency, you should also [install git on your computer](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) to access from the command line. 

Github works kind of like a google doc, but not in real time. You take a copy of a file, make changes to it, and then "commit" or save your changes to the original file.

### Getting Started
Once you have installed git, open up the terminal and navigate (using `cd`) to where you would like to make your first repository. A repository (often called 'repo') is a collection of files and their history, kind of like a folder on your computer.

To set the folder you are in as a git repository, use the command `git init`. You should get a message that says "Initialized empty Git repository in ..."

Next, make a file that you can add to your repository using a text editor like vim or nano. You can also make an empty text file using the command `touch testfile.txt`. You can use `git status` to see that your text file is listed as an untracked file.

To start tracking this file, you add it to the staging environment, or area where a file is stored temporarily before it is added to your repository. Use `git add testfile.txt` to add a file to the staging area, then use `git status` to see that your file is about to be committed.

Finally, use `git commit -m "This is my first commit"` to commit your file to the repository. You should always include a message at the end of your commit so that your collaborators will know what you are doing. Remember, your main collaborator is you two years from now!

### Branches, Github and Pull requests
One of the great things that git allows you to do is create [branches](https://git-scm.com/book/en/v1/Git-Branching-What-a-Branch-Is) to edit just one portion of the project without affecting the rest of the project. Once you are done editing your branch, you can [merge](http://git-scm.com/docs/git-merge) your changes onto the master branch.

If you're working collaboratively on a project, it's a good idea to use GitHub. After logging in to GitHub, click the green button that says "New Repository" to create a new repository. Add a name and a description and then click "Create Repository". You can then upload the repository you just created by following the directions listed under "…or push an existing repository from the command line."
```shell
git remote add origin https://github.com/username/newrepo.git
git push -u origin master
```
Now you should see your testfile in your repository on GitHub! 

### Github Commands

`git clone <URL>` 
	pulls a repository in using its URL that you get from github
  
`git add <file>` 
	adds a file to the staging environment
  
`git status` 
	shows what's different between us and the cloud
  
`git commit -m "added file to thing"` 
	commits change with a message
  
`git push` 
	syncs things on my machine to github.com
  
`git pull` 
	get of the changes
	
esc :wq is how you get out of changes.

See [this](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners) useful guide for more information on using git and github.
