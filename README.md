# ⚠️⚠️⚠️ DEPRECATED ⚠️⚠️⚠️ #

SimpleLocalProcessSpawner is now a [part of JupyterHub core](https://github.com/jupyterhub/jupyterhub/blob/3800ceaf9edf33a0171922b93ea3d94f87aa8d91/jupyterhub/spawner.py#L1647). 
You can migrate to it by setting:

```python
c.JupyterHub.spawner_class = "simple"
```

The JupyterHub documentation has more information on [how to setup a development environment](https://jupyterhub.readthedocs.io/en/stable/contributing/setup.html)

# JupyterHub Simple Spawner #

A very simple [Spawner](https://github.com/jupyter/jupyterhub/wiki/Spawners) for
[JupyterHub](https://github.com/jupyter/jupyterhub) that spawns local processes.

**DO NOT USE THIS FOR PRODUCTION USE CASES!** It is incredibly insecure, and
offers no user isolation *at all*. This is intended only for testing purposes.

## What? ##

It spawns new notebooks for users, but as the same user as jupyterhub. This
has the following advantages:
    1. No need to run JupyterHub as root
    2. Users don't need to exist in the system.

However, it offers absolutely *no* isolation whatsoever, so users can very
easily mess with each others' processes. So do not use this in a production
environment of any sort.

## Installation ##

You can install it from pip via:

```
pip install jupyterhub-simplespawner
```

You can set JupyterHub to use this spawner with the following line in your
`jupyterhub_config.py`:

```
c.JupyterHub.spawner_class = 'simplespawner.SimpleLocalProcessSpawner'
```

## Configuration ##

You can configure where the users have their homes with the `home_path_template`
config parameter. You can use `{userid}` and `{username}` in the template and
they will be expanded to appropriate values.

## Use with... ##

This can be used to good effect with the [DummyAuthenticator](https://github.com/yuvipanda/jupyterhub-dummy-authenticator)
to provide simple testing environments.
