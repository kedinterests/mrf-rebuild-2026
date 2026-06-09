# MineralRightsForum Redesign 2026

A comprehensive Discourse theme component implementing the visual rebrand of MineralRightsForum.com. Navy + gold palette, Playfair Display typography, hero banner, and opt-in switcher for a phased rollout.

## Overview

This theme component brings the existing directory site's design language (navy, gold, Playfair Display, Inter) to the Discourse forum, establishing visual consistency across the MRF ecosystem.

**Status:** Phase 1 development (opt-in banner with theme switcher)

## Design System

- **Colors**: Navy (#0a192f), Gold (#c5a059), Off-white (#f8f6f1)
- **Typography**: Playfair Display 700 (headings) + Inter (body/UI)
- **Logo**: Strata concept (4 horizontal gold bars)
- **Components**: Hero banner, opt-in switcher, custom footer

See `docs/DESIGN_TOKENS.md` for complete color, typography, and spacing specifications.

## Repository Structure

```
mrf-rebuild-2026/
├── about.json                      # Discourse component metadata (required)
├── settings.json                   # Color definitions for admin settings
├── stylesheets/
│   ├── desktop.scss               # Desktop styles (colors, typography, components)
│   └── mobile.scss                # Mobile-specific adjustments
├── common/
│   ├── opt-in-banner.hbs          # Phase 1 opt-in switcher banner
│   ├── header.hbs                 # Hero banner (Playfair Display heading + subtitle)
│   └── footer.hbs                 # Custom footer with theme switcher
├── assets/
│   └── images/
│       └── mrf-strata-logo.svg   # Strata logo (4 gold bars) — add after export
└── docs/
    ├── DESIGN_TOKENS.md           # Design system reference (colors, typography, spacing)
    ├── mrf-redesign-proposal.md   # Original proposal (Phase 1–3 transition plan)
    └── IMPLEMENTATION.md          # Step-by-step Discourse deployment guide
```

## Implementation Phases

### Phase 1: Opt-in (Months 1–3)
- Old design stays default for all members
- Dismissible opt-in banner: "The new MRF is here — try it now"
- Members who opt in are switched to new theme; preference saved
- **Fully reversible** — removing banner ends Phase 1 with zero forced migrations

### Phase 2: Soft Switch (Months 4–6)
- New design becomes default for visitors and new sign-ups
- Members using old design keep it automatically
- "Back to classic view" link in footer for opt-out

### Phase 3: Migration Complete (Month 7+)
- Old design retired when adoption data supports it
- Kenny controls timing

## Development

To test this theme component:

1. Create a new Discourse instance or use staging
2. Navigate to Admin → Customize → Themes
3. Upload this theme component
4. Set "MRF Navy & Gold" color scheme
5. Test hero banner, footer, and topic list styling across desktop and mobile

## Key Files

- **Component Metadata**: `about.json` (required for Discourse import)
- **Color Definitions**: `settings.json` (accessible in Discourse admin)
- **Desktop Styles**: `stylesheets/desktop.scss` (~150 lines)
- **Mobile Styles**: `stylesheets/mobile.scss` (~80 lines)
- **Opt-in Banner**: `common/opt-in-banner.hbs` with localStorage + preview_theme_id
- **Hero Banner**: `common/header.hbs` with Playfair Display heading
- **Footer**: `common/footer.hbs` with theme switcher
- **Design Reference**: `docs/DESIGN_TOKENS.md`

## Next Steps

- [ ] Create opt-in banner component with localStorage + theme preview
- [ ] Implement Strata logo SVG export and upload to `assets/images/`
- [ ] Test theme in Discourse staging environment
- [ ] Verify mobile responsiveness
- [ ] Deploy Phase 1 (opt-in banner live)

## Related

- **Proposal**: See `docs/mrf-redesign-proposal.md` for full context, logo concepts, and transition rationale
- **Live Mockups**: `/mrf-redesign-mockup` at directory.mineralrightsforum.com
- **Design Tokens**: Canonical specs in `docs/DESIGN_TOKENS.md`
