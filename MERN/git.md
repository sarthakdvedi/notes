
## .gitignore -
/ -> only folder, not file
without / -> ignore all files and folders both



## point existing local project to different cloud repo -
```cmd
git remote set-url origin <PASTE_YOUR_NEW_GITHUB_REPO_URL_HERE>
```

### For Future Projects:

Whenever you want to start another new project using your template, the cleanest workflow is:

1. Create a brand new folder on your computer.
    
2. Clone your [folder-str](https://github.com/sarthakdvedi/folder-str) repo into it.
    
3. Change the remote URL (`git remote set-url origin <new-repo-url>`) so you don't accidentally push back to the template.