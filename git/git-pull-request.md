# How To Pull Request

## Fork and Start Contributing

As you don't have access to the original repository, you need to fork (copy) the repository to your account and start working on your copy.

﻿
## Create relevant branches

Never work directly in the 'main' or 'master' branch, you need to create branches for each issue following the correct convention.

Bug - fix/<bug_name>

New Feature - feat/<feature_name>

﻿
## Test Before Creating Pull Request

 are sure that you have solved an issue, make sure you test it properly before raising a PR, as creating PRs without proper testing code makes a bad impression.

﻿
## Linking PR with Issue

Once you open a PR, make sure you link it with the issue you worked on by mentioning the issue number in the description of your PR.

Example:

fixes: #issue_number

resolves: #issue_number

﻿
## Wait for the Maintainer to Merge

At this point, you need to wait for the maintainer to check your PR and be a part of the discussion if there is any. If everything goes right, your PR will be merged.

## commands:
```
1. fork the repository which you want to contribute
[copy the code into your own repository]
2. clone the code into local environ ment
git clone forked url
git checkout -b fix-typo
git add .
git commit -m "fixed typo"
git push 
git push --set-upstream origin fix-typo
```

﻿
