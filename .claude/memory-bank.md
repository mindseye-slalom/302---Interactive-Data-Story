# Memory Bank: Key Decisions & Learnings

## Phase 1: Setup
- ✓ Created BRIEF.md with full 5-act narrative and design system
- ✓ Generated 9 mock data JSON files
- ✓ Set up Git repo and pushed to GitHub
- ✓ Fixed "src refspec main does not match any" by creating initial commit

## Phase 1-2 Transition: Scaffolding
- Vite create-vite interactive prompt blocks on non-empty directory
- Solution: Manually created Vue 3 structure instead of scaffolder
- This was faster and gave better control over folder layout

## Design Decisions
1. **Dark theme**: Aerospace/manufacturing aesthetic, not generic
2. **Cyan accent color**: Suggests AR/holographic tech (subtle Vision Pro hint)
3. **Traffic light colors**: Universal understanding of status (green/amber/red for shifts)
4. **GSAP for animations**: ScrollTrigger plugin perfect for scroll-based reveals
5. **Chart.js over D3**: Simpler for this project, built-in Vue integration
6. **Vue Composition API**: Modern, no Pinia needed for this scope

## Component Architecture
- Keep components focused and single-purpose
- Use composables for shared scroll/animation logic
- Props for data, emits for interactions
- Global CSS variables for theming

## Data Strategy
- Mock JSON files in `/src/data/` — easy to swap for real data later
- Keep data structure flat (no deep nesting)
- Number field names for easy parsing

## Accessibility Notes
- Focus on keyboard nav first, styling second
- Use semantic HTML (header, main, section, article)
- ARIA labels for charts and interactive elements
- Reduced-motion support at CSS level

## Testing Strategy
1. Narrative flow test (user can follow story)
2. Data credibility test (numbers feel realistic)
3. Interaction test (all features work)
4. Visual design test (matches brief aesthetic)
5. Performance test (<3s load, 60fps)

## Known Issues/Blockers
- None currently

## Next Session Context
- Continue from Phase 2: Build base story structure
- Create StorySection wrapper component
- Implement scroll detection for animation triggers
- Build Act 1 & Act 2 in Phase 3
