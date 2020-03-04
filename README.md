eleventy-til-blog
A simple blog you can use for sharing things you learned, built off of Eleventy Base Blog on Glitch.

Demos
Cassey-Til
Getting Started
1. Remix this project.
Then have a look at .eleventy.js to see if you want to configure any Eleventy options differently.

This project's config differs from 11ty/eleventy-base-blog on Github by the following config section, which enables 404 pages to work in your remix and when hosting your site using eleventy --serve. It also disables ghost mode, which when enabled, makes clicks and scroll positions that one of your readers do mirror on all your users browser windows. 🙀

  eleventyConfig.setBrowserSyncConfig({
    callbacks: {
     ready: function(err, bs) {
       const content_404 = fs.readFileSync('_site/404.html');
       bs.addMiddleware("*", (req, res) => {
        // Provides the 404 content without redirect.
        res.write(content_404);
        res.end();
      });
     }
    },
    ghostMode: {
      clicks: false,
      forms: false,
      scroll: false,
    },
  });
2. Installing dependencies happens automatically - thanks, Glitch!
3. Rename your project, if you'd like
3. Edit _data/metadata.json
Fill in your author info, change the URLs and feed IDs to match your projects, name, etc. You can change the favicon and social sharing image if you want, or leave them alone.

4. Press 'Show' to view your new site
The site will reload automatically when something changes. In a normal Glitch project, you would be able to turn this off by unchecking 'Refresh App on Changes', but eleventy --serve is what we're using to serve files, and it always --watches.

Optional Steps
Consider remixing your site to have a work-in-progress (WIP) space.
This isn't strictly necessary, but if you want to be able to work on posts in private without your site updating while you're mid-post, you can have a second Glitch project where you draft posts. When your post is done, make sure it's been committed (by waiting a while for the auto-commit to happen, or running git commit yourself in the terminal).

Add your WIP project as a git remote in this project:

git remote add wip https://api.glitch.com/git/your-wip-project-name

Then pull changes in from the WIP project to this project when you have a new post that you've committed:

git pull wip master

Change Colors in _sass/base.scss
The $background-color variable might be of particular interest!

Add info about yourself in about/index.md
Implementation Notes
Glitch-specific
On Glitch, image files should be stored in assets. After uploading a new image, you can use the CDN link the assets drawer provides in your pages.
This means you can remove png from templateFormats, because Glitch won't allow you to store a png outside of assets.
watch.json controls when Glitch refreshes the server, but since Eleventy is watching for us, we can safely tell it to ignore most of our files. Instead, Eleventy will rebuild and restart BrowserSync when you make changes.
General Eleventy Help
about/index.md shows how to add a content page.
posts/ has the blog posts but really they can live in any directory. They need only the post tag to be added to this collection.
Add the nav tag to add a template to the top level site navigation. For example, this is in use on index.njk and about/index.md.
Content can be any template format (blog posts needn’t be markdown, for example). Configure your supported templates in .eleventy.js -> templateFormats.
Because css and png are listed in templateFormats but are not supported template types, any files with these extensions will be copied without modification to the output (while keeping the same directory structure).
The blog post feed template is in feed/feed.njk. This is also a good example of using a global data files in that it uses _data/metadata.json.
This example uses three layouts:

_includes/layouts/base.njk: the top level HTML structure
_includes/layouts/home.njk: the home page template (wrapped into base.njk)
_includes/layouts/post.njk: the blog post template (wrapped into base.njk)
_includes/postlist.njk is a Nunjucks include and is a reusable component used to display a list of all the posts. index.njk has an example of how to use it.
Credits

<div>Icons made by Freepik from www.flaticon.com is licensed by CC 3.0 BY</div>