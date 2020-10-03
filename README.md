# git workflow

How I use [git](https://git-scm.com) and [gitHub](https://github.com).

Git is super powerful tool with lots of ways to use it. Like with coding,
following certain patterns help to avoid lots of troubles here.

Whenever possible, I use a variation of
[GitFlow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow),
even in my private projects.

## Roles
Setting roles is essential for teamwork and for any kind of cooperation.

Even when soloing, it is good to be aware of what role am I in when doing something.

### Implementor
Creates actual content by adding to / improving it. Without _**implementor**_, nothing happens.

### Manager
Is responsible for updating a non-personal branch. There may be a number of managers with personal
responsibility scope in big projects.

## Branches
   * the _**`master`**_ branch represents the "official" state of the project. In case of app development,
   the deployments reflect the master contents.
      - for ideological reasons, _`main`_ is sometimes preferred over _`master`_.
      Here we talk about branch hierarchies, not importance, so let's keep using  _"master"_ for clarity. 
   * the _**`develop`**_ branch is for development team and for monitoring.
   * the _**feature branch**_ under the _`develop`_ are essentially bound to an issue list ticket or alike.
   * the _**personal branch**_ is exclusively owned by an implementor. It may emerge from a _feature branch_ or
   be a _feature branch_ itself.
   
## Workflows

### Initializing
Role: _Manager_.
1. Create a new directory containing at least .gitignore and README.md file. The README contains
project title, a short description and status statement, e.g. "No useful data yet.";
1. `git init && git add -A && git commit -m "Initial commit"`
1. `git remote add origin https://github.com/{OWNER}/{PROJECT}.git`
1. `git push -u origin master`
1. `# Create 'develop' branch and both are sync it with the central repository` <br />
   `git checkout -b develop && git push --set-upstream origin develop`
1. Now, it may be a good idea to make the _`develop`_ a default branch of the central repository.

### Create a personal feature branch
Role: implementor. 
1. `git checkout develop && git pull --rebase` -- make sure your copy is up-to-date;
1. `git checkout -b <my-ticket> && git push --set-upstream origin <my-ticket>` 
1. Now do whatever you like in this branch, but commit and push often!

### Complete a feature (phase #1)
Role: _implementor_. Tests run nicely, everything feels fine... but let the others decide.
1. Send a message to other team members:
   * I think I'm done with \<my-ticket\>. Please check it out and let me know -
   * visit `https://github.com/valango/git-workflow/pull/new/<my-ticket>`
1. A code review or other form of communication should follow, you may have to redo something.

### Complete a feature (phase #2)
Role: _implementor_. Finally, you've got the _manager's_ blessing.
1. `git checkout develop && git pull --rebase` -- make sure your copy is up-to-date;
1. `git checkout <my-ticket>`   -- do not forget this! ;)
1. `git tag -a done#<N>`  -- by this tag you'll know later what was sent and when;
1. `git rebase -i <branch-root>`  -- interactively leave only the meaningful descriptions;
1. `git rebase develop` -- make sure the merge will be as clean as possible;
1. `git merge <my-ticket>-tmp develop`
1. `git push`  -- update 'develop' branch in central repo.

In case you think you'll need a detailed commit history as it was
until the step #4, create a separate branch before it.

In bigger projects, the last 3 steps should be done by _manager_, so nobody will update
the central _`develop`_, while other steps in progress.

## References
1. [Git: official reference](https://git-scm.com/docs/)
1. [Git: other documentation](https://git-scm.com/doc/)
1. [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)
1. [Git (at) Atlassian Bitbucket](https://www.atlassian.com/git)
