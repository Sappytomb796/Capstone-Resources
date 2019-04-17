# Capstone-Resources
Team Resources

Each member should have their own branch, for any notes they want to take, and then compiled team notes will occupy the master branch.  

When making your branch, please use your first-last name in all lowercase (ex. alice-michael).
To make your own branch:
   git checkout -b name-for-branch

Pushing your branch to github:
   git push origin name-for-branch

Merging master into your branch (Note: make sure you are on the branch you 
want to change)
     git checkout user-name-branch
     git merge --no-ff master



PATCH PROCESS:
One note on why this is a simple and strong way to do things:  It allows
you to take only what you want into your tree, and the original author
remains in tact.  So if you run a git blame on a file, it will show you
their name and what patch/commit added it.  It is true that the commit
id will be different, but the date will not and the author will not be
and you can apply it to your tree that way.  It also allows you to not
merge in bugs as a merge will take anything different, and will take in
any commits that have different contents and you don't always want that.
Selectivity is sometimes our greatest tool, in a resources tree it's nice
to be able to use that selective tool and retain authorship of work.


To make a series of patches to apply to a different branch or tree:
   git format-patch -N -o ~/directory/path/to/store/patches
   git checkout branch-name
   git am ~/directory/path/to/store/patches/*.patch
To use this, N is a number of patches that you wish to generate.  If you 
want the top 5, it'd be that.  The -o flag allows you to place the 
patches in any directory so you can seperate them (which is useful when
using the * part for application and later referal).  Checkout the branch
that you want to apply the patches to, assuming that they apply cleanly,
you can use git am ~/path/*.patch and it will apply them in their numbered
order.  If you have problems, the way I always do it is apply them one
at a time, and then the one that has a problem I run the command:
   patch -p1 < ~/path/000N-title.patch
This will apply the lines that it can do, and create a .rej file that you
can run git status to look at and then open to see what the attempted 
changes are.  Open the .rej file and the real file in split screen and 
make the appropriate changes.  
Once all those changes are done for that patch, remove the .rej files,
add the files that were changed with
    git add filename.ext
Then run 
    git am --resolved
If you were doing a *.patch it will continue patching all the original 
patches you fed it.  It is easy to screw this up if you are learning 
the patching process, and I would recommend doing them one at a time
if you are new to the process.

If you run into a problem and want to end the patching process, you 
can abort the patch process on a single patch.  So for example, you
run git am, and then you try to apply the changes and realize they
did not apply because they are already there?  git thinks you are 
attempting to apply that patch still and you need to abort.  To 
do that, run:
   git am --abort
After that, do a git status and clean the tree up accordingly, if that
means a hard reset or cleaning up .rej files, or checking out files, 
the git status command will help you with options.  It's better to work
in a clean environment so you don't make as many mistakes or add things
you don't mean to when patching.


Team notes will include:
     * Planning Documents
     * Meeting Notes
     * Agendas
