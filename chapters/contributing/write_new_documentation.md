# Write new documentation

For documenting we using [gitbook](https://www.gitbook.com/). It employs markdown files with little wrapper structure
to allow you to write well formatted content in a snap, keeping a git version control.

1. Install gitbook client tool
```bash
npm install -g gitbook-cli
```

1. Clone our docs repo:
```bash
git clone https://github.com/netbeast/docs.git
```

1. Serve it locally
```bash
cd docs
gitbook serve
```

1. Open a new shell or open it with your favorite editor
```bash
atom /path/to/docs
```

###Once you are done
Push it to the main stream or make a pull request!
```bash
git add -A
git commit -m "adds my chapter to the docs"
git push origin master
```



### References
[Gitbook github](https://github.com/GitbookIO/gitbook)
