# Space Invaders Enhanced - Developer Specification

## Architecture Overview

This document provides a comprehensive technical specification for the Space Invaders Enhanced game, designed to help developers understand the codebase structure, game mechanics, and implementation details.

## File Structure

```
space-invaders-enhanced/
├── index.html          # Main game file (single-file architecture)
├── package.json        # NPM configuration for deployment
├── vercel.json         # Vercel deployment configuration
├── README.md           # User documentation
├── SPEC.md            # This developer specification
└── .gitignore         # Git ignore configuration
```

## Core Game Classes

### 1. Player Class
**Location**: `index.html:~200-300`

```javascript
class Player {
  constructor(x, y, width, height)
  update()
  draw()
  fire()
  specialAttack()
  applyPowerUp(type)
  takeDamage()
}
```

**Key Features**:
- Movement with keyboard/touch controls
- Regular and special attack systems
- Power-up management with timers
- Invulnerability frames after damage
- Mobile touch control integration

### 2. Invader Class
**Location**: `index.html:~400-500`

```javascript
class Invader {
  constructor(x, y, type)
  update()
  draw()
  fire()
}
```

**Invader Types**:
- `normal`: Standard movement pattern
- `zigzag`: Alternating horizontal movement
- `fast`: Increased movement speed

### 3. Boss Class
**Location**: `index.html:~600-700`

```javascript
class Boss {
  constructor(x, y)
  update()
  draw()
  fire()
  takeDamage(damage)
}
```

**Boss Mechanics**:
- 3-phase combat system (100 HP each phase)
- Phase-specific attack patterns
- Spawns every 5 levels
- Drops guaranteed power-up on defeat

### 4. PowerUp Class
**Location**: `index.html:~800-900`

```javascript
class PowerUp {
  constructor(x, y, type)
  update()
  draw()
}
```

**Power-Up Types**:
- `rapid`: 3x fire rate for 10 seconds
- `multi`: Triple-shot for 15 seconds  
- `shield`: Repairs all shields instantly

### 5. Particle Class
**Location**: `index.html:~1000-1100`

```javascript
class Particle {
  constructor(x, y, vx, vy, life, color)
  update()
  draw()
}
```

**Particle System**:
- Explosion effects on enemy destruction
- Configurable lifetime and physics
- Color-coded by source (enemy type, power-ups)

### 6. Shield Class
**Location**: `index.html:~1200-1300`

```javascript
class Shield {
  constructor(x, y)
  takeDamage(x, y)
  draw()
  getCollisionPoints()
}
```

**Shield Mechanics**:
- Inverted U-shape design (7x5 grid)
- Cellular damage system
- 2 HP per cell with visual degradation
- Realistic collision detection

### 7. Achievement Class
**Location**: `index.html:~1400-1500`

```javascript
class Achievement {
  constructor(id, name, description, condition)
  check(gameState)
  unlock()
}
```

**Achievement System**:
- Persistent localStorage tracking
- 10+ achievements with varied conditions
- Visual notification system
- Progress tracking for incremental achievements

## Game Systems

### Audio System
**Location**: `index.html:~1600-1800`

- **Web Audio API** integration
- **Background Music**: Stage-based music switching
- **Sound Effects**: Player actions, enemy destruction, power-ups
- **UFO Tremolo**: Dynamic frequency modulation
- **State Management**: Proper audio cleanup on pause/resume

### Mobile Controls
**Location**: `index.html:~1900-2000`

```javascript
// Touch event handlers
canvas.addEventListener('touchstart', handleTouchStart)
canvas.addEventListener('touchmove', handleTouchMove)
canvas.addEventListener('touchend', handleTouchEnd)
```

**Touch Zones**:
- Left 1/3: Move left
- Right 1/3: Move right
- Center 1/3: Fire
- Two-finger tap: Special attack

### Combo System
**Location**: `index.html:~2100-2200`

- **Combo Multiplier**: 1.2x, 1.5x, 2.0x at 5/10/20 consecutive hits
- **Combo Reset**: 3-second timer without hits
- **Visual Feedback**: Dynamic combo counter display

### Collision Detection
**Location**: `index.html:~2300-2500`

```javascript
function checkCollision(rect1, rect2)
function pointInRect(px, py, rect)
function checkShieldCollision(bullet, shield)
```

**Collision Types**:
- Rectangle-based (bullets, entities)
- Point-based (shield cellular damage)
- Custom shield collision with damage radius

## Game Configuration

