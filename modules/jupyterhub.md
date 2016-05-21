For all user based jupyter applications we shall use jupyterhub. 
Jupyterhub is a multi user environment for single user jupyter servers.
For the sake of modularity we aim to put the hub it self in to a docker container.
[Jupyterhub](https://github.com/jupyterhub/jupyterhub-deploy-docker) deployment setup
seems to be a neatly boundled up solution for containerized hub deployment. 
This setup also includes an alternative to user data management,
namely keeping all user data in docker [data voulmes](https://docs.docker.com/engine/userguide/containers/dockervolumes/).
