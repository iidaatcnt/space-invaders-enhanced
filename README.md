# Space Invaders Enhanced

A modern take on the classic Space Invaders arcade game, built with HTML5 Canvas and vanilla JavaScript.

## Features

- Classic Space Invaders gameplay
- Responsive design with high-DPI support
- Special attack system (Shift key - once per game)
- UFO bonus targets
- Progressive difficulty levels
- High score tracking
- Sound effects using Web Audio API

## Controls

- **Arrow Keys / A,D**: Move left/right
- **Space**: Fire
- **Shift**: Special attack (7-shot spread, once per game)
- **P**: Pause/Resume
- **R**: Restart game

## Development

```bash
# Install dependencies
npm install

# Run locally
npm run dev
```

Open http://localhost:3000 in your browser.

## Deployment

This project is configured for easy deployment on Vercel:

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel
```

## Game Mechanics

- **Scoring**: 
  - Bottom row invaders: 10 points
  - Middle rows: 20 points  
  - Top rows: 30 points
  - UFO: 50/100/150/300 points (random)

- **Lives**: 3 lives per game
- **Shields**: 3 shields with 2 hit points each cell
- **Difficulty**: Speed increases with each level

## Browser Compatibility

Works on all modern browsers that support:
- HTML5 Canvas
- Web Audio API
- ES6 JavaScript

## License

MIT