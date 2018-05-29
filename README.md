# PEARG Documentation

This repository contains documentation related to bioinformatics for the PEARG
lab. 

The documentation is hosted at 
[pearg.github.io/pearg_documentation/](https://pearg.github.io/pearg_documentation/).


## How to build and deploy the documentation

Build the site with `hugo` or `blogdown::build_site()`.

To deploy the site using GitHub pages on the `gh-pages` branch:

```
# Prune old git worktrees
git worktree prune

# Remove old public directory
rm -r public

# Add new worktree
git worktree add -B gh-pages public origin/gh-pages

# Build the site again in R
blogdown::build_site()

# Commit changes
cd public
git add --all
git commit -m "Publishing to gh-pages"
git push
```

Or follow the more detailed [Hugo documentation](https://gohugo.io/hosting-and-deployment/hosting-on-github/).


## How to edit the documentation

Pages are stored in the `content/` directory and are written in Markdown.
Create a pull request when you want to submit a change.
