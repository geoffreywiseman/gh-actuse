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
```

## Usage
The current usage is extremely simple -- invoke `gh actuse` from any locally checked out repository:

```
❯ gh actuse
GitHub Actions Usage

Workflow 'CI' Usage: 15h (911m)
Workflow 'CodeQL' Usage: 3h (183m)
Repo 'project' Total Usage: 18h (1094m)
```

Or if you prefer, `gh actuse <repos>` to specify one or more GitHub repositories to which you have access:

```
❯ gh actuse google/go-github google/guava
GitHub Actions Usage

Repo google/go-github:
- Workflow 'linter' Usage: 0ms
- Workflow 'tests' Usage: 0ms
- Total Usage: 0ms

Repo google/guava:
- Workflow 'CI' Usage: 0ms
- Workflow '.github/workflows/dependabot.yml' Usage: 0ms
- Workflow 'Validate Gradle Wrapper' Usage: 0ms
- Total Usage: 0ms
```

Or, if you want to get information across a whole organization:
```
❯ gh actuse google
```

You need admin scope access to the organization to access the list of repos enabled for GH Actions, though.


## Future Enhancements

Things I've already considered adding and that seem possible to accomplish are listed in GitHub Issues. You're welcome to vote or contribute, or suggest a feature that you'd like that I haven't already listed.

Some things that I'd like to add, but don't see a way to accomplish using the API:

- Actions Storage
    - I haven't found the storage usage of actions in the API anywhere, so I'm not displaying it.
- Other Timeframes
    - You can only get actions usage for the current time window, near as I can see, so you can't say "for the past three days" or "over the past six months" or "total by week for the past six weeks"

On the technology side of things, I was originally planning on building this in Go (golang) as I've seen other GH extensions in Go but near as I can tell that would make it harder to work with private repos -- I'd need some way to get the authorization information, whereas wrapping Bash around `gh api`, ugly tho it is, lets me piggy back on the authorization you've already given `gh`.  I may look into this a bit more, because enhancing this extension by building more bash around more GH invocations with limited ability to handle JSON output isn't very appealing.
