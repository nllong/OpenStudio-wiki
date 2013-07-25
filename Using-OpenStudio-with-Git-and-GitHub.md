> [Wiki](Home) ▸ **Using OpenStudio with Git and GitHub**

## Contents
- [Interacting with Git](Using-OpenStudio-with-Git-and-GitHub#interacting-with-git)
    * [GitHub for Windows](Using-OpenStudio-with-Git-and-GitHub#github-for-windows)
    * [Command Line](Using-OpenStudio-with-Git-and-GitHub#command-line)
    * [TortoiseGit](Using-OpenStudio-with-Git-and-GitHub#tortoisegit)
    * [SmartGit/Hg](Using-OpenStudio-with-Git-and-GitHub#smartgithg)
    * [Git Extensions](Using-OpenStudio-with-Git-and-GitHub#git-extensions)
- [Creating an SSH Key](Using-OpenStudio-with-Git-and-GitHub#creating-an-ssh-key)
- [Configuring Git Settings](Using-OpenStudio-with-Git-and-GitHub#configuring-git-settings)
- [Information for Third Party Collaborators](Using-OpenStudio-with-Git-and-GitHub#information-for-third-party-collaborators)
- [OpenStudio's Git Workflow](Using-OpenStudio-with-Git-and-GitHub#openstudios-git-workflow)
- [Cloning the Repository to your Local Computer](Using-OpenStudio-with-Git-and-GitHub#cloning-the-repository-to-your-local-computer)
- [Listing Branches](Using-OpenStudio-with-Git-and-GitHub#listing-branches)
- [Creating a Branch](Using-OpenStudio-with-Git-and-GitHub#creating-a-branch)
- [Switching to an Existing Branch](Using-OpenStudio-with-Git-and-GitHub#switching-to-an-existing-branch)
- [Committing Your Changes](Using-OpenStudio-with-Git-and-GitHub#committing-your-changes)
- [Updating Your Local Repository, and Stashing](Using-OpenStudio-with-Git-and-GitHub#updating-your-local-repository-and-stashing)
- [Reintegrating a Branch into Develop](Using-OpenStudio-with-Git-and-GitHub#reintegrating-a-branch-into-develop)
- [Pushing All of Your Local Commits to GitHub](Using-OpenStudio-with-Git-and-GitHub#pushing-all-of-your-local-commits-to-github)
- [Deleting A Branch](Using-OpenStudio-with-Git-and-GitHub#deleting-a-branch)
- [Other Useful Commands](Using-OpenStudio-with-Git-and-GitHub#other-useful-commands)
    * [Getting the Latest Commit Hash](Using-OpenStudio-with-Git-and-GitHub#getting-the-latest-commit-hash)
    * [Viewing the Log](Using-OpenStudio-with-Git-and-GitHub#viewing-the-log)
    * [Reverting All Working Directory Changes](Using-OpenStudio-with-Git-and-GitHub#reverting-all-working-directory-changes)
    * [File Operations](Using-OpenStudio-with-Git-and-GitHub#file-operations)

## Interacting with Git
Depending on your operating system and personal preferences, there are a variety of options for interacting with the repository on your computer:

### GitHub for Windows
A very simple, intuitive GUI for Windows users.  This GUI will be sufficient for most third party contributors.  Only works with github.com.

[Windows](http://github-windows.s3.amazonaws.com/GitHubSetup.exe)
### Command Line
deal for power users and for running commands directly on the repository.  It also includes a basic Git GUI, as well as gitk, a low-level Git GUI.  This may be a prerequisite for some of the following tools, and also comes packaged with some of the following tools.

[Windows](http://git-scm.com/download/win) – [OS X](http://git-scm.com/download/mac) – [Linux](http://git-scm.com/download/linux)
### TortoiseGit
A helpful GUI for normal users who are already familiar with TortoiseSVN and its Explorer integration.  In some cases, the interface can be unintuitive.

[Windows](https://code.google.com/p/tortoisegit/wiki/Download)
### SmartGit/Hg
The best graphical interface for Git – Understand that the non-commercial license can ONLY be used for open-source, non-commercial projects, such as OpenStudio.

[Windows](http://www.syntevo.com/smartgithg/download?file=smartgithg/smartgithg-win32-setup-jre-4_6.zip) – [OS X](http://www.syntevo.com/smartgithg/download?file=smartgithg/smartgithg-macosx-4_6.dmg) – [Linux](http://www.syntevo.com/smartgithg/download?file=smartgithg/smartgithg-generic-4_6.tar.gz)
### Git Extensions
A useful GUI for visualizing tree changes, Git Extensions also includes context-menu integration in Explorer.

[Windows](http://sourceforge.net/projects/gitextensions/files/latest/download?source=navbar) – [OS X](https://git-extensions-documentation.readthedocs.org/en/latest/getting_started.html#installation-mac) – [Linux](https://git-extensions-documentation.readthedocs.org/en/latest/getting_started.html#installation-linux)
## Creating an SSH Key
Establishing a secure connection to GitHub.com can be achieved over HTTPS with a username and password, or with SSH keys and an optional passphrase.  SSH keys are highly recommended for security and performance.  GitHub has thoroughly documented the process: Carefully follow the instructions for your platform to create an SSH key and add it to GitHub.com.

[Windows](https://help.github.com/articles/generating-ssh-keys#platform-windows) – [OS X](https://help.github.com/articles/generating-ssh-keys#platform-mac) – [Linux](https://help.github.com/articles/generating-ssh-keys#platform-linux)

On Windows, some GUI tools like TortoiseGit require a Putty SSH key instead of an OpenSSH key.  To convert the key you just generated to Putty format, launch Puttygen from the start menu, load your private key (~/.ssh/id_rsa), and then save the new private key (~/.ssh/id_rsa.ppk):

## Configuring Git Settings
To start, you should configure some of Git’s global settings (which are saved in ~/.gitconfig).  If you leave out the --global flag, the settings will be applied only to your current repository, which is also fine.
```sh
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global push.default simple
```
The [user.name setting](https://help.github.com/articles/setting-your-username-in-git) can be anything, although we recommend using your real name.  The user.email setting should match an email that you have associated with your GitHub account.  Finally, the push.default setting is just to set the push behavior to the new default for Git 2.0 and avoid notices on the command line.

There are [many more configuration settings](http://git-scm.com/book/en/Customizing-Git-Git-Configuration) as well.  To see all of your current settings:
```sh
git config --list
```
## Information for Third Party Collaborators

## OpenStudio's Git Workflow






## Cloning the Repository to your Local Computer
## Listing Branches
## Creating a Branch
## Switching to an Existing Branch
## Committing Your Changes
## Updating Your Local Repository, and Stashing
## Reintegrating a Branch into Develop
## Pushing All of Your Local Commits to GitHub
## Deleting A Branch
## Other Useful Commands
### Getting the Latest Commit Hash
### Viewing the Log
### Reverting All Working Directory Changes
### File Operations