### Difficulty Scaling
```javascript
const DIFFICULTY_CONFIG = {
  speedIncrease: 0.02,      // Per level speed multiplier
  fireRateIncrease: 0.01,   // Enemy fire rate increase
  bossLevels: [5, 10, 15],  // Boss spawn levels
  maxEnemies: 35            // Reduced for casual play
}
```

### Balance Parameters
```javascript
const BALANCE_CONFIG = {
  playerLives: 5,           // Increased for casual play
  powerUpChance: 0.3,       // 30% drop rate
  shieldHitPoints: 2,       // Per cell
  invulnerabilityTime: 2000 // Player iframe duration (ms)
}
```

### Screen Adaptation
```javascript
const SCREEN_CONFIG = {
  minWidth: 800,
  minHeight: 600,
  aspectRatio: 4/3,
  dpiScaling: window.devicePixelRatio || 1
}
```

## Development Guidelines

### Code Style
- **ES6+ JavaScript**: Use modern syntax (classes, arrow functions, const/let)
- **Single File Architecture**: All code in `index.html` for simplicity
- **Modular Design**: Clear class separation with defined responsibilities
- **Comment Standards**: Document complex algorithms and game mechanics

### Performance Considerations
- **Particle Pooling**: Reuse particle objects to reduce GC pressure
- **Canvas Optimization**: Use `requestAnimationFrame` for smooth rendering
- **Audio Management**: Proper cleanup of audio contexts and nodes
- **Mobile Optimization**: Touch event throttling and responsive scaling

### Testing Approach
- **Manual Testing**: Cross-browser compatibility verification
- **Mobile Testing**: Touch controls on various screen sizes
- **Performance Testing**: Frame rate monitoring on lower-end devices
- **Audio Testing**: Web Audio API compatibility across browsers

### Deployment Pipeline
1. **Development**: `npm run dev` for local testing
2. **Build**: Static files (no build process required)
3. **Deploy**: `vercel` command for automatic deployment
4. **Monitoring**: Vercel analytics and error tracking

## Game State Management

### Core Game Loop
```javascript
function gameLoop() {
  update()    // Entity updates and physics
  draw()      // Rendering all game objects  
  checkCollisions() // Collision detection
  updateUI()  // HUD and achievement notifications
  requestAnimationFrame(gameLoop)
}
```

### State Transitions
- **MENU**: Title screen and controls
- **PLAYING**: Active gameplay
- **PAUSED**: Game suspended with overlay
- **GAME_OVER**: Score display and restart option
- **BOSS_FIGHT**: Special boss encounter mode

### Save System
```javascript
// localStorage persistence
achievements: JSON object with unlock status
highScore: Integer value
gameSettings: Audio/control preferences
```

## Extension Points

### Adding New Enemy Types
1. Extend `Invader` class with new type parameter
2. Implement custom movement pattern in `update()`
3. Add type-specific rendering in `draw()`
4. Update spawn logic in level generation

### Adding New Power-Ups
1. Add new type to `PowerUp` class constructor
2. Implement effect in `Player.applyPowerUp()`
3. Add visual representation and pickup sound
4. Configure drop rates and durations

### Adding New Achievement Types
1. Define achievement in `achievements` array
2. Implement condition check in `Achievement.check()`
3. Add unlock notification in UI system
4. Update persistent storage handling

## Browser Compatibility

### Minimum Requirements
- **HTML5 Canvas**: Full 2D context support
- **Web Audio API**: For sound effects and music
- **ES6 JavaScript**: Class syntax and modern features
- **localStorage**: For save system persistence
- **Touch Events**: For mobile compatibility

### Tested Browsers
- Chrome 90+ ✓
- Firefox 88+ ✓  
- Safari 14+ ✓
- Edge 90+ ✓
- Mobile Safari ✓
- Chrome Android ✓

## Known Issues & Limitations

### Performance
- Particle system can impact frame rate on older devices
- Audio context creation requires user interaction
- Canvas scaling may affect touch precision on some devices

### Browser Specific
- Safari requires touch event `preventDefault()` for proper control
- Firefox Web Audio API has slight latency differences
- Mobile Chrome may throttle `requestAnimationFrame` in background

### Future Improvements
- WebGL rendering for better performance
- Service Worker for offline play
- Multiplayer support via WebRTC
- Level editor for custom stages

---

**Last Updated**: 2025-08-27
**Version**: 1.0.0
**Maintainer**: iidaatcnt