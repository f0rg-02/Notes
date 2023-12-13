---
Name: git push
Platform: Linux
tags: Resources
---
Commands to push new changes to GitHub repository.

Clone GitHub repo.
`git clone <repo>`

Add all the new files that need to be committed and pushed.
`git add .`

Commit the changes with a short description.
 `git commit -m "Add existing project files to Git"`

Git remote add origin isn't always needed if git cloned from GitHub or similar.
`git remote add origin **<repo.**`

Push the changes to origin.
`git push -u -f origin`