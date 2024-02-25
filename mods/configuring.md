---
description: How to configure Geode mods using mod.json
---

# Configuring mods

Geode mods are configured through a file called `mod.json`, located at the root of your project. The file contains general information about the mod, such as the name, ID, version, and also things like settings, resources, and dependencies.

If you're using VS Code, you should [install the Geode VS Code extension](https://marketplace.visualstudio.com/items?itemName=GeodeSDK.geode), as it provides automatic checking for `mod.json` and intellisense for what keys are available.

## Required settings

There are 6 required properties for every mod: the target Geode version, the ID and name of the mod, its developer, and its version.

```json
{
    "geode": "v1.0.0",
    "gd": "2.200",
    "id": "my.awesome-mod",
    "name": "My Awesome Mod",
    "version": "v1.0.0",
    "developer": "Me"
}
```
You can also use the `developers` property instead of `developer`

```json
{
    "geode": "v1.0.0",
    "gd": "2.200",
    "id": "my.awesome-mod",
    "name": "My Awesome Mod",
    "version": "v1.0.0",
    "developers": ["Me","Friendly Developer"]
}
```

## List of keys

### `geode`

The target Geode version. Should be in the format of an exact version, such as `v1.0.0` or `v1.2.0`. The target version should always be the exact version of Geode you are developing with.

### `gd`

The target Geometry Dash version exactly, or `*` for **any** GD version (whether your mod actually works on any GD version is your responsibility.) 

This key can either be a string, or an object for specifying per platform GD version:
```json
{
    "gd": "2.204"
}
```
or
```json
{
    "gd": {
        "android": "2.200",
        "win": "2.204"
    }
}
```
The valid platform keys are `win`, `mac`, `android` and `ios`.
```json
{
    "gd": "*" // Mod works on any gd version
}
```


### `id`

The ID of the mod. May only contain lowercase ASCII characters (`a-z`), periods (`.`), underscores (`_`) and dashes (`-`). Otherwise may be formatted in any way you like, but it is common to make the ID be in the form of `developer.mod-name`. The ID is used to uniquely identify the mod in things such as folder names, URLs, and save data.

### `name`

The name of the mod that is displayed in-game, and in other situations where the mod is displayed. May be any UTF-8 valid string, however do note that GD does not normally support many characters beyond the ASCII character set, so unless the user has a mod or texture pack that extends the character set, not all characters in the name may be displayed.

### `version`

The version of the mod; should follow [semver](https://semver.org), especially if the mod can be used as a dependency (see [the API key](#api)).

### `developer`

The name of the mod's developer. Should be a single name, like "HJfod" or "Alk". If the mod has multiple developers, this should be a team name like "Geode Team".

### `developers` 

The name of the mod's developers. Replaces developer. Can be a single name, like ["HJfod"] or ["Alk"]. If the mod has multiple developers, you should list the names of each developer, as the developers property is a(n) list/array. The first developer listed is the main developer. If you have 3 or more developers listed, the developers names will show main developer + 2 more. If you have 2 developers listed, the developers names will show Developer 1 & Developer 2. 

### `description`

A short description of the mod. Should only be a single sentence; for longer descriptions, see [about.md](/mods/md-files.md).

### `repository`

The Git repository of the mod.

### `issues`

Describes where users can report problems with the mod. Value is an object with the following properties:

 * `info` - Free-form description of where / whom to report issues to

 * `url` - URL to a Discord server, GitHub repository etc. where the issues are reported

### `dependencies`

The dependencies of a mod; see [Dependencies](/mods/dependencies.md) for details

### `settings`

The settings of a mod; see [Settings](/mods/settings.md) for details

### `resources`

The resources of a mod; see [Resources](/mods/resources.md) for details

### `early-load`

If true, specifies that this mod must have finished loading before the loading screen appears in GD. For example, [TextureLdr](https://github.com/geode-sdk/textureldr) uses this to apply texture packs at startup.

### `api` (since Geode `v1.0.0-beta3` / CLI `v1.4.0`)

Specifies that this mod can be [used as a dependency](/mods/dependencies.md). Value is an object with the following properties:

### `headers`

An array specifying the list of headers that should bundled with this mod. Supports [globbing](/mods/resources.md).
