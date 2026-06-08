# Agent Notes for h4cii.github.io

This repository is Hao Yunlai's GitHub Pages CV site. Future agents should treat it as a public-facing research homepage, not as a private scratchpad.

## Site Goal

- Build and maintain a CV-style personal homepage at `https://h4cii.github.io`.
- Positioning: robotics control, reinforcement learning, Sim2Real, dynamics modeling, and embodied intelligence.
- Audience: prospective supervisors, research groups, collaborators, and technically serious visitors.
- Tone: concise, research-oriented, bilingual where useful, privacy-aware.
- Visual direction: personal CV / academic homepage with a light geek/robot-debugging feel. Prefer paper-like layout, compact CV structure, restrained terminal/code accents, and robot evidence sections. Avoid full black-background academic severity, oversized marketing heroes, product-style metric panels, feature-card sales copy, and public-facing maintenance instructions.

## Repository Facts

- Remote repository: `git@github.com:h4cii/h4cii.github.io.git`.
- GitHub Pages user site URL: `https://h4cii.github.io`.
- Framework: Astro static site.
- Main page: `src/pages/index.astro`.
- Project content lives in `src/content/projects/*.md`.
- Project schema is defined in `src/content/config.ts`.
- Preview video assets should go under `public/media/previews/`.
- Public resume attachment is `public/resume/hao-yunlai-cv.pdf`.
- GitHub Actions deployment workflow is `.github/workflows/deploy.yml`.
- `astro.config.mjs` sets `site: 'https://h4cii.github.io'`; do not add `base` for this user site.

## Development Configuration

Runtime and package setup:

- Package manager: npm.
- Project module type: ESM (`"type": "module"` in `package.json`).
- Primary dependencies: `astro`, `@astrojs/check`, and `typescript`.
- GitHub Actions uses Node 20 and `npm ci`.
- Local Node observed during setup: `v20.15.0`. Some transitive packages warned that they prefer `>=20.19.0`; the build still passed. Prefer Node `20.19+` for future local development when convenient.

Available npm scripts:

- `npm run dev`: start the Astro dev server.
- `npm run build`: run `astro check && astro build`.
- `npm run preview`: preview the generated static site after a build.

Recommended local commands:

- Dev server: `npm run dev -- --host 127.0.0.1 --port 4321`.
- Static preview: `npm run preview -- --host 127.0.0.1 --port 4323`.
- If a port is occupied, choose another local port instead of killing unrelated user processes.

Astro configuration:

- Config file: `astro.config.mjs`.
- Required site value: `site: 'https://h4cii.github.io'`.
- Do not set `base`, because this is a GitHub Pages user site at the root domain path.
- Build output is the Astro default `dist/` directory.

Deployment configuration:

- Workflow file: `.github/workflows/deploy.yml`.
- Triggers: push to `main` and manual `workflow_dispatch`.
- Build job: checkout, setup Node 20 with npm cache, run `npm ci`, run `npm run build`, upload `./dist`.
- Deploy job: `actions/deploy-pages@v4`.
- GitHub Pages repository setting should use `GitHub Actions` as the Pages source, not the legacy branch/Jekyll source.

Content and media configuration:

- Main page and styling currently live together in `src/pages/index.astro`; there is no component split yet.
- Project metadata lives in `src/content/projects/*.md`.
- Project schema lives in `src/content/config.ts`.
- The current preferred video model is `demos`, an optional array with `title`, `src`, `caption`, and optional `muted`.
- Public video/image assets should be placed under `public/media/previews/` and referenced with root-relative URLs such as `/media/previews/example.mp4`.
- The current video renderer declares MP4 sources. If adding `.webm`, update the source `type` logic in `src/pages/index.astro`.
- Legacy fields `previewLabel`, `mediaStatus`, `previewSrc`, and `fullDemoUrl` may still be present for placeholders or external links, but new embedded homepage clips should use `demos[]`.

Current preview assets known in the worktree:

- `public/media/previews/quadruped-slope-stairs.mp4`.
- `public/media/previews/quadruped-flat-sim2real-muted.mp4`.

## Privacy Rules

Allowed public information:

