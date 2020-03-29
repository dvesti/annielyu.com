---
title: Fun blogdown in R to design a personal website
author: Annie Lyu
date: '2020-01-12'
slug: blogdown-website
categories:
  - R
tags:
  - rstats
subtitle: ''
summary: ''
authors: 
- admin
lastmod: '2020-01-12T23:20:39-06:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

Inspired by [David Robinson](http://varianceexplained.org/)'s [keynote talk](https://resources.rstudio.com/rstudio-conf-2019/the-unreasonable-effectiveness-of-public-work) at the RStudio conference 2019 (summary in the following tweet), I decided to write a post about how I use [Yihui](https://yihui.org/)'s fantastic R package blogdown to develop my own personal website.

<center>{{< tweet 928447584712253440 >}}</center>

Well, there are a lot of useful references to check out. Here are a few of them that I would recommend. And you can always search by keyword in Yihui's [book on blogdown](https://bookdown.org/yihui/blogdown/) whenever you'd like to figure out how things work.

- Yihui's video tutorial
{{< youtube CjTLN-FXiFA >}}
- [Weicheng's slides](http://slides.com/mingsnu/deck/#/)
- [Slide sets from Alison Hill](https://summer-of-blogdown.netlify.com/)

The whole process is actually pretty intuitive and quite straightforward if you use RStudio and are comfortable with R, git and markdown. For the following part of this post, I'll give some general guidelines and explain a few tricky steps (at least for me). Let's get ready to fire it up! :fire:

## A brand new start

By default, I assume you like the Hugo theme called `academic` I'm currently using and the following guidelines are trying to show you how to build a personal website with a similar style to mine.

#### Get the template
  1. Run `install.packages("blogdown")` in R if you haven't yet.
  1. In RStudio, click *Project -> New Project -> New Directory -> Website using blogdown*. Configure the directory name and path, and the hugo theme is `gcushen/hugo-academic`. By default, this will download the most updated theme version for you[^2].
  1. In RStudio, click *Addins -> Serve Site (BLOGDOWN)* or run `blogdown::serve_site()`, then you should be able to preview the example website.

If everything works well for you so far, you've made a big move! Congratulations! :clap:

#### Personalize everything for yourself 
Everyone has his own taste, and the following steps show how I modify the template for mine. :stuck_out_tongue_closed_eyes:
  1. Go to the folder `content/home` which contains the files that configure the home page. Each markdown (.md) file can be regarded as one section horizontally displayed on the home page. Remove any unwanted sections by setting `active = false` in the corresponding markdown files[^1]. The contact information at the bottom of the home page is editable in the file `config/_default/params.toml`.
  1. All the personal information at the top of the home page (Name, Role, Organization, Avatar, Social Media, Biography, Interests, Education) is editable in the file `content/authors/admin/_index.md`.
  1. You can adjust the order of each section on the home page by changing the value of `weight` in the markdown files in the folder `content/home`. The sections with smaller `weight` would go before those with larger `weight`.
  1. The menu bar on the top of the home page is also editable in the file `config/_default/menus.toml`. Here `weight` adjusts the order of the menu items and works in the same way as for the sections. And you'll see the instructions in the comments to add a link to your resume[^3] in the menu bar. 
  1. Great! Until now you're done with the self introduction. :thumbsup: Now it's time to show people your achievements by editing the file `content/home/experience.md`. If you keep the `gallery` section on the home page[^4], you can personlize the photo wall by replacing the images in the folder `content/home/gallery/gallery` with your own. Try adding your amazing work to the folder `post`, `project`, `publication` and `talk` under the directory `content`. Just follow the template format and you'll find a way to put your own stuff there. :muscle:
  
#### Configure the website name
  1. Name it in your own way! Change `title` in the file `config.toml` and modify `description` in `config/_default/params.toml`.
  1. If you'd like, you could personalize the URL of your site by modifying the `baseurl` in `config.toml`. But nothing comes free. :joy: I purchased my domain name (http://annielyu.com/) from [Google Domains](https://domains.google/). The registration fee costs me $12 per year. And you can add [Google Analytics](https://analytics.google.com/analytics/web/) to your site by setting the `google_analytics` to be `UA-ACCOUNTID-1` in `config/_default/params.toml`. Your Google Analytics account ID can be found at *setting -> admin -> account settings*.
  
By the way, if you'd like to enable comments on your site, you can sign up an account on [Disqus](https://disqus.com/) and configure the `Comments` part in the file `config/_default/params.toml`.
  
#### Deploy your website

Now comes the most exciting part. :sparkles: Are you ready to show your profile to the whole world? The following steps will guide you how to use [GitHub](https://github.com/) and [Netlify](https://www.netlify.com/) to maintain and update your website in a most effortless way!

1. First of all, go :point_right: and get yourself a GitHub and an Netlify account you haven't yet.
2. Publish the project directory as a GitHub repository under your account. If you are uncomfortable with git command lines like me, I highly recommend downloading [GitHub Desktop](https://desktop.github.com/) or [Source Tree](https://www.sourcetreeapp.com/) for easy manipulation of your Git repo. The following steps assume you are using GitHub Desktop and have linked your GitHub account already.
  + Open GitHub Desktop, click *New -> Add an Existing Repository* and open the project directory.
  + Before you commit adding all the files, add a new file `.gitignore` to the project repository so that some files or folders such as `public` won't be tracked[^5]. For your reference, my `.gitignore` file looks like the following:
  ```
  .Rhistory
  .RData
  .Ruserdata
  .DS_Store
  
  public/
  .Rproj.user/
  .Rproj.user
  ```
3. Make your GitHub repo online by clicking *Publish repository*. Next let's log in to Netlify and click *New site from Git*. Follow the instructions and pick the GitHub repo you just created. It's important in the 3rd step, you change the basic building setting by clicking *show advanced -> new variable*, setting `Key` as `HUGO_VERSION` and `Value` as the minimum hugo version you need for the current version of the academic theme[^6]. If the site is deployed successfully, you've hit another milestone, bravo! :tada:
4. You can change the site name so that the web address would be `xxxx.netlify.com`. Wait?!!! You've already purchased a custom domain name like I do? Go to *Settings -> Domain management -> Add custom domain*, then follow the instructions. Once you complete all the steps, you are all set! :thumbsup:

From now on, once you push your changes to the remote GitHub repo, the website would be updated accordingly as if by magic! :star2:

## Some useful tips

Now you've come a long way to collect all the fundamentals to buid your site. There are still a lot of interesting features you can explore out there. Below are some tips based on my exploration. Take whichever you like to decorate your site! :hibiscus:

+ You can use emoji everywhere in your site. Check out the [emoji cheatsheet](https://www.webfx.com/tools/emoji-cheat-sheet/). By default, `enableEmoji = true` in `config.toml`.
+ Don't forget to set `hasCJKLanguage = true` in `config.toml` if you use Chinese/Japanese/Korean languages somewhere.
+ Set a rule to generate permanent links of your posts using `slug` instead of `title` by adding the following to `config.toml`. Here `slug` can be regarded as an unique ID for your post. It turns out to be pretty useful if you can't help changing your post title after sharing the post link on social media.
```
# Rules to generate permanent links of your pages
[permalinks]
    post = "/:year/:month/:day/:slug/"
```
+ Check out [Hugo's Build-in Shortcodes](https://gohugo.io/content-management/shortcodes/). That's how I embed the twitter and the Youtube video in this post. :smile:
+ You may notice there is a section called `Shiny` on my website which is not included in the template. Well, I almost adapted everything from the `projects` section. :joy: All I did is: (1) renaming `projects.md` under `content/home` into `shiny.md`; (2) renaming the folder `project` under `content` into `shiny`; (3) adding the following in `config/_default/menus.toml`
```
[[main]]
  name = "Shiny"
  url = "#shiny"
  weight = 10
```
+ As you may see it, `[Shiny](#shiny)` would create a hyperlink that would take site visitors to the `Shiny` section. The same logic applies to `tags` and `categories`. Below is part of the source code for my biography. And I bet you've seen how the hyperlinks work. If not, check it out! :laughing:
```
I enjoy [programming](/tags/rstats/), [photographing](#gallery) and [dessert-making](/tags/foodie/).
```
+ It's suggested to delete any non-customized files in the folders under `content` such as `courses` and `slides` so that the links to those files won't be accidentally exposed to visitors. By default, those files are searchable on the site and may appear in the `Related` section such as below a post.
+ Somehow the old way of making a foonote such as `^[here is a footnote]` is not working for a newer version of Hugo. Check their [new manual](https://www.markdownguide.org/extended-syntax/#footnotes) for guidance.

Well, that's all I have to suggest for developing your personal website with R blogdown. And finally I can check :white_check_mark: *write a post about blogdown* in my to-do list for winter break (on the last day :sweat_smile:)! Please feel free to comment below this post if you have any questions or would like to share your own website with me. Have fun blogging and exploring! 

[^1]: For me, I disabled `accomplishments`, `demo`, `hero`, `skills`, `slider` and `tags`.
[^2]: At the time when I write this post, it's version 4.7.0.
[^3]: If you're having great fun using R to make HTML files, I highly recommend Yihui's another wonderful package [pagedown](https://github.com/rstudio/pagedown) to help you build a nicely formatted HTML file for your resume just like [mine](/files/resume_lyu.html)!
[^4]: You can also disable the `gallery` section by setting `active = false` in the file `content/home/gallery/index.md`.
[^5]: You should always keep the folder `public` untouched and this folder is not needed for deployment.
[^6]: You can check the miminum Hugo version from the [academic theme introduction page](https://themes.gohugo.io/academic/). At this time, version `0.61.0` would work.
