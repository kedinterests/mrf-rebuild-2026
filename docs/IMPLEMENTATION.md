# MRF Theme Implementation Guide

**Step-by-step deployment of the MineralRightsForum redesign (Phase 1).**

---

## Prerequisites

- Discourse 3.1+ instance with admin access
- SVG logo file (Strata concept)
- Access to Discourse theme admin panel

---

## Phase 1: Opt-in Launch

### Step 1: Upload Theme Component to Discourse

1. **Navigate to Admin → Customize → Themes**
2. Click **"Import"** button
3. Paste GitHub repo URL: `https://github.com/kedinterests/mrf-rebuild-2026`
4. Click **"Import"** — Discourse will clone and parse the component
5. Verify files appear: `theme.json`, stylesheets, templates

### Step 2: Create New Color Scheme (Optional)

The theme includes a pre-configured "MRF Navy & Gold" color scheme in `theme.json`.

1. In Admin → Customize → Colors, you can import or create:
   - **Primary**: `#0a192f` (Navy)
   - **Secondary**: `#ffffff` (White)
   - **Tertiary**: `#c5a059` (Gold)
   - **Header Background**: `#0a192f` (Navy)
   - **Header Primary**: `#ffffff` (White)
   - **Highlight**: `#c5a059` (Gold)

### Step 3: Upload Strata Logo

1. Export the Strata logo as SVG (4 horizontal gold bars)
2. In Admin → Customize → Colors, upload under **"Logo"**
   - Or use Admin → Settings → **"Logo"**
3. Verify it appears in header (max-height: 45px, responsive)

### Step 4: Configure Theme Variables

The component expects these Discourse settings to be passed:

**In `theme.json` (already configured):**
```json
"color_schemes": {
  "MRF Navy & Gold": {
    "primary": "#0a192f",
    "secondary": "#ffffff",
    "tertiary": "#c5a059",
    ...
  }
}
```

### Step 5: Test in Staging Environment

1. Clone a production database to staging
2. Import the theme component into staging (Admin → Customize → Themes → Import)
3. Enable the "MRF Navy & Gold" color scheme
4. Test on desktop and mobile:
   - [ ] Hero banner displays after header (Playfair Display heading, gold subtitle)
   - [ ] Opt-in switcher banner shows with "Try it now" / "Later" buttons
   - [ ] Topic list styling: navy headings, gold hover states
   - [ ] Tags styled with gold borders and backgrounds
   - [ ] Footer displays with "Back to classic view" link
   - [ ] Colors render correctly (navy, gold, off-white)
   - [ ] Typography: Playfair Display for headings, Inter for body
   - [ ] Mobile responsiveness: stacked layout, touch-friendly buttons

### Step 6: Deploy to Production (Phase 1 Live)

1. Import component into production Discourse instance
2. **Do NOT** set as default theme yet
3. The opt-in banner will appear for all members
4. Members who click "Try it now" → theme switcher saves preference in localStorage
5. Members who click "Later" → banner dismissed for that session

---

## Component Structure

### `theme.json`
- Color scheme definitions
- Theme metadata
- Asset references (logo)

