# Space Invaders Enhanced

A modern take on the classic Space Invaders arcade game, built with HTML5 Canvas and vanilla JavaScript.

## クレジット / Credits

このプログラムは、**Nao@あなたの夢を叶えるFP**さんが作成したオリジナルのインベーダーゲームをベースに改良・拡張したものです。

素晴らしい基盤となるゲームを作成していただいたNaoさんに心より感謝申し上げます。オリジナルの完成度の高いコードとゲームデザインがあったからこそ、これらの拡張機能を追加することができました。

### 開発経緯

Naoさんが作成されたHTML5 Canvasベースのインベーダーゲームに以下の機能を追加しました：
- パーティクル爆発エフェクト
- パワーアップシステム（3種類）
- コンボシステム
- モバイル対応
- Vercelデプロイ設定

## フィードバック / Feedback

このゲームに関するご意見、ご要望、不具合報告などは、改良版の開発者である私（iidaatcnt）までお願いいたします。オリジナル作者のNaoさんではなく、私にご連絡ください。

- GitHub Issues: https://github.com/iidaatcnt/space-invaders-enhanced/issues
- 改良版開発者: iidaatcnt

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

## Recent Updates

- 🎮 Enhanced gameplay with boss battles every 5 levels
- 💥 Particle explosion effects and power-up systems  
- 📱 Mobile-friendly touch controls
- 🏆 Achievement system with persistent tracking
- 🎵 Improved audio effects and background music
- 🛡️ Redesigned shield system with realistic physics

## License

MIT