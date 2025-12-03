# BakeLab Landing Page

## Purpose

Marketing landing page for BakeLab, an industry research lab specializing in high-quality datasets for AI/ML training. The site introduces the company's mission, services (off-the-shelf and customized datasets), and provides contact information for sales and careers.

## Project Type

Static website with two design iterations (v1 and v2), featuring pure HTML/CSS/JavaScript without build tools or frameworks.

## Technology Stack

### Core Technologies
- **HTML5** - Semantic markup
- **CSS3** - Embedded styles with custom properties, animations, responsive design
- **Vanilla JavaScript** - Interactive features, animations, mini-game

### External Dependencies
- **Google Fonts**
  - v1: Noto Serif, Cal Sans
  - v2: Baloo 2, Cormorant Garamond, Inter
- **Umami Analytics** - Privacy-focused analytics (data-website-id: 82364d02-ef99-45f6-b1f2-37c338543b86)

### Browser APIs Used
- Canvas API (v2 - game rendering)
- Web Audio API (v2 - sound effects)
- Intersection Observer API (v2 - visibility detection)
- RequestAnimationFrame (v2 - game loop)

## Project Structure

```
bakelab_page/
├── v1/                       # Version 1 - Minimalist design
│   ├── index.html           # Simple serif-based landing page
│   ├── bakelab.png          # Logo (395KB)
│   └── robots.txt           # Disallow all crawling
│
├── v2/                       # Version 2 - Interactive design
│   ├── index.html           # Animated landing with easter egg game
│   ├── BakeLab-01.png       # Primary logo (155KB)
│   ├── BakeLab-02.png       # Variant logo 2 (165KB)
│   ├── BakeLab-03.png       # Variant logo 3 (166KB)
│   ├── BakeLab-04.png       # Variant logo 4 (175KB)
│   ├── BakeLab-05.png       # Rare variant logo 5 (173KB)
│   ├── bake192.png          # Game character sprite (20KB)
│   ├── favicon.ico          # Site favicon
│   └── robots.txt           # Disallow all crawling
│
└── .gitignore               # Ignores .DS_Store files
```

## Design Versions

### V1 - Minimalist Landing Page
**Design Philosophy:** Clean, editorial, text-focused

