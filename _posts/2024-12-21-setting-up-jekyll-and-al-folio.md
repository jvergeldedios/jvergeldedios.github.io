---
layout: post
title: "Setting up Jekyll and al-folio"
tags: ["blog", "tech"]
author: flyingburrito
---

When I decided to set up my blog I had a few requirements:

- Manage content entirely via git
- Static pages only (no backend rendering pages dynamically)
- Deploy to Github Pages or equivalent
- RSS feed compatibility
- SEO best practices implemented automatically
- Accessibility best practices implemented automatically

I'm a Rubyist at heart, so [Jekyll](https://jekyllrb.com) seemed to be the most logical choice. It checks a lot of the boxes above by default, with others being supported by plugins. I followed the quickstart and in short order had a basic Jekyll dev instance set up with the default Minima theme.

While an excellently flexible tool, the base install leaves a lot to be desired. Minima isn't _bad_ but it left a lot of things for me to do myself and I wanted a little bit more of a full package included. I started searching for themes that would fulfill what I wanted while being minimalist and content focused. That's when I found [al-folio](https://github.com/alshedivat/al-folio). It definitely benefitted from the phonebook effect of showing up first in an alphabetical list, but it had pretty much the rest of the list that I wanted and a few other bonuses. Weird quirk: it's designed for academics to share their CV, projects, and publications, which I don't currently need, but could come in handy in the future I guess.

I did run into a few issues getting the Github Actions to run without errors as well as having to dig into issues and other places to get some customizations that I wanted, so I'm documenting what I found here to hopefully save other people time.

# Github Actions errors

I kept getting broken link errors when building my pages which didn't prevent the site from deploying but were annoyingly sending failure emails with every push. Interestingly the main things causing errors were actually the default documentation markdown files for al-folio. After I deleted `README.md`, `INSTALL.md`, `CONTRIBUTING.md`, and `CUSTOMIZE.md` those errors all went away.

# Hiding Pages

I didn't need most of the pages that were included in the default al-folio installation, but didn't exactly know how to remove them without literally deleting them from the template (which I didn't want to do if I needed to bring them back). The answer was in this Github question: https://github.com/alshedivat/al-folio/discussions/2031

In the frontmatter for any of the pages there is an optional `nav` variable that you can set to `false` if you want to omit it from the nav bar. Here is my `cv.md` file's frontmatter:

```markdown
---
layout: cv
permalink: /cv/
title: cv
nav: false # <---- this is what you want to change
nav_order: 5
---
```

# Post Metadata

There were a few pieces of metadata that aren't directly documented that I had to figure out:

- `author`: I assumed this would be inferred from the name in `_config.yml` but it has to be explicitly set per post
- `og_image`: I assumed that this could be automatically pulled from the first image in the post body, but this also needs to be explicitly set
