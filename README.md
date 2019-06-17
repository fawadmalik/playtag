# playtag
Test renaming tags 

## Instructions
This answer covers lightweight tags that are added without the '-a' parameter
-a is for annotated tags which are objects saved in the repo and a bit more is involved in their usage. You did not specify which type so I'll go with lightweight tags.

To rename a tag you have to delete it from its commit and then re-add the tag to that commit 
So lets select 'ver1.0.t' as the tag to rename to 'ver1.0.2' because you mistyped 2 as t
Lets assume that you have also pushed this mistyped tag to the remote repo
// first push some commits
// . . . la la la

// Now mistype the tag
// push your changes
$ git push origin master
// add tag locally
$ git tag ver1.0.t
// push the tag as they are pushed by default when you push commits to remote
$ git push origin ver1.0.t
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/fawadmalik/playtag.git
 * [new tag]         ver1.0.0 -> ver1.0.0

// push some more commits
// . . . la la la

Then you realized your mistake at some point and need to correct the tag. You can do it in the middle of the repo history and not necessarily right away.
So lets assume that after pushing a few commits you found the tag typo and needed to correct the tag name.

// find the commit hash this tag belongs to
$ git show ver1.0.t
commit 59b565d24abe8c285cbc17ec4f81ac7487768306 (tag: ver1.0.t)
Author: Fawad Malik <fawad.malik@hotmail.com>
Date:   Sun Jun 16 16:17:39 2019 -0700

- - - other details about the commit - - -

// note the commit hash 59b565d24abe8c285cbc17ec4f81ac7487768306
// cross reference to ensure that you have the correct data for the tag
$ git log 59b565d24abe8c285cbc17ec4f81ac7487768306
commit 59b565d24abe8c285cbc17ec4f81ac7487768306 (tag: ver1.0.t)
Author: Fawad Malik <fawad.malik@hotmail.com>
Date:   Sun Jun 16 16:17:39 2019 -0700

    Adds more instructions about tag typo

// delete this tag locally
$ git tag -d ver1.0.t
Deleted tag 'ver1.0.t' (was 59b565)

// verify that tag was deleted
$ git show ver1.0.t
fatal: ambiguous argument 'ver1.0.t': unknown revision or path not in the working tree.
Use '--' to separate paths from revisions, like this:
'git <command> [<revision>...] -- [<file>...]'

// now push this deletion to remote
$ git push origin --delete ver1.0.t

// cross reference commit hash to see tag is gone
$ git log 59b565d24abe8c285cbc17ec4f81ac7487768306
commit 59b565d24abe8c285cbc17ec4f81ac7487768306
Author: Fawad Malik <fawad.malik@hotmail.com>
Date:   Sun Jun 16 15:06:24 2019 -0700

- - - the rest of the log info - - -

// now add and push the correct tag
$ git tag ver1.0.2 59b565d24abe8c285cbc17ec4f81ac7487768306

// push this tag to remote
$ git push origin ver1.0.2
