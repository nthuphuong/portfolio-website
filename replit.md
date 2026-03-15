# Thu Phuong Nguyen – Portfolio Website

## Overview
A modern, interactive creative portfolio website for Thu Phuong Nguyen, a UI/UX Product Designer. Built with a bold, agency-style aesthetic inspired by madeinhaus.com, featuring smooth scroll animations, custom cursor interactions, and vibrant section-based color transitions.

## Tech Stack
- **Frontend:** React, Tailwind CSS v4, Framer Motion, Wouter (routing)
- **Backend:** Express.js, Node.js
- **Database:** PostgreSQL with Drizzle ORM
- **Fonts:** Space Grotesk (headlines), Inter (body)

## Architecture
```
client/src/
├── components/
│   ├── sections/      # Hero, About, Skills, Experience, Projects, Contact, Footer
│   ├── ui/            # Shadcn UI components
│   ├── Cursor.tsx     # Custom mouse cursor with hover effects
│   └── BackgroundMusic.tsx  # Audio player with toggle button
├── pages/
│   ├── Home.tsx       # Main portfolio page composing all sections
│   ├── Blog.tsx       # Blog page with article cards (fetches from DB)
│   ├── ProjectDetail.tsx  # Project case study page (fetches from DB)
│   └── not-found.tsx  # 404 page
├── assets/images/     # Profile photo, logo, trail images
├── hooks/
│   └── useProjects.ts # Hooks: useProjects, useProject, useBlogPosts (fetch from API)
└── data/
    └── projects.ts    # LEGACY static data (no longer used by components)

client/public/images/  # Project images served as static assets (referenced by DB)

server/
├── index.ts           # Express server setup
├── routes.ts          # API routes (/api/contact, /api/projects, /api/projects/:slug, /api/blog-posts)
├── storage.ts         # Database storage layer using Drizzle
├── seed.ts            # Database seed script for projects & blog posts
├── vite.ts            # Vite dev server integration
└── static.ts          # Static file serving (production)

shared/
└── schema.ts          # Drizzle schema (users, contact_messages, projects, blog_posts)
```

## Key Features
- **Custom Cursor:** Circle cursor with scale effect on interactive elements
- **Scroll Animations:** Section reveals, parallax effects via Framer Motion
- **Background Music:** Ambient audio with play/pause toggle (bottom-right)
- **Contact Form:** Connected to PostgreSQL database via /api/contact endpoint
- **CV Download:** Direct PDF download from /ThuPhuong_CV.pdf
- **Blog Page:** `/blog` — fetches posts from database via /api/blog-posts
- **Project Detail Pages:** `/project/:slug` — fetches from database via /api/projects/:slug
- **Projects Section:** Fetches all projects from database via /api/projects
- **Responsive:** Works on desktop, tablet, and mobile
- **Hero:** Interactive mouse trail effect, scroll indicator, cycling background colors

## Color Palette (CSS Variables)
- Yellow: `#EFFF82` / `#D7EF6F` (hero bg)
- Purple: `#B9B2FD`
- Green: `#0BA13A`
- Orange: `#FF8643`
- Dark: `#121212`

## Section Order (Home)
Hero → About → Skills → Experience → Projects → Contact → Footer

## Database Schema
- `users`: id (UUID), username, password
- `contact_messages`: id (serial), name, email, message, created_at
- `projects`: id (serial), slug (unique), title, description, tech, tags (text[]), category, date, image, showcase_image, color, overview, problem, process, solution, result, sort_order
- `blog_posts`: id (serial), title, excerpt, category, date, read_time, color, link, sort_order

## API Endpoints
- `GET /api/projects` — All projects ordered by sort_order
- `GET /api/projects/:slug` — Single project by slug
- `GET /api/blog-posts` — All blog posts ordered by sort_order
- `POST /api/contact` — Submit contact form message

## Public Assets
- `/ThuPhuong_CV.pdf` – Downloadable CV
- `/music/background.mp3` – Background ambient music
- `/images/*.png` – Project images (referenced by database entries)

## Important Notes
- Project images stored in `client/public/images/` and referenced by URL path in the database
- Nav logo: `@/assets/images/logo.png` with `brightness-0 invert` filter
- Behance link: https://www.behance.net/jennynguyen0598
- Custom cursor hides on mobile, uses `mix-blend-difference`, reacts to `data-interactive="true"`
- Navigation uses `mix-blend-difference` and `pr-24` to avoid music button
- `.scrollbar-hide` and `.hero-btn*` CSS classes defined in `client/src/index.css`
- Seed script: `npx tsx server/seed.ts` (idempotent — skips if data exists)
