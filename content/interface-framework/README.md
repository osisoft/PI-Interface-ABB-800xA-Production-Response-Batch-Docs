# PI Batch Interface Framework

This repository is intednded to be used as a dependency in each PI Batch Interface document repository. Inject it into the applicable doucment repository using the `git subtree` command. For more information, see [Documentation Frameworks](https://dev.azure.com/osieng/engineering/_wiki/wikis/Content%20Guild%20playbook.wiki/24425/Documentation-Frameworks).

directory is a subtree of the https://github.com/osisoft/PI-Interface-Framework repository, pointed at the **main** branch. This repository is populated with documents intended to be reused in other PI Batch Interface document repositories.

To pull the latest subtree content: `git subtree pull --prefix interface-framework https://github.com/osisoft/PI-Interface-Framework main --squash`

For usage on how to use subtrees, see https://docs.gitlab.com/ee/topics/git/subtree.html
