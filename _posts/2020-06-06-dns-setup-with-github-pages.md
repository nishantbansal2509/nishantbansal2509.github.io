---
layout: post
title: DNS setup for hosting on Github Pages
---

Static site generators are a great way to host your personal page and a blog on web. There are several great static site generators available out there. I used jekyll, primarily because it is the most used site generator and github pages hosts jekyll sites seamlessly. If you are familiar with ruby, its another reason for you to look at jekyll. If you want to try out others, you can take a look at hugo, a go based static site generator or Gatsby, a JavaScript based static site generator. Whichever you end up choosing there are ample resources for each one for you to get started. YouTuber [Mike Dane](https://www.youtube.com/channel/UCvmINlrza7JHB1zkIOuXEbw) has great resources to get started on any of the widely used generators out there.

So you have setup a website, but hosting it is the next logical step. The best and cheapest way to host your static site is with github pages. Its free and there is a lot of documentation that comes along with it. In fact its so easy to use, that I never looked at any other place to host my page.

GitHub provides you a custom url for your visitors to load your site from. The only drawback, if at all you can call it a drawback, is that your url will be appended with `.github.io`. I am sure most people can live with it. But configuring your purchased domain with github acting as your hosting platform is super simple barring some barring some details of setting up DNS records properly. I had my fair share of foraging across internet to find this amazing [article](https://hackernoon.com/how-to-set-up-godaddy-domain-with-github-pages-a9300366c7b) which solved the problem easily. Also if, only if, I had looked up github page [documentation](https://help.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site) sincerely, I would have saved myself a couple of days I spent finding already documented information.

1. Go to manage DNS on the platform where you purchased your domain from.
2. Add 4 type A records to your DNS settings. These records essentially directs your name servers, which the domain seller has already configured for you, to github servers for your page to be served.
    1. 185.199.108.153
    2. 185.199.109.153
    3. 185.199.110.153
    4. 185.199.111.153
3. Add a CNAME record of Name `www` and set it to your github page url, which will look like `<your-username>.github.io`.
4. One last step, you need to tell github to serve your content when your purchased domain is requesting content. Add a file named "CNAME" to your repository and have the newly purchased domain name as the only content of the file.

That's it, now your custom domain is routed to github pages to present your content. It will take some time for your settings to propagate across the DNS servers.
