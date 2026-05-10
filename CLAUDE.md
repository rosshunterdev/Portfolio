# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Static HTML/CSS portfolio site for Ross Crawford, deployed on Netlify. No build step, no package manager, no JavaScript framework — open any `.html` file directly in a browser to develop.

## File structure

- `index.html` — single-page portfolio (home, about, projects, skills, contact sections)
- `case-study-drama-geeks.html` — standalone case study page
- `portfolio.css` — all styles for both pages; case study page also imports `case-study.css`
- `case-study.css` — case study-specific styles layered on top of `portfolio.css`

## CSS architecture

`portfolio.css` is the source of truth for design tokens and shared components. It is structured with section comments (`/* === SECTION NAME === */`) in this order: Design Tokens → Base → Buttons → Navbar → Hero → Projects → Testimonial → Skills → About → Contact → Footer → Scroll Reveal → Responsive → Reduced Motion.

Design tokens are CSS custom properties on `:root` (`--color-*`, `--font-*`, `--space-*`, `--radius-*`, `--transition-default`). Use these rather than hardcoded values.

The hero section uses a two-column flex layout (`.hero-editorial-grid`): `.hero-top-left` anchors to `flex-start` (top), `.hero-bottom-right` uses `align-self: flex-end` (bottom). This creates the editorial split. The grid collapses to a vertical stack below 768px.

Responsive breakpoints: 992px (project cards switch to side-by-side), 900px, 768px (mobile nav), 600px, 480px.

## Typography

Two fonts loaded from Google Fonts:
- `Inter` — body text (`--font-sans`)
- `Fraunces` — display/headings (`--font-display`), optical sizing enabled (`font-optical-sizing: auto`)

## Scroll reveal

`js-loaded` is added to `<html>` on page load. The CSS rule `html.js-loaded section, html.js-loaded .project-card` sets `opacity: 0; transform: translateY(30px)` — the JS `IntersectionObserver` and `revealOnScroll` function reset these inline. Respects `prefers-reduced-motion`.

## Deployment

Hosted on Netlify at `https://ross-crawford-portfolio.netlify.app/`. Pushing to `main` on the GitHub remote triggers a deploy. There is no build command — Netlify serves the files as-is.
