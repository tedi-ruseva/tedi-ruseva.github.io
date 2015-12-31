# My personal blog built with Hugo

[Hugo](https://gohugo.io/) is a static site generator. Unlike other systems
which dynamically build a page every time a visitor requests one, Hugo does the
building when you create your content. Hugo sites can be hosted anywhere, and
run without dependencies on expensive runtimes like Ruby, Python or PHP and
without dependencies on any databases.

## How to build the site

GitHub allows [one site](https://pages.github.com/) per user and serves it
automatically from a repository named `username.github.io`, where *username* is
your username on GitHub. So we will keep the HTML of the site in the `master`
branch of the repo and the source code in the `source` branch (this branch).

This is how to create a new post and make it live using Hugo:

  1. Create a new Markdown file in the `content/post` directory. You can either
     copy an old post or let Hugo create it with default metadata (we use
     [casper](http://themes.gohugo.io/casper/) as a theme):

     ```bash
     $ hugo new -t casper post/my-post.md
     ```

  * Edit your post content in
    [Markdown](https://guides.github.com/features/mastering-markdown/) with your
    [favorite](https://atom.io/) text editor. You can put images to
    `static/images` folder and reference them in you post like so:

    ```markdown
    Check the photo I took yesterday:

    ![Image of Sunrise](/images/sunrise.jpg)
    ```

  * See how your post looks like by running a Hugo server locally:

    ```bash
    # --renderToDisk is needed to prevent hugo server from hanging on 32-bit
    # Windows until Hugo v0.16 is released
    $ hugo server --renderToDisk
      3 pages created
      in 51 ms
      Watching for changes in {data,content,layouts,static,themes}
      Serving pages from \public
      Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
      Press Ctrl+C to stop
    ```

  * When you are done, you can commit your changes to the `source` branch on
    GitHub:

    ```bash
    $ git add . # prepare all new files for commit
    $ git commit -m "Add new post" # commit to local repo
    $ git push origin source # push to remote repo (GitHub)
    ```

  * Now you are ready to publish your new post. First, you need to generate the
    HTML for your site with Hugo:

      ```bash
      $ hugo
      ```

  * Your site HTML is ready inside the `public` folder. Go inside that folder
    and push to your `master` branch on GitHub:

    ```bash
    $ cd public
    $ git add .
    $ git commit -m "Add new post"
    $ git push origin master
    ```

  * Your new content should be live shortly - fire up a browser and go to
  [http://tedi-ruseva.github.io](http://tedi-ruseva.github.io).
