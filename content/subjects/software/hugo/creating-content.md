---
title: "Creating Hugo Content"
date: 2022-02-03T15:36:09+05:30
draft: true
---

The content stuff is put in this folder in a hugo site:



{{< figure src="/content/subjects/software/hugo/content-folder.png" >}}


This is the structure of the inside of the *content* folder:

{{< figure src="/content/subjects/software/hugo/content-folder-inside.png" >}}


The above folders inside the *content* folder can be created manually or by command.

for example if you want to create a file *test.md* in a new folder *mydir1*, then:

    $ hugo new mydir1/test.md


{{< figure src="/content/subjects/software/hugo/new-folder-creation-by-command.png" >}}


Now suppose you want to add a new file to the *mydir1* folder:

    $ hugo new mydir1/test1.md
	
	
	
{{< figure src="/content/subjects/software/hugo/new-file-creation-by-cmd.png" >}}


**Final Notes:**

1. If a folder does not exit in the *content* folder then it will be created automatically when you will give command to create a new file. There is not separate command for creating a new folder.
2. Don't give this command for new file:

    $ hugo new content/mydir/myfile1.md
	
	
The above creates a duplicate *content* folder inside the already existing *content* folder (I have seen). But when you create only a new file then it does not create).	

Give this

    $ hugo new mydir/myfile1.md
	
	
