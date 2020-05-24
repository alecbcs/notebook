# Solus Survival Guide

## eopkg:

##### Deleting the `eopkg` cache:

```bash
sudo eopkg dc
```

##### Repairing Broken Packages:

```bash
sudo eopkg check|grep Broken|awk '{print $4}'|xargs sudo eopkg -y it --reinstall
```

##### Rebuilding `eopkg` Database:

Sometimes this will help if `eopkg` is failing to install packages without error messages.

```bash
sudo eopkg -y rdb
```

##### Backing Up Installed Packages

```bash
eopkg li | cut -d " " -f 1 | tr '\n' ' ' > ~/InstalledPackages.txt
```
