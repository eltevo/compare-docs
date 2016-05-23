# High level vision of a collaborative Juypter environment

## How does a user interact with the system

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
	- keystone: keystone over LDAP
	- krb: kerberos over LDAP
- docker: module to wrap and execute kernels (and certain sevices)
- nfs: provide file access for kernels with custom user database
- jupyterhub: web-based access to files and scripts, spawn kernels
- gitlab: store and manage git repos


### Add-ons

- biostar: user forum
- binder: running ipynb directly from a git repo
- nbdashboard: render ipynbs into working html without the scripts
- influxdb+cadvisor+graphana for monitoring of the whole ecosystem

## User landing page

Primary purpose is to offer a selection of pre-built worksheets and notebooks for the general biologist public. Worksheets are nbdashboard documents organized into areas (field of biology) and projects. When a worksheet is selected it automatically spawns a docker to execute the kernel behind the worksheet. Notebooks work similarly, except allow editing of scripts. Output of worksheets is persisted in the users home directory. The landing page will provide links to the user's locally stored data, git repos and other authoring tools for more advanced users.

## Worksheets

Notebooks can be compiled into nbdashboard format which we will term worksheets as they only allow changing certain parameters but not the underlying code.

## Notebooks

These are real jupyter notebooks.

## Repositories

We should organize scripts into repositories. A repo will be the unit of code that can be shared among users, i.e., no single file sharing will be possible. Repos should be able to be shared among users, made public in groups, made public for everyone or made public on the landing page (latter will probably require admin interaction to make the repo "official").