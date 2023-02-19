# git+drives experiment
1. Maintainer initializes the project and does initial seed:
```bash
[maintainer:~/project]$ drives touch --corestore .pit/corestore
keyA
[maintainer:~/project]$ drives mirror .git keyA --corestore .pit/corestore
[maintainer:~/project]$ drives seed keyA --corestore .pit/corestore
```

2. Second user clones manually:
````bash
[contributor:~/]$ mkdir project
[contributor:~/]$ cd project/
[contributor:~/project]$ git init . # empty repo without commits.
[contributor:~/project]$ ls -a
. .. .git
[contributor:~/project]$ drives mirror keyA .pit/repos/main --corestore .pit/corestore
[contributor:~/project]$ git remote add -f origin .pit/repos/main
[contributor:~/project]$ git merge origin/master
[contributor:~/project]$ ls -a
. .. .git .pit README.md
```

3.  Attempt upgrade to Contributor.
```bash
[contributor:~/project]$ drives touch --corestore .pit/corestore
keyB
[contributor:~/project]$ drives mirror .git/ keyB --corestore .pit/corestore
[contributor:~/project]$ drives seed keyB --corestore .pit/corestore
```

And this is where things get wierd: 

 4.  Maintainer adds contributor
```bash
[maintainer:~/project]$ drives mirror keyB .pit/repos/bob --corestore .pit/corestore
[maintainer:~/project]$ git remote add -f bob .pit/repos/bob
```
# result
At this point everything works, maintainer sees the contributor drive, BUT :
- :x:  when maintainer seeds on keyA no subsequent commits get downloaded from keyB.
- :x: if additional contributor clones using keyA, they don't get keyB.
