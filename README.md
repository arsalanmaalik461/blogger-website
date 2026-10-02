<p align="center">
  <img src="docs/assets/banner.svg" alt="Blogger Website Banner" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=next.js&logoColor=white" alt="Next.js">
  <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=white" alt="Sass">
  <img src="https://img.shields.io/badge/Bootstrap-7952B5?style=for-the-badge&logo=bootstrap&logoColor=white" alt="Bootstrap">
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node.js">
</p>

> **Developed by [Arslan Malik](https://github.com/arsalanmaalik461)**
> 📱 WhatsApp: [+92 300 8987448](https://wa.me/923008987448) · 🌐 Website: [arslanmalik.tech](https://arslanmalik.tech)

---

## 🌟 Executive Overview

**Blogger Website** (package name `blogar`) is a complete personal blogging platform built on **Next.js 12** and **React 18**. Instead of a database-backed CMS, it uses a file-based content system: every article is a Markdown file in the `posts/` directory with YAML front matter, parsed by `gray-matter` and rendered to HTML by `remark`. Publishing a new post is literally as simple as dropping a `.md` file into a folder — no admin panel, no database, no server required.

Every page is statically generated at build time with `getStaticProps` / `getStaticPaths` (`fallback: false` in `src/pages/post/[slug].js`), so the site ships as fast, SEO-friendly static HTML while keeping the full React component model for interactivity. The repository ships with **42 sample posts** and a rich editorial UI out of the box: twelve homepage post-section layouts, five post formats (standard, video, gallery, audio, quote), category / author / tag archive routes, a dark-light mode color switcher, an EmailJS-powered contact form, and a Sass design system with dedicated RTL stylesheets.

## 📑 Table of Contents

- [✨ Key Features & Highlights](#-key-features--highlights)
- [🖥️ Feature Showcase](#️-feature-showcase)
- [🏗️ System Architecture](#️-system-architecture)
- [🚀 Quickstart & Installation Guide](#-quickstart--installation-guide)
- [📂 Project Structure](#-project-structure)
- [🛡️ Security & Notes](#️-security--notes)

---

## ✨ Key Features & Highlights

| Feature | Description |
| :--- | :--- |
| 📝 File-based Markdown CMS | Posts live in `posts/` as Markdown with YAML front matter; `gray-matter` extracts metadata and `remark` + `remark-html` renders the body |
| ⚡ Static Site Generation | `getStaticProps` / `getStaticPaths` pre-render every post, category, author, and tag page at build time for speed and SEO |
| 🎞️ 5 post formats | Standard, video (YouTube embed), gallery, audio, and quote — selected per post via the `postFormat` front-matter field |
| 📰 12 homepage sections | `PostSectionOne` … `PostSectionTwelve` editorial layouts: sliders, grids, lists, featured video, and ad slots |
| 🗞️ 6 blog home variants | `index`, `creative-blog`, `lifestyle-blog`, `seo-blog`, `tech-blog`, and `post-list` entry pages |
| 🏷️ Dynamic archive routes | Category, author, and tag archive pages (`src/pages/category/[slug].js`, `author/[slug].js`, `tag/[slug].js`) |
| 🔍 Search & pagination | Client-side post search (`react-search-box`) and paginated listings (`react-paginate`) |
| 🌙 Dark / light mode | `ColorSwitcher` toggles `active-dark-mode` / `active-light-mode` on the body and persists the choice in `localStorage` |
| ✉️ Contact form | Serverless contact form powered by EmailJS (`@emailjs/browser` via `FormOne.jsx`) |
| 📱 Responsive UI | Bootstrap 5 + React Bootstrap grid with a dedicated mobile menu and sticky headers |
| 🎨 Sass design system | Organized SCSS partials (variables, mixins, typography, spacing, header/footer/post styles) plus a dedicated RTL stylesheet |
| 📊 42 sample posts | Ready-made editorial content covering tech, lifestyle, SEO, design, and travel |

---

## 🖥️ Feature Showcase

### 1. 📝 File-Based Markdown CMS

> "No database, no admin panel — publishing is just a Markdown file."

- Each post is a `.md` file with front matter: `title`, `postFormat`, `featureImg`, `date`, `cate`, `author_name`, `author_img`, `tags`, `read_time`, and more
- `lib/api.js` provides the data layer — reading post slugs, fetching posts by slug, and aggregating posts across the whole collection
- `lib/markdownToHtml.js` converts Markdown bodies to HTML with `remark` + `remark-html`
- The privacy policy page is itself rendered from a Markdown source (`src/data/privacy/PrivacyPolicy.md`)

### 2. 🎞️ Post Formats & Editorial Layouts

> "Five ways to tell a story, twelve ways to lay out the front page."

- `post/[slug].js` picks the right renderer automatically: `PostFormatStandard`, `PostFormatVideo`, `PostFormatGallery`, `PostFormatAudio`, or `PostFormatQuote`
- Video posts embed YouTube via a `videoLink` front-matter field; audio posts use `react-audio-player`
- The homepage composes twelve `PostSection*` components — hero sliders (`react-slick`), category grids, featured video, and inline ad banners
- Six blog home variants (`index`, `creative-blog`, `lifestyle-blog`, `seo-blog`, `tech-blog`, `post-list`) give the site multiple editorial faces from the same post collection

### 3. 🌙 Theme, Motion & Interaction

> "Dark mode that remembers you, and a cursor that follows your lead."

- Global `ColorSwitcher` in `_app.js` toggles the theme class on the body and persists the choice in `localStorage`
- Framer Motion powers a custom dual-layer mouse cursor that tracks the pointer
- Scroll-triggered section layouts, hover animations, and `react-slick` carousels throughout
- A complete contact page (`contact.js`) with the EmailJS-backed `FormOne` component — form submissions go to your inbox with no backend

### 4. 🏷️ Archives, Search & Mobile UX

> "Find anything: by topic, by author, by tag — on any screen."

- Dynamic archive routes for every category, author, and tag — all statically pre-rendered
- `react-search-box` search plus `react-paginate` pagination on listing pages
- Dedicated mobile menu data (`src/data/mobilemenu`) and sticky, responsive headers via Bootstrap 5 / React Bootstrap
- Sidebar widgets (search, categories, tags, newsletter, Instagram feed, social share) complete the editorial experience

---

## 🏗️ System Architecture

```mermaid
graph TD
    A[posts/*.md<br/>Markdown + front matter] --> B[lib/api.js<br/>getPostSlugs / getAllPosts]
    B --> C[gray-matter<br/>metadata extraction]
    B --> D[lib/markdownToHtml.js<br/>remark + remark-html]
    C --> E[getStaticPaths]
    D --> F[getStaticProps]
    E --> G[Static HTML pages]
    F --> G
    G --> H[5 post formats<br/>Standard · Video · Gallery<br/>Audio · Quote]
    G --> I[12 PostSection layouts<br/>hero sliders, grids, lists]
    G --> J[Archive routes<br/>category / author / tag]
    K[ColorSwitcher] -->|localStorage| G
    L[FormOne.jsx] -->|@emailjs/browser| M[Owner inbox]
    N[Sass design system<br/>+ RTL styles] --> G
    O[Bootstrap 5 grid<br/>mobile menu] --> G
```

**Flow:** Markdown posts are parsed at build time and pre-rendered into static pages. The React runtime adds client-side interactivity — theme switching, search, pagination, carousels, and the serverless contact form — while Sass and Bootstrap handle the responsive editorial design.

---

## 🚀 Quickstart & Installation Guide

### Prerequisites

- **Node.js** 16+ and **npm** (or yarn)
- An [EmailJS](https://www.emailjs.com/) account (only needed if you want the contact form to send mail)

### Step-by-Step Installation

```bash
# 1. Clone the repository
git clone https://github.com/arsalanmaalik461/blogger-website.git
cd blogger-website

# 2. Install dependencies
npm install

# 3. Run the development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the blog.

```bash
# Production build & serve
npm run build
npm start
```

### Publish a New Post

```bash
# Create a Markdown file in posts/ — that is the entire CMS
posts/my-new-post.md
```

Use this front-matter template:

```yaml
---
title: "My New Post"
postFormat: "standard"
featureImg: "/images/post/post-img-01.jpg"
date: "2026-10-03"
cate: "Technology"
author_name: "Arslan Malik"
author_img: "/images/author/author_img.jpg"
tags: "nextjs, react"
read_time: "5 Min read"
---
Your Markdown content here...
```

Then `npm run build` — every page, including archives, regenerates automatically.

### Enable the Contact Form

Open `src/common/components/form/FormOne.jsx` and replace the EmailJS credentials in `emailjs.sendForm(...)` with your own service ID, template ID, and public key from your [EmailJS dashboard](https://dashboard.emailjs.com/).

### Base Path (Optional)

To deploy under a sub-path, set the environment variable read by `next.config.js`:

```bash
NEXT_PUBLIC_BASEPATH=/blog npm run build
```

---

## 📂 Project Structure

```
blogger-website/
├── posts/                          # 42 sample posts (Markdown + front matter)
├── src/
│   ├── pages/                      # Next.js routes
│   │   ├── index.js                # Main blog home
│   │   ├── creative-blog.js / lifestyle-blog.js
│   │   ├── seo-blog.js / tech-blog.js / post-list.js
│   │   ├── post/[slug].js          # Individual post (SSG, fallback: false)
│   │   ├── category/[slug].js      # Category archives
│   │   ├── author/[slug].js        # Author archives
│   │   ├── tag/[slug].js           # Tag archives
│   │   ├── about.js / contact.js / privacy-policy.js
│   │   └── _app.js / _document.js / 404.js / maintenance.js
│   ├── common/
│   │   ├── components/
│   │   │   ├── post/               # PostSectionOne..Twelve + layouts + formats
│   │   │   ├── sidebar/            # Sidebar widgets
│   │   │   ├── slider/             # react-slick sliders
│   │   │   ├── category/ / instagram/ / ad-banner/
│   │   │   ├── form/               # EmailJS contact form (FormOne)
│   │   │   └── social/
│   │   ├── elements/               # Header, footer, breadcrumb, color-switcher
│   │   └── utils/
│   ├── data/                       # Social links, Instagram, mobile menu, privacy
│   └── styles/                     # Sass partials (default, header, footer, post, elements) + RTL
├── lib/
│   ├── api.js                      # File-based data layer
│   └── markdownToHtml.js           # remark pipeline
├── public/                         # Images, fonts, static assets
├── docs/assets/banner.svg          # Project banner
├── next.config.js / package.json / .eslintrc.json
└── README.md
```

---

## 🛡️ Security & Notes

- **No database, no API server** — the entire site is static output, which removes whole classes of backend vulnerabilities.
- **EmailJS credentials:** the sample service/template/public key in `FormOne.jsx` is a public client-side key by design (EmailJS keys are meant to be browser-visible), but it is a shared demo account — replace it with your own before going live so submissions reach you.
- **Static builds are safe to host anywhere** — Vercel, Netlify, or any static file host; there is no runtime secret to leak.
- Dependencies are pinned in `package-lock.json`; run `npm audit` and update Next.js/React periodically to stay on supported releases.
- Sample images and posts are placeholder/demo content — swap them for your own before production use.

---

<p align="center">
  <sub>Developed with ❤️ by <a href="https://github.com/arsalanmaalik461">Arslan Malik</a> · 📱 <a href="https://wa.me/923008987448">WhatsApp: +92 300 8987448</a> · 🌐 <a href="https://arslanmalik.tech">arslanmalik.tech</a></sub>
</p>
