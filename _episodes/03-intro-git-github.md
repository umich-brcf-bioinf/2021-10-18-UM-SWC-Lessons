teaching: 0
- "How can I use version control to collaborate with other people?"
- "Learn the basic git workflow."
- "Push, pull, or clone a remote repository."
- "Describe the basic collaborative workflow with GitHub."
1. [Glossary of terms](#glossary)
[![Piled Higher and Deeper by Jorge Cham, http://www.phdcomics.com/comics/archive_print.php?comicid=1531](../fig/git/phd101212s.png)](http://www.phdcomics.com)
![Changes Are Saved Sequentially](../fig/git/play-changes.svg)
![Different Versions Can be Saved](../fig/git/versions.svg)
![Multiple Versions Can be Merged](../fig/git/merge.svg)
```
```
Please use your own name and email address instead of Riley's.
This user name and email will be associated with your subsequent Git activity,
> ## GitHub, GitLab, & BitBucket
>
> GitHub, GitLab, & BitBucket are websites where you can store your git
> repositories, share them with the world, and collaborate with others.
> You can think of them like email applications. You may have a gmail address,
> and you can choose to manage your email through one of many services such as
> the Gmail app, Microsoft Outlook, Apple's Mail app, etc.
> They have different interfaces and features, but all of them allow you to
> manage your email. Similarly, GitHub, GitLab, & BitBucket have different
> interfaces and features, but they all allow you to store, share, and
> collaborate with others on your git repos.
> ```
> ```
> ```
> ```
```
```
> ```
> ```
> ```
> ```
> ```
> ```
[git-privacy]: https://help.github.com/articles/keeping-your-email-address-private/

## Basic Workflow
_[Back to top](#contents)_

![git-basics-flow-01-opt1](../fig/git-basics/20201117-git-01-opt1.png)  

Once Git is configured, we can start using it.


First, let's make sure we are in our `un-report` directory, if not we need to move into that directory:

```
$ pwd
```
{: .language-bash}

```
$ /home/USERNAME/Desktop/un-report
```
{: .output}

> To get back to your `un-report` directory you can use the following command:
>
>Mac/git-bash:
>```
>cd Desktop/un-report
>```
>{: .language-bash}
>
>Unix subsystem for Windows:
>```
>cd c/USERNAME/Desktop/un-report
>```
>{: .language-bask}
{: .callout}

What is currently in our directory?

```
$ ls
```
{: .language-bash}

```
code    data    figures
```
{: .output}


Now we tell Git to make `un-report` a [repository]({{ page.root }}{% link reference.md %}#repository)
-- a place where Git can store versions of our files:


```
$ git init
```
{: .language-bash}

It is important to note that `git init` will create a repository that
includes subdirectories and their files---there is no need to create
separate repositories nested within the `un-report` repository, whether
subdirectories are present from the beginning or added later. Also, note
that the creation of the `un-report` directory and its initialization as a
repository are completely separate processes.

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

```
$ ls
```
{: .language-bash}

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `un-report` called `.git`:

```
$ ls -a
```
{: .language-bash}

```
.	..	.git
```
{: .output}

Git uses this special subdirectory to store all the information about the project,
including all files and sub-directories located within the project's directory.
If we ever delete the `.git` subdirectory,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

```
$ git status
```
{: .language-bash}
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

nothing added to commit but untracked files present (use "git add" to track)
```
{: .output}

If you are using a different version of `git`, the exact
wording of the output might be slightly different.

> ## Places to Create Git Repositories
>
> Along with tracking information about un-report (the project we have already created),
> Riley would also like to track information about countries.
> Despite our concerns, Riley creates a `countries` project inside his `un-report`
> project with the following sequence of commands:
>
> ```
> $ cd ~/Desktop   # return to Desktop directory
> $ cd un-report     # go into un-report directory, which is already a Git repository
> $ ls -a          # ensure the .git subdirectory is still present in the un-report directory
> $ mkdir countries    # make a subdirectory un-report/countries
> $ cd countries       # go into countries subdirectory
> $ git init       # make the countries subdirectory a Git repository
> $ ls -a          # ensure the .git subdirectory is present indicating we have created a new Git repository
> ```
> {: .language-bash}
>
> Is the `git init` command, run inside the `countries` subdirectory, required for
> tracking files stored in the `countries` subdirectory?
>
> > ## Solution
> >
> > No. Riley does not need to make the `countries` subdirectory a Git repository
> > because the `un-report` repository will track all files, sub-directories, and
> > subdirectory files under the `un-report` directory.  Thus, in order to track
> > all information about countries, Riley only needed to add the `countries` subdirectory
> > to the `un-report` directory.
> >
> > Additionally, Git repositories can interfere with each other if they are "nested":
> > the outer repository will try to version-control
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown
> > above:
> >
> > ```
> > $ git status
> > ```
> > {: .language-bash}
> > ```
> > fatal: Not a git repository (or any of the parent directories): .git
> > ```
> > {: .output}
> {: .solution}
{: .challenge}
> ## Correcting `git init` Mistakes
> We explain to Riley how a nested repository is redundant and may cause confusion
> down the road. Riley would like to remove the nested repository. How can Riley undo
> his last `git init` in the `countries` subdirectory?
>
> > ## Solution -- USE WITH CAUTION!
> >
> > ### Background
> > Removing files from a git repository needs to be done with caution. To remove files from the working tree and not from your working directory, use
> > ```
> > $ rm filename
> > ```
> > {: .language-bash}
> >
> > The file being removed has to be in sync with the branch head with no updates. If there are updates, the file can be removed by force by using the `-f` option. Similarly a directory can be removed from git using `rm -r dirname` or `rm -rf dirname`.
> >
> > ### Solution
> > Git keeps all of its files in the `.git` directory.
> > To recover from this little mistake, Riley can just remove the `.git`
> > folder in the countries subdirectory by running the following command from inside the `un-report` directory:
> >
> > ```
> > $ rm -rf countries/.git
> > ```
> > {: .language-bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire Git history of a project you might want to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}


First let's make sure we're still in the right directory.
You should be in the `un-report` directory.

```
$ cd ~/Desktop/un-report
```
{: .language-bash}

Let's create a file called `analysis.txt` that contains some notes
about the plot we have made so far.
We'll use `nano` to edit the file;
you can use whatever text editor you like.

```
$ nano analysis.txt
```
{: .language-bash}

Type the text below into the `analysis.txt` file:

```
We plotted life expectancy over time.
```

Let's first verify that the file was properly created by running the list command (`ls`):


```
$ ls
```
{: .language-bash}

```
analysis.txt
```
{: .output}


`analysis.txt` contains a single line, which we can see by running:

```
$ cat analysis.txt
```
{: .language-bash}

```
We plotted life expectancy over time.
```
{: .output}

If we check the status of our project again,
Git tells us that it's noticed the new file:

```
$ git status
```
{: .language-bash}

```
On branch master

No commits yet

Untracked files:
   (use "git add <file>..." to include in what will be committed)

	analysis.txt

nothing added to commit but untracked files present (use "git add" to track)
```
{: .output}

The "untracked files" message means that there's a file in the directory
that Git isn't keeping track of.
We can tell Git to track a file using `git add`:

```
$ git add analysis.txt
```
{: .language-bash}

and then check that the right thing happened:

```
$ git status
```
{: .language-bash}

```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   analysis.txt

```
{: .output}

Git now knows that it's supposed to keep track of `analysis.txt`,
but it hasn't recorded these changes as a commit yet.
To get it to do that,
we need to run one more command:

```
$ git commit -m "Start notes on analysis"
```
{: .language-bash}

```
[master (root-commit) f22b25e] Start notes on analysis
 1 file changed, 1 insertion(+)
 create mode 100644 analysis.txt
```
{: .output}

When we run `git commit`,
Git takes everything we have told it to save by using `git add`
and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a [commit]({{ page.root }}{% link reference.md %}#commit)
(or [revision]({{ page.root }}{% link reference.md %}#revision)) and its short identifier is `f22b25e`. Your commit may have another identifier.

We use the `-m` flag (for "message")
to record a short, descriptive, and specific comment that will help us remember later on what we did and why.
If we just run `git commit` without the `-m` option,
Git will launch `nano` (or whatever other editor we configured as `core.editor`)
so that we can write a longer message.

[Good commit messages][commit-messages] start with a brief (<50 characters) statement about the
changes made in the commit. Generally, the message should complete the sentence "If applied, this commit will" <commit message here>.
If you want to go into more detail, add a blank line between the summary line and your additional notes. Use this additional space to explain why you made changes and/or what their impact will be.

If we run `git status` now:

```
$ git status
```
{: .language-bash}

```
On branch master
nothing to commit, working directory clean
```
{: .output}

it tells us everything is up to date.
If we want to know what we've done recently,
we can ask Git to show us the project's history using `git log`:

```
$ git log
```
{: .language-bash}

```
commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Riley Shor <Riley.Shor@fake.email.address>
Date:   Thu Aug 22 09:51:46 2020 -0400

    Start notes on analysis
```
{: .output}

`git log` lists all commits  made to a repository in reverse chronological order.
The listing for each commit includes
the commit's full identifier
(which starts with the same characters as
the short identifier printed by the `git commit` command earlier),
the commit's author,
when it was created,
and the log message Git was given when the commit was created.

> ## Where Are My Changes?
>
> If we run `ls` at this point, we will still see just one file called `analysis.txt`.
> That's because Git saves information about files' history
> in the special `.git` directory mentioned earlier
> so that our filesystem doesn't become cluttered
> (and so that we can't accidentally edit or delete an old version).
{: .callout}

Now suppose Riley adds more information to the file.
(Again, we'll edit with `nano` and then `cat` the file to show its contents;
you may use a different editor, and don't need to `cat`.)

```
$ nano analysis.txt
$ cat analysis.txt
```
{: .language-bash}

```
We plotted life expectancy over time.
Each point represents a country.
```
{: .output}

When we run `git status` now,
it tells us that a file it already knows about has been modified:

```
$ git status
```
{: .language-bash}

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   analysis.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
{: .output}

The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with `git add`)
nor have we saved them (which we do with `git commit`).
So let's do that now. It is good practice to always review
our changes before saving them. We do this using `git diff`.
This shows us the differences between the current state
of the file and the most recently saved version:

```
$ git diff
```
{: .language-bash}

```
diff --git a/analysis.txt b/analysis.txt
index df0654a..315bf3a 100644
--- a/analysis.txt
+++ b/analysis.txt
@@ -1 +1,2 @@
 We plotted life expectancy over time.
+Each point represents a country.
```
{: .output}

The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which versions of the file
    Git is comparing;
    `df0654a` and `315bf3a` are unique computer-generated labels for those versions.
3.  The third and fourth lines once again show the name of the file being changed.
4.  The remaining lines are the most interesting, they show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` marker in the first column shows where we added a line.

After reviewing our change, it's time to commit it:

```
$ git commit -m "Add information on points"
$ git status
```
{: .language-bash}

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   analysis.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
{: .output}

Whoops:
Git won't commit because we didn't use `git add` first.
Let's fix that:

```
$ git add analysis.txt
$ git commit -m "Add information on points"
```
{: .language-bash}

```
[master 34961b1] Add information on points
 1 file changed, 1 insertion(+)
```
{: .output}

Git insists that we add files to the set we want to commit
before actually committing anything. This allows us to commit our
changes in stages and capture changes in logical portions rather than
only large batches.
For example,
suppose we're adding a few citations to relevant research to our thesis.
We might want to commit those additions,
and the corresponding bibliography entries,
but *not* commit some of our work drafting the conclusion
(which we haven't finished yet).

To allow for this,
Git has a special *staging area*
where it keeps track of things that have been added to
the current [changeset]({{ page.root }}{% link reference.md %}#changeset)
but not yet committed.

> ## Staging Area
>
> If you think of Git as taking snapshots of changes over the life of a project,
> `git add` specifies *what* will go in a snapshot
> (putting things in the staging area),
> and `git commit` then *actually takes* the snapshot, and
> makes a permanent record of it (as a commit).
> If you don't have anything staged when you type `git commit`,
> Git will prompt you to use `git commit -a` or `git commit --all`,
> which is kind of like gathering *everyone* to take a group photo!
> However, it's almost always better to
> explicitly add things to the staging area, because you might
> commit changes you forgot you made. (Going back to the group photo simile,
> you might get an extra with incomplete makeup walking on
> the stage for the picture because you used `-a`!)
> Try to stage things manually,
> or you might find yourself searching for "git undo commit" more
> than you would like!
{: .callout}

![The Git Staging Area](../fig/git/git-staging-area.svg)

Let's watch as our changes to a file move from our editor
to the staging area
and into long-term storage.
First,
we'll add another line to the file:

```
$ nano analysis.txt
$ cat analysis.txt
```
{: .language-bash}

```
We plotted life expectancy over time.
Each point represents a country.
Continents are grouped by color.
```
{: .output}

```
$ git diff
```
{: .language-bash}

```
diff --git a/analysis.txt b/analysis.txt
index 315bf3a..b36abfd 100644
--- a/analysis.txt
+++ b/analysis.txt
@@ -1,2 +1,3 @@
 We plotted life expectancy over time.
 Each point represents a country.
+Continents are grouped by color.
```
{: .output}

So far, so good:
we've added one line to the end of the file
(shown with a `+` in the first column).
Now let's put that change in the staging area
and see what `git diff` reports:

```
$ git add analysis.txt
$ git diff
```
{: .language-bash}

There is no output:
as far as Git can tell,
there's no difference between what it's been asked to save permanently
and what's currently in the directory.
However,
if we do this:

```
$ git diff --staged
```
{: .language-bash}

```
diff --git a/analysis.txt b/analysis.txt
index 315bf3a..b36abfd 100644
--- a/analysis.txt
+++ b/analysis.txt
@@ -1,2 +1,3 @@
 We plotted life expectancy over time.
 Each point represents a country.
+Continents are grouped by color.
```
{: .output}

it shows us the difference between
the last committed change
and what's in the staging area.
Let's save our changes:

```
$ git commit -m "Add note about point color"
```
{: .language-bash}

```
[master 005937f] Add note about point color
 1 file changed, 1 insertion(+)
```
{: .output}

check our status:

```
$ git status
```
{: .language-bash}

```
On branch master
nothing to commit, working directory clean
```
{: .output}

and look at the history of what we've done so far:

```
$ git log
```
{: .language-bash}

```
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Riley Shor <Riley.Shor@fake.email.address>
Date:   Thu Aug 22 10:14:07 2020 -0400

    Add note about point color

commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Riley Shor <Riley.Shor@fake.email.address>
Date:   Thu Aug 22 10:07:21 2020 -0400

    Add information on points

commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Riley Shor <Riley.Shor@fake.email.address>
Date:   Thu Aug 22 09:51:46 2020 -0400

    Start notes on analysis
```
{: .output}

> ## Word-based diffing
>
> Sometimes, e.g. in the case of the text documents a line-wise
> diff is too coarse. That is where the `--color-words` option of
> `git diff` comes in very useful as it highlights the changed
> words using colors.
{: .callout}

> ## Paging the Log
>
> When the output of `git log` is too long to fit in your screen,
> `git` uses a program to split it into pages of the size of your screen.
> When this "pager" is called, you will notice that the last line in your
> screen is a `:`, instead of your usual prompt.
>
> *   To get out of the pager, press <kbd>Q</kbd>.
> *   To move to the next page, press <kbd>Spacebar</kbd>.
> *   To search for `some_word` in all pages,
>     press <kbd>/</kbd>
>     and type `some_word`.
>     Navigate through matches pressing <kbd>N</kbd>.
{: .callout}

> ## Limit Log Size
>
> To avoid having `git log` cover your entire terminal screen, you can limit the
> number of commits that Git lists by using `-N`, where `N` is the number of
> commits that you want to view. For example, if you only want information from
> the last commit you can use:
>
> ```
> $ git log -1
> ```
> {: .language-bash}
>
> ```
> commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
> Author: Riley Shor <Riley.Shor@fake.email.address>
> Date:   Thu Aug 22 10:14:07 2020 -0400
>
>    Add note about point color
> ```
> {: .output}
>
> You can also reduce the quantity of information using the
> `--oneline` option:
>
> ```
> $ git log --oneline
> ```
> {: .language-bash}
> ```
> 005937f Add note about point color
> 34961b1 Add information on points
> f22b25e Start notes on analysis
> ```
> {: .output}
>
> You can also combine the `--oneline` option with others. One useful
> combination adds `--graph` to display the commit history as a text-based
> graph and to indicate which commits are associated with the
> current `HEAD`, the current branch `master`, or
> [other Git references][git-references]:
>
> ```
> $ git log --oneline --graph
> ```
> {: .language-bash}
> ```
> * 005937f (HEAD -> master) Add note about point color
> * 34961b1 Add information on points
> * f22b25e Start notes on analysis
> ```
> {: .output}
{: .callout}

> ## Directories
>
> Two important facts you should know about directories in Git.
>
> 1. Git does not track directories on their own, only files within them.
>    Try it for yourself:
>
>    ```
>    $ mkdir analysis
>    $ git status
>    $ git add analysis
>    $ git status
>    ```
>    {: .language-bash}
>
>    Note, our newly created empty directory `analysis` does not appear in
>    the list of untracked files even if we explicitly add it (_via_ `git add`) to our
>    repository. This is the reason why you will sometimes see `.gitkeep` files
>    in otherwise empty directories. Unlike `.gitignore`, these files are not special
>    and their sole purpose is to populate a directory so that Git adds it to
>    the repository. In fact, you can name such files anything you like.
>
> 2. If you create a directory in your Git repository and populate it with files,
>    you can add all files in the directory at once by:
>
>    ```
>    git add <directory-with-files>
>    ```
>    {: .language-bash}
>
>    Try it for yourself:
>
>    ```
>    $ touch analysis/plot-1 analysis/plot-2
>    $ git status
>    $ git add analysis
>    $ git status
>    ```
>    {: .language-bash}
>
>    Before moving on, we will commit these changes.
>
>    ```
>    $ git commit -m "Add some initial thoughts on analysis"
>    ```
>    {: .language-bash}
>
{: .callout}

To recap, when we want to add changes to our repository,
we first need to add the changed files to the staging area
(`git add`) and then commit the staged changes to the
repository (`git commit`):

![The Git Commit Workflow](../fig/git/git-committing.svg)

> ## Choosing a Commit Message
>
> Which of the following commit messages would be most appropriate for the
> last commit made to `analysis.txt`?
>
> 1. "Changes"
> 2. "Added line 'Continents are grouped by color.' to analysis.txt"
> 3. "Describe grouping"
>
> > ## Solution
> > Answer 1 is not descriptive enough, and the purpose of the commit is unclear;
> > and answer 2 is redundant to using "git diff" to see what changed in this commit;
> > but answer 3 is good: short, descriptive, and imperative.
> {: .solution}
{: .challenge}

> ## Committing Changes to Git
>
> Which command(s) below would save the changes of `myfile.txt`
> to my local Git repository?
>
> 1. ```
>    $ git commit -m "my recent changes"
>    ```
>    {: .language-bash}
> 2. ```
>    $ git init myfile.txt
>    $ git commit -m "my recent changes"
>    ```
>    {: .language-bash}
> 3. ```
>    $ git add myfile.txt
>    $ git commit -m "my recent changes"
>    ```
>    {: .language-bash}
> 4. ```
>    $ git commit -m myfile.txt "my recent changes"
>    ```
>    {: .language-bash}
>
> > ## Solution
> >
> > 1. Would only create a commit if files have already been staged.
> > 2. Would try to create a new repository.
> > 3. Is correct: first add the file to the staging area, then commit.
> > 4. Would try to commit a file "my recent changes" with the message myfile.txt.
> {: .solution}
{: .challenge}

> ## Committing Multiple Files
>
> The staging area can hold changes from any number of files
> that you want to commit as a single snapshot.
>
> 1. Add some text to `analysis.txt` noting your decision
> to consider manuscript
> 2. Create a new file `manuscript.txt` with your initial thoughts
> about manuscript for you and your friends
> 3. Add changes from both files to the staging area,
> and commit those changes.
>
> > ## Solution
> >
> > First we make our changes to the `analysis.txt` and `manuscript.txt` files:
> > ```
> > $ nano analysis.txt
> > $ cat analysis.txt
> > ```
> > {: .language-bash}
> > ```
> > Maybe I should start with a draft manuscript.
> > ```
> > {: .output}
> > ```
> > $ nano manuscript.txt
> > $ cat manuscript.txt
> > ```
> > {: .language-bash}
> > ```
> > manuscript is a good start and I definitely should consider it.
> > ```
> > {: .output}
> > Now you can add both files to the staging area. We can do that in one line:
> >
> > ```
> > $ git add analysis.txt manuscript.txt
> > ```
> > {: .language-bash}
> > Or with multiple commands:
> > ```
> > $ git add analysis.txt
> > $ git add manuscript.txt
> > ```
> > {: .language-bash}
> > Now the files are ready to commit. You can check that using `git status`. If you are ready to commit use:
> > ```
> > $ git commit -m "Write plans to start a draft manuscript"
> > ```
> > {: .language-bash}
> > ```
> > [master cc127c2]
> >  Write plans to start a draft manuscript
> >  2 files changed, 2 insertions(+)
> >  create mode 100644 manuscript.txt
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

> ## `workshop` Repository
>
> * Create a new Git repository on your computer called `workshop`.
> * Write a three lines about what you have learned about R and bash a file called `notes.txt`,
> commit your changes
> * Modify one line, add a fourth line
> * Display the differences
> between its updated state and its original state.
>
> > ## Solution
> >
> > If needed, move out of the `un-report` folder:
> >
> > ```
> > $ cd ..
> > ```
> > {: .language-bash}
> >
> > Create a new folder called `workshop` and 'move' into it:
> >
> > ```
> > $ mkdir workshop
> > $ cd workshop
> > ```
> > {: .language-bash}
> >
> > Initialise git:
> >
> > ```
> > $ git init
> > ```
> > {: .language-bash}
> >
> > Create your biography file `notes.txt` using `nano` or another text editor.
> > Once in place, add and commit it to the repository:
> >
> > ```
> > $ git add notes.txt
> > $ git commit -m "Add notes file"
> > ```
> > {: .language-bash}
> >
> > Modify the file as described (modify one line, add a fourth line).
> > To display the differences
> > between its updated state and its original state, use `git diff`:
> >
> > ```
> > $ git diff notes.txt
> > ```
> > {: .language-bash}
> >
> {: .solution}
{: .challenge}

[commit-messages]: https://chris.beams.io/posts/git-commit/
[git-references]: https://git-scm.com/book/en/v2/Git-Internals-Git-References
{% include links.md %}
As we saw in the previous lesson, we can refer to commits by their
identifiers.  You can refer to the _most recent commit_ of the working
directory by using the identifier `HEAD`.
We've been adding one line at a time to `analysis.txt`, so it's easy to track our
progress by looking, so let's do that using our `HEAD`s.  Before we start,
let's make a change to `analysis.txt`, adding yet another line.
```
$ nano analysis.txt
$ cat analysis.txt
```
{: .language-bash}
```
We plotted life expectancy over time.
Each point represents a country.
Continents are grouped by color.
An ill-considered change
```
{: .output}
Now, let's see what we get.
$ git diff HEAD analysis.txt
```
diff --git a/analysis.txt b/analysis.txt
index b36abfd..0848c8d 100644
--- a/analysis.txt
+++ b/analysis.txt
@@ -1,3 +1,4 @@
 We plotted life expectancy over time.
 Each point represents a country.
 Continents are grouped by color.
+An ill-considered change.
```
{: .output}
which is the same as what you would get if you leave out `HEAD` (try it).  The
real goodness in all this is when you can refer to previous commits.  We do
that by adding `~1`
(where "~" is "tilde", pronounced [**til**-d*uh*])
to refer to the commit one before `HEAD`.
$ git diff HEAD~1 analysis.txt
If we want to see the differences between older commits we can use `git diff`
again, but with the notation `HEAD~1`, `HEAD~2`, and so on, to refer to them:
$ git diff HEAD~3 analysis.txt
```
diff --git a/analysis.txt b/analysis.txt
index df0654a..b36abfd 100644
--- a/analysis.txt
+++ b/analysis.txt
@@ -1 +1,4 @@
 We plotted life expectancy over time.
+Each point represents a country.
+Continents are grouped by color.
+An ill-considered change
```
{: .output}

We could also use `git show` which shows us what changes we made at an older commit as
well as the commit message, rather than the _differences_ between a commit and our
working directory that we see by using `git diff`.
$ git show HEAD~3 analysis.txt
```
commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Riley Shor <Riley.Shor@fake.email.address>
Date:   Thu Aug 22 09:51:46 2020 -0400

    Start notes on analysis as a base

diff --git a/analysis.txt b/analysis.txt
new file mode 100644
index 0000000..df0654a
--- /dev/null
+++ b/analysis.txt
@@ -0,0 +1 @@
+We plotted life expectancy over time.
```
{: .output}

In this way,
we can build up a chain of commits.
The most recent end of the chain is referred to as `HEAD`;
we can refer to previous commits using the `~` notation,
so `HEAD~1`
means "the previous commit",
while `HEAD~123` goes back 123 commits from where we are now.

We can also refer to commits using
those long strings of digits and letters
that `git log` displays.
These are unique IDs for the changes,
and "unique" really does mean unique:
every change to any set of files on any computer
has a unique 40-character identifier.
Our first commit was given the ID
`f22b25e3233b4645dabd0d81e651fe074bd8e73b`,
so let's try this:
$ git diff f22b25e3233b4645dabd0d81e651fe074bd8e73b analysis.txt
```
diff --git a/analysis.txt b/analysis.txt
index df0654a..93a3e13 100644
--- a/analysis.txt
+++ b/analysis.txt
@@ -1 +1,4 @@
 We plotted life expectancy over time.
+Each point represents a country.
+Continents are grouped by color.
+An ill-considered change
```
{: .output}
That's the right answer,
but typing out random 40-character strings is annoying,
so Git lets us use just the first few characters (typically seven for normal size projects):
```
$ git diff f22b25e analysis.txt
```
{: .language-bash}
```
diff --git a/analysis.txt b/analysis.txt
index df0654a..93a3e13 100644
--- a/analysis.txt
+++ b/analysis.txt
@@ -1 +1,4 @@
 We plotted life expectancy over time.
+Each point represents a country.
+Continents are grouped by color.
+An ill-considered change
```
{: .output}
All right! So
we can save changes to files and see what we've changed. Now, how
can we restore older versions of things?
Let's suppose we change our mind about the last update to
`analysis.txt` (the "ill-considered change").
`git status` now tells us that the file has been changed,
but those changes haven't been staged:
$ git status
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   analysis.txt
no changes added to commit (use "git add" and/or "git commit -a")
{: .output}

We can put things back the way they were
by using `git checkout`:

```
$ git checkout HEAD analysis.txt
$ cat analysis.txt
```
We plotted life expectancy over time.
Each point represents a country.
Continents are grouped by color.
```
{: .output}
As you might guess from its name,
`git checkout` checks out (i.e., restores) an old version of a file.
In this case,
we're telling Git that we want to recover the version of the file recorded in `HEAD`,
which is the last saved commit.
If we want to go back even further,
we can use a commit identifier instead:
```
$ git checkout f22b25e analysis.txt
```
{: .language-bash}
$ cat analysis.txt
```
 We plotted life expectancy over time.
```
{: .output}
$ git status
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    modified:   analysis.txt
{: .output}

Notice that the changes are currently in the staging area.
Again, we can put things back the way they were
by using `git checkout`:

```
$ git checkout HEAD analysis.txt
> ## Don't Lose Your HEAD
>
> Above we used
>
> ```
> $ git checkout f22b25e analysis.txt
> ```
> {: .language-bash}
>
> to revert `analysis.txt` to its state after the commit `f22b25e`. But be careful!
> The command `checkout` has other important functionalities and Git will misunderstand
> your intentions if you are not accurate with the typing. For example,
> if you forget `analysis.txt` in the previous command.
>
> ```
> $ git checkout f22b25e
> ```
> {: .language-bash}
> ```
> Note: checking out 'f22b25e'.
>
> You are in 'detached HEAD' state. You can look around, make experimental
> changes and commit them, and you can discard any commits you make in this
> state without impacting any branches by performing another checkout.
>
> If you want to create a new branch to retain commits you create, you may
> do so (now or later) by using -b with the checkout command again. Example:
>
>  git checkout -b <new-branch-name>
>
> HEAD is now at f22b25e Start notes on analysis as a base
> ```
> {: .error}
>
> The "detached HEAD" is like "look, but don't touch" here,
> so you shouldn't make any changes in this state.
> After investigating your repo's past state, reattach your `HEAD` with `git checkout master`.
{: .callout}

It's important to remember that
we must use the commit number that identifies the state of the repository
*before* the change we're trying to undo.
A common mistake is to use the number of
the commit in which we made the change we're trying to discard.
In the example below, we want to retrieve the state from before the most
recent commit (`HEAD~1`), which is commit `f22b25e`:

![Git Checkout](../fig/git/git-checkout.svg)

So, to put it all together,
here's how Git works in cartoon form:


We start by creating a local working directory. Our working directory is `un-report`

![git-basics-flow-01-opt1]({{ page.root }}/fig/git-basics/20201117-git-01-opt1.png =400x)  

Then we initialize git
git init
Now our working directory also is being tracked by the git repo

![git-basics-flow-02]({{ page.root }}/fig/git-basics/20201117-git-02.png =400x)  
Then if we add a file to our working directory, it is only in our working directory.
![git-basics-flow-03]({{ page.root }}/fig/git-basics/20201117-git-03.png =400x)  

If we want to begin tracking this file, we need to add it to the staging area
git add NEWFILE
git status
![git-basics-flow-04]({{ page.root }}/fig/git-basics/20201117-git-04.png =400x)  

Now we can commit this file to our git repository for the changes to be saved.
git commit -m "Added NEWFILE"
git status
![git-basics-flow-05]({{ page.root }}/fig/git-basics/20201117-git-05.png =400x)  

If we make changes to the file now, we can see the differences between the commited file and the new edits.

```
git diff
```
{: .language-bash}
![git-basics-flow-10]({{ page.root }}/fig/git-basics/20201117-git-10.png =400x)  
Let's commit this change
git add NEWFILE
![git-basics-flow-12]({{ page.root }}/fig/git-basics/20201117-git-12.png =400x)  
Now we can commit this file to our git repository for the changes to be saved.
git commit -m "editted NEWFILE"
![git-basics-flow-13]({{ page.root }}/fig/git-basics/20201117-git-13.png =400x)  
We can check the history of our commits
![git-basics-flow-14]({{ page.root }}/fig/git-basics/20201117-git-14.png =400x)  
We can also check the differences between commits
```
git diff <commit>..<commit>
```
{: .language-bash}
![git-basics-flow-15]({{ page.root }}/fig/git-basics/20201117-git-15.png =400x)  
If we introduce a bug and break our code, no problem! We can `revert` to a previous commit.
![git-basics-flow-30]({{ page.root }}/fig/git-basics/20201117-git-30.png =400x)  
![git-basics-flow-32]({{ page.root }}/fig/git-basics/20201117-git-32.png =400x)  
We have now reverted our current file and commit to the latest version without the bug. But we have kept the commit and history from the commit that had the error.
In the next section, we will learn how to share our git repository across networks. We can do this by creating a link to another location, like Github (remote repository) which we can `push` and `pull` our repository to and from to share our files with others as well as backing up our local repository.
![git-basics-flow-27]({{ page.root }}/fig/git-basics/20201117-git-27.png =400x)  
> ## Simplifying the Common Case
>
> If you read the output of `git status` carefully,
> you'll see that it includes this hint:
>
> ```
> (use "git checkout -- <file>..." to discard changes in working directory)
> ```
> {: .language-bash}
>
> As it says,
> `git checkout` without a version identifier restores files to the state saved in `HEAD`.
> The double dash `--` is needed to separate the names of the files being recovered
> from the command itself:
> without it,
> Git would try to use the name of the file as the commit identifier.
{: .callout}
The fact that files can be reverted one by one
tends to change the way people organize their work.
If everything is in one large document,
it's hard (but not impossible) to undo changes to the introduction
without also undoing changes made later to the conclusion.
If the introduction and conclusion are stored in separate files,
on the other hand,
moving backward and forward in time becomes much easier.
> ## Recovering Older Versions of a File
>
> Jennifer has made changes to the Python script that she has been working on for weeks, and the
> modifications she made this morning "broke" the script and it no longer runs. She has spent
> ~ 1hr trying to fix it, with no luck...
>
> Luckily, she has been keeping track of her project's versions using Git! Which commands below will
> let her recover the last committed version of her Python script called
> `data_cruncher.py`?
>
> 1. `$ git checkout HEAD`
>
> 2. `$ git checkout HEAD data_cruncher.py`
>
> 3. `$ git checkout HEAD~1 data_cruncher.py`
>
> 4. `$ git checkout <unique ID of last commit> data_cruncher.py`
>
> 5. Both 2 and 4
>
>
> > ## Solution
> >
> > The answer is (5)-Both 2 and 4.
> >
> > The `checkout` command restores files from the repository, overwriting the files in your working
> > directory. Answers 2 and 4 both restore the *latest* version *in the repository* of the file
> > `data_cruncher.py`. Answer 2 uses `HEAD` to indicate the *latest*, whereas answer 4 uses the
> > unique ID of the last commit, which is what `HEAD` means.
> >
> > Answer 3 gets the version of `data_cruncher.py` from the commit *before* `HEAD`, which is NOT
> > what we wanted.
> >
> > Answer 1 can be dangerous! Without a filename, `git checkout` will restore **all files**
> > in the current directory (and all directories below it) to their state at the commit specified.
> > This command will restore `data_cruncher.py` to the latest commit version, but it will also
> > restore *any other files that are changed* to that version, erasing any changes you may
> > have made to those files!
> > As discussed above, you are left in a *detached* `HEAD` state, and you don't want to be there.
> {: .solution}
{: .challenge}

> ## Reverting a Commit
>
> Jennifer is collaborating on her Python script with her colleagues and
> realizes her last commit to the project's repository contained an error and
> she wants to undo it.  `git revert [erroneous commit ID]` will create a new
> commit that reverses Jennifer's erroneous commit. Therefore `git revert` is
> different to `git checkout [commit ID]` because `git checkout` returns the
> files within the local repository to a previous state, whereas `git revert`
> reverses changes committed to the local and project repositories.  
> Below are the right steps and explanations for Jennifer to use `git revert`,
> what is the missing command?
>
> 1. `________ # Look at the git history of the project to find the commit ID`
>
> 2. Copy the ID (the first few characters of the ID, e.g. 0b1d055).
>
> 3. `git revert [commit ID]`
>
> 4. Type in the new commit message.
>
> 5. Save and close
{: .challenge}

> ## Understanding Workflow and History
>
> What is the output of the last command in
>
> ```
> $ cd planets
> $ echo "Venus is beautiful and full of love" > venus.txt
> $ git add venus.txt
> $ echo "Venus is too hot to be suitable as a base" >> venus.txt
> $ git commit -m "Comment on Venus as an unsuitable base"
> $ git checkout HEAD venus.txt
> $ cat venus.txt #this will print the contents of venus.txt to the screen
> ```
> {: .language-bash}
>
> 1. ```
>    Venus is too hot to be suitable as a base
>    ```
>    {: .output}
> 2. ```
>    Venus is beautiful and full of love
>    ```
>    {: .output}
> 3. ```
>    Venus is beautiful and full of love
>    Venus is too hot to be suitable as a base
>    ```
>    {: .output}
> 4. ```
>    Error because you have changed venus.txt without committing the changes
>    ```
>    {: .output}
>
> > ## Solution
> >
> > The answer is 2.
> >
> > The command `git add venus.txt` places the current version of `venus.txt` into the staging area.
> > The changes to the file from the second `echo` command are only applied to the working copy,
> > not the version in the staging area.
> >
> > So, when `git commit -m "Comment on Venus as an unsuitable base"` is executed,
> > the version of `venus.txt` committed to the repository is the one from the staging area and
> > has only one line.
> >  
> >  At this time, the working copy still has the second line (and
> >  `git status` will show that the file is modified). However, `git checkout HEAD venus.txt`
> >  replaces the working copy with the most recently committed version of `venus.txt`.
> >  
> >  So, `cat venus.txt` will output
> >  ```
> >  Venus is beautiful and full of love.
> > ```
> > {: .output}
> {: .solution}
{: .challenge}

> ## Checking Understanding of `git diff`
>
> Consider this command: `git diff HEAD~9 analysis.txt`. What do you predict this command
> will do if you execute it? What happens when you do execute it? Why?
>
> Try another command, `git diff [ID] analysis.txt`, where [ID] is replaced with
> the unique identifier for your most recent commit. What do you think will happen,
> and what does happen?
{: .challenge}
> ## Getting Rid of Staged Changes
>
> `git checkout` can be used to restore a previous commit when unstaged changes have
> been made, but will it also work for changes that have been staged but not committed?
> Make a change to `analysis.txt`, add that change, and use `git checkout` to see if
> you can remove your change.
{: .challenge}
> ## Explore and Summarize Histories
>
> Exploring history is an important part of Git, and often it is a challenge to find
> the right commit ID, especially if the commit is from several months ago.
>
> Imagine the `analysis` project has more than 50 files.
> You would like to find a commit that modifies some specific text in `analysis.txt`.
> When you type `git log`, a very long list appeared.
> How can you narrow down the search?
>
> Recall that the `git diff` command allows us to explore one specific file,
> e.g., `git diff analysis.txt`. We can apply a similar idea here.
>
> ```
> $ git log analysis.txt
> ```
> {: .language-bash}
>
> Unfortunately some of these commit messages are very ambiguous, e.g., `update files`.
> How can you search through these files?
>
> Both `git diff` and `git log` are very useful and they summarize a different part of the history
> for you.
> Is it possible to combine both? Let's try the following:
>
> ```
> $ git log --patch analysis.txt
> ```
> {: .language-bash}
>
> You should get a long list of output, and you should be able to see both commit messages and
> the difference between each commit.
>
> Question: What does the following command do?
>
> ```
> $ git log --patch HEAD~9 *.txt
> ```
> {: .language-bash}
{: .challenge}
create a new repository called `un-report`.
![Creating a Repository on GitHub (Step 1)](../fig/git/github-create-repo-01.png)
Name your repository `un-report` and then click `Create Repository`.

> ## Important options
>
> Since this repository will be connected to a local repository, it needs to be empty. Leave
> "Initialize this repository with a README" unchecked, and keep "None" as options for both "Add
> .gitignore" and "Add a license." See the "GitHub License and README files" exercise below for a full
> explanation of why the repository needs to be empty.
{: .checklist}
In the screenshots below, the Owner is 'mkuzak' and the Repository name is 'planets'.
You should instead see your own username for the Owner and you should name the
repository `un-report`.
![Creating a Repository on GitHub (Step 2)](../fig/git/github-create-repo-02.png)
![Creating a Repository on GitHub (Step 3)](../fig/git/github-create-repo-03.png)
$ mkdir un-report
$ cd un-report
committed our earlier work on `analysis.txt`, we had a diagram of the local repository
![The Local Repository with Git Staging Area](../fig/git/git-staging-area.svg)
![Freshly-Made GitHub Repository](../fig/git/git-freshly-made-github-repo.svg)
Note that our local repository still contains our earlier work on `analysis.txt`, but the
![Where to Find Repository URL on GitHub](../fig/git/github-find-repo-string.png)
Copy that URL from the browser, go into the local `un-report` repository, and run
$ git remote add origin https://github.com/USERNAME/un-report.git
origin   https://github.com/USERNAME/un-report.git (push)
origin   https://github.com/USERNAME/un-report.git (fetch)
To https://github.com/USERNAME/un-report.git
![GitHub Repository After First Push](../fig/git/github-repo-after-first-push.svg)
From https://github.com/USERNAME/un-report
> Browse to your `un-report` repository on GitHub.
> > From https://github.com/USERNAME/un-report
> > From https://github.com/USERNAME/un-report
For the next step, get into pairs.  One person will be the "Owner" and the other
will be the "Collaborator". The goal is that the Collaborator add changes into
the Owner's repository. We will switch roles at the end, so both persons will
play Owner and Collaborator.

> ## Practicing By Yourself
>
> If you're working through this lesson on your own, you can carry on by opening
> a second terminal window.
> This window will represent your partner, working on another computer. You
> won't need to give anyone access on GitHub, because both 'partners' are you.
{: .callout}

The Owner needs to give the Collaborator access. On GitHub, click the settings
button on the right, select Manage access, click Invite a collaborator, and
then enter your partner's username.

![Adding Collaborators on GitHub](../fig/git/github-add-collaborators.png)

To accept access to the Owner's repo, the Collaborator
needs to go to [https://github.com/notifications](https://github.com/notifications).
Once there she can accept access to the Owner's repo.

Next, the Collaborator needs to download a copy of the Owner's repository to her
 machine. This is called "cloning a repo". To clone the Owner's repo into
her `Desktop` folder, the Collaborator enters:

```
$ git clone https://github.com/USERNAME/un-report.git ~/Desktop/USERNAME-un-report
```
{: .language-bash}

Replace `USERNAME` with the Owner's username.

The Collaborator can now make a change in her clone of the Owner's repository,
exactly the same way as we've been doing before:

```
$ cd ~/Desktop/USERNAME-un-report
$ nano README.md
$ cat README.md
```
{: .language-bash}

You can write anything you like. Now might be a good time to list the
**dependencies** of the project -- the tools and packages that are needed
to run the code.
```
Dependencies:
- R >= 4.0
- tidyverse
```
{: .output}

```
$ git add README.md
$ git commit -m "List dependencies"
```
{: .language-bash}

```
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```
{: .output}

Then push the change to the *Owner's repository* on GitHub:

```
$ git push origin master
```
{: .language-bash}

```
Enumerating objects: 4, done.
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 306 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/USERNAME/un-report.git
   9272da5..29aba7c  master -> master
```
{: .output}

Note that we didn't have to create a remote called `origin`: Git uses this
name by default when we clone a repository.  (This is why `origin` was a
sensible choice earlier when we were setting up remotes by hand.)

Take a look at the Owner's repository on its GitHub website now (you may need
to refresh your browser.) You should be able to see the new commit made by the
Collaborator.

To download the Collaborator's changes from GitHub, the Owner now enters:

```
$ git pull origin master
```
{: .language-bash}

```
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/USERNAME/un-report
 * branch            master     -> FETCH_HEAD
   9272da5..29aba7c  master     -> origin/master
Updating 9272da5..29aba7c
Fast-forward
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```
{: .output}

Now the three repositories (Owner's local, Collaborator's local, and Owner's on
GitHub) are back in sync!

> ## A Basic Collaborative Workflow
>
> In practice, it is good to be sure that you have an updated version of the
> repository you are collaborating on, so you should `git pull` before making
> our changes. The basic collaborative workflow would be:
>
> * update your local repo with `git pull`,
> * make your changes and stage them with `git add`,
> * commit your changes with `git commit -m`, and
> * upload the changes to GitHub with `git push`
>
> It is better to make many commits with smaller changes rather than
> of one commit with massive changes: small commits are easier to
> read and review.
{: .callout}

> ## Switch Roles and Repeat
>
> Switch roles and repeat the whole process.
{: .challenge}

> ## Review Changes
>
> The Owner pushed commits to the repository without giving any information
> to the Collaborator. How can the Collaborator find out what has changed with
> on GitHub?
>
> > ## Solution
> >
> > On GitHub, the Collaborator can go to the repository and click on
> > "commits" to view the most recent commits pushed to the repository.
> {: .solution}
{: .challenge}

> ## Comment Changes in GitHub
>
> The Collaborator has some questions about one line change made by the Owner and
> has some suggestions to propose.
>
> With GitHub, it is possible to comment the diff of a commit. Over the line of
> code to comment, a blue comment icon appears to open a comment window.
>
> The Collaborator posts comments and suggestions using GitHub interface.
{: .challenge}

> ## Version History, Backup, and Version Control
>
> Some backup software can keep a history of the versions of your files. They also
> allows you to recover specific versions. How is this functionality different from version control?
> What are some of the benefits of using version control, Git and GitHub?
{: .challenge}

> ## Some more about remotes
>
> In this episode and the previous one, our local repository has had
> a single "remote", called `origin`. A remote is a copy of the repository
> that is hosted somewhere else, that we can push to and pull from, and
> there's no reason that you have to work with only one. For example,
> on some large projects you might have your own copy in your own GitHub
> account (you'd probably call this `origin`) and also the main "upstream"
> project repository (let's call this `upstream` for the sake of examples).
> You would pull from `upstream` from time to
> time to get the latest updates that other people have committed.
>
> Remember that the name you give to a remote only exists locally. It's
> an alias that you choose - whether `origin`, or `upstream`, or `fred` -
> and not something intrinstic to the remote repository.
>
> The `git remote` family of commands is used to set up and alter the remotes
> associated with a repository. Here are some of the most useful ones:
>
> * `git remote -v` lists all the remotes that are configured (we already used
> this in the last episode)
> * `git remote add [name] [url]` is used to add a new remote
> * `git remote remove [name]` removes a remote. Note that it doesn't affect the
> remote repository at all - it just removes the link to it from the local repo.
> * `git remote set-url [name] [newurl]` changes the URL that is associated
> with the remote. This is useful if it has moved, e.g. to a different GitHub
> account, or from GitHub to a different hosting service. Or, if we made a typo when
> adding it!
> * `git remote rename [oldname] [newname]` changes the local alias by which a remote
> is known - its name. For example, one could use this to change `upstream` to `fred`.
{: .callout}

## Glossary
