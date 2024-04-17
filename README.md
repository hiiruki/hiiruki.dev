# hiiruki.dev

_yet another personal website._

[![Cloudflare Build Status](https://img.shields.io/endpoint?url=https://pages.hiiruki.dev/project/hiiruki-dev?label=hiiruki.dev)](hiiruki.dev) [![Netlify Build Status](https://api.netlify.com/api/v1/badges/73730c94-7f54-47c9-bd39-054054829340/deploy-status)](https://app.netlify.com/sites/hiiruki/deploys "Netlify Status")

This is my personal website. It's built with [Hugo](https://gohugo.io/) and hosted on [Cloudflare](https://cloudflare.com/) and [Netlify](https://www.netlify.com/) and using [Kamigo](https://github.com/hiiruki/hugo-Kamigo) theme. You can visit [here](https://hiiruki.dev).

> [!NOTE]
> Main hosting is on Cloudflare and Netlify is used as a backup hosting. The website is served over HTTPS and has a valid SSL certificate. I moved from Netlify to Cloudflare because of the better performance and security features and most of my domains are already on Cloudflare. Netlify is still used as a backup hosting.

![light mode](.github/images/light_mode.webp#center "Light mode")
![dark mode](.github/images/dark_mode.webp#center "Dark mode")

## Pagespeed Insights

[Google Pagespeed Insights](https://pagespeed.web.dev/analysis/https-hiiruki-dev/rqaiq47qyp?form_factor=mobile) score for this website.

#### Mobile

![mobile](.github/images/mobile.webp#center "Mobile")

#### Desktop

![desktop](.github/images/desktop.webp#center "Desktop")

## Architecture

- [Hugo](https://gohugo.io/) is responsible for using templates and markdown files to create pages, as well as building other files needed for cosmetics (it's a static site generator).
- [Cloudflare Pages](https://pages.cloudflare.com/) is responsible for building the website and deploying it to the Cloudflare edge network. It's used as the [main hosting](https://hiiruki-dev.pages.dev/).
- [Netlify](https://www.netlify.com/) is responsible for building the website and deploying it to the Netlify edge network. Now it's used as a secondary or [backup hosting](https://hiiruki.netlify.app/).
- [Kamigo](https://github.com/hiiruki/hugo-Kamigo) is a Hugo theme that I created for this website. It's a fork of the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme. It's focused on customization, improving code quality, UI/UX improvement, and security improvement or hardening to the original/previous mod theme.
- [GitHub](https://github.com) is used for version control and hosting the source code of the website.

## Flow

```mermaid
graph TD

subgraph GitHub Repo
  A[Website Code] --> B[Commit Changes]
  B --> C[Push to Repo]
end

subgraph Cloudflare & Netlify CI/CD Pipeline
  C --> D[Trigger CI/CD<br>from main branch]
  D --> E[Build with Hugo<br>hugo --gc --minify<br>Publish Directory: public]
  E --> F[Deploy to Cloudflare Pages<br>and Netlify Site]
end

subgraph Cloudflare & Netlify Hosting
  F --> G[Live Website<br>https://hiiruki.dev]
end
```

## License

### Content

 <p xmlns:cc="http://creativecommons.org/ns#" ><a href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1" alt=""><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1" alt=""></a></p>


The content of this website is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

### Source Code

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

The source code of this website is licensed under [MIT](/LICENSE)
