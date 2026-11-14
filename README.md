# CREED Neurovascular Framework

**Knowledge • Intelligence • Discovery — Learn Beyond Boundaries.**

A static learning-platform website that joins neuroscience, exam preparation and study tools in one place. It runs entirely in the browser, so it can be hosted free on GitHub Pages with no build step.

Live site: https://oluwafemoli.github.io/creed-neurov-framework/

## Features

| Area | What it does |
|---|---|
| **Home** | Welcome hero with founder photo, a brief introduction to the framework, and feature cards |
| **About** | Mission and the 5-stage roadmap (Foundation → Advanced ecosystem) |
| **Neuroscience** | Lessons on Brain Anatomy, Neurobiology, Cognitive Neuroscience, Nervous System and Neurovascular Coupling; mark lessons complete |
| **Exam Prep** | WAEC, JAMB, NECO, GCE, IELTS, Post-UTME, SAT/TOEFL |
| **University Learning** | Portals, online courses, lecturers, student dashboard (planned items are labelled) |
| **AI Assistant** | In-browser tutor that answers from the lesson library and generates flashcards |
| **Digital Library** | Searchable list of reference resources |
| **Study Tools** | Links to the calculator and timer, plus flashcards with export |
| **Calculator** | Scientific calculator: trig and inverse trig, hyperbolics, ln/log, powers, roots, factorial, nPr/nCr, mod, memory, Ans, DEG/RAD, history, keyboard input |
| **Pomodoro** | Focus/short/long breaks, custom durations, progress ring, alerts, daily and 7-day statistics |
| **Quizzes** | Multiple-choice quizzes with instant feedback, scores and printable certificates at 70%+ |
| **Community** | Discussion posts (login required) |
| **Reels** | TikTok-style vertical video feed for YouTube, TikTok, Facebook and `.mp4` links |
| **Pricing** | Free, Student and Institution plans (payment not yet connected) |
| **Login / Register** | Student accounts and a personal dashboard |

## Project structure

```
creed/
├── index.html      # Page shell (header, footer, mount point)
├── style.css       # All styling and animations
├── app.js          # Routing, pages, calculator, timer, quizzes, reels logic
├── reels.json      # Reels shown to every visitor (starts empty)
├── .nojekyll       # Tells GitHub Pages to serve files as-is
└── assets/         # Logo, icon and photos
```

The site is a single-page app using hash routing (`#/about`, `#/quiz`, …), which works on GitHub Pages without extra configuration.

## Deploy to GitHub Pages

1. Unzip and upload the **contents** of the `creed` folder to the root of your repository (`index.html` must be at the root).
2. In the repository go to **Settings → Pages**.
3. Under **Source**, choose **Deploy from a branch**, select `main` and `/ (root)`, then **Save**.
4. After a minute the site is live at `https://<username>.github.io/<repository>/`.

To test locally, open `index.html` in a browser, or run `python3 -m http.server` in the folder and visit `http://localhost:8000`. (`reels.json` needs a server or GitHub Pages to load.)

## Customising

**Add reels for all visitors** — edit `reels.json`:

```json
[
  {"url": "https://www.youtube.com/shorts/VIDEO_ID", "title": "How neurons fire", "cat": "Neuroscience"},
  {"url": "https://www.tiktok.com/@user/video/1234567890", "title": "JAMB maths tip", "cat": "JAMB"}
]
```

Categories: `Neuroscience`, `JAMB`, `WAEC`, `Study Tips`, `Motivation`. Use full TikTok links (containing `/video/`); Facebook videos must be public.

**Edit content** — in `app.js`:
- `TOPICS` — lessons (also used by the AI assistant)
- `QZ` — quiz questions: `[question, correctAnswer, [options]]`
- `EXAMS`, `LIB`, `REELS` — exam cards, library items, starter reels

**Edit branding** — colours are CSS variables at the top of `style.css` (`--n`, `--b`, `--c`, `--g`). Replace images in `assets/` keeping the same file names.

## Data and privacy

