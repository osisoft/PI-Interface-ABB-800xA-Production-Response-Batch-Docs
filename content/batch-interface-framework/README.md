# PI Interface Doc Framework

This repository is intednded to be used as a dependency in each PI Batch Interface document repository. Inject it into the applicable doucment repository using the `git subtree` command. For more information, see [Documentation Frameworks](https://dev.azure.com/osieng/engineering/_wiki/wikis/Content%20Guild%20playbook.wiki/24425/Documentation-Frameworks).

## To add this repo as a subtree

```bash
git subtree add --prefix <TARGET_DIRECTORY> https://github.com/osisoft/PI-Batch-Interface-Doc-Framework main --squash
```

Replace `<TARGET_DIRECTORY>` with the directory path where you want your subtree to live.

## To pull latest repo updates into subtree

```bash
git subtree pull --prefix <TARGET_DIRECTORY> https://github.com/osisoft/PI-Batch-Interface-Doc-Framework main --squash
```

## About Subtrees

For subtree documentation, see https://github.com/git/git/blob/master/contrib/subtree/git-subtree.txt
