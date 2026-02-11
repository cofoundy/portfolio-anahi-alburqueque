# QA Report: Anahi Alburqueque Vasquez

**Date:** 2026-02-11
**URL:** https://cofoundy.github.io/portfolio-anahi-alburqueque/
**Status:** FAIL

## Data Validation
- [x] Name matches source ("Anahi Alburqueque Vasquez" -- Sheet has uppercase, page uses proper casing with accents, acceptable)
- [x] Email matches source (anahi@bocperu.com -- exact match Sheet + config + page)
- [ ] No hallucinated data -- **ISSUES FOUND:**
  1. **Degree name mismatch**: Config says "Licenciatura en Administracion de Empresas" but LinkedIn/research says "Licenciada en Administracion de Servicios" (UDEP). The degree name was changed.
  2. **Job title upgrade**: LinkedIn says "Consultora Especialista" but config/page says "Consultora Senior". Title was inflated.
  3. **Start date discrepancy (BOC)**: Config says "Ene 2005" but LinkedIn says "Dic 2006". BOC start date moved 2 years earlier.
  4. **Education start date**: Config says "1999 - 2005" for UDEP but research says "2000 - 2005". Start year moved 1 year earlier.
  5. **Experience years inflated**: About says "mas de 20 anos de experiencia" but LinkedIn shows BOC since Dec 2006 (~19 years). The "desde 2005" claim compounds with the inflated BOC start date.

## Clean Deploy
- [x] No watermarks (no "Powered by", "Made with", "Built with" text found)
- [x] No placeholder text (no "Lorem ipsum", "[placeholder]", "undefined", "null" found)
- [x] No template links (no "View source", "Fork this", "GitHub" template links)

## Technical
- [x] Page loads (HTTP 200)
- [x] CSS loads (HTTP 200 -- /_astro/index.DjP8OqGM.css)
- [x] Profile image loads (HTTP 200 -- /profile.jpg)
- [x] Favicon loads (HTTP 200 -- /favicon.svg)
- [x] astro.config.mjs has both site + base correctly configured
- [x] HTML lang="es" correct for Spanish content
- [ ] Console errors -- Chrome MCP unavailable, could not verify

## Visual / Content Issues
- [ ] **ESCAPED HTML IN EDUCATION**: The degree field for UTP shows literal `<strong>Maestria</strong>` as visible text instead of rendering bold. Visible in the Education section heading for the first entry. Source: config.ts line 49 uses HTML in `degree` field but the Education.astro component escapes it instead of using `set:html`.
- [ ] **MISSING ACCENT MARKS in section headings**: "Educacion" should be "Educacion" (with tilde on o), "Sobre Mi" should be "Sobre Mi" (with tilde on i). Affects Header, About, Education, and Footer components.
- [ ] **PROFILE PHOTO NOT DISPLAYED**: profile.jpg exists in public/ and returns HTTP 200, but is NOT referenced anywhere in the page HTML. The hero section is text-only with no photo visible.
- [ ] **LINKEDIN NOT INCLUDED**: Client has a LinkedIn profile (found in research-notes.md: linkedin.com/in/anahi-alburqueque-vasquez-27052629) and mentioned "Linkedln" in the form, but social config only has email. No LinkedIn icon/link appears on the page.
- [ ] **NO MOBILE NAVIGATION**: Desktop nav uses `hidden md:block` class, meaning it disappears on mobile. There is no hamburger menu or any mobile navigation alternative. On mobile (<768px), users have no navigation.

## Issues Found (Summary)

### CRITICAL (must fix before delivery)
1. **Escaped HTML tags visible to user** -- Education section shows literal `<strong>` tags as text for "Maestria en Docencia Universitaria"
2. **Profile photo not displayed** -- Photo exists but hero section does not render it
3. **Data accuracy concerns** -- Multiple date/title discrepancies vs LinkedIn source data

### MODERATE (should fix)
4. **Missing accent marks** -- "Educacion" and "Sobre Mi" need tildes for correct Spanish
5. **LinkedIn link missing** -- Client has LinkedIn, form mentions it, research found it, but it's not on the page
6. **No mobile navigation** -- Nav disappears entirely on mobile with no hamburger alternative

### MINOR (nice to fix)
7. **AFP Horizonte experience omitted** -- Minor early career role, acceptable to omit for brevity
8. **Chrome MCP unavailable** -- Could not take screenshot evidence or check console errors

## Evidence
- Screenshots could not be captured (Chrome MCP server connection failed)
- All findings verified via curl HTTP checks and HTML source analysis
