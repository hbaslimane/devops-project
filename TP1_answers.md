# TP1 — Source Control Management

**Name:** BASLIMANE HADJ AISSA  
**GitHub username:** hbaslimane

## Exercise 1

### (a)
The two hidden files are `.env.example` and `.gitignore`.

### (b)
Using `cp -r .../ctf-scoreboard/*` copies the non-hidden files and directories matched by `*`, but normally excludes dotfiles such as `.gitignore` and `.env.example`. Using `cp -r .../ctf-scoreboard/. .` also copies the hidden files.

### (c)
Adding `.env` to `.gitignore` does not remove it from Git tracking if it was already committed. The file remains in the repository history, so the secret may still be accessible from earlier commits.


## Exercise 2

### (a)
Git cannot merge automatically because both branches modified the same part of `data/challenges.yaml`, changing the points value to different values (600 and 450). Git cannot determine which value should be kept.

### (b)
If the changes were made to two different challenges in the same file, Git could usually merge them automatically because the edits would not overlap.

### (c)
A conflict-marker check can run automatically in a CI pipeline or GitHub Actions workflow before a change is accepted or merged.


## Exercise 3

### (a)
Git bisect tested 5 commits to identify the first bad commit in this lab run.

### (b)
The theoretical number of steps is approximately \(\lceil \log_2 31 \rceil = 5\). This matches the 5 commits tested during the bisect run.

### (c)
If `check.sh` were inside the repository and modified during the bisect process, Git could switch between commits where the script differs or does not exist. This could make the test unreliable. Keeping it in `/tmp` avoids that problem.

### (d)
If the 31 commits were squashed into one commit, bisect could not identify the original bug-introducing commit within that squashed history. It could only identify the available commit boundary as bad.


## Exercise 4

### (a)
The directory scan (`gitleaks dir .`) returned exit code `0` because no leaks were found in the current files. The Git history scan (`gitleaks git -v .`) returned exit code `1` because it found one leak in an earlier commit.

### (b)
The matched rule ID was `aws-access-token`.

### (c)
Each Git commit records a snapshot of the tracked files and links to its parent commit. The second commit removed the fake key from the current version of the file, but the earlier commit still contains it in Git history. Therefore, Gitleaks can still detect it.

### (d)
First, immediately revoke or rotate the exposed credential so it can no longer be used. Second, remove the secret from the repository and, if necessary, clean the Git history. Rewriting history alone is not enough because the exposed credential may already have been copied.


## Exercise 5

### (a)
Branch protection is a security control because it requires changes to important branches to be submitted through pull requests and reviewed before merging. It also prevents force pushes and branch deletion, helping protect the integrity of the repository.

### (b)
It makes it harder for an attacker or compromised account to push malicious changes directly to `main` or overwrite trusted branch history using a force push.

### (c)
The lab requires a public repository because the branch protection and pull request features used in this exercise must be available under the GitHub plan being used.