### `stylesheets/desktop.scss`
- **Colors**: Navy (#0a192f), gold (#c5a059), off-white (#f8f6f1)
- **Typography**: Playfair Display 700 (headings), Inter 400/600 (body)
- **Components**: Topic list, tags, buttons, nav pills, categories, posts, forms
- **Hover states**: Navy light, gold hover colors
- **~150 lines total**

### `stylesheets/mobile.scss`
- Breakpoints: 768px, 480px
- Stacked layouts, touch-friendly spacing
- Adjusted font sizes for smaller screens
- **~80 lines total**

### `common/header.hbs`
- Hero banner template
- Playfair Display h2 + subtitle
- Gold border, navy gradient background
- Inline styles (~40 lines)

### `common/footer.hbs`
- Custom footer with 3 link sections + CTA
- "Back to classic view" theme switcher button
- Responsive grid layout (3 cols desktop, 1 col mobile)
- Inline styles (~80 lines)

### `common/opt-in-banner.hbs`
- Dismissible opt-in banner
- "Try it now" → enables new theme via `preview_theme_id`
- "Later" → dismisses for session (stored in localStorage)
- Slide animation, close button
- Mobile-responsive flex layout
- JavaScript event handlers for theme switching
- **~200 lines total**

---

## Opt-in Logic

### For Logged-in Users
1. Click "Try it now"
2. JavaScript detects user via `window.Discourse.User`
3. Redirect to `/?preview_theme_id={newThemeId}`
4. Discourse preview system shows the new theme
5. User can click "Save" or use "Back to classic" to revert

### For Logged-out Visitors
1. Click "Try it now"
2. Store preference in localStorage: `mrf-theme-preference`
3. Redirect to `/?preview_theme_id={newThemeId}`
4. Discourse renders new theme for this visitor
5. Preference persists on return visits (until localStorage clears)

### Dismissing Banner
1. Click "Later" or X button
2. Store `mrf-banner-dismissed: true` in localStorage
3. Banner hidden for remainder of session
4. Returns on next page visit (unless user has account and saved preference)

---

## Phase 1 → Phase 2 Transition

When adoption data shows readiness (typically 2–3 months):

1. **Set as default theme** in Admin → Customize → Themes
2. Old theme remains available as opt-out
3. Footer link "Back to classic view" becomes primary switcher
4. New members default to MRF Navy & Gold
5. Existing members keep their preference

---

## Troubleshooting

### Hero banner not showing
- Check `common/header.hbs` is in theme component
- Verify outlet is hooked correctly (should be `after_header`)
- Check browser console for JavaScript errors

### Opt-in banner buttons not working
- Ensure `opt-in-banner.hbs` is imported in theme
- Check localStorage is enabled in browser
- Verify `preview_theme_id` parameter is supported (Discourse 3.1+)

### Colors not applying
- Check color scheme is selected in Admin → Customize → Colors
- Verify SCSS compiles without errors
- Clear browser cache

### Logo not displaying
- Check SVG is uploaded to Admin → Settings → "Logo"
- Verify max-height CSS in `desktop.scss` allows display
- Test SVG dimensions (recommend 200x60px or 300x90px)

### Mobile layout broken
- Check viewport meta tag is present in Discourse
- Test in Chrome DevTools device emulation
- Verify mobile breakpoints in `mobile.scss`

---

## Next Steps (After Phase 1)

- Monitor opt-in adoption rates (target: 40%+ within 2 months)
- Gather feedback in community categories
- Phase 2: Set as default for new visitors/members
- Phase 3: Retire old design based on adoption data

---

## Files Summary

| File | Lines | Purpose |
|---|---|---|
| `theme.json` | 30 | Metadata, color scheme |
| `stylesheets/desktop.scss` | 150 | All desktop styles |
| `stylesheets/mobile.scss` | 80 | Mobile breakpoints |
| `common/header.hbs` | 40 | Hero banner |
| `common/footer.hbs` | 80 | Custom footer |
| `common/opt-in-banner.hbs` | 200 | Opt-in switcher + JS |
| **Total** | **~580** | **Full theme component** |

---

## Testing Checklist

### Visual
- [ ] Navy + gold colors render correctly
- [ ] Playfair Display headings display (not fallback)
- [ ] Inter body text displays (not fallback)
- [ ] Hero banner shows after header
- [ ] Footer displays at bottom
- [ ] Opt-in banner appears at top of page

### Interaction
- [ ] "Try it now" button switches theme
- [ ] "Later" button dismisses banner
- [ ] Close (X) button dismisses banner
- [ ] Footer theme toggle button works
- [ ] Theme preference persists on page reload
- [ ] Logged-out users can opt-in

### Responsive
- [ ] Desktop: 3-column footer, horizontal opt-in layout
- [ ] Tablet (768px): 1-column footer, stacked buttons
- [ ] Mobile (480px): Compact hero, full-width buttons
- [ ] Touch targets: Buttons 44px+ tall

### Accessibility
- [ ] Close button has `aria-label`
- [ ] Focus rings visible (navy light or gold)
- [ ] Color contrast passes WCAG AA (4.5:1 for text)
- [ ] Keyboard navigation works (tab through buttons)

---

## Deployment Completed
Once all tests pass, Phase 1 is live:
- ✅ Opt-in banner visible to all members
- ✅ Theme switcher functional
- ✅ Desktop + mobile responsive
- ✅ Ready to measure adoption
