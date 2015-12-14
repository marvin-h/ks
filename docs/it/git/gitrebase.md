#git rebase

衍合，也是合并分支操作，和一次性合并不同
衍合会回到两个分支的共同祖先，提取每次提交的差异，对需要衍合入的分支依次提交差异。
衍合会有清晰的提交历史

不要rebase已经提交到公共仓库的分支

##命令

###git rebase frombranch

```
git checkout master
git rebase test
```


###git rebase tobranch frombranch

```
git rebase master test
```