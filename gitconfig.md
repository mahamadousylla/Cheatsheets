# This is Git's per-user configuration file.
[user]
	email = msylla@uci.edu
# Please adapt and uncomment the following lines:
#	name = Mahamadou Sylla
#	email = msylla@uci.edu
[url "git@github.com:"]
	insteadOf = https://github.com/
[pull]
	rebase = true
[url "ssh://git@github.com/"]
	insteadOf = https://github.com/
[rebase]
	autoStash = true
[fetch]
	pruneTags = true
	prune = true
[alias]
	count = rev-list --count main..HEAD
	pushf = push --force-with-lease
	undo = reset --soft HEAD~
	count-head = rev-list --count HEAD
[push]
	default = current
[core]
	editor = code --wait
