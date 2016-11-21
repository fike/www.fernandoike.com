+++
title = "Wordpress to octopress performance comparisions"
date = "2013-02-26"
draft = false
Categories = ["blog", "english", "SL"]
Tags = ["blog", "octopress", "wordpress"]
+++
Continuing to comment a little bit more about the blog change.
Previously it was Wordpress and now it’s Octopress. I’ll show you data
based little test.

To make the test, I used Webpagetest that is avaliable in many cities
around the world to test performance from user perspective. It’s very
interesting to test it in many countries, but for this test I used only
its Brazilian instance that is in Sao Paulo.

### Wordpress

![](/images/wpt_wp_notes.png)

My old blog (wordpress) was hosted in Dallas and its major audience is
in Brazil, it isn’t bad. In the test, its time is 6 seconds and 37
requests. Considering that I haven’t done any performance tuning (linux
kernel, apache, etc.).

Only one of the test tasks was worse: FBT (First Byte Time). Probably,
the numbers would be better if I changed Apache, PHP or MySQL. Bellow,
see more data about this test.

![](/images/wpt_wp_sum.png)

### Octopress

To migrate to Octopress, my blog lost a little bit of functionalities
but nothing essencial. The main functionalities as text posts were
preserved.

Octopress is Jekyll based, and it is a powerful framework that generates
static pages. To write a post, it’s very simple. You write using
Markdown syntax. It is fantastic because the web server doesn’t need to
process some languages (Python, PHP, Ruby, etc.). Take a look below and
you’ll see that my blog has improved.

![](/images/wpt_octo_notes.png)

![](/images/wpt_octo_sum.png)

If I keep my enthusiasm, I will make more comparisions. My partial
conclusion about Octopress and Jekyll: They are fantastic tools to post
on blogs. Following there is a comparative summary table.

  blog           |  requests       |  time
:-------------: | :-------------: | --------:
  wordpress   |       37          |   6,437s
  octpress      |      32          |  4,371s
