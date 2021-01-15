---
title: Git
---

Binary search repo revisions in specified path:  
  `git bisect start —`  
   ...  

git
	List tags:
		`git tag`

git:
	Check if pwd is git repo:
	  [ -d .git ] || git rev-parse --git-dir > /dev/null 2>&1
	for repo in {this-repo,that-repo}; do cd ${repo}; git remote set-url origin git@github.com:some/${repo}.git; cd ..; done

