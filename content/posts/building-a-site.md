+++
title = "from org"
author = ["pankaj"]
draft = false
+++

## build a site {#build-a-site}

Ref: <https://gohugo.io/getting-started/quick-start/>

Go to the folder where you want to create your site.

I go to `/home/pankaj/project/hugo/` for this

And run this from that folder:

`hugo new site pankaj_site`

{{< figure src="/ox-hugo/build-a-new-site.png" >}}

And a folder is created:

{{< figure src="/ox-hugo/site-folder-created.png" >}}

This dir structure is created:

{{< figure src="/ox-hugo/default-dir-structure.png" >}}

Create  the first content:

{{< figure src="/ox-hugo/first-content-creation.png" >}}

Here the first content is created:

{{< figure src="/ox-hugo/dir-after-first-content-creation.png" >}}

Now, start the Hugo server with drafts enabled:

`hugo server -D`

{{< figure src="/ox-hugo/server-started-first-time.png" >}}

but the browser gave nothing.

For this you need to have a theme first:

`git init`

and then

`git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke`

`echo theme = \"ananke\" >> config.toml`

theme is loaded:

{{< figure src="/ox-hugo/first-theme-loaded.png" >}}

and new start the server:

`hugo server -D`

Now opens

To create static html pages give:

`hugo -D`

it creates a `public` folder and creates pages inside it.

{{< figure src="/ox-hugo/public-folder-created.png" >}}

<https://lucidmanager.org/productivity/create-websites-with-org-mode-and-hugo/>
