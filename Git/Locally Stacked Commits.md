#Git #GitDebug

Imagine a bug you want to track down, so you create a few debug commands and print statements. These are all in their own commits. After fixing the bug, you want to get the branch *bugFix* back into the *main* branch. However, if you fast-forwarded *main*, then the debug statements would be put into main. 