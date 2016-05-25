# High level vision of a collaborative Juypter environment

## Users and groups

A user account will correspond to a single person. Users can form groups and assign roles to each other (read, write, admin).

Users will have a git repo to store their code and a limited amount of data relevant to the execution of their notebooks. Users will also have a home directory to store settings, temporary files and private data, like ssh keys to access git.

### User registration

There are many options. Do we give out passwords to everyone or accept eduroam (or maybe google) identities?

### User levels

There are three basic levels, depending on user involvment in script development:

- public: lay public, citizen scientists
- end-user: someone who wants to run existing scripts, possibly on own data
- script author: someone who can write their own scripts from scrath or edit and tweak existing scripts
- developer: someone who knows how to deal with all the tools (ipython, gitlab, databases, etc.) and want to use them all

We should strip down the user interface as much as we can for each user level.

### User groups for projects

Users should be able to interact on projects accessible to a group of users. Hence users should be able to form groups, assign users to a group with varying levels of access (admin, writer, reader) and create group-level files and scripts. Level of access will be determined by the role a user is in when accessing the resources of a group.

## System modules

### Core infrastructure modules

- auth: user authentication, provide a user database
	- user portal (registration, etc.)
	- ldap: user store
	- keystone: keystone over LDAP?
	- krb: kerberos over LDAP?
- docker: module to wrap and execute kernels (and certain sevices)
- nfs: provide file access for kernels with custom user database
- jupyterhub: web-based access to files and scripts, spawn kernels
- gitlab: store and manage git repos
- nginx: reverse-proxy web services
- nfs: server home directories

### Add-ons

- biostar: user forum
- binder: running ipynb directly from a git repo
- nbdashboard: render ipynbs into working html without the scripts
- influxdb+cadvisor+graphana for monitoring of the whole ecosystem

## User landing page

Primary purpose is to offer a selection of pre-built worksheets and notebooks for the general biologist public. Worksheets are nbdashboard documents organized into areas (field of biology) and projects. When a worksheet is selected it automatically spawns a docker to execute the kernel behind the worksheet. Notebooks work similarly, except allow editing of scripts. Output of worksheets is persisted in the users home directory. The landing page will provide links to the user's locally stored data, git repos and other authoring tools for more advanced users.

## Code execution

Code (jupyter notebooks, scripts, nbdashboard worksheets) will be stored in git repos with all relevant settings. When being executed, the git repo will be checked out to the user's home directory server from NFS. Changes to the code then can be commited locally and pushed back to the repo. The repo will have to have all necessary information about how to spawn a docker container for the repo. Here we either use proejct 'binder' directly, or come up with a custom solution.

## Repositories

We should organize scripts into repositories. A repo will be the unit of code that can be shared among users, i.e., no single file sharing will be possible. Repos should be able to be shared among users, made public in groups, made public for everyone or made public on the landing page (latter will probably require admin interaction to make the repo "official").

## Projects

### User projects

User create projects to start working on something new. A project will consist of a git repo that can contain source code, nbdashboard worksheets, data required by the workflow not available on-line elsewhere and documentation. A project will have a type which determines its activation: notebook, dashboard, shell execute etc.

### Group projects

Group projects are accessible by more than one user.

### Sharing projects

Project will be shared by forking into someone else's git repo. Public projects will be forked into a repo under the name of a public user. Versions of a project will be new commits to the git repo. Since a repo will be edited by one person only, merging, in normal circumstances, will not be an issue for personal projects. Changes from one project to another will be able to be done by making pull requests. We will hide git functionality from the users as much as we can and only allow simple operations. Developers will be able to open an advanced view or switch to console to get full access to the git repos.

## Code execution

## Types of projects

### Worksheets

Notebooks can be compiled into nbdashboard format which we will term worksheets as they only allow changing certain parameters but not the underlying code.

### Notebooks

These are real jupyter notebooks.

### Other code

We won't directly support executing binary code in a container.