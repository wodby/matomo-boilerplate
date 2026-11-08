# Matomo boilerplate

Keep your own Matomo plugins in Git and deploy them with Wodby. This
repository holds only your plugins: Wodby builds them on top of the prebuilt
[`wodby/matomo`](https://github.com/wodby/matomo) image, so Matomo itself
keeps getting updates from Wodby.

Use it with the [Matomo with custom plugins](https://github.com/wodby/service-matomo-custom)
service. For Matomo without your own plugins, use the
[Matomo](https://github.com/wodby/service-matomo) service instead.

## Adding a plugin

Put each plugin in its own directory under `plugins/`, named like the plugin:

```
plugins/
  MyPlugin/
    plugin.json
    MyPlugin.php
```

On every deployment Wodby:

- installs Matomo on the first deployment, or updates its database;
- activates every plugin in `plugins/`;
- deactivates plugins you removed from `plugins/` since the last deployment.

The build fails if a directory in `plugins/` has no `plugin.json`, or has the
name of one of Matomo's own plugins.

## Marketplace plugins

Plugins from the Matomo Marketplace don't belong here. Install them from
Matomo's administration: Wodby keeps them in the files storage, where they
survive deployments.

## Files

| Path | Purpose |
| --- | --- |
| `plugins/` | Your Matomo plugins |
| `.wodby/pipeline.yml` | The Wodby CI pipeline that builds and deploys the image |
| `.dockerignore` | Files left out of the image |
