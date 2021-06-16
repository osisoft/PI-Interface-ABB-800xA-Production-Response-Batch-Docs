# PI Interface Doc Framework

This repository is intednded to be used as a dependency in each PI Batch Interface document repository. Inject it into the applicable doucment repository using the `git subtree` command. For more information, see [Documentation Frameworks](https://dev.azure.com/osieng/engineering/_wiki/wikis/Content%20Guild%20playbook.wiki/24425/Documentation-Frameworks).

## To add this repo as a subtree

```bash
git subtree add --prefix content/batch-interface-framework https://github.com/osisoft/PI-Batch-Interface-Doc-Framework main --squash
```

## To pull latest repo updates into subtree

```bash
git subtree pull --prefix content/batch-interface-framework https://github.com/osisoft/PI-Batch-Interface-Doc-Framework main --squash
```

For usage on how to use subtrees, see https://docs.gitlab.com/ee/topics/git/subtree.html
