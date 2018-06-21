---
layout: post
title: Git CRLF Error
---

I created new repo and I cloned it. I make some coding and I made
```bash
git add .
```
after that I made
```bash
git commit -m"Bla bla bla"
```
Everything looks good but when I type 
```
git push origin master
```
I get a lot of errors like

"fatal: CRLF would be replaced by LF in”

and I solve this problem with ==> 
```bash
git config --global core.autocrlf false
```

I hope If you have this problem too you can solve with this command. 

Have a nice day!