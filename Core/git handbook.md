1. `git pull`: if conflict, **accept ourselves**, then commit message: "FI from master".
2. `git stash push`: save your work then free to switch branch
3. `git stash pop`: get your work back
4. `git reset --hard`: undo your work
5. `git checkout master -- WebApp/Sources/xml/DataDef.Logging.xml`: undo changes on current branch, so same to master


## GIT LOG
```bash
git log -3
git log --since=2024-11-11
git log --until="3 days ago"
git log --after=2.weeks --before=3.days
git log --author="Teng Xing Tan"
git log --grep="bug" # filter commit message by keyword "bug"
git log <SHA>..<SHA>
git log index.html
```


# Production Branching Strategy
![[Pasted image 20241211173707.png]]
