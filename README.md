# fed-to-brew
fed-to-brew is a multipurpose tool to help tracking, syncing, and building packages between fedora and brew.

--

Usage fed-to-brew [command] <options> <[package 1] ... [package n]>                                                                                                                    
                                                                                                                                                                                       
Multipurpose tool to help tracking, syncing, building packages between                                                                                                                 
  fedora and brew.                                                                                                                                                                     
                                                                                                                                                                                       
**Commands:** (there must be one command, only one)                                                                                                                                        
    --sync                                                                                                                                                                               
        Sync package(s) from Fedora dist-git to Brew dist-git.                                                                                                                             
        Only syncs from one git commit, does not do entire history.                                                                                                                        
        Mandatory: --brew-branch                                                                                                                                                           
        Mandatory: --yaml OR --txt OR [package]                                                                                                                                                                               
  --check                                                                                                                                                                              
    Check the status of builds                                                                                                                                                                               
  --build --rebuild                                                                                                                                                                               
    Build package(s) in brew, if they have not already been built.                                                                                                                                                                               
    Will sync packages Fedora dist-git to Brew dist-git if needed.                                                                                                                                                                               
    Mandatory: --brew-branch                                                                                                                                                                               
    Mandatory: --brew-dist                                                                                                                                                                               
    Mandatory: --yaml OR --text OR [package]                                                                                                                                                                               

**Options:**
  -c --checkout [branch or hash]                                                                                                                                                                               
    What to checkout of the fedora dist-git, can be branch or hash                                                                                                                                                                               
    Warning: If using hash, only use one package                                                                                                                                                                               
    Default: master                                                                                                                                                                               
    Example branch: f26                                                                                                                                                                               
    Example hash: 082464dc0d06d48d2f9c4d2110e8aafe4ef1c957                                                                                                                                                                               
  -bb --brew-branch [branch]                                                                                                                                                                               
    What brew branch to sync to                                                                                                                                                                               
  -fd --fed-dist [dist]                                                                                                                                                                               
    What to dist to pull the fedora source from                                                                                                                                                                               
    Should only be needed if using a hash for checkout                                                                                                                                                                               
    Default: rawhide                                                                                                                                                                               
    Example: f26                                                                                                                                                                               
  -bd --brew-dist [dist]                                                                                                                                                                               
    What dist tag to use when checking brew build status                                                                                                                                                                               
    Example: .el7                                                                                                                                                                               
  -m --message [message]                                                                                                                                                                               
    Use a custom commit message for brew dist-git                                                                                                                                                                               
  --text [file]                                                                                                                                                                               
    Text file to use for list of packages                                                                                                                                                                               
      Each package is on its own line in format <n-v-r>.src                                                                                                                                                                               
      Example:acl-2.2.52-15.fc27.src                                                                                                                                                                               
  --yaml [file]                                                                                                                                                                               
    yaml file to use for list of packages                                                                                                                                                                               
      Should be in the standard fedora module yaml file format.                                                                                                                                                                               
  -v --verbose --debug                                                                                                                                                                               
    Be verbose, for debugging                                                                                                                                                                               
  -h, --help                                                                                                                                                                               
    Show this options menu                                                                                                                                                                               

**Other:**                                                                                                                                                                               
  [package]                                                                                                                                                                               
    If you want to do just a single file, list just the name                                                                                                                                                                               
    Not applied if either --yaml or --text are used.                                                                                                                                                                               

