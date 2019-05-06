---
title: building a blog with next.js
subtitle: build a server rendered, static, easy to use, flexible blog without the overhead of a static site generator
date: April 22, 2019
---

For a long time now, I've wanted my own blog to record and share the snippets I collect throughout my time programming. So I decieded to venture into the blogging world to find the best software to host my ideas but in the end I came out dissapointed with the current options (reasons are below)... Soooooo being the CS student that I am, I deceided to make my own custom blogging software.

#### Why I Didn't Use Existing Software

- **Ghost** - Hard to find a place to host it for free
- **Wordpress** - Extremely complex for such a simple purpose
- **Medium** - No custom domains
- **Blogger** - Meh UI

Jekyll, Hugo, Gastby... Nope
============================

The first set of libraries/frameworks that stood out were Jekyll, Hugo, and Gastby. However, I ended up quickly giving up on them. Each of them have their own templating syntax which I was not familiar with. Additionally each of them had some or the other overhead associated that made it not worth it. For example, Gatsby took over 3 minutes to `npm install` and another minute to start the dev server just for a hello world page. Is that really worth it just for a simple blog? I'm a web developer (among other things) and so I just want to be able to toss in a few styles and markdown files and just have it work...

Next.js, My Savior
==================

React (and Next) are two projects I've been learning and so I thought it would be a good idea to start with them. At the time, I didn't even realize how powerful Next actually is, but now I am thoroughly impressed and plan to use it for most projects. Here are some of the key features that made it a perfect framework for this.

- `exportPathMap` lets you generate all of the routes when you compile the website
- Next pre-renders all of the blog posts so that your SEO doesn't take a hit
- When Next pre-renders, it executes the logic. For example, compare the navbar on this page versus the home page

This doesn't sound that impressive, because after all React + all other static site generators do this, **BUT** Next makes this process *fast*, and *easy*. In fact, I'll show you how to make your own blog now!

Getting Started
---------------

I'm going to skip this step because it is already well documented [here](https://nextjs.org/docs#how-to-use).

Data Sources
------------

The first problem I wanted to solve was to make creating and adding blog posts as easy as possible. The simplest solution I came with invloves two files, one to give an index of posts (in the correct order), and one that actually contains the blog post.

`static/data/posts.json`

```json
// you can have as many files as you want, just add them to the posts folder
{
  // The `COMMIT_REF` part is very important, leave it there for now
  // Change your GitHub username and repo in the URL below
  "baseURL": "https://raw.githubusercontent.com/nahtnam/blog/COMMIT_REF/src/static/data/posts",
  "posts": [
    "building-a-blog-with-next-js.md",
    "hello-world.md"
  ]
}
```

The `baseURL` is where the files will be hosted in production (we will configure it to use localhost when we are running the server later). The `COMMIT_REF` in the URL is required to avoid GitHub's cache (discussed in a later part of the code).

`static/data/posts/hello-world.md`

```txt
---
title: hello world
subtitle: hello world in all of my favorite languages!
date: April 22, 2019
---

hello world...
```

With these two files (you can have as many posts as you want), you can both **a)** get a list of all of the posts **b)** make an additional request to get the metadata or the post itself.

Posts List
----------

Getting the list of posts (for the home page) is as simple as a fetch request. Once you have the list of posts, you will need to fetch each of the posts to get their metadata (title, subtitle, date). You could avoid these extra requests by duplicating the data into `posts.json`, but I wanted to make it as simple as possible to adding new posts so duplicating data was a big no for me.

**NOTE: You will need to install `isomorphic-unfetch` and do `import fetch from 'isomorphic-unfetch'` on EVERY page you use the `fetch` function**.

`pages/index.jsx` (simplified)

```jsx
import React from 'react';
import Link from 'next/link';
import { resolve } from 'url';
import fetch from 'isomorphic-unfetch';

export default class Index extends React.Component {
  static async getInitialProps() {
    // get a list of all of the posts
    const fetchPosts = await fetch(resolve(process.env.baseURL, 'posts.json'));
    const { posts } = await fetchPosts.json();

    // fetch each of the posts
    const fetchPages = await Promise.all(posts.map(post => fetch(resolve(process.env.baseURL, `posts/${post}`))));
    const texts = await Promise.all(fetchPages.map(page => page.text()));

    // extract the metadata and content from each post
    const res = texts.map((text, index) => {
      const split = text.split('---');
      split.shift();
      const metadata = split.shift().trim();
      const content = split.join('---').trim();

      const post = {};
      post.content = content;
      [post.path] = posts[index].split('.');

      metadata.split('\n').forEach((line) => {
        const [attr, val] = line.split(':');
        post[attr.trim()] = val.trim();
      });

      return post;
    });

    // return an array of posts
    return {
      posts: res,
    };
  }

  render() {
    // render each of the posts
    const { posts } = this.props;
    return (
      <div>
        { posts.map(post => (
          <Link href={{ pathname: '/posts', query: { title: post.path } }} as={post.path} key={post.title}>
            <a>
              <div>{ post.title }</div>
              <div>{ post.subtitle }</div>
            </a>
          </Link>
        )) }
      </div>
    );
  }
}

```

Wow... That's a lot! It's not too complex but essentially it makes a request to `posts.json` and then makes a request to every post in that JSON response. After all of the metadata is collected, it just creates an array of posts with the title, subtitle, and url. The `Link` defined in the render is slightly weird but essentially it generates a URL that looks like `/posts?title=hello%20world` but shows up in the URL bar as `/hello-world`.

Additionally, you may be worried that GitHub will be spammed with a bunch of requests every time someone loads the blog. To deter this we `getInitialProps` instead of `componentDidMount`. This helps because when we export the website, it is only run once and then converted to HTML. Therefore, these requests will only be run once at build time.

Getting it to Work
------------------

So go ahead and save that and try to run it. It won't work. That's because we are missing a few bits and pieces. It's kind of hard to explain the snippets but bear with me.



Posts
-----

Additionally we need to

Netlify
-------

To be continued...
