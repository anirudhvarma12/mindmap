# Bash

## Git Alias

**Current Branch**
outputs the current branch name
```bash
# Define
git config --global alias.current-branch "rev-parse --abbrev-ref HEAD"

# Use
git current-branch
```

**Branch List**
list branches along with date, easily remove older branches
```bash
# Define
git config --global alias.branch-list "for-each-ref --sort='-committerdate' --format='%(refname)%09%(committerdate)' refs/heads"

# Use
git branch-list
```

**Changelog**
Generate formatted changelog, optionally get list of changes b/w two branches, commits or tags.

```bash
# Define
git config --global alias.changelog "log --pretty=format:'- %an : %s %n %H'  --no-merges"

# Use
git changelog branchA...master

# Send to file, use 
git changelog branchA...master > changelog.txt
```

## Docker Helpers

### Kill & Remove the latest container


```bash
# in .bashrc or .zshrc
alias docker_kill_latest="docker ps --format "{{.Names}}" --latest | xargs docker kill | xargs docker container rm "

# Use
docker_kill_latest
```

How it works?
- `docker ps --format "{{.Names}}" --latest` - Outputs the name of the latest container
- `| xargs docker kill` - feed the output from (1) into the `docker kill` command
- `xargs docker container rm` - (2) outputs the name of the container which can them be removed.

### Run different images with similar config
If we want to develop against docker images which require certain fixed options like port or volume mounts, we can create an alias to fix those while passing image ids at run time

```bash
# in .bashrc or .zshrc
alias run_dev_server="docker run -v /some_path_in_host:/some_path_in_container -p 5000:80"
```

After defining, we can run this easily by passing different image ids

```bash
run_dev_server 99f443911263
# or
run_dev_server 3065d7c5f71b
```