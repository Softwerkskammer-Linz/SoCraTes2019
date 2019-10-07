# Advanced Git for the Lazy

As always (especially with git), please do not blindly copy but _read the docs_! This is only meant as an inspiration, not something to copy religiously!

Some of my aliases. Put in your lobal `.git/config`:

    [alias]
    # most used, for lazyness
    br          = branch -vv
    co          = checkout
    ds          = diff --staged
    rbc         = rebase --continue
    mt          = mergetool
    pf          = push --force-with-lease
    st          = status -uall
    # pull with prune and .gitattributes
    pp          = pull -p -Xrenormalize
    # create new remote branch with same name as local
    ppush       = !git push --set-upstream origin `git rev-parse --abbrev-ref HEAD`
    rbi         = !git rebase --interactive --autosquash `git log --format=%H origin/master... | tail -n 1`^
    rbm         = !git fetch && git rebase origin/master -Xrenormalize

    # others
    addn        = add --chmod=-x
    addx        = add --chmod=+x
    wdiff       = diff --word-diff=color
    cdiff       = diff --word-diff=color --word-diff-regex=.
    # tries to remove merged branches
    brprune     = !git remote prune origin && git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -d
    commita     = commit --amend --reset-author
    editconf    = config --global --edit
    # show log for current (feature) branch only, not for master
    lb          = log origin/master..
    lgo         = log --graph --pretty=format:'%C(yellow)%h%Creset%C(cyan)%C(bold)%d%Creset %C(cyan)(%cr)%Creset %C(green)%ce%Creset %s'
    # make stash listing useful
    ls          =  stash list --date=relative
    merged      = branch --merged
    stashall    = stash --include-untracked
    undo        = reset --soft HEAD^

Settings I find useful, also in global `.git/config`:

    [core]
    # windows: use notepad++
    editor = 'c:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin "$*"
    # windows: ignore executable bits (but see addn/addx above!)
    filemode = false
    ignorecase = true
    [diff]
    # 3-way merge tool
    tool = kdiff3
    # show moved lines in different color
    colorMoved = zebra
    [merge]
    tool = kdiff3
    # for .gitattribues
    renormalize = true
    cmd = 'C:/Program Files (x86)/WinMerge/WinMergeU.exe' \"$LOCAL\" \"$REMOTE\"
    [difftool "kdiff3"]
    cmd =  "c:/Program\\ Files/KDiff3/kdiff3.exe" \"$LOCAL\" \"$REMOTE\"
    trustExitCode = false
    [mergetool "kdiff3"]
    cmd = "c:/Program\\ Files/KDiff3/kdiff3.exe" \"$BASE\" \"$LOCAL\" \"$REMOTE\" -o \"$MERGED\"
    keepBackup = false
    trustExitCode = false
    [mergetool]
    prompt = false
    [difftool]
    prompt = false
    [log]
    decorate = auto
    [fetch]
    # useful if you have a lot of churn
    prune = true
    [rebase]
    # super easy updates, see rbm above
    autostash = true
    [rerere]
    # partly automate repeated merges
    enabled = true

Put something like this in your repo's `.git/config` to limit what you fetch, e.g. to avoid others' feature branches:

    [remote "origin"]
    fetch = +refs/heads/master:refs/remotes/origin/master
    fetch = +refs/heads/release/*:refs/remotes/origin/release/*

If you want to dive into `.gitattributes`, this could be another place to pick and choose from: https://github.com/alexkaratarakis/gitattributes

I don't recommend concatenating all files you could use, only take what you really need and remember to `git add -u --renormalize` before committing changes to `.gitattributes`