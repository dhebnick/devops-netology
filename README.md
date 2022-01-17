mkdir branching
vim branching/merge.sh
cp branching/merge.sh branching/rebase.sh
git add --all
git commit -a -m "prepare for merge and rebas"
git checkout -b git-merge
vim branching/merge.sh
git commit -a -m "merge: @ instead *"
git push origin git-merge
vim branching/merge.sh
git commit -a -m "merge: use shift"
git push origin git-merge
git checkout main
vim branching/rebase.sh
git commit -a -m "modified file rebase.sh"
git push origin main
git checkout 6a66ba1
git checkout -b git-rebase
vim branching/rebase.sh
git commit -a -m "git-rebase 1"
git push origin git-rebase
vim branching/rebase.sh
git commit -a -m "git-rebase 2"
git push origin git-rebase
git checkout main
git merge git-merge
git push origin
git checkout git-rebase
git rebase -i main
vim branching/rebase.sh
git add branching/rebase.sh
git rebase --continue
vim branching/rebase.sh
git add branching/rebase.sh
git rebase --continue
git push origin
git push -u origin git-rebase
git push -u origin git-rebase -f
git checkout main
git merge git-rebase
git push origin

По идее можно ещё git branch -d сделать на ветки, но я пока оставлю для проверки.
