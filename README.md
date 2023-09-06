# hiiruki.dev

_yet another personal website._

[![Netlify Status](https://api.netlify.com/api/v1/badges/73730c94-7f54-47c9-bd39-054054829340/deploy-status)](https://app.netlify.com/sites/hiiruki/deploys "Netlify Status")

This is my personal website. It's built with [Hugo](https://gohugo.io/) and hosted on [Netlify](https://www.netlify.com/) and using [Kamigo](https://github.com/hiiruki/hugo-Kamigo) theme. You can visit [here](https://hiiruki.dev).

![light mode](.github/images/light_mode.webp#center "Light mode")
![dark mode](.github/images/dark_mode.webp#center "Dark mode")

## Pagespeed Insights

[Google Pagespeed Insights](https://pagespeed.web.dev/analysis/https-hiiruki-dev/rqaiq47qyp?form_factor=mobile) score for this website.

#### Mobile

![mobile](.github/images/mobile.webp#center "Mobile")

#### Desktop

![desktop](.github/images/desktop.webp#center "Desktop")

## Flow

```mermaid
graph TD

subgraph GitHub Repo
  A[Website Code] --> B[Commit Changes]
  B --> C[Push to Repo]
end

subgraph Netlify CI/CD Pipeline
  C --> D[Trigger CI/CD from main branch]
  D --> E[Build with Hugo]
  E --> F[Deploy to Netlify]
end

subgraph Netlify Hosting
  F --> G[Live Website]
end
```

## License

The content of this website is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).

The source code of this website is licensed under [MIT](/LICENSE).
