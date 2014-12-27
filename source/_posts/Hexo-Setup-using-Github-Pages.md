title: Hexo Setup using GitHub Pages
date: 2014-12-19 14:59:08
layout: false
tags:
- git
- GitHub
- hexo
---

If you did not know [GitHub pages](https://pages.GitHub.com/) allows static website hosting for free! And free I can do. In digging through the GitHub pages walkthrough a bit more I learned about [Jekyll](http://jekyllrb.com/) which is a static website generator written in Ruby. It looks pretty amazing, but more recently I have been bent on JavasScript. [Hexo](http://hexo.io)! Hexo is another fantastic static website generator, but this one is powered by Node! With Hexo you can scaffold out posts, add layouts, generate the static files, then deploy, using node and command line, to your GitHub repo.

So, Hexo will generate static website and then will deploy those files to a GitHub repo which will serve it to the public. One thing I need in a blogging engine is the ability to write posts from any one of my computers, anywhere. Well, this is simple! Because we are dealing with a git repository already we can use another for the config/original posts markdown files! In fact, we can use the same repo that we are deploying to, but a different branch.

Thus my git strategy is _master_ branch for deployed static files, and I made a new _hexo_ branch where I initialized my hexo project and I make my config changes or layouts changes or anything of the sort.

##GitHub Setup

You can host your pages on GitHub by creating a special repository named **yourusername.github.io**. In my case I named mine [mitchellparsons.github.io](https://GitHub.com/mitchellparsons/mitchellparsons.GitHub.io). Just add an _index.html_ to _master_ and GitHub Pages will serve it.

1. Create github repo. Login to github.com and just create a new repo following the naming convention I just talked about. OR I highly reccomend following github pages [guide](https://pages.github.com/).

2. After you create your github repo go ahead and clone it locally. I try to use terminal for most of these things, but there are some good git gui clients out there.

```shell
$ git clone yourrepo
$ cd yourrepo
```

3. Branch hexo configuration branch
```shell
$ git branch hexo
$ git checkout hexo
```
or shorthand for doing a branch and checkout at once
```shell
$ git checkout -b hexo
```

##Hexo Setup

1. Install hexo with npm
```shell
$ npm install -g hexo
```

2. In your recently cloned repo directory (and _hexo_ branch) lets initialize a new project
```shell
$ hexo init .
```

3. Test it out locally
```shell
$ hexo server
[info] Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```
if successful you should be able to navigate to http://localhost:4000/

4. Setup _\_config_ file for deployment
What we have is default vanilla. Hexo can be configured for deployment to github in the the _\_config.yml_ file. This is the [yaml](http://www.yaml.org/) config file for your website. I will leave it up to the reader to learn more about these options here. But, lets look at the deployment section of __config.yml_. Add your github repo and make it look something like the following

```yaml
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
type: github
repo: https://github.com/YOURNAME/YOURNAME.github.io.git
branch: master
message: "Hexo Deploy Blog."
```

5. Deploy
```shell
$ hexo deploy
```

Awesome! Go to _yourname.github.io_ and see your new website!
*note that it may take a few for changes to show up.

6. Version control your hexo project
Now that you have hexo setup and are deploying lets go ahead and commit and push the changes to github.
```shell
$ git add --all
$ git commit -m "whatever yo"
$ git push origin hexo
```
Now all of the configuration changes, layout changes, original and unfinished posts are in your github repo hexo branch.
