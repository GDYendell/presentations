---
theme: night
transition: fade
loop: true
width: 1920
height: 1080
---

## Useful Git History

### The Lazy Way

---

#### Content Warning

This talk may contain opinions.

---

#### Why Does Git History Matter?​

Creates a clear story of what will change to main when something is merged

Reduces cognitive load in understanding a PR

Allows changes to be split into smaller PRs or removed entirely if not agreed

![|250](https://media.tenor.com/qaNEp-0gKPIAAAAM/shrek-mad.gif)

notes: 
- Small, atomic commits that update/add tests/docs as appropriate with good descriptions of what they change and why.
- Viewing the entire diff in one go can be overwhelming, it is much easier if it is possible to click through each commit and consider it separately.
- If one part needs to go in urgently and another needs more thought - or is not accepted - they can be split.

---

#### What is Clean History?

Atomic commits that add a minimal unit of change, with tests and documentation

Any mistakes, work-in-progress, dead-ends and refactoring squashed to the final result

Provides a good overview of what the changes are without looking at the diff

notes:
- If there is a typo, or you forgot to add docs, or the new feature doesn't work, or it doesn't actually fix a bug like it says.
- If it is important to show that you tried to do it one way and then changed it, it can be noted in PR description, with code snippets if necessary.
- Someone in the future may have to look at old commits and figure out why something was done and what problem it was trying to solve. 

--
#### Descriptive commit messages

Short subject line with imperative mood

Use the commit body to add detail

```text
Add format field to Text{Read,Write} widgets

A new TextFormat enum is used to store generic text format
types and each UI formatter implements them by inserting the
appropriate widget field during formatting.

This allows configuring the diplay format of the widget for
individual signals, for example in exponential format rather
than decimal.

Fixes #7
```

notes:
- Subject line should be 50 charactesr if you don't want it to be truncated in GitHub
- Can use prose, bullet points, ascii art in body
- Description of what the commit will changed, why things are done in a certain way, ticket numbers, dependencies and related issues or changes

---

![|300](https://media.tenor.com/PonTZwa1nsYAAAAd/wandavision-loki.gif)

#### What is (Semi-)Linear History?

`main` is now, all dev branches are proposing the future​

If  `main` moves forward, `future` moves to come afterwards

Rebase `future` on `main` rather than merging `main` into `future`

notes:
- Orders commits by the time they were added to main, not by the time they were created.
- main has happened, releases have been made and people are using it, don't merge older things in afterwards
- Time Variance Authority will prune your timeline if it is deemed too dangerous to exist
- Avoids pointless merge commits and more importantly avoids merge commits where conflicts were resolved, which are particularly hard to read.
- Stops git graph becoming unreadable.
- Linear history means also no merge commits, just one straight line with fast-forward

--
<grid drag="100 20" drop="top">
#### Merging Branches
</grid>
<grid drag="50 50" drop="left">
![](https://www.bitsnbites.eu/wp-content/uploads/2015/12/1-nonlinear-vs-linear.png)
</grid>
<grid drag="50 30" drop="right">
![|500](https://www.bitsnbites.eu/wp-content/uploads/2015/12/3-merging-master-into-topic.png)
![|500](https://www.bitsnbites.eu/wp-content/uploads/2015/12/4-rebasing.png)
</grid>

notes:
- This is what linear and non-linear history looks like
- Merge left, rebase right
- Even if you have merge commits on your dev branch, you can rebase with `--rebase-merges`

---

### Worklog vs Recipe

Worklog - What was changed in the order it happened while a feature was developed

Recipe - What needs to happen to main to add the feature

notes: 
- These can both be done well or badly

---
#### Pull Request Workflow

Options to add further changes based on review:
1. Push more commits and squash-merge
2. Push fixup commits and squash before merge
3. Amend existing commits and force push

notes:
- Third option can be a pain to review if the changes are small, sometimes you just want to see a typo fix has been made and not have to look through the whole diff again.
- If large changes are requested then sometimes the third option is actually easier to work with, and because a large chunk of it will need reviewing again it makes sense.
- The first option means you lose any separation of the changes, but if the commits are a mess already then this is a good option, but you don't get an explicit merge commit.
- But if you have some small code changes and some massive diff from some test output then it would be better to retain separate commits.

---
`</opinions>`

notes:
- You don't need to agree with any of this for the rest of the talk to be useful
---

That's great, but git CLI makes me sad

notes:
- You may say that git makes you sad, and you would be right

---
Git CLI
```bash
❯ git stash
❯ git rebase -i HEAD~5
❯ git stash apply
❯ git add --patch ...
Stage this hunk [y/n/a/d/K/j/J/e/?]? n
Stage this hunk [y/n/a/d/K/j/J/e/?]? y
Stage this hunk [y/n/a/d/K/j/J/e/?]? s
Stage this hunk [y/n/a/d/K/j/J/e/?]? n
Stage this hunk [y/n/a/d/K/j/J/e/?]? y
❯ git commit --amend
❯ git rebase --continue
```

![|250](https://media2.giphy.com/media/BbJdwrOsM7nTa/200.webp?cid=ecf05e47nuq9p0al272y07hjy1gbss4g03xbejyfs75pszrg&ep=v1_gifs_search&rid=200.webp&ct=g)

notes:
- I'm not here to tell you that this is the answer to your problems
- But it doesn't have to be like this

---

![|500](https://user-images.githubusercontent.com/8456633/174470852-339b5011-5800-4bb9-a628-ff230aa8cd4e.png)

<small>

> If you're a mere mortal like me and you're tired of hearing how powerful git is when in your daily life it's a powerful pain in your ass, lazygit might be for you.

\- Jesse Duffield, author of Lazygit
</small>

---
### Lazygit makes simple commands faster

fetch, reset, pull, rebase, stage, commit, push

in a few key presses

notes:
- or mouse clicks

---
<grid drag="90 20" drop="top">
### Browse Files, Branches, Commits 
</grid>

<grid drag="45 45" drop="left">
![[files.png]]
</grid>
<grid drag="45 45" drop="right">
![[branches.png]]
</grid>
<grid drag="45 45" drop="bottom">
![[commits.png]]
</grid>

---
## Graph

![|800](https://github.com/jesseduffield/lazygit/raw/assets/demo/commit_graph-compressed.gif)

---
### Stage, Commit, Push

![|800](https://github.com/jesseduffield/lazygit/raw/assets/demo/commit_and_push-compressed.gif)

---
### Lazygit makes complicated commands easier

Stage specific lines of file

Add staged changes to any commit

Change commit messages

Remove changes from a commit

notes:
- or move to a different commit
- or pull back into index

---
## Stage Individual Lines

![|800](https://github.com/jesseduffield/lazygit/raw/assets/demo/stage_lines-compressed.gif)

---
## Interactive Rebase

![|800](https://github.com/jesseduffield/lazygit/raw/assets/demo/interactive_rebase-compressed.gif)

notes:
- VSCode support for this is also pretty great.

---
## Amend Commits

![|800](https://github.com/jesseduffield/lazygit/raw/assets/demo/amend_old_commit-compressed.gif)

---
## Remove Changes From A Commit

![|800](https://github.com/jesseduffield/lazygit/raw/assets/demo/custom_patch-compressed.gif)

---

<grid drag="100 20" drop="top">
## Install
</grid>

<grid drag="40 65" drop="left">
![](https://camo.githubusercontent.com/ce934b17e865da1908bae8152933a9e1032decd68510479b29169ddaf0716cf2/68747470733a2f2f7265706f6c6f67792e6f72672f62616467652f766572746963616c2d616c6c7265706f732f6c617a796769742e737667)
</grid>

<grid drag="35 10" drop="-7 45">
```
alias lg="lazygit $@"
```
</grid>

<grid drag="100 10" drop="bottom">
https://github.com/jesseduffield/lazygit#installation
</grid>

notes:
- If you are super lazy like me alias lg is nice
---

### Links

- https://github.com/jesseduffield/lazygit
- https://www.bitsnbites.eu/a-tidy-linear-git-history/
- https://medium.com/@catalinaturlea/clean-git-history-a-step-by-step-guide-eefc0ad8696d
- https://cbea.ms/git-commit/
- https://congtuanle.medium.com/git-the-power-of-fixup-autosquash-f1c91f7d962b
- https://adamj.eu/tech/2022/11/07/pre-commit-run-hooks-rebase/
- https://mszturc.github.io/obsidian-advanced-slides/

---
### Things I Left Out

- Pull changes from commit into index
- Cherry pick
- Bisect to find breaking commit
- Undo from reflog
- Diff any two refs
- View changes in remote branches 
- View and apply stashes

---
## Thanks!

##### (Bonus Action - Nuke Working Tree)

![|500](https://github.com/jesseduffield/lazygit/raw/assets/demo/nuke_working_tree-compressed.gif)