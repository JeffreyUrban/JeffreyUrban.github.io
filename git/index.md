---
title: Git
---

# Binary search repo revisions in specified path

`git bisect start —`  

# List tags:

`git tag`

# Check if pwd is git repo

`[ -d .git ] || git rev-parse --git-dir > /dev/null 2>&1`

# Change origins to Git SSH

```
for repo in {this-repo,that-repo}
	do cd ${repo}
	git remote set-url origin git@github.com:some/${repo}.git
	cd ..
done
```
