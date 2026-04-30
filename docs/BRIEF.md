# Project Brief: Seeing in the Dark - A Quality Control Data Story

## Overview
An interactive data story that reveals how shift timing dramatically impacts defect rates in satellite component manufacturing, and explores the future of quality inspection through augmented reality assistance.

## Project Context

### Industry & User
- **Industry:** Advanced Manufacturing (Satellite Components)
- **Target Audience:** Quality Control Managers, Operations Directors, Manufacturing Engineers
- **Technical Level:** High - familiar with quality metrics, statistical analysis, manufacturing operations
- **Viewing Context:** Desktop or tablet, likely in office or conference room setting

### Personal Context
This project connects to my upcoming Apple Vision Pro engagement for satellite quality control, establishing narrative foundation and demonstrating understanding of quality inspection challenges in aerospace manufacturing.

---

## The Story

### Core Narrative
"Everyone knows night shift is harder. But the data reveals something more specific: night shift produces 3.2x more defects than day shift in satellite manufacturing. This isn't just about fatigue—it's about staffing, experience, lighting, and process. And it points to a future where augmented reality could level the playing field."

### Story Hook
> "2,847 defects. $4.2M in rework and scrap. One satellite launch delayed by 6 months. The data revealed a pattern we couldn't ignore: the shift you work determines the quality you produce. Here's what we learned—and what we're doing about it."

### What Makes This Story Work
1. **Surprising insight:** Most assume defects are random or equipment-related; data shows it's shift-dependent
2. **Clear villain:** Night shift conditions (not night shift workers)
3. **Actionable solution:** Specific interventions that work
4. **Future vision:** Hints at AR/Vision Pro without being sales-y
5. **High stakes:** Aerospace quality failures have massive consequences

---

## The 5-Act Structure

### Act 1: The Problem
**Title:** "The $4.2M Quality Problem"

**Purpose:** Establish stakes and context

**Content:**
- Hero metric: **2,847 defects detected last year**
- Financial impact: **$4.2M total cost**
  - $1.8M in rework
  - $1.2M in scrap
  - $900K in warranty claims
  - $300K in delayed launches
- Industry context: "In satellite manufacturing, a single defect can doom a $50M mission"
- Transition: "We thought defects were random. The data told a different story."