Accounts, progress, flashcards, posts, quiz scores, timer statistics and user-added reels are stored in the visitor's own browser (`localStorage`). Nothing is sent to a server. Passwords are only lightly encoded, not securely hashed, so do not treat this as production authentication.

## Known limitations

- No shared database: data does not sync between devices, and community posts are visible only on the device that made them.
- The AI assistant uses built-in lesson text, not a cloud AI model.
- Live classrooms, payments, parent dashboard, lecturer analytics and mobile apps are placeholders for future stages.
- Videos are embedded by link; the site cannot search or pull videos from YouTube, TikTok or Facebook automatically.
- Calculator factorial works on plain numbers (`5!`); for expressions use `fact(3+2)`.

## Roadmap

1. **Foundation** — brand, website, registration, basic assessments *(current)*
2. **Diagnostic intelligence** — stability index, assessments, diagnostic reports
3. **AI solutions** — action plans, root-cause analysis, progress tracking
4. **Industry intelligence** — benchmarking, expert network
5. **Advanced ecosystem** — corporate dashboards, predictive monitoring, partnerships, international expansion

Suggested next technical steps: a backend (Firebase or Supabase) for real accounts, shared community and cloud sync; a server-side AI tutor; payment integration; a larger question bank.

## Credits

Created by Oluwafemi. © 2026 CREED Neurovascular Framework.

## Update: roles, plans and e-learning

- **Roles:** sign up as a **Student** or a **Tutor** (tutors add subjects and a WhatsApp number or meeting link).
- **Gated features:** Calculator and Pomodoro need an account; reels can be watched by anyone, but like, follow, save, share and adding reels need sign-in. A reels rail sits above the header menu on every page.
- **Tutors page:** free students can connect with **2 tutors**; free tutors can take **2 students**. Paid plans remove the limit. List tutors for all visitors in `tutors.json` (`id`, `name`, `subj`, `bio`, `contact`).
- **Assignments:** tutors publish and grade; connected students submit text or a file under 400 KB.
- **Plans:** Student and Tutor, each Free / Monthly / Lifetime (`PL` in `app.js`, prices are placeholders). Plans activate in demo mode (`DEMO=true`). To charge real money, add payment links in `PAY` (e.g. `PAY['student-month']='https://...'`) and set `DEMO=false`, then verify payments on a backend.
- **Reels content:** put real video links in `reels.json`; add a `"by"` field to enable per-creator Follow.
- **Pages added:** FAQ and Resources (mirrors the Neurovascular Dynamic Lab resources page).
- **Important:** all data is stored per browser, so students and tutors on different devices cannot yet see each other's assignments, submissions or connections without a backend (Firebase/Supabase).

## Update: menu, profiles, AI tutors, reels

- **Dropdown menu:** pages are grouped into Learn, Tutors, Tools, Community and More (tap to open on mobile). Reels now live only in the menu (Community → Reels).
- **Profiles:** `#/profile` lets students and tutors edit their profile (photo under 150 KB). Tutors add headline, subjects, experience, rate, availability and a contact link; each tutor has a public page (`#/tutorprofile`).
- **AI Tutors page:** CREED's built-in assistant plus links to third-party AI tutors (ChatGPT Study Mode, Claude, Gemini Guided Learning, Khanmigo, Perplexity, Wolfram|Alpha, Photomath, Quizlet). They are independent services, so check each one's terms and pricing; they do not count toward the free 2-tutor limit.
- **Reels:** a vertical TikTok/Shorts-style viewer with For You / Following / Saved tabs, an action rail (follow, like, comment, save, share), pause on tap and auto-advance. It ships with **20 animated demo reels** (CREED study cards, not filmed video). Edit them in `RD` in `app.js`.
- **Reel settings (⚙️):** theme (Auto, Ocean, Sunset, Forest, Midnight, Gold), autoplay, voice narration, animations, text size and reel length. Settings save per device.
- Real video links (YouTube, TikTok, Facebook, .mp4) still work through "Add video reels" or `reels.json`.
