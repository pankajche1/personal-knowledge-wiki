---
title: "Hugo: Static site building"
---

## Starting the server

    $ hugo server -D

## Building the `public` html pages folder:

First *delete* the already existing `public` folder, then run this command:

    $ hugo -D

## uploading to github.com

First add the updated work into local git

    $ git add .
    $ git commit -m 'some comment'

Now run the command to upload to github

    $ git push -u origin master

The above will ask you your `username` and `password`.

 **Important:** the `password` is the `token` that you generate at the github site. It is not your site `password`


## Generating tokens in github

Go to the site:

> github.com/settings/tokens

In the above page you can create a new token

{{< figure src="/content/subjects/software/hugo/personal-access-token-on-github.png" >}}

**Note:** In the above you can set the **expiration** time. You can set an expiration time to be no limit also. If you set the expiration time to be 30 days, then you need to generate a new token after 30 days.

Next step is to set the scope of access to the the new token:

{{< figure src="/content/subjects/software/hugo/token-access-scopes-on-github.png" >}}

In the above just tick the `repo` checkbox only. If you leave the checkbox empty then you will not be able to upload your stuff with the new token.