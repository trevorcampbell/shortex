# TC LaTeX Header
Just a header file with useful mathematics definitions and package includes.

Modified from the original by Jonathan Huggins / Dan Roy / Ryan Adams.

To use this in your latex git project:

1. Set tchdr as a remote: 

`git remote add git@github.com:trevorcampbell/tchdr.git`

2. Pull tchdr as a subtree into the tchdr folder: 

`git subtree pull --prefix [your_repository_location]/tchdr tchdr master --squash`

3. In your main LaTeX file, add tchdr to the preamble: 

`\usepackage{tchdr/tchdr}`

Any time you want an updated version of tchdr.sty, run 2. again.

In order to push your own changes to tchdr:

1. Create your own fork of tchdr, and add it as a remote: 

`git remote add tchdrfork [url_to_your_fork]`

2. Push the changes to your fork: 

`git subtree push --prefix [your_repository_location]/tchdr tchdrfork master`

3. Open a pull request for your fork to merge into tchdr 
