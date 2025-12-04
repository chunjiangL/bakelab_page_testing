# BakeLab Landing Page

## Purpose

Static landing page for BakeLab, a data lab company specializing in high-quality datasets for AI/ML training. The site features a hidden interactive endless runner game triggered by user interaction with an animated bake factory.

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
│   ├── BakeLab-01.png       # Primary logo - 90% probability (152KB)
│   ├── BakeLab-02.png       # Uncommon logo - 3% probability (161KB)
│   ├── BakeLab-03.png       # Uncommon logo - 5% probability (162KB)
│   ├── BakeLab-04.png       # Rare logo - 1.9% probability (171KB)
│   ├── BakeLab-05.png       # Very rare logo - 0.1% probability (169KB)
│   ├── bake192.png          # Game player sprite - bread character (20KB)
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
  - Three obstacle types: rolling pin, baguette, jam trap (plus sudden jam trap)
  - Player character: Bread sprite (bake192.png)
  - Jam trap mechanic: Player falls into jar and gets stuck
  - Particle effects and parallax clouds
  - Responsive scaling for mobile
  - Web Audio API sound effects
  - Score tracking with progressive difficulty
  - Score-based bonus logos on game over (thresholds: 5, 10, 20, 50)

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

The BakeLab Runner game features progressive difficulty with three regular obstacle types that unlock based on score, plus a special sudden jam trap mechanic:

1. **Rolling Pin** (Available from start)
   - Low horizontal obstacle (40x15px)
   - Player must jump over it
   - Always present at all score levels
   - Basic jump mechanic

2. **Baguette** (Unlocks at score > 10, spawns when 0.5 < random <= 0.7)
   - Tall vertical obstacle (20x70px)
   - Requires high or early jump
   - 20% spawn probability when unlocked

3. **Jam Trap** (Unlocks at score > 5, spawns when random > 0.7)
   - Large jar obstacle (60x60px) embedded in ground
   - Player falls into jar and gets stuck in jam
   - ~30% spawn probability when unlocked
   - Special physics: Player falls into jar center and becomes stuck

4. **Sudden Jam Trap** (Special mechanic after score > 10)
   - Not part of regular spawn cycle
   - Appears close to player position
   - Adds surprise difficulty element
   - Same jam trap physics as regular jam trap

**Player Jar Physics Properties:**
- `fallingIntoJar`: Boolean tracking if player is falling into a jar
- `jarRef`: Reference to the jar obstacle player is interacting with
- `jarBottom`: Y position of bottom inside the jar (jar.y + 20px)
- `stuckInJar`: Boolean indicating player is stuck in jam (triggers game over)

**Obstacle Spawn Rate Progression:**
- Score 0-5: Rolling pin only
- Score 6-10: Rolling pin + Jam trap (30%)
- Score 11+: Rolling pin + Jam trap (30%) + Baguette (20%) + Sudden jam trap (special)

## Key Files and Their Purposes

### /v1/index.html
Simple, professional landing page implementation. Self-contained with embedded CSS. Uses semantic HTML with accessible structure.

### /v2/index.html
Advanced interactive experience with multiple JavaScript subsystems:
1. **Logo randomizer** - Probabilistic logo selection on page load
2. **Auto-scroll** - Automatically scrolls to content after 3 seconds
3. **Factory animation controller** - Interactive bake factory with speed mechanics
4. **Game engine** - BakeLab Runner endless runner game
   - Player physics with jam trap properties (fallingIntoJar, jarRef, jarBottom, stuckInJar)
   - Obstacle spawn logic with three types (rolling pin, baguette, jam trap)
   - Sudden jam trap mechanic (triggers after score > 10)
   - Jam trap collision detection and falling physics
   - Score-based bonus logo rewards

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
Designed to work as GitHub Pages static site:
1. Choose version (v1 or v2)
2. Deploy entire folder to GitHub Pages or any static web server
3. Ensure MIME types are correctly configured:
   - `.png` → `image/png`
   - `.ico` → `image/x-icon`
   - `.html` → `text/html`
4. For GitHub Pages: Push to repository and enable Pages in settings

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
- **Rolling pin dimensions:** 40x15px (basic obstacle)
- **Baguette dimensions:** 20x70px (tall obstacle)
- **Jam trap dimensions:** 60x60px (jar obstacle)
- **Jam trap spawn probability:** Modify `typeRand > 0.7` condition (spawns at score > 5)
- **Baguette spawn probability:** Modify `0.5 < typeRand <= 0.7` condition (spawns at score > 10)
- **Sudden jam trap:** Triggers after score > 10, appears close to player
- **Jam trap physics:** Player falls to `jar.y + 20px` and becomes stuck
- **Obstacle unlock thresholds:** Change score comparisons (score > 5 for jam trap, score > 10 for baguette)

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
