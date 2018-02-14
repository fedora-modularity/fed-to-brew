# fed-to-brew
fed-to-brew is a multipurpose tool to help tracking, syncing, and building packages between fedora and brew.

fed-to-brew.conf has to be in the same directory as fed-to-brew, or in /etc/.  This seperate configuration file allows you to customize variables so you do not have to keep setting them as options.

## Configuration

### Setup
**fed-to-brew** can be set anywhere.  If it is not in your path, you will need to specifically call it with ./fed-to-brew

**fed-to-brew.conf** needs to be either in /etc/ or in the same directory as fed-to-brew

### User Setable Variables
 * WORKDIR
   * Where all the maps, results, logs, and general work gets done
   * Example: ${HOME}/fedtobrew
 * FED_GIT_CHECKOUT
   * What to checkout of the fedora dist-git to sync to brew
   * Can be a dist-git branch or a git hash
   * Example1: master  Example2: f26
   * Example3: 082464dc0d06d48d2f9c4d2110e8aafe4ef1c957
 * FED_DIST
   * What is %dist set to in fedora
   * Used when pulling sources for syncing
   * Set to rawhide if using rawhide branch
   * Example: f26
 * BREW_WEB_URL
   * What is URL to Brew Koji Web interface?
   * Example: https://brewweb.example.com/brew
 * BREW_DISTGIT_URL
   * What is URL to packages dis-git?
   * Example: http://packages.example.com/cgit
 * BREW_BRANCH
   * What branch in brew dist-git to sync into
   * Examples: rhel-7.4
 * BREW_DIST
   * What is %dist set to in brew
   * Used for checking if a package is built in brew.
   * Example: .el7
 * SYNC_REMOTE
   * Where to rsync maps and results
   * Blank - No rsync, local only
   * Example: SYNC_REMOTE="user@mymachine.mydomain:/home/user/fedtobrew/"

## Usage

Usage fed-to-brew [command] <options> <[package 1] ... [package n]>

Multipurpose tool to help tracking, syncing, building packages between
  fedora and brew.

**Commands:** (there must be one command, only one)
 * --sync
   * Sync package(s) from Fedora dist-git to Brew dist-git.
   * Only syncs from one git commit, does not do entire history.
   * Mandatory: --yaml OR --txt OR [package]
 * --check
   * Check the status of builds
 * --double-check --dc --doublecheck
   * Goes through an entire release and double checks all the builds
 * --check-modules --checkmodules
   * Check the modules to see if all their packages built.
 * --build --rebuild
   * Build package(s) in brew, if they have not already been built.
   * Will sync packages Fedora dist-git to Brew dist-git if needed.
   * Mandatory: --brew-branch
   * Mandatory: --brew-dist
   * Mandatory: --yaml OR --text OR [package]

**Options:**
 * -c --checkout [branch or hash]
   * What to checkout of the fedora dist-git, can be branch or hash
   * Warning: If using hash, only use one package
   * Default: master
   * Example branch: f26
   * Example hash: 082464dc0d06d48d2f9c4d2110e8aafe4ef1c957
 * -bb --brew-branch [branch]
   * What brew branch to sync to
 * -fd --fed-dist [dist]
   * What to dist to pull the fedora source from
   * Should only be needed if using a hash for checkout
   * Default: rawhide
   * Example: f26
 * -bd --brew-dist [dist]
   * What dist tag to use when checking brew build status
   * Example: .el7
 * -m --message [message]
   * Use a custom commit message for brew dist-git
 * --text [file]
   * Text file to use for list of packages
   * Each package is on its own line in format <n-v-r>.src
   * Example:acl-2.2.52-15.fc27.src
 * --yaml [file]
   * yaml file to use for list of packages
   * Should be in the standard fedora module yaml file format.
 * --no-remote --noremote
   * Do not sync map ore results remotely.  Default: FALSE 
 * -v --verbose --debug
   * Be verbose, for debugging
 * -h, --help
   * Show this options menu

**Other:**
 * [package]
   * If you want to do just a single file, list just the name
   * Not applied if either --yaml or --text are used.

