Description:

We have:
0) git log --oneline
>>>	91506b7 (HEAD -> main) New feature commit 2
>>>	9fd490d New feature commit 1
>>>	013a10a init

As all existing commits should remain in history (according to the condition of the task 1.2), 
we can revert all unreviewed changes and cherry-pick them to the new branch.

Steps:

1) git checkout -b dev 013a10a
>>>	Switched to a new branch 'dev'

2) git cherry-pick 9fd490d^..91506b7
>>>	[dev 93b0fad] New feature commit 1
>>>	Date: Fri Dec 24 06:21:43 2021 +0300
>>>	1 file changed, 0 insertions(+), 0 deletions(-)
>>>	create mode 100644 feature.txt
>>>	[dev 7c41c25] New feature commit 2
>>>	Date: Fri Dec 24 06:22:06 2021 +0300
>>>	1 file changed, 0 insertions(+), 0 deletions(-)
>>>	create mode 100644 feature_helpers.txt

3) git checkout main

(We can make a reverse commit in a separate branch and then merge the changes into the main branch.)
4) git revert --no-commit HEAD~2..

5) git commit -m "Revert commits with new feature"

Now we can create a pull request.