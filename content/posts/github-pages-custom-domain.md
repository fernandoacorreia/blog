---
title: "Custom domain with GitHub Pages"
date: 2020-08-15T04:35:19Z
tags: ["blogging", "DNS", "GitHub Pages"]
# description: "Article description." # Description used for search engine.
# featured: true # Sets if post is a featured post, making appear on the home page side bar.
# toc: false # Controls if a table of contents should be generated for first-level links automatically.
# menu: main
# featureImage: "/images/path/file.jpg" # Sets featured image on blog post.
# thumbnail: "/images/path/thumbnail.png" # Sets thumbnail image appearing inside card on homepage.
# shareImage: "/images/path/share.png" # Designate a separate image for social media sharing.
# codeMaxLines: 10 # Override global value for how many lines within a code block before auto-collapsing.
# codeLineNumbers: false # Override global value for showing of line numbers within code block.
# figurePositionShow: true # Override global value for showing the figure label.
# categories:
#   - Technology
---

I am hosting my blog on GitHub Pages. I wanted to use my own domain name instead of a `github.io` subdomain.

GitHub's documentation is very helpful. Even so, it took me some effort to figure out all the details, so I'm going to
share what I learned.

These instructions are for using an "apex domain" e.g. `fernandocorreia.dev`. The settings are a bit different when
using a subdomain like `www.fernandocorreia.dev`. Again, GitHub's [documentation](https://docs.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site) is very helpful and does a good job of
explaining these differences.

# Step 1: DNS entry for Let's Encrypt

These days, every website needs an SSL certificate so that it's not blocked by browsers.

GitHub Pages integrates with Let's Encrypt to obtain an SSL certificate on your behalf so that your website can be safely accessed.
This is extremely helpful because you don't have to pay for the certificate, and you don't have to deal with the details
of creating it and setting it up, which can be quite involved.

Go to your domain DNS provider and add a CAA record following this pattern:

```
DOMAIN CAA 0 issue “letsencrypt.org”
```

For example, see this picture showing how I created that record on my DNS provider (Namecheap):

![CAA record for GitHub Pages and Let's Encrypt on Namecheap](/images/github-pages-caa-record.png)

Hint: If by any chance you had already configured the domain on GitHub (explained on the next step), just delete your `CNAME` file from your GitHub
Pages repository before proceeding:

```
rm CNAME
git add .
git commit -m "Remove custom domain"
git push
```

# Step 2: Set domain name on GitHub

The next step is to enter the custom domain name on your GitHub repository's settings page, under the section "GitHub
Pages".

To be clear, in my case that was on this URL: https://github.com/fernandoacorreia/fernandoacorreia.github.io/settings.

Type the domain name in the "Custom domain" field and press Save (see the pictur below).

![GitHub Pages custom domain setting](/images/github-pages-domain-setting.png)

This will create a commit that adds a file named `CNAME` in the root of your repository, like this:

```
❯ cat CNAME
fernandocorreia.dev
```

# Step 3: Point your domain to GitHub Pages

Once that is done, go back to your domain DNS provider and add 4 A records with these IP addresses:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

That will point your domain to GitHub Page's servers.

See this example of how I set that up on Namecheap:

![A records for GitHub Pages on Namecheap](/images/github-pages-a-records.png)

You can use the `dig` command to check that the settings are in effect:

```
❯ dig fernandocorreia.dev +noall +answer
fernandocorreia.dev.	1799	IN	A	185.199.110.153
fernandocorreia.dev.	1799	IN	A	185.199.111.153
fernandocorreia.dev.	1799	IN	A	185.199.109.153
fernandocorreia.dev.	1799	IN	A	185.199.108.153
```

Hint: for security reasons, GitHub recommends doing this only **after** setting your domain name on your repository's
settings (the previous step). That's why we're jumping back and forth between DNS settings and GitHub settings.

# Step 4: Enforce HTTPS on GitHub Pages

Back to your GitHub repository's Settings page, turn on the "Enforce HTTPS" field under the "GitHub Pages" section:

![GitHub Pages HTTPS setting](/images/github-pages-https-setting.png)

Hint: If the field is disabled (i.e. can't be changed), wait a few minutes for your DNS changes to be propagated,
refresh the Settings page and try again.

# Step 5: Pull changes to GitHub repository

If you use a static site generator (like [Hugo](https://gohugo.io/)), pull the latest commit of your GitHub Pages
repository so that it pulls the recently created `CNAME` file.

If you forget to do that, when the static site generator modifies files in your GitHub Pages repository, and you try to
push those changes to GitHub, you'll get a merge conflict. In that case, fetch from upstream and rebase.

E.g. in my case my GitHub Pages repository is a submodule of my static site's repository, so this works for me:

```
❯ cd public
❯ git pull
```

# Trying it out

At this point, your DNS provider should be pointing your domain name to GitHub Pages, and GitHub pages should be aware
of it, and also it should have created an SSL certificate. You are ready to try to access your website like this:

https://fernandocorreia.dev/

That's it! I hope this helps. I am fully aware that some of this jargon may be new to you and that you may not know
exactly how to configure your DNS provider, how to troubleshoot DNS settings or to deal with the intricacies of git
submodules and merge conflicts. Hopefully these instructions and hints will be a starting point for your googling if you
run into trouble. I didn't get it right on the first try either.

# References

These pages were super helpful for me to figure out exactly what I had to do:

- [Managing a custom domain for your GitHub Pages site](https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site)
- [How to use lets Encrypt SSL with github pages with custom subdomain](http://localhost:1313/posts/github-pages-custom-domain/)
