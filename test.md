## Branches

  - [1.1](#) Choose short and descriptive names.
    > Identifiers from corresponding tickets in an external service (eg. a GitHub issue) are also good candidates for use in branch names.
  
    ```
    # good
    $ git checkout -b feature/oauth
    
    # good: using identifiers
    $ git checkout -b fix/issue-15

    # bad: too vague
    $ git checkout -b login_fix
    ```
    
  - [1.2](#) Use dashes to separate words.
  
    ```sh
    # good
    $ git checkout -b feature/add-webhook

    # bad
    $ git checkout -b feature/add_webhook
    ```
    
## Commits

  - [2.1](#) Each commit should be a single logical change. 
    > Don't make several logical changes in one commit. For example, if a patch fixes a bug and optimizes the performance of a feature, split it into two separate commits.
    
    > **Tip:** Use git add -p to interactively stage specific portions of the modified files.
    
  - [2.2](#) Don't split a single logical change into several commits.
    > For example, the implementation of a feature and the corresponding tests should be in the same commit.
      
  - [2.3](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.
    
    > **Tip:** Use git add -p to interactively stage specific portions of the modified files.
    
  - [2.4](#) Commits should be ordered logically.
    > If commit X depends on changes done in commit Y, then commit Y should come before commit X. Similarly, if commit A solves a bug introduced by commit B, it should also be stated in the message of commit A.


  - [2.5](#) NEVER let a commit break any working functionality.
    > ALWAYS guarantee that master only contains commits that work, have their own tests and fixes.  
    
    > **Note:** While working alone on a local branch that has not yet been pushed, it's fine to use commits as temporary snapshots of your work. However, it still holds true that you should apply all of the above before pushing it. To do that it's really important to understand git rebase -i 
    
## Messages

  - [3.1](#) Use the editor, not the terminal, when writing a commit message.
  
    ```sh
    # good
    $ git commit

    # bad: no commit message
    $ git commit -m "Quick fix"
    ```
  
  - [3.2](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.
  - [2.8](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.
  - [2.9](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.
   
  - [2.6](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.
  - [2.7](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.
  - [2.8](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.
  - [2.9](#) Commit early and often.
    > Small, self-contained commits are easier to understand and revert when something goes wrong.


Messages
Use the editor, not the terminal, when writing a commit message:
# good
$ git commit

# bad
$ git commit -m "Quick fix"

Committing from the terminal encourages a mindset of having to fit everything in a single line which usually results in non-informative, ambiguous commit messages.
A commit messages consists of three distinct parts separated by a blank line: the title, an optional body and an optional footer. The layout looks like this:
type: subject

body

footer
The title consists of the type of the message and subject.
Type
The type is contained within the title and can be one of these types:
feat: a new feature
fix: a bug fix
docs: changes to documentation
style: formatting, missing semi colons, etc; no code change
refactor: refactoring production code
test: adding tests, refactoring test; no production code change
chore: updating build tasks, package manager configs, etc; no production code change
Subject
Subjects should be no greater than 50 characters, should begin with a capital letter and do not end with a period.
Use an imperative tone to describe what a commit does, rather than what it did. For example, use change; not changed or changes.
Body
Not all commits are complex enough to warrant a body, therefore it is optional and only used when a commit requires a bit of explanation and context. Use the body to explain the what and why of a commit, not the how.
When writing a body, the blank line between the title and the body is required and you should limit the length of each line to no more than 72 characters.
Ultimately, when writing a commit message, think about what you would need to know if you run across the commit in a year from now.
Footer
The footer is optional and is used to reference issue tracker IDs.
Example Commit Message
feat: Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
Merging
Do not rewrite published history. The repository's history is valuable in its own right and it is very important to be able to tell what actually happened. Altering published history is a common source of problems for anyone working on the project.
However, there are cases where rewriting history is legitimate. These are when:
You are the only one working on the branch and it is not being reviewed.
You want to tidy up your branch (eg. squash commits) and/or rebase it onto the "master" in order to merge it later.
That said, never rewrite the history of the "master" branch or any other special branches (ie. used by production or CI servers).
Keep the history clean and simple. Just before you merge your branch:
Make sure it conforms to the style guide and perform any needed actions if it doesn't (squash/reorder commits, reword messages etc.)
Rebase it onto the branch it's going to be merged to (Note: This strategy is better suited for projects with short-running branches. Otherwise it might be better to occasionally merge the "master" branch instead of rebasing onto it):
[chore/refactor] $ git fetch
[chore/refactor] $ git rebase origin/master
# then merge
This results in a branch that can be applied directly to the end of the "master" branch and results in a very simple history.
NEVER commit something like "Fix linter" or "Fix tests". These "fixes" should be squashed to the commits that originated the change. 
NEVER fully squash a branch before merging it, unless the whole branch (all commits) are related to a single logical change.
NEVER use  git merge master on a branch. ALWAYS use git rebase master, then force-push, wait for the CI to clear and only then merge into master.
CONVENTION is to always use Github's web interface to merge into master and NEVER using Git on the command-line (i.e. git checkout master; git merge --no-ff branch; git push). This avoids confusion and forgetting about some really important things such as non-fast-forward merge.
Use the Common Sense, Luke. 
Use the Common Sense, Luke. FOLLOW THIS GUIDE! This is really important, otherwise we would not make you read this before contributing to our repositories. 
Be consistent. This is related to the work-flow but also expands to things like commit messages, branch names and tags. Having a consistent style throughout the repository makes it easy to understand what is going on by looking at the log, a commit message etc.
Test before you push. Do not push half-done work.
Use annotated tags for marking releases or other important points in the history. Prefer lightweight tags for personal use, such as to bookmark commits for future reference.
Keep your repositories at a good shape by performing maintenance tasks occasionally:
git-gc(1)
git-prune(1)
git-fsck(1)