**Visual Design:**
- Full-screen hero section with dark aerospace background
- Animated counter that counts up to 2,847
- Cost breakdown appears on scroll
- Subtle satellite imagery (blurred, atmospheric)
- Color: Deep blue background (#0D1B2A) with bright cyan accents (#00D9FF)

**Interaction:**
- Scroll to reveal cost breakdown
- Hover on cost categories for details

**Data Required:**
- `qualityOverview.json` - Total defects, costs, year-over-year trends

---

### Act 2: The Surprise
**Title:** "It's Not What You Think"

**Purpose:** Reveal the core insight that drives the story

**Content:**
- **Expected:** Defects evenly distributed across shifts
- **Reality:** Massive variation by shift
  - **Day Shift (6am-2pm):** 1.2% defect rate | 512 defects | 40% of production
  - **Swing Shift (2pm-10pm):** 2.1% defect rate | 712 defects | 35% of production
  - **Night Shift (10pm-6am):** 3.8% defect rate | 1,623 defects | 25% of production
- Key stat: **"Night shift produces 57% of all defects, despite only 25% of production volume"**
- Transition: "So what's happening on night shift?"

**Visual Design:**
- Split screen: "Expected" (3 equal bars) vs "Actual" (dramatically different bars)
- Animated transition from expected to actual as user scrolls
- Color-coded by severity:
  - Day shift: Green (#06D6A0)
  - Swing shift: Amber (#FFB703)
  - Night shift: Red (#E63946)
- Large callout stat: "3.2x higher defect rate"

**Interaction:**
- Scroll triggers animation from expected to actual
- Hover on bars for exact numbers
- Click shift to highlight related data

**Data Required:**
- `defectsByShift.json` - Defect counts, rates, production volume by shift

---

### Act 3: The Pattern
**Title:** "The Root Causes"

**Purpose:** Deep dive into why night shift has higher defects

**Content - Section 3A: Defect Types**
- Breakdown by defect category:
  - **Visual defects** (scratches, dents, misalignment): 5x higher on night shift
  - **Dimensional defects** (out of tolerance): 2.8x higher on night shift
  - **Assembly defects** (missing/wrong parts): 3.1x higher on night shift
  - **Electrical defects** (wiring, connections): 2.2x higher on night shift
- Insight: "Visual inspection defects dominate—night shift inspectors are missing things day shift catches"

**Content - Section 3B: Time-Based Patterns**
- Heat map: Hour-by-hour defect rate across 7 days
- Shows clear patterns:
  - Defect rate spikes 2am-4am (fatigue peak)
  - Defect rate drops during shift changes (fresh eyes)
  - Weekend night shift even worse (skeleton crew)
- Insight: "The 2am-4am window is the danger zone: 4.8% defect rate"

**Content - Section 3C: The Real Culprits**
- **Staffing:**
  - Day shift: 8 inspectors for 4 production lines (2:1 ratio)
  - Night shift: 4 inspectors for 4 production lines (1:1 ratio)
- **Experience:**
  - Day shift: Average 15 years experience
  - Night shift: Average 3 years experience
- **Environment:**
  - Day shift: 800 lux lighting, natural light from windows
  - Night shift: 400 lux lighting, artificial only
- **Process:**
  - Day shift: Peer review on critical components
  - Night shift: Single inspector sign-off
- Insight: "Night shift isn't failing—they're set up to fail"

**Visual Design:**
- 3-column layout for the 3 subsections
- Stacked bar chart for defect types by shift
- Heat map with time (X-axis) and day of week (Y-axis)
- Comparison cards for staffing/experience/environment
- Highlight the "danger zone" (2am-4am) in red
- Icons for each factor (people, lightbulb, checklist)

**Interaction:**
- Filter defect types: Toggle between visual/dimensional/assembly/electrical
- Heat map hover: Show exact defect count for that hour
- Click on staffing/experience/environment cards to expand details

**Data Required:**
- `defectTypes.json` - Defect categories by shift
- `defectHeatmap.json` - Hour-by-hour, day-by-day defect rates
- `inspectorStats.json` - Staffing, experience, environment by shift

---

### Act 4: The Impact
**Title:** "The Ripple Effect"

**Purpose:** Show the full cost and consequences of shift-based quality issues

**Content - Section 4A: Cost Breakdown**
- Where the $4.2M goes:
  - **Rework:** $1.8M (43%) - Defects caught before shipping
  - **Scrap:** $1.2M (29%) - Defects caught too late, parts destroyed
  - **Warranty:** $900K (21%) - Defects found by customers
  - **Delays:** $300K (7%) - Schedule impact, expedited shipping
- Insight: "Night shift defects cost 2.3x more because they're caught later in the process"

**Content - Section 4B: Correlation Analysis**
- **Production speed vs. defect rate:**
  - Scatter plot shows: faster production = more defects
  - Night shift runs 15% faster (trying to compensate for lower output)
- **Inspector experience vs. defect rate:**
  - Clear inverse correlation: more experience = fewer defects
  - Each year of experience reduces defect rate by 0.12%
- **Part complexity vs. defect rate:**
  - Complex parts (solar arrays) have 3x higher defect rate on night shift
  - Simple parts (brackets) show minimal shift variation

**Content - Section 4C: Customer Impact**
- 1 satellite launch delayed by 6 months due to night shift defect
- Customer satisfaction scores:
  - Day shift production: 94/100
  - Night shift production: 78/100
- Repeat defects: Same issues appearing multiple times on night shift

**Visual Design:**
- Waterfall chart for cost breakdown (flows from total to categories)
- Scatter plots for correlations (with trend lines)
- Timeline showing delayed launch with cost impact
- Customer satisfaction gauge charts

**Interaction:**
- Hover on cost categories for breakdown
- Click scatter plot points to see specific examples
- Filter by part complexity

**Data Required:**
- `costBreakdown.json` - Detailed cost categories
- `correlations.json` - Speed, experience, complexity vs defects
- `customerImpact.json` - Satisfaction scores, delays, repeat defects

---

### Act 5: The Solution
**Title:** "The Path Forward"

**Purpose:** Show what works and hint at future innovations

**Content - Section 5A: Best Practices from Day Shift**
- What day shift does right:
  - **Adequate staffing:** 2:1 inspector-to-line ratio
  - **Experienced team:** Average 15 years, mentorship program
  - **Better lighting:** 800 lux + natural light
  - **Peer review:** Two inspectors on critical components
  - **Slower pace:** Quality over speed
- Insight: "Day shift proves it's possible—we just need to replicate their conditions"

**Content - Section 5B: Pilot Program Results**
- 6-month pilot on night shift:
  - **Added 2 inspectors:** 42% defect reduction
  - **Improved lighting to 800 lux:** 28% fewer visual defects
  - **Implemented peer review:** 35% fewer critical defects
  - **Slowed production 10%:** 31% defect reduction (net positive)
- Combined impact: **67% defect reduction on night shift**
- Insight: "The interventions work—and they pay for themselves in 4 months"

**Content - Section 5C: Future Vision (AR Hint)**
- "What if every inspector had superhuman vision?"
- Concept visualization: AR overlay showing:
  - Highlighted defect areas
  - Measurement overlays
  - Real-time guidance
  - Historical defect patterns for this part type
- Text: "What if inspectors had augmented reality assistance? AI that could flag potential defects in real-time? The experience of a 20-year veteran, available to every inspector?"
- Subtle, not branded—just suggestive of AR/Vision Pro potential
- Insight: "Technology can level the playing field between shifts"

**Content - Section 5D: ROI Calculator**
- Interactive calculator:
  - **Slider 1:** Staffing increase (0-4 inspectors) | Cost: $80K/inspector/year
  - **Slider 2:** Lighting upgrade | Cost: $50K one-time
  - **Slider 3:** Training investment | Cost: $30K/year
  - **Slider 4:** Technology adoption (AR assistance) | Cost: $200K one-time + $50K/year
- Output:
  - Projected defect reduction %
  - Annual cost savings
  - Payback period
  - 5-year ROI
- Default scenario: "Reduce night shift defects by 50% → Save $1.4M annually → Payback in 6 months"

**Visual Design:**
- Cards for best practices (icon + title + description)
- Before/after bar chart for pilot results
- Futuristic AR visualization (subtle, atmospheric)
  - Dark background with cyan/blue holographic overlays
  - Shows inspector's POV with AR assistance
  - Not branded, just conceptual
- Interactive calculator with sliders and real-time results

**Interaction:**
- Hover on best practice cards for more details
- Click pilot results to see month-by-month improvement
- AR visualization: Subtle animation (pulsing highlights, scanning effect)
- Calculator: Drag sliders to see impact on savings and ROI

**Data Required:**
- `pilotResults.json` - Before/after intervention data
- `roiCalculator.json` - Cost and savings scenarios

---

## Design System

### Color Palette

**Primary Colors:**
- Deep Blue: `#0D1B2A` (main background, aerospace feel)
- Bright Cyan: `#00D9FF` (highlights, tech accents, AR elements)
- Steel Gray: `#415A77` (secondary elements, borders)

**Shift Status Colors:**
- Day Shift Green: `#06D6A0` (success, good quality)
- Swing Shift Amber: `#FFB703` (warning, moderate issues)
- Night Shift Red: `#E63946` (error, critical issues)

**Accent Colors:**
- Bright Blue: `#1B98E0` (interactive elements, links)
- Purple: `#7209B7` (future vision, AR elements)

**Neutral Colors:**
- Background Dark: `#0D1B2A`
- Card Background: `#1B263B`
- Border: `#2D3E50`
- Text Primary: `#E0E1DD` (light gray, high contrast)
- Text Secondary: `#778DA9` (muted blue-gray)
- Text Muted: `#4A5568`

**Why These Colors:**
- Dark theme evokes precision manufacturing, aerospace, high-tech quality control
- Cyan accents pop against dark background and suggest AR/holographic tech
- Traffic light colors (green/amber/red) are universally understood for status
- Purple reserved for future vision section to differentiate from current state

---

### Typography

**Font Families:**
- **Display (Story Titles):** Orbitron Bold
  - Used for: Act titles, major section headers
  - Why: Futuristic, aerospace feel without being cheesy
  - Fallback: 'Rajdhani', 'Roboto Condensed', sans-serif
  
- **Headings:** Roboto Condensed Bold
  - Used for: Subsection titles, chart labels
  - Why: Technical, clean, excellent readability
  - Fallback: 'Arial Narrow', sans-serif
  
- **Body:** Roboto Regular
  - Used for: Paragraphs, descriptions, tooltips
  - Why: Highly readable, professional, web-optimized
  - Fallback: Arial, sans-serif
  
- **Data/Metrics:** Roboto Mono
  - Used for: Numbers, percentages, data labels
  - Why: Monospace provides precision feel, easy to scan
  - Fallback: 'Courier New', monospace

**Size Scale:**
- Display (Act Titles): 64px / 4rem
- H1 (Section Headers): 48px / 3rem
- H2 (Subsection Headers): 32px / 2rem
- H3 (Card Titles): 24px / 1.5rem
- Body Large: 20px / 1.25rem
- Body: 18px / 1.125rem
- Small: 16px / 1rem
- Caption: 14px / 0.875rem

**Line Height:**
- Display: 1.1
- Headings: 1.2
- Body: 1.6
- Data: 1.4

---

### Spacing System

**Base Unit:** 8px

**Scale:**
- xs: 8px (0.5rem)
- sm: 16px (1rem)
- md: 24px (1.5rem)
- lg: 32px (2rem)
- xl: 48px (3rem)
- 2xl: 64px (4rem)
- 3xl: 96px (6rem)

**Section Spacing:**
- Between acts: 96px (3xl)
- Between subsections: 64px (2xl)
- Between elements: 32px (lg)
- Card padding: 24px (md)
- Chart margins: 16px (sm)

---

### Component Patterns

**Story Section:**
- Full-width container
- Max-width: 1400px (centered)
- Padding: 48px horizontal, 96px vertical
- Background: Alternating (dark / slightly lighter dark)

**Metric Card:**
- Background: Card background (#1B263B)
- Border: 1px solid border color (#2D3E50)
- Border-radius: 8px
- Padding: 24px
- Shadow: 0 4px 12px rgba(0, 0, 0, 0.3)
- Hover: Lift effect (translateY: -4px, stronger shadow)

**Chart Container:**
- Background: Card background
- Border: 1px solid border color
- Border-radius: 12px
- Padding: 32px
- Title above chart (Roboto Condensed Bold, 24px)
- Legend below or to right of chart

**Interactive Filter:**
- Button group style
- Active state: Bright cyan background (#00D9FF), dark text
- Inactive state: Transparent background, light text
- Hover: Border glow effect
- Transition: 200ms ease

**Scroll Progress Indicator:**
- Fixed position, top of viewport
- Horizontal bar, 4px height
- Bright cyan color (#00D9FF)
- Animates width based on scroll position (0-100%)

**AR Visualization:**
- Dark background with subtle grid pattern
- Cyan/purple holographic overlays
- Pulsing glow effect on highlighted areas
- Scanning line animation (top to bottom, repeating)
- Semi-transparent UI elements overlaid on "part"

---

### Chart Specifications

**Global Chart Settings:**
- Background: Transparent (inherits card background)
- Grid lines: Subtle (#2D3E50), 1px, dashed
- Axis labels: Roboto Regular, 14px, text secondary color
- Data labels: Roboto Mono, 16px, text primary color
- Tooltips: Card background, border, padding 12px, shadow
- Animation: 800ms ease-out on load, 300ms on interaction

**Chart-Specific Styles:**

**Bar Charts:**
- Bar width: 40px (desktop), 24px (mobile)
- Border-radius: 4px (top corners only)
- Spacing: 16px between bars
- Colors: Shift status colors (green/amber/red)
- Hover: Brighten by 20%, lift effect

**Line Charts:**
- Line width: 3px
- Point radius: 6px
- Point hover radius: 8px
- Colors: Bright cyan (#00D9FF) for primary, bright blue (#1B98E0) for secondary
- Fill: Gradient from line color (50% opacity) to transparent

**Heat Map:**
- Cell size: 40px × 40px
- Border: 1px solid background color (creates grid)
- Color scale: Green (#06D6A0) → Amber (#FFB703) → Red (#E63946)
- Hover: Border glow, tooltip with exact value
- Labels: Days of week (Y-axis), Hours (X-axis)

**Scatter Plot:**
- Point radius: 8px
- Point opacity: 0.7
- Point hover: Opacity 1, radius 10px, border
- Trend line: Dashed, 2px, bright blue (#1B98E0)
- Colors: Shift status colors

**Waterfall Chart:**
- Bar width: 60px
- Connector lines: 2px, dashed, steel gray (#415A77)
- Positive values: Green (#06D6A0)
- Negative values: Red (#E63946)
- Total bar: Bright cyan (#00D9FF)

---

## Technical Stack

### Framework & Build Tools
- **Vue 3** with Composition API and TypeScript
- **Vite** for fast development and optimized builds
- **Vue Router** (if multi-page, likely single-page scroll story)

### Component Library
- **Vuetify 3** for base UI components
  - Cards, buttons, containers, grids
  - Not for charts (use Chart.js)
  - Custom theme with aerospace color palette

### Charts & Visualization
- **Chart.js 4** with **vue-chartjs 5**
  - Bar charts, line charts, scatter plots
- **Custom heat map component** (SVG-based)
  - Chart.js doesn't have great heat map support
  - Build custom with D3-like approach or use chart.js matrix plugin

### Animation & Scroll
- **GSAP (GreenSock)** for scroll-based animations
  - ScrollTrigger plugin for scroll-based reveals
  - Smooth counter animations
  - Chart reveal animations
- **Intersection Observer API** for triggering animations when sections enter viewport

### State Management
- **Vue Composition API** with reactive refs (no Pinia needed)
- Local JSON files for mock data
- Composables for shared logic (scroll position, animation triggers)

### Deployment
- **Vercel** for hosting
- **Password protection** enabled
- **GitHub** for version control

---

## Data Structure

### Data Files & Schemas

#### 1. `qualityOverview.json`
```json
{
  "year": 2025,
  "totalDefects": 2847,
  "totalCost": 4200000,
  "costBreakdown": {
    "rework": 1800000,
    "scrap": 1200000,
    "warranty": 900000,
    "delays": 300000
  },
  "yearOverYear": {
    "2023": 2456,
    "2024": 2698,
    "2025": 2847
  },
  "targetDefectRate": 0.5,
  "actualDefectRate": 2.1
}