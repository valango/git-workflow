# git workflow

How I use [git](https://git-scm.com/) and [gitHub](https://github.com/).

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
project title, a short description and status statement, e.g. _"No useful data yet.";
1. `git init && git add -A && git commit -m "Initial commit"`
1. `git remote add origin https://github.com/{OWNER}/{PROJECT}.git`
1. `git push -u origin master`
1. `# Create 'develop' branch and both are sync it with the central repository` <br />
   `git checkout -b develop && git push --set-upstream origin develop`
1. Now, it may be a good idea to make the _`develop`_ a default branch of the central repository.

### Create a personal feature branch
Role: implementor. 
1. `git checkout develop && git pull --rebase` -- make sure your copy is up-to-date;
1. `git checkout -b {my-assigned-ticket}` -- do whatever you like in this branch; commit and push often!

## References
1. [Git: official reference](https://git-scm.com/docs/)
1. [Git: other documentation](https://git-scm.com/doc/)
1. [Patterns for Managing Source Code Branches](https://martinfowler.com/articles/branching-patterns.html)
1. [Git (at) Atlassian Bitbucket](https://www.atlassian.com/git)
