---
layout: post
title: Website Redesign 2017
date: 2017-02-11 00:00:00.000000000 -04:00
categories: jekyll update
---

This is meant to be a short blog post on the process I went through to revamp my personal website. I'll walk through some of the design decisions as well as some of the mistakes ( at times horrendous ) that I made.

I personally think it is important to have your own home page. You could have myriad reasons to have one ranging for showcasing your talents, presenting it as an online resume or in my case, just a place that I could tinker with technologies that I do not use in my day job.

The first iteration of my home page was hosted on Heroku. For those who don't know how Heroku works, it's a PaaS( Platform as a service ). Now this is a handy tool for people who don't have their own infrastructure to deploy production applications. It's very similar to AWS in that regard except that it abstracts away many of the nitty gritty details that AWS requires to configure deployment of an application. Long story short, I chose Heroku because of its convenience factor and because I was on the Developer plan that was completely free! So I built my website using Sparkjava which is a micro framework to create web applications. It is inspired by Sinatra, the Ruby framework. I am a big proponent of Sparkjava for prototyping applications, so for a personal website that was just gonna serve static pages, it was the easiest for me to get off the ground with. Since I had personally never built a "portfolio" website, I took the help of <a href="https://startbootstrap.com/template-categories/all/"> Start Bootstrap </a> to help me get inspiration. And by inspiration, I pretty much mean all of the CSS and JS that I needed for my site. Don't judge me, I didn't know any better! As Pablo Picasso said, 'good artists borrow, great artists steal.'. Not sure which one I am, but I atleast did one of those. I chose the coffee themed template, partially because I liked the rugged brick look which seemed to give the website a very Victorian feel. Once I had all the basic boilerplate code in place, I hacked around it to make sure it displayed the content I wanted it to with the mods that I wanted to display.

This was a very simple first exercise and I definitely had no problems getting this up and running locally on my computer. Deploying it to Heroku was a bit of a challenge, because at the time Spark was not natively supported by Heroku. Some simple google searches, however, paved the way to some kind soul who posted how she/he had deployed their app to Heroku and from there it was a breeze. So I got my first site up and running and it was great! I thought the look and feel was good and it showed the content I wanted to display.

I am a clean freak by nature and computer cleanliness is not excluded from this. So in my very energetic sprees of freeing up space on my Mac by deleting unwanted files, I accidentally deleted my website code from the computer. And no, I had forgotten to check it into GitHub ( my choice of SCM ). And yes, that is unpardonable. So for a long time, everytime I had an urge to futz around with my website, I was brutally reminded of my idiocy, so I'd lay those ideas to rest.

ANYWAY, then came 2017 and I figured the new year needed a fresh burst of vitality and the website was the hallowed ground upon which I would consecrate the focus of my arts. My initial instict was to just go back to Heroku and do the same spiel all over again but then the more I started thinking about what I had on my website, the more I realized that there were things that were fundamentally wrong. I will walk through some of the issues that I found and how I solved them in my personal page 2.0

1. Choice of hosting service ( Heroku v/s GitHub )

If you want to use the free plan, Heroku is a good place to test out greenfield prototypes that you don't want to invest too much money into. It is a good place to test request/response type of apps that actually need a server to function ( I am not getting into the discussion of Backend as a Service which a whole different conversation ). However, for my personal website, the most complex thing that I would have wanted to do was maybe accept form inputs when people wanted to reach out to me. There was no fancy interaction that would need any real-time response. The other big problem with the free plan of Heroku is the way they maintain uptime. You only get "dynos" which are up only when they are needed. So if you haven't had any hits on your website for say 6 hours, the next hit to come to your website, will take about 20 seconds for the page to render, because the dyno is in the process of being woken up. As a result, whenever I had to show my page to someone, I always had to "pre-warm" the dyno, so they could see the page being responsive. ( I mean lets be real, nobody is interested in my site, so the only people seeing it are probably people I am forcing to see my site ). To solve the "sleeping dyno" problem, I started using <a href="https://uptimerobot.com/" target="_blank">Uptime Robot</a> which would ping my website every 5 minutes to keep it up and running. Which sounds great right? There is a catch though. As I was on the Free heroku plan, Heroku lets my account ( which includes upto 5 free applications ) have a total uptime of 1000 dyno hours per month, after which they would shut down all applications until the next month started. Since I had a couple of other apps that I was testing out as well, my website would be shut down pretty much around the 20th day of the month mark. Shucks! Guess I am not so smart after all, with the whole uptime thing.

I had come across GitHub hosting in the past, but I had never really used it. This time around, I was determined to use Github hosting for my website by using it in conjunction with Jekyll ( which I will go into detail in a bit ) because of how well suited it seemed for the purpose I wanted. No databases, built for blog hosting and easy templating. The lagniappe was the fact that there were no uptime restrictions on Github hosting and they could handle upto 100,000 hits per month! Which of course, is most likely 99,999 more than I will be getting each month. Works for me!

2. To Server or not to Server ( Spark Java v/s No server )

In my previous version of the website, I was using Sparkjava for literally just serving static pages. As light as Sparkjava is, it still needs some boilerplate configuration like using Maven ( as I did ) for dependency management/builds or setting up routes in Java to assign paths to how people interact with your page and writing some barebones response handlers. With Github hosting + Jekyll, all of that went away. All I needed to do was concentrate on building the application.

3. Website templates ( Handlebar v/s Liquid )

Sparkjava does not come with its own templating mechanism, however it has support for several such as Handlebar, Mustache, Pebble etc. I chose Handlebar because it was fairly simple to use. This time around I used Jekyll's templating mechanism called Liquid, developed by the folks over at Shopify. I would say I didn't find anything particularly fantastic or particularly annoying about Liquid. It got the job done and that is what I was looking for.

4. Use an existing css template v/s building from scratch

In my website's 2.0 version, I wanted a very clean and sparse look. I felt that the previous version was very "heavy" and being the minimalist that I am, I am a bit surprised I went down that route. So the new website, was going to be minimal, it was going to have lots of whitespace and above all, content would be front and center, undistracted by unnecessary CSS styling.

5. Page layout and design consideration

* Title Bar

Changed the font type to Cardo from Josefin Slab. It is much "lighter" and gives a cleaner look

<div id="container1">
  <img src="sample-before.png">
  <img src="sample-after.png">
</div>

* Navigation Bar

The Nav Bar isn't that conspicuous now in terms of styling. It is just surrounded by 2 thin lines instead of being embedded within a bar.



* Footer
* Favico
* Home Page
* About
* Blog
sharing buttons, disqus, tagging
* Photos
* Travel
* Projects
* Contact Me

6. Some of the other bells and whistles on the site

Google analytics. Definitely like to have metrics associated with anything I do. Its the only way you can measure your performance. Google Analytics is super easy to use and gives me a swath of information which I can make some very telling observations off of, including bounce rates and places people access my site for. Definitely a must-have. If not google, then some other analytics like Hotjar. Adding SEO as well as Google Adsense is possibly in the works.

I'd say it was real fun rebuilding my website as it helped me make some UX design decisions. Is this the final version of the website? I am pretty sure the answer to that is a strong No because I will always be looking to learn something new. As Brian Herbert said, "The capacity to learn is a gift; the ability to learn is a skill ; the willingness to learn is a choice." and its a choice I am making willfully.
