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

On Windows, some GUI tools like TortoiseGit require a Putty SSH key instead of an OpenSSH key.  To convert the key you just generated to Putty format, launch Puttygen from the start menu, load your private key `~/.ssh/id_rsa`, and then save the new private key `~/.ssh/id_rsa.ppk`:

## Configuring Git Settings
To start, you should configure some of Git's global settings, which are saved in `~/.gitconfig`.  If you leave out the `--global` flag, the settings will be applied only to your current repository, which is also fine.

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
git config --global push.default simple
```

The [user.name setting](https://help.github.com/articles/setting-your-username-in-git) can be anything, although we recommend using your real name.  The user.email setting should match an email that you have associated with your GitHub account.  Finally, the push.default setting is just to set the push behavior to the new default for Git 2.0 and avoid notices on the command line.

There are [many more configuration settings](http://git-scm.com/book/en/Customizing-Git-Git-Configuration) as well.  To see all of your current settings:

    git config --list

## Information for Third Party Collaborators
If you'd to use a GUI for managing the repository, follow the [GUI instructions for third party collaborators](instructions-for-third-party-collaborators).

Otherwise, in the following clone step, replace _NREL_ in the clone URL with your GitHub username.
Finally, when your changes are ready to be approved for inclusion in the main OpenStudio repository, click the Compare button in your fork and follow [GitHub's instructions](https://help.github.com/articles/creating-a-pull-request) for submitting a pull request.

## OpenStudio's Git Workflow
All work should be completed in feature branches created from the _develop_ branch.  Biweekly iterations will be branched from _develop_ to _iteration_, and releases will be branched from _iteration_ to _master_.  No commits or development work should be made to _iteration_ or _master_ unless you are authorized to modify that iteration or release.

## Cloning the Repository to your Local Computer
Now that you have your SSH key configured, you can create a local clone of the repository.  If you want to download the latest stable release, select the _master_ branch.  Otherwise, if you want to work with the latest development code, use the _develop_ branch:

    git clone -b develop git@github.com:NREL/OpenStudio.git .

The final dot is required if you want to clone into your current directory.  Without the dot, this command will create a directory called OpenStudio and clone into that.  This clone operation will download ~87MB of files and reconstruct the full develop branch within that directory (which will then total ~337MB).  This command also makes all branches available locally.

If you choose to use the HTTPS protocol instead of SSH, you may encounter a SSL certificate issue.  This can be caused by enterprise network equipment.  If you determine that the warning is a false positive, you can instruct Git to ignore the warning:

    git config http.sslVerify "false"

## Listing Branches
When viewing branches, the current branch is marked with an asterisk.  To view local branches:

    git branch

To view remote branches that you have available:

    git branch -r

To view all local and remote branches that you have available:

    git branch -a

## Creating a Branch
To create a new local branch and switch to it:

    git checkout -b mynewbranch

To make this branch available to everyone, push the branch to GitHub:

    git push origin mynewbranch

Alternatively, you can do both these steps by typing the new branch name into the branch filter on GitHub and click Create branch:


## Switching to an Existing Branch
To switch to a remote branch that you haven’t already downloaded (branches that were created after you cloned the repository or after your most recent fetch/pull), you should run the following command to get an updated list of remote branches and prune your branches.  Pruning removes all branches that have been deleted from GitHub:

    git fetch -p

Then, you can checkout and switch to any local or remote branch with the following command:

    git checkout mybranch
        or
    git checkout develop

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