- Name: Hao Yunlai.
- School and broad academic identity: SWJTU / Applied Physics undergraduate.
- Email: `hyl00250083@outlook.com`.
- Research interests, project categories, generalized technical stack, and generalized achievement language.
- A public resume PDF may be linked, but the homepage body should still keep sensitive details summarized.

Do not expose:

- Exact rank numbers or cohort-level ranking details.
- Exact grade/year details.
- Exact national scholarship count.
- Phone number, address, student ID, device serials, IP addresses, usernames, file paths, or lab-private details.
- Unpublished paper internals, team strategy, unreleased robot configuration details, or sensitive competition material.

Use generalized phrasing such as:

- `top-ranked undergraduate`
- `national scholarship recipient`
- `national-level robotics competition experience`
- `publishable robotics/control research contribution`

The attached resume PDF may contain more detailed personal information than the homepage. Do not copy those details into page text unless explicitly requested and reviewed for public exposure.

## Video Policy

- The homepage should show short sanitized preview clips, not full raw debugging videos.
- Recommended preview duration: 5-15 seconds.
- Recommended preview size: about 3-8 MB each.
- Preferred formats: `.webm` or compressed `.mp4`.
- Full-resolution demos should be linked externally through Bilibili, YouTube, GitHub Releases, object storage, or another stable host.
- Before publishing any video, crop or blur sensitive lab background, terminal paths, usernames, IP addresses, device IDs, wiring labels, unreleased mechanism details, and paper-specific experimental details.
- If no video is available yet, keep the current placeholder card instead of adding fake media.
- RoboCON and quadruped RL materials are expected to have real videos/images available later. Use those assets as evidence, not decoration.
- Drift/MPPI research may later add an arXiv link and a paper screenshot/figure after public release.

To add a preview video:

1. Put the file in `public/media/previews/`.
2. Edit the relevant file in `src/content/projects/`.
3. Add an entry under `demos`, for example:

   ```yaml
   demos:
     - title: "Terrain traversal"
       src: "/media/previews/quadruped-demo.mp4"
       caption: "Short sanitized hardware preview."
       muted: true
   ```

4. Set `fullDemoUrl` only when a public full demo link is ready.
5. Run `npm run build`.

## Current Content Priorities

Keep these projects visible, in this order:

1. Quadruped RL and Sim2Real.
2. High-Speed Drift Control with nonlinear tire dynamics and MPPI.
3. RoboCON Robot Control for embedded multi-DOF mechanism control.

Do not turn the site into a generic landing page. The first screen should quickly answer:

- Who is this?
- What research direction does he work on?
- What robot systems or demos can I inspect?

## Development Notes

- Local Node during this session was `v20.15.0`; `npm install` warned that some transitive packages prefer `>=20.19.0`, but `npm run build` passed.
- `npm run build` runs `astro check && astro build`.
- Astro telemetry may try to write under the user config directory on first run. In this sandbox it required elevated execution once.
- The in-app browser plugin failed during this session on Windows sandbox startup, so visual QA was done with Microsoft Edge headless screenshots.
- A 390px Edge headless screenshot appeared cropped due to tooling behavior; a 500px narrow screenshot rendered correctly after responsive fixes.
- Current dev server was started with `npm run dev -- --host 127.0.0.1` and served `http://127.0.0.1:4321`.

## Previous Profile README Context

- There is a separate GitHub Profile README repository: `h4cii/h4cii`.
- A separate local checkout for the Profile README may exist beside this repository.
- The Profile README was optimized earlier to be privacy-aware and had the broken `GitHub Stats` section removed.
- The local Profile README repo may show `ahead 2` because SSH push failed and the cloud README was updated through the GitHub App instead.
- Do not reintroduce third-party GitHub stats cards unless they are reliable and add real value.

## Validation Checklist

Before finishing any change:

- Run `npm run build`.
- Scan for sensitive details: exact rank, exact year, exact scholarship count, device IDs, IPs, terminal paths, lab-private details.
- Check desktop and narrow layouts for text overflow.
- Confirm video placeholders or preview clips do not break layout.
- Confirm GitHub Pages workflow still targets `main` and deploys `dist`.
