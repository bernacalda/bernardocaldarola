# Bernardo Caldarola's personal website (source)

Personal academic website built with [Quarto](https://quarto.org).

## Structure

```
_quarto.yml            site settings: navbar, footer, theme
index.qmd              home page (photo, bio, links, interests, education, 3 newest news items)
news.qmd               news page (reads data/news.yml)
research.qmd           research page (reads data/publications.yml)
policy.qmd             policy page (reads data/policy.yml and data/consultancy.yml)
teaching.qmd           teaching page (reads data/teaching.yml)
talks.qmd              talks page (reads data/talks.yml)
404.qmd                "page not found" page
data/*.yml             all the lists: edit these to add papers, talks, teaching
assets/                styling (SCSS), list templates (EJS), fonts, filter script
images/                headshot and site icon
files/                 CV PDF
```

## Everyday updates

**Add news.** Open `data/news.yml`, copy an entry to the top, and edit it. It appears on the
News page and, if it is among the three newest, in the "Latest" box on the home page.
Items are sorted by date, so the order in the file doesn't matter. Write the text in Markdown,
after `text: >` on indented lines, so quotes and colons need no escaping:

```yaml
- date: 2026-11-04        # or 2026-11; only month and year are shown
  text: >
    Our paper "[Paper Title](https://doi.org/...)" with Co-Author is out in *Journal Name* 🎉
```

Items dated after the day you render go under "Upcoming"; after that date, the next render
moves them into their year. To show more or fewer items on the home page, change
`max-items` in the header of `index.qmd`.

**Add a paper.** Open `data/publications.yml`, copy an existing entry, and edit it.
`type: article`, `wp` or `wip` decides the section. Entries appear in the order written.
The header of the file lists every available field. New `themes` automatically become filter buttons.

```yaml
- type: article
  title: "Paper Title"
  url: "https://doi.org/..."
  authors: "with Co-Author One and Co-Author Two"
  venue: "Journal Name"
  details: "2027, 12(3), 45–67"
  themes: [Digital technologies, Structural change]
  abstract: "Paste the abstract here."
  links:
    - {label: Paper, url: "https://doi.org/..."}
    - {label: Working paper, url: "https://..."}
    - {label: Code, url: "https://github.com/..."}
  media:
    - {outlet: "Newspaper", url: "https://..."}
  note: "Funded by ..."
```

**Move a working paper to published.** Change `type: wp` to `type: article` and update `venue` and `details`.

**Add a talk, course or event.** Add an entry to `data/talks.yml` or `data/teaching.yml` with
`group`, `when`, `title`, `detail` and `place`.

**Update the CV.** Replace `files/CV_Bernardo_Caldarola.pdf` with a new file of the same name.

**Change the bio.** Edit `index.qmd`. (The "Latest" box fills itself from `data/news.yml`.)

## Preview and publish

```bash
quarto preview          # live preview in your browser while you edit
quarto render           # build the site into _site/
```

### First-time setup on GitHub Pages

1. Create a GitHub repository. Naming it `<your-username>.github.io` gives you the address
   `https://<your-username>.github.io`; any other name gives `https://<your-username>.github.io/<repo>`.
2. Push this folder to the `main` branch.
3. From this folder, run:

   ```bash
   quarto publish gh-pages
   ```

   This renders the site and pushes it to a `gh-pages` branch. The first time, confirm the prompt.
4. In the repository on GitHub, go to Settings, then Pages, and check that the source is the
   `gh-pages` branch. The site is live a minute or two later.
5. Uncomment `site-url` in `_quarto.yml` and set it to the live address, so link previews on
   social media show your photo.

After that, every update is: edit, commit and push the source to `main`, then run `quarto publish gh-pages`.

### Custom domain (optional)

Buy a domain (for example `bernardocaldarola.com`), add a file named `CNAME` containing just the domain
to this folder, add `CNAME` to `resources` in `_quarto.yml`, and follow GitHub's instructions for the DNS records.

## Still to do

- Replace every `url: "#"` in `data/publications.yml` and `data/policy.yml` with real links.
- Paste abstracts over the `Abstract to be added.` placeholders (or delete the `abstract:` line to hide the button).
- Replace the GitHub and LinkedIn placeholder links in `index.qmd`.
- Add the media coverage links (Forbes, The Telegraph, Daily Mail, Nemo Kennislink).
- Consider a version of the CV PDF without your phone number and office address.
