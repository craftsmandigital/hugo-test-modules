## Hugo modules for "dummies"

For the first time I have been able to use the **Hugo modules** feature. Thanks to @chreliot and his [post](https://discourse.gohugo.io/t/how-to-add-a-theme-using-modules-for-beginners/20665), I finally figured out how to use it. I'm not smart enough to figure it out out through the documentation that are available so far.

For other **Hugo modules** noobs that are fighting with **Hugo modules**. I have made an extremely detailed description how to install a theme with **Hugo modules**. I am not going in detail on anything. Just get a site up and running. [Here is the Link to the final Hugo site](https://github.com/craftsmandigital/hugo-test-modules). Just follow the steps carefully to create that Hugo site.

Here is what you have to do:

* Install latest version of **go** on your computer
* Prepare a test site to implement a theme as a **Hugo module**
* Finally you dive into the tasks and code to implement the **Hugo module**

## Install latest version of **go** on your computer

Make sure that you have installed a recent version of go on your computer. [Here is the link to the **go** install](https://golang.org/dl/). Follow the instructions carefully. [The **Hugo mod** commands](https://gohugo.io/commands/hugo_mod/) do not work without doing this. If you use the **Hugo mod** commands, without installing **go**, nothing happens. You don't get an error message as feedback.

## Prepare a test site to implement a theme as a **Hugo module**

The theme **[hugo-xmin](http://github.com/yihui/hugo-xmin)** are used as an example (yes that's exactly the same as @chreliot used in his [post](https://discourse.gohugo.io/t/how-to-add-a-theme-using-modules-for-beginners/20665))

First you have to prepare a Hugo site to test out the **[hugo-xmin](http://github.com/yihui/hugo-xmin)** theme as a **Hugo module**

1. Download the example site for the **hugo-xmin** theme:
You can [download the zip file here](https://github.com/yihui/hugo-xmin/archive/master.zip)
2. Extract the folder [exampleSite](https://github.com/yihui/hugo-xmin/tree/master/exampleSite) to your harddrive
3. Rename exampleSite to **hugo-test-modules**

Later on, you will add the hugo-xmin theme as a **Hugo module**.

## Finally you dive into the tasks and code to implement the **Hugo module**

There are different ways to use **Hugo modules** to add a theme to your Hugo site. This is one of them.

When you test your site in this stadium. You vil get an error message.

```
hugo serve
```
`Error: module "hugo-xmin" not found; ...`

That's because no theme is added to the site.

Now its time to upload your unfinished site to **GitHub**. This is very important( I suppose it will work with another git provider like GitLab or GitBucket). Later on we have to locate **GitHub** repo with the [**hugo mod init** command](https://gohugo.io/commands/hugo_mod_init/).

[Create a **GitHub** Repo](https://github.com/new) and name it **hugo-test-modules**

Git commands to upload repo
```
git init
git add -A && git commit -m "Initial Commit"
git remote add origin https://github.com/< your username >/hugo-test-modules.git
git push -u origin master
```

For now it has only been bureaucracy. The fun part is starting now:

1. Comment out or delete the variable **theme** in **[config.toml](https://github.com/craftsmandigital/dummy/blob/master/config.toml)** file

   ```
   # theme = "hugo-xmin
   ```
   We no longer need this variable since we make use of **Hugo modules**

1. Add this to your **[config.toml](https://github.com/craftsmandigital/dummy/blob/master/config.toml)** to specify a theme as Hugo module:
   ```
   [module]
     [[module.imports]]
       path = "github.com/yihui/hugo-xmin"
   ```
1. Initialize project as **Hugo module**. Go to CLI and type in this command in your Hugo site:
   ```
   hugo mod init github.com/< your username >/hugo-test-modules
   ```
   The command could output something like this:
   
   `go: creating new go.mod: module github.com/< your username >/hugo-test-modules`
   
   *information: a new file* **go.mod** *was created*

1. Test your site:
   ```
   hugo serve
   ```
   
   Your site should look exactly the same as [this site](https://xmin.yihui.name/)
   
   *information: a new file* **go.sum** *was created*

1. Commit your changes and push it to **GitHub**
   ```
   git add -A && git commit -m "Added theme as Hugo component"
   git push -u origin master
   ```

1. When you now clone your newly updated repo to your machine, there is no need for **git clone --recursive**. It's just plug and play. Just do a regular **git clone**
   ```
   git clone https://github.com/< your username >/hugo-test-modules.git
   ```


That was all “happy moduling”
