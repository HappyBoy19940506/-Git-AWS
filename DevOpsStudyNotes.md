1. what is the difference between SVN and Git version control systems?
   1. Easy to roll back to the history version, especially when the host shuts down.
2. git add
   1. git add f.txt
3. Git commit
   1. git commit -m 'ID 1234545' f.txt
4. git clone
5. git pull
6. git push
7. git fork   git pull request git merge
8. git init
9. git status --- this can only show status on this specific branch.
10. git log （space and "B" key to next page and last page. click "Q" to quit the log page)
11. git log --pretty=oneline
12. git log --online
13. git reflog (will show how many steps if you need to roll back to that version)
14. git reset -- hard COMMIT ID  
15. git rest --(hard)(mixed)(soft) commitID
16. use git reset --hard to go back version if some files are deleted unexpectedly.
17. every time u do the git add. it will take a screenshot of the current working space if u change the files in the working space, You can use `git diff` to compare the differences.ss. 
18. `git diff`------compare diff between working space and cache space.
19. `git diff HEAD`----- compare differences between caching space and  HEAD in the commit repository.
20. `git diff COMMIT_ID`   ---- compare cache space and any commit_ID space.
21. `git branch -v` ---- show all braches including the latest commit info.
22. `git branch new_branch_name` create a new branch`new_branch_name`.
23. `git checkout branch_name` switch to another branch.
24. IF you want to dev-branch merge into the main branch.
    YOU should go into the Main branch And type ` git merge `
        So, in branch A, git merge branch B
        	---->` A absorbs B.  A takes away B features into A. so A grows. B stays.`
25. `git reflog` will show all logs on this computer, including all branch's activities.
26. Locally, if you only push one branch, the `origin` remote host can only record this particular branch. it has no record about other branches on your local computer.
27. `conflict resolve` finds the conflict file, after resolving,  use `git add` and `git commit -m 'xxx' ` to finish the conflict, it will then merge automatically.
28. test demo demo demo


​    

​    