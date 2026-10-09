# Chris Potter’s articles

Public blog: https://chrpotr.github.io

## Write and publish an article in your browser

1. Open [ARTICLE_TEMPLATE.md](ARTICLE_TEMPLATE.md) and copy its contents.
2. Open the [_posts folder](https://github.com/chrpotr/chrpotr.github.io/tree/main/_posts), then choose **Add file → Create new file**.
3. Name the file `YYYY-MM-DD-short-article-title.md`, replacing the date and title. Use the current date or a past date, for example `2026-10-09-my-first-article.md`.
4. Paste the template. Change `title` and `excerpt`, then write your article below the second `---` line. Keep the quotes around the title and excerpt.
5. Use **Preview** to check your Markdown. This previews the text formatting, not the final blog design.
6. Choose **Commit changes**, add a brief description, and commit to `main` when you are ready to publish.
7. GitHub Pages rebuilds automatically. Check the [Actions tab](https://github.com/chrpotr/chrpotr.github.io/actions) for a successful Pages deployment. Publishing can take up to 10 minutes.
8. Open the blog, select your article, and copy its address to share it. The example filename above normally becomes `https://chrpotr.github.io/articles/my-first-article/`.

No software installation is needed. Readers do not need a GitHub account.

## Edit an article

Open the article in `_posts`, click the pencil button, make your changes, and commit to `main`. The same article link updates after the next successful deployment. Keep the filename unchanged to preserve that link. Use unique filename slugs for each article.

## Drafts and privacy

**This entire repository is public**, including files, branches, pull requests, and commit history. Keep private drafts and sensitive information outside it. A file excluded from the blog is still visible on GitHub. A public-repository draft branch is also public.

Committing to `main` is the publishing step. You can write a draft in a private document and paste it here only when ready. Do not add API keys, passwords, or other secrets anywhere in this repository.

## Images

Add public-ready images to `assets/images/`, then use Markdown such as `![Description of the image](/assets/images/example.jpg)`. Use your own images or ones you have permission to publish. Remove location metadata and other private details first.

## Site settings

- **Title and description:** `_config.yml`
- **Home page:** `index.html`
- **About page:** `about.md`
- **Article layout:** `_layouts/post.html`
- **Colors and typography:** `assets/style.css`
- **Publishing:** Settings → Pages → Deploy from a branch → `main` → `/(root)`

`README.md` and `ARTICLE_TEMPLATE.md` are excluded from the generated blog. No example article is published.

## Following and sharing

- Readers can subscribe in an RSS reader using `https://chrpotr.github.io/feed.xml`. This is an Atom feed, supported by common RSS readers; it updates automatically when articles are published.
- A sitemap is generated at `https://chrpotr.github.io/sitemap.xml`.
- Every page has a title, description, canonical URL, and social-sharing metadata. Articles use their own title and excerpt, with the site-wide preview image at `assets/images/social-card.png` (1200 × 630 pixels).
- To use an article-specific preview image, upload a public-ready PNG or JPEG and add `image: /assets/images/your-image.jpg` to that article's front matter. Use a 1200 × 630 image for a consistent preview; optionally add `description` to override the excerpt in sharing metadata.
- The favicon lives at `assets/favicon.svg`, with a PNG fallback at `assets/favicon-32.png`.