**Key Features:**
- Centered layout with max-width constraint (900px)
- Serif typography (Noto Serif) with Cal Sans display font
- Cream background (#faf8f3) with brown accents (#8B5A3C, #6B4423)
- Minimal decoration, emphasis on content
- Fully responsive (768px, 480px breakpoints)
- Logo + text header combination
- SEO blocked (noindex, nofollow meta tags)

**Content Structure:**
- Hero with logo and title
- Mission statement
- Service description
- Contact section (sales, careers)
- Footer

### V2 - Interactive Landing Page
**Design Philosophy:** Playful, animated, gamified brand experience

**Key Features:**
- **Probabilistic Logo Loading:** Randomizes logo variant on page load
  - BakeLab-01: 90% probability
  - BakeLab-02: 3%
  - BakeLab-03: 5%
  - BakeLab-04: 1.9%
  - BakeLab-05: 0.1% (rare)

- **Animated Bake Factory:** Fixed-position SVG animation
  - Conveyor belt with moving dough/bread
  - Oven with shaking animation
  - Interactive speed control (click/spacebar)
  - Speed decay system (98% per frame)
  - Audio feedback (machine sounds tied to speed)
  - Hidden until user scrolls past hero

- **Easter Egg Game:** "BakeLab Runner" triggered by factory acceleration
  - Canvas-based infinite runner
  - Four obstacle types: rolling pin, baguette, jam jar, hole trap
  - Particle effects and parallax clouds
  - Responsive scaling for mobile
  - Web Audio API sound effects
  - Score tracking with progressive difficulty

- **Auto-Scroll Behavior:** Automatically scrolls to content after 3 seconds

- **Typography:** Mixed font strategy
  - Display: Baloo 2 (playful, rounded)
  - Serif: Cormorant Garamond (elegant body text)
  - Sans: Inter (UI elements)

**Responsive Behavior:**
- Adaptive layout at 768px breakpoint
- Dynamic canvas resizing (high-DPI support)
- Mobile-optimized game physics (0.7x scale ratio)
- Touch-enabled game controls

**Game Mechanics:**

The BakeLab Runner game features progressive difficulty with four obstacle types that unlock based on score:

1. **Rolling Pin** (Available from start)
   - Low horizontal obstacle
   - Player must jump over it
   - Always present at all score levels

2. **Hole Trap** (Unlocks at score > 5, 30% spawn chance)
   - Dark pit (#1a1a1a) below ground line
   - Size: 60px wide × 80px deep (scaled for mobile)
   - Visual: Brown edge markers and depth lines
   - Gameplay: Player must be AIRBORNE when crossing - if grounded over hole center, player falls and dies
   - Inverse mechanic to barriers: barriers require jumping, holes punish being grounded

3. **Baguette** (Unlocks at score > 10, 20% spawn chance)
   - Tall vertical obstacle
   - Requires high or early jump

4. **Jam Jar** (Unlocks at score > 20, rare spawn when random > 0.85)
   - Block-style obstacle
   - Overrides hole spawn when conditions met

**Obstacle Spawn Rate Progression:**
- Score 0-5: Rolling pin only
- Score 6-10: Rolling pin + Hole (30%)
- Score 11-20: Rolling pin + Hole (30%) + Baguette (20%)
- Score 21+: All obstacles + Jam jar (rare, >0.85)

## Key Files and Their Purposes

### /v1/index.html
Simple, professional landing page implementation. Self-contained with embedded CSS. Uses semantic HTML with accessible structure.

### /v2/index.html
Advanced interactive experience with multiple JavaScript subsystems:
1. **Logo randomizer** (lines 358-385)
2. **Auto-scroll** (lines 387-393)
3. **Factory animation controller** (lines 395-545)
4. **Game engine** (lines 960-1427)
   - Obstacle spawn logic with hole trap (lines 1210-1232)
   - Hole collision detection (lines 1295-1305)

**Code Organization:**
- Hero section with dynamic logo
- Content section with gradient background
- Fixed factory SVG with CSS animations
- Game overlay (canvas + UI)
- Three IIFEs for feature encapsulation

### robots.txt (both versions)
Blocks all search engine crawling. Indicates this is a private or staging site not intended for public indexing.

## Build and Deployment

### Local Development
No build process required. Simply open HTML files in a browser:

```bash
# Serve v1
open v1/index.html
# or use a local server
python3 -m http.server 8000
# Navigate to http://localhost:8000/v1/

# Serve v2
open v2/index.html
# or http://localhost:8000/v2/
```

### Production Deployment
1. Choose version (v1 or v2)
2. Deploy entire folder to web server
3. Ensure MIME types are correctly configured:
   - `.png` → `image/png`
   - `.ico` → `image/x-icon`
   - `.html` → `text/html`

### Performance Considerations
- All CSS/JS is inlined (no external requests except fonts/analytics)
- Images are not optimized (consider compression for production)
- No caching headers configured
- Umami analytics script is async/deferred

## Design Patterns and Decisions

### 1. Version-Based Structure
**Decision:** Maintain two separate implementations rather than single source with variants

**Rationale:**
- Clean separation of design philosophies
- Easy A/B testing by deploying different versions
- No complex branching logic in code

### 2. Inline Styles and Scripts
**Decision:** Embed all CSS and JavaScript directly in HTML

**Rationale:**
- Zero HTTP overhead for styles/scripts
- Single-file portability
- Faster initial render (no blocking external resources)
- Trade-off: Larger HTML file, no browser caching

### 3. No Framework Dependency
**Decision:** Pure vanilla JavaScript for all interactions

**Rationale:**
- Lightweight (v1: ~8KB, v2: ~48KB HTML)
- No build step complexity
- Full control over animations and game loop
- Fast load time on slow connections

### 4. Probabilistic Content
**Decision:** Randomize logo selection in v2

**Rationale:**
- Creates surprise/delight for repeat visitors
- Reinforces brand playfulness
- Rare variants encourage exploration
- Console logging for developer transparency

### 5. Progressive Enhancement
**Decision:** Game features require user interaction to activate audio

**Rationale:**
- Respects browser autoplay policies
- Better UX (no unexpected sounds)
- Audio initializes on first user gesture
- Degrades gracefully if audio fails

### 6. SEO Blocking
**Decision:** Both versions block search engine indexing

**Rationale:**
- Indicates staging/preview environment
- Prevents duplicate content issues if production site exists elsewhere
- May need to be updated for public launch

### 7. Animation Performance
**Decision:** Use CSS animations for factory, requestAnimationFrame for game

**Rationale:**
- CSS animations are GPU-accelerated and declarative
- Game loop needs precise timing control for physics
- Hybrid approach balances performance and flexibility

### 8. Responsive Strategy
**Decision:** Mobile-first with specific breakpoints at 768px and 480px (v1)

**Rationale:**
- Targets common device sizes
- Scales typography and spacing proportionally
- v2 uses JavaScript-based canvas scaling for game

## Development Guidelines

### Adding New Content
1. Edit HTML directly (no templating system)
2. Maintain semantic structure (`<section>`, `<header>`, etc.)
3. Keep inline styles organized by section
4. Test responsive breakpoints after changes

### Modifying Animations
- **Factory:** Edit SVG keyframes in `<style>` block (lines 577-677 in v2)
- **Game Physics:** Adjust physics constants in game initialization (lines 1046-1057)
- **Obstacle Spawn Rates:** Modify score thresholds and probability values (lines 1211-1216)
- **Speed variable:** `--speed-factor` CSS custom property

### Modifying Game Obstacles
To adjust obstacle behavior:
- **Hole trap dimensions:** Change `w` and `h` values for `type === 'hole'` (line 1222)
- **Hole spawn probability:** Modify `typeRand > 0.7` condition (line 1214)
- **Hole collision detection:** Adjust hitbox inset at `10 * scaleRatio` (lines 1297-1298)
- **Obstacle unlock thresholds:** Change score comparisons (lines 1214-1216)

### Analytics
Current Umami instance ID: `82364d02-ef99-45f6-b1f2-37c338543b86`

To change: Update `data-website-id` attribute in both HTML files.

### Brand Colors
**V1:**
- Background: `#faf8f3` (cream)
- Primary text: `#1a1a1a` (near-black)
- Brand brown: `#8B5A3C`, `#6B4423`

**V2:**
- Background: `#faf8f3` (cream)
- Brand color: `#593513` (dark brown) - `rgb(89, 53, 19)`
- Accent: `#D4AF37` (gold)
- CSS variables defined in `:root` (lines 16-24)

## Known Limitations

1. **No Image Optimization:** PNGs are uncompressed, totaling ~1.3MB for v2
2. **No Lazy Loading:** All images load immediately
3. **Single Language:** English only, no i18n support
4. **No Accessibility Audit:** ARIA labels and keyboard navigation may be incomplete
5. **Game Performance:** May lag on low-end mobile devices
6. **No Error Handling:** Game assumes all assets load successfully
7. **Analytics Privacy:** Third-party Umami instance (cloud.umami.is)

## Contact Integration

**Sales Inquiries:** sales@bakelab.ai
**Career Inquiries:** careers@bakelab.ai

Email links use `mailto:` protocol. No form validation or backend integration.

## Future Enhancements (Potential)

- Image optimization (WebP format, compression)
- Service worker for offline support
- Preloading critical fonts
- ARIA labels for improved accessibility
- Dark mode toggle
- Internationalization
- Contact form with backend
- Enhanced game features (leaderboards, sound toggle)
- Remove analytics or self-host for privacy
- Update robots.txt for public launch
