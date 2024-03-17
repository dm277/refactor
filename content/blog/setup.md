---
title: Jak vyrobit blog
date: 2024-03-17T07:06:21+01:00
draft: false
tags:
  - technika
  - hugo
categories:
  - blog
---

# Hugo a Ananke na GitHub pages

Používám Hugo. Recept na uvaření stránek vypadá asi takhle:

```shell
hugo create new site siteName

# init git in emacs C-x g, get ananke
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke

hugo new blog/welcome.md
```

Teď musíme upravit *hugo.toml*:

```toml
baseURL = '/'
languageCode = 'cs-cz'
title = 'čn'
theme = 'ananke'
canonifyURLs = true
SectionPagesMenu = 'main'
DefaultContentLanguage = 'cs'
[params]
  favicon = 'favicon.ico'
  body_classes = 'avenir bg-near-white'
```

main říká starej se mi o menu, každá složka je jedna položka v menu. A cs říká místo *read more* mi tam dej *čti dále* Tak to chci. Je to v souboru *themes/ananke/i18n/cs.toml*. A favicon se dá do přímo do složky static. Ještě si menu přejmenuju, v *content/blog/_index.md*:

```yaml
---
title: blog
featured_image: images/blog.jpg
---
```

Aby se mi nový blogy stavěly s rozumnou front matter, v yamlu, upravíme
*archetypes/default.md*

```yaml
---
title: {{ replace .Name "-" " " | title }}
date: {{ .Date }}
draft: true
tags:
  - moje
categories:
  - blog
---
```

Tak už to něco bude dělat, tak teď už jenom dát to online. První co udělám, po otestování webu na lokálu, je vybrat stránky co chci dát na web a dát u drafts false.

- Přidám nový web do github desktop a pošlu ho na github a jdu na online GitHub
- potom už můžu commitovat přímo z emacs, magit push - P
- jdu do repository settings, pages, a upgraduju site na public
- z deployment vybrat github actions
- najít hugo action, komitnout jí

Pak už to jede samo. Při každým dalším *commitu* stránek se spustí automaticky action a uploaduje na gitHub pages.

🏄‍♂️
