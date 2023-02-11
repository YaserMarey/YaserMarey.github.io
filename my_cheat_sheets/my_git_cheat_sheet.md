---
title: "My Git Cheat Sheet" 
layout: home
nav_order: 10
nav_exclude: true
---
![ ](x.png)
# My Git Cheat Sheet


### Stage all changes, commit them, and push them
```
git add .;git commit -am".";git push
```

### Rebase master with development
```
git checkout master
git rebase --hard development
```

### List all cofnig 
```
git config --list
```

### Add remote url
```
git remtoe add origin https://......git
```

### Change remote url 
```
git remote set-url origin https://.....git
```

### Cach login credentials in the current repository
```
git config credential.helper cache
```


----
Salam
