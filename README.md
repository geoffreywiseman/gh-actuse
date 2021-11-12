# GitHub Actions Usage

A simple extension to display the usage (in time) of the GitHub Actions workflows in the current repository. This can be used to look at how various repositories are contributing to your overall GitHub Actions usage without needing to download the usage report and calculate subtotals.

The current implementation is a bash script wrapped around the `gh` cli.

## Installing

You can install the extension using `gh`:

```
❯ gh extension install geoffreywiseman/gh-actuse
Cloning into '~/.local/share/gh/extensions/gh-actuse'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 4 (delta 0), pack-reused 0
Receiving objects: 100% (4/4), done.
❯
```

## Usage
The current usage is extremely simple -- invoke `gh actuse` from any locally checked out repository:

```
❯ gh actuse
GitHub Actions Usage

Workflow 'CI' Usage: 15h (911m)
Workflow 'CodeQL' Usage: 3h (183m)
Repo 'project' Total Usage: 18h (1094m)
❯
```

## Future Expansion

Some things that would be nice to add (and you're welcome to encourage):

- Org-Level Usage
    - Iterate over all the workflows in all the repos of an org and display all usage
    - Display the included minutes from the billing resource.
- Specify Repo
    - Right now the extension assumes you want the current repo; wouldn't be that hard to allow you to specify a different repo

Some things that I'd like to add, but don't see a way to accomplish:

- Actions Storage
    - I haven't found the storage usage of actions in the API anywhere, so I'm not displaying it.

On the technology side of things, I was originally planning on building this in Go (golang) as I've seen other GH extensions in Go but near as I can tell that would make it harder to work with private repos -- I'd need some way to get the authorization information, whereas wrapping Bash around `gh api`, ugly tho it is, lets me piggy back on the authorization you've already given `gh`.  I may look into this a bit more, because enhancing this extension by building more bash around more GH invocations with limited ability to handle JSON output isn't very appealing.
