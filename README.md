For the first time I have been able to use the **Hugo modules** feature. Thanks to @chreliot and his [post](https://discourse.gohugo.io/t/how-to-add-a-theme-using-modules-for-beginners/20665), I finally figured out how to use it. I'm not smart enough to figure it out out through the documentation that are available so far.

For other **Hugo modules** noobs that are fighting with **Hugo modules**. This is a step by step guide to help you to get up and running with Hugo modules. 


Table of Contents:
* Part 1. Prepare a Hugo site to test out Hugo modules
  * Install latest version of go on your computer
  * Prepare a test site to implement a theme as a Hugo module
* Part 2. Add a theme as a Hugo module
  * For now it has only been bureaucracy. The fun part is starting now
* Part 3. Add content as a Hugo module
  * Adding content as a module, that is what you really, really, really whant
  * Upload your site to GitHub with two modules added.
  * You can use Hugo modules to mount any kind of resources to your Hugo site.



## Part 1. Prepare a Hugo site to test out Hugo modules
### Install latest version of **go** on your computer

Make sure that you have installed a recent version of **go** on your computer. [Here is the link to the **go** install](https://golang.org/dl/). Follow the instructions carefully. [The `hugo mod` commands](https://gohugo.io/commands/hugo_mod/) do not work without doing this. If you use the `hugo mod` commands, without installing **go**, nothing happens. You don't get an error message as feedback.

### Prepare a test site to implement a theme as a Hugo module

The theme **[hugo-xmin](http://github.com/yihui/hugo-xmin)** are used as an example (yes that`s exactly the same as @chreliot used in his [post](https://discourse.gohugo.io/t/how-to-add-a-theme-using-modules-for-beginners/20665))

First you have to prepare a Hugo site to test out the **[hugo-xmin](http://github.com/yihui/hugo-xmin)** theme as a **Hugo module**

1. Download the example site for the **hugo-xmin** theme:
You can [download the zip file here](https://github.com/yihui/hugo-xmin/archive/master.zip)
2. Extract the folder [exampleSite](https://github.com/yihui/hugo-xmin/tree/master/exampleSite) to your harddrive
3. Rename exampleSite to `hugo-test-modules`

Later on, you will add the **hugo-xmin** theme as a **Hugo module**.

## Part 2. Add a theme as a Hugo module

There are different ways to use **Hugo modules** to add a theme to your Hugo site. This is one of them.

When you test your site in this stadium. You get an error message.

```bash
hugo serve
```
`Error: module "hugo-xmin" not found; ...`

That's because no theme is added to the Hugo site.

### For now it has only been bureaucracy. The fun part is starting now:

1. Comment out or delete the variable `theme` in [`config.toml` file](https://github.com/craftsmandigital/hugo-test-modules/blob/master/config.toml)

   ```toml
   # theme = "hugo-xmin
   ```
   We no longer need this variable since we make use of **Hugo modules** (It is possible to use the `theme` variable to mount modules. For simplicity you use the new preferred method).

   

1. Add this to your [`config.toml` file](https://github.com/craftsmandigital/hugo-test-modules/blob/master/config.toml) to specify a theme as Hugo module:
   ```toml
   [module]
     [[module.imports]]
       path = "github.com/yihui/hugo-xmin"
   ```
   
   > You don't have to specify the folder to mount to, neither that it is a theme you are mounting. By default **Hugo modules** behave as it is a theme. Hugo mounts github.com/yihui/hugo-xmin in the Hugo theme folder.
   
1. Initialize project as **Hugo module**. Go to CLI and type in this command in your Hugo site:
   ```bash
   hugo mod init ugly-dummy
   ```
   YES IT WAS `ugly-dummy` (It really doesn't mater what the parameter is to the `hugo mod init` command, but there are some restrictions on ".", "/", etc.). I think it's more appropriate to name the module as your Hugo site name. In this case hugo-test-modules. but ugly-dummy is also fine.
   
   The command could output something like this:
   
   `go: creating new go.mod: module ugly-dummy`

   *information: a new file* `go.mod` *was created*
   
1. Test your site:
   ```bash
   hugo serve
   ```
   
   Your site should look exactly the same as [this site](https://xmin.yihui.name/)
   
   *information: a new file* `go.sum` *was created*

1. Now its time to upload your finished site to **GitHub**. 
   
   [Create a **GitHub** Repo](https://github.com/new) and name it `hugo-test-modules`
   
   Git commands to upload repo:

   ```bash
   git init
   git add -A && git commit -m "Initial Commit"
   git remote add origin https://github.com/< your username >/hugo-test-modules.git
   git push -u origin master
   ```
   
1. When you now clone your newly updated repo to your machine, there is no need for `git clone --recursive`. It's just plug and play. Just do a regular `git clone`
   ```bash
   git clone https://github.com/< your username >/hugo-test-modules.git
   ```


That was all “happy moduling”

## Part 3. Add content as a Hugo module
### Adding content as a module, that is what you really, really, really whant

Your site is up and running with a **Hugo module**, the theme **[hugo-xmin](http://github.com/yihui/hugo-xmin)** . Now lets add some markdown files to your content. You can mount folders with markdown files from any git repo(It's also possible to mount folders from your hard drive). The repo you mount, don't has to be a Hugo repo. You are going to mount a folder from this [repo](https://github.com/craftsmandigital/markdown-content-repo). Check it out and be familiar with it. The repo contains a folder `testing-hugo-modules`, that could be mounted. The folder contains two files:

* testing-hugo-modules/file-1.md
* testing-hugo-modules/file-2.md

Here is the configuration that you could drop in your [`config.toml` file](https://github.com/craftsmandigital/hugo-test-modules/blob/master/config.toml). Add it just under the theme stuff, under `[module]` section:
```toml
[[module.imports]]
    path = "github.com/craftsmandigital/markdown-content-repo"
    disabled = false

    [[module.imports.mounts]]
    source = "testing-hugo-modules"
    target = "content/new-stuff"
```
* `path` describe the repo you mount content from
* `source` describe witch folder(from root) in mounted repo you could append to your Hugo site ([this link brings you inside the actual folder](https://github.com/craftsmandigital/markdown-content-repo/tree/master/testing-hugo-modules))
* `target` describe witch folder(from root) in your Hugo site the mount could appear (`content/new-stuff`)

After updating [`config.toml` file](https://github.com/craftsmandigital/hugo-test-modules/blob/master/config.toml) there is nothing more to do. It's time to test your site.
```bash
hugo serve
```
Now you can see your two new posts at the bottom of the start page (http://localhost:1313/)

* 2019/09/12 file 1 for testing Hugo modules for content
* 2019/09/12 file 2 for testing Hugo modules for content

Click on one of the posts. Check out the URL address

* http://localhost:1313/new-stuff/file-2/

Do you recognize `new-stuff` from your [`config.toml` file](https://github.com/craftsmandigital/hugo-test-modules/blob/master/config.toml). That was your `target` for your mounting point(`content/new-stuff`)

### Upload your site to GitHub with two modules added.

```bash
git add -A && git commit -m "Initial Commit"
git push -u origin master
```

Try to clone your Hugo site:

```bash
git clone https://github.com/< your username >/hugo-test-modules.git
```

Your site could work right out of the box:

```bash
hugo serve
```

### You can use Hugo modules to mount any kind of resources to your Hugo site. 

You can mount `layouts` like `partials` `shortcodes` resources like JS libraries. Etc. Use your Imagination.

That was all, really really really “happy moduling”
