# GIT

All code developed for our projects must be tracked in version control through
GIT. With the exception of generic components that we choose to
[open source](./OPEN_SOURCE.md), all repositories will be set to private in our
GitHub account. Even so, care should be taken against committing any credentials
or potentially sensitive information.

## Branching

Projects follow the GIT Flow branching model, with development being performed
on named branches. When a feature is complete, a pull request is opened in
GitHub for review by another member of the team. Traditional GIT Flow allows for
`feature`, `bug`, and `chore` branches. In addition, we encourage the use of any
of the following types which are used when composing the final commit message:

- **feat**: A new feature representing added user functionality
- **fix**: A bug fix
- **docs**: Documentation only changes
- **style**: Changes that do not affect the meaning of the code (white-space,
  formatting, missing semi-colons, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing tests or correcting existing tests
- **build**: Changes that affect the build system or external dependencies
  (example scopes: gulp, broccoli, npm)
- **ci**: Changes to our CI configuration files and scripts (example scopes:
  Travis, Circle, BrowserStack, SauceLabs)
- **chore**: Other changes that don't modify src or test files

Once the feature is complete and marked as Ready to Merge, all commits are
squashed into a single commit following our
[Commit Message Format guidelines](#commit-message-format). The approved pull
request will be merged as a fast-forward commit.

For this reason it is important that work on a feature or bug branch represent a
narrow vertical slice of complete functionality. Refactoring neighboring code or
fixing bugs should happen on their own branch unless they are directly required
for the feature work being performed.

## Commit message format

We follow Google's Commit Message Guidelines to maintain consistent and more
readable commit messages that are easier to follow when looking through the
project history.

The header of a commit message has a special format that includes a **type**,
a **scope** and a **subject**. Any line of the commit message should never
exceed 100 characters:

```
<type>(<scope>): <subject>
```

Both the type and the scope should correspond with the labels attached to the
issue. The subject should contain a succinct description of the change
introduced:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize first letter
* no dot (.) at the end

Work in progress development happening on feature branches do not need to adhere
to this commit message format until a pull request is opened and marked as
ready for merge. While a feature is in progress it is encouraged to commit often
with descriptive messages.

All commits representing a vertical slice of usable functionality will be
squashed upon approval prior to merge.
