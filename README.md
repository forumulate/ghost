# Forumulate for Ghost

Add Forumulate comments, the docs search / ask-AI box, the "What's new"
changelog bell and a feed of your forum topics or blog posts to a Ghost site —
either as theme partials (recommended, settings live in Ghost Admin) or by
pasting snippets into Code Injection (no theme edits).

## Option A: theme partials

1. Copy `partials/forumulate/` into your theme's `partials/` folder.
2. Merge the `config.custom` block from `package.custom.json` into your theme's
   `package.json` (Ghost allows 20 custom settings; this adds 3).
3. Upload the theme, then set **Forumulate org**, **space** and **URL** under
   Settings → Design → Theme.
4. Use the partials in your templates:

```handlebars
{{!-- post.hbs, inside {{#post}} … {{/post}} --}}
{{> "forumulate/comments"}}
{{> "forumulate/comments" space="blog-comments" theme="dark"}}

{{!-- default.hbs header --}}
{{> "forumulate/changelog" space="changelog"}}

{{!-- anywhere --}}
{{> "forumulate/widget" space="docs" mode="ask" placeholder="Ask the docs"}}
{{> "forumulate/feed" space="community" kind="forum" limit="5"}}
```

Every value is printed with `{{ }}`, which Handlebars HTML-escapes. The comments
embed finds (or creates) one forum topic per post from the post's URL.

## Option B: Code Injection (no theme changes)

Replace `acme` and the space names with yours. Code Injection is pasted as raw
HTML, so type the values in directly.

**Settings → Code injection → Site footer** — the changelog bell, docs search:

```html
<script async src="https://forumulate.com/api/embed/changelog.js"
  data-org="acme" data-space="changelog" data-mount="#forumulate-bell"></script>
```

(Add an element with `id="forumulate-bell"` to your navigation, or omit
`data-mount` to append the bell at the end of the page.)

**A post → Settings → Code injection → Post footer** — comments under that post:

```html
<div id="forumulate-comments"></div>
<script async src="https://forumulate.com/api/embed/comments.js"
  data-org="acme" data-space="blog-comments" data-mount="#forumulate-comments"></script>
```

To put comments under every post without editing each one, use Option A.

## Server-rendered content

Ghost themes cannot fetch from other sites on the server, so the feed partial
renders in the browser with the `<forumulate-feed>` element. For crawlable
lists, link to your Forumulate blog, forum and docs from Ghost's navigation —
those pages are server-rendered by Forumulate.

## License

MIT

---

## About this repository

This repository is a public mirror, refreshed on each Forumulate release
(one commit per release). Pull requests are welcome; accepted changes are
applied upstream and arrive here with the next release.

- API reference: https://forumulate.com/reference
- Guides: https://forumulate.com/guides
- Community and support: https://forumulate.com/community
- Source: https://github.com/forumulate/ghost
