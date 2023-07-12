:construction: Under construction !!! :construction:

[[_TOC_]]

# `git`

## About `git`

*TODO*

## `git`: what NOT to do

- always check the status, `git status`, **before** doing `git add`
- avoid using the flag `--all` with `git add`, except you really know what you are doing
- do **NOT** add large and/or binary files
  - for exceptions use `git-lfs` (see below)

## `git`: basic commands

*TODO*

# GitHub

## GitHub: useful links

- [project member permissions](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/managing-teams-and-people-with-access-to-your-repository)

## GitHub: access

There are two options to access repositories from the UKCEH: SSH and HTML.

### Access via SSH

You need to add your public ssh key(s) to GitHub.
Specifying it in LUMS is **not** sufficient as there is no synchronization.

- Click on your logo (upper right corner) -> Settings -> SSH Keys
- Copy and paste your **PUBLIC** SSH key into the box (optionally add a title and expiration date)

**Note**: do **NOT** put your **PRIVATE** key online! Ever!

Optionally, you can add GitHub to your SSH configuration: specify the connection in your ssh-config (typically under `$HOME/.ssh/config`):

```
Host github-server.com
    HostName github-server.com
    User git # do NOT change
    Port 8022
    IdentityFile ~/.ssh/id_rsa # adjust if needed
```

- do not change the `User`
- adjust the path for `IdentityFile`, i.e. it should be the file containing the private key for the registered public key

### Access via HTML

Using HTML, you need to specify your username and password, i.e. the credentials defined in LUMS which you also use to login to UKCEH's GitHub.

If you use Two-Factor Authorization (2FA), this is [no longer possible](https://docs.github.com/ee/user/profile/personal_access_tokens.html), your "normal" credentials no longer work and you *must* create and use Personal Access Tokens:

> Personal access tokens are required when Two-Factor Authentication (2FA) is enabled
> This may require you to handle those tokens separately, e.g., using LastPass.
> Access via *ssh* is thus encouraged as you anyways have to create and store the key-pair.

## GitHub: renaming and transferring repositories

- Change displayed project's name (will **NOT** change the URL or namespace)
  - go to `Settings` -> `General` -> change the string in the field `Project name`
- Change project's **URL** (will **NOT** change displayed name or namespace)
  - [docs](https://docs.github.com/12.10/ee/user/project/settings/#renaming-a-repository)
  - if you try to push to the old URL `git` will tell you to do `git remote set-url origin <new url>`
- Change project's **namespace**, i.e. transfer your project:
  - [docs](https://docs.github.com/12.10/ee/user/project/settings/#transferring-an-existing-project-into-another-namespace)
  - also see notes below

## GitHub: create a new project

To create and setup a new project in a GitHub group (e.g. in `moleco`):

- create a new project
- in most cases you will need the `maintainer` permissions to maintain your project
  - if you are not already an `owner` or `maintainer`, ask an `owner` or `maintainer` to change your permissions

## GitHub: transfer a project

To transfer an existing project to a GitHub group (e.g. to `moleco`):

- make sure that you are a member of the group
- ask an `owner` in `moleco` to give you `maintainer` permissions in the **group**
- [transfer](https://docs.github.com/12.10/ee/user/project/settings/#transferring-an-existing-project-into-another-namespace) your project to `moleco`
- inform the `moleco` `owner` so he can restore your **original group permissions**

See [here](https://github.com/groups/moleco/-/group_members) for a list of `moleco` group members.

## GitHub: adding members to a project

- you need to be at least an `owner` or `maintainer` of the project
- you should be able to add any UKCEH GitHub member to a project and set their permissions

# Useful `git` and GitHub features

- use `branches`, e.g. different users should work on different `branches`
- the `master` branch is for the final code version(s)
- use `tags` to add version labels
- use `submodules` to add other repositories, e.g.
  - tools which cannot be installed automatically and have no precompiled binaries
  - code from other projects
- create milestones and issues to define TODOs
  - milestones can be attached to issues
  - issues can be references in commit messages, e.g. `commit -m "fixed bug #<issue number>"`
- in case of multiple users: having separate sub-folders for code might make it easier to merge different branches
  - useful if the tasks are rather independent
- use `git-lfs` to store large files
  - [git-lfs](https://git-lfs.github.com/)
  - use only if storing files somewhere else (e.g. on [zenodo](https://zenodo.org/) and [fighare](https://figshare.com/)) is not an option and these files are relevant for your code
