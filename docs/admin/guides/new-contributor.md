# New contributors

Things to do for new contributors.

## Build contributors

- Grant them OP on the build server (feel free to give this out to anyone, the server has frequent backups)

## Code contributors

- Invite them to the GitHub organisation, and encourage minigame repositories that are going on the main server to be transfered to the org.

## Assigning roles

Try to complete all of these when you get the chance

### Discord

Grant them the contributor role, along with whichever specific roles fit (eg. code contributor, build contributor, translations contributor, etc).

### In game

```mcfunction
/role assign <username> contributor
# Code contributor
/role assign <username> dev
/role assign <username> builder
```

### Website cards

1. Create a new file in the [`NucleoidMC/nucleoid-contributors`](https://github.com/NucleoidMC/nucleoid-contributors), under the folder `data/people/` named `theirusername.toml` (use all lower case, and no spaces or special characters)..
2. Fill out the file using the following template:
```toml
name = "their perfered display name (if unsure, ask)"
groups = [
    "code",
    "building",
    "art",
    "community",
    "translations",
    "contributor", # generic contributor role, should only be added if none of the others apply
]

[socials]
minecraft = "their minecraft uuid (for consistency, remove the -)"
```
3. Commit the file back to the repo, and run `sudo git pull` in `/var/www/nucleoid-contributors` (unfortunately we don't have auto-deployment yet, poke Ash if you get annoyed by this).
4. Invite them to update the file (or if they're not familiar with GitHub, provide extras for you to put in) - see [Ash's card](https://github.com/NucleoidMC/nucleoid-contributors/blob/main/data/people/ashhhleyyy.toml) as a template. Members of the GitHub org should automatically get write permissions to the repo, so can update their own.
