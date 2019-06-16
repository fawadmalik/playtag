# playtag
Test renaming tags 

## Instructions
This answer covers lightweight tags that are added without the '-a' parameter
-a is for annotated tags which are objects saved in the repo and a bit more is involved in their usage. You did not specify which type so I'll go with lightweight tags.

To rename a tag you have to delete it from its commit and then re-add the tag to that commit 
So lets select 'ver1.0.t' as the tag to rename to 'ver1.0.5' because you mistyped 5 as t
Lets assume that you have also pushed this mistyped tag to the remote repo
// first push some commits
// . . . la la la

// Now mistype the tag
// push your changes
> git push origin master
// add tag locally
> git tag ver1.0.t
// push the tag as they are pushed by default when you push commits to remote
> git push origin ver1.0.t
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/fawadmalik/playtag.git
 * [new tag]         ver1.0.0 -> ver1.0.0
