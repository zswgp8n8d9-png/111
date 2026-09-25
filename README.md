# 111
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🌕 中秋祝福 | 计算机服务队</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    background: #0a0a1a;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-family: 'Courier New', 'Microsoft YaHei', monospace;
    overflow: hidden;
    color: #00f0ff;
  }
  /* 粒子背景画布 */
  #particles {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    z-index: 0;
  }
  .container {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 40px;
    border: 1px solid rgba(0, 240, 255, 0.3);
    border-radius: 12px;
    background: rgba(10, 10, 30, 0.7);
    box-shadow: 0 0 40px rgba(0, 240, 255, 0.15),
                inset 0 0 20px rgba(0, 240, 255, 0.05);
    backdrop-filter: blur(8px);
    max-width: 600px;
    width: 90%;
  }
  .moon {
    width: 100px; height: 100px;
    border-radius: 50%;
    background: radial-gradient(circle at 35% 35%, #fffde8, #f0c040 60%, #c08020);
    margin: 0 auto 30px;
    box-shadow: 0 0 60px #f0c040, 0 0 120px rgba(240, 192, 64, 0.4);
    animation: pulse 3s ease-in-out infinite;
  }
  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 60px #f0c040, 0 0 120px rgba(240,192,64,0.4); transform: scale(1); }
    50% { box-shadow: 0 0 80px #f0c040, 0 0 160px rgba(240,192,64,0.6); transform: scale(1.05); }
  }
  .title {
    font-size: 28px;
    font-weight: bold;
    margin-bottom: 10px;
    background: linear-gradient(90deg, #00f0ff, #b400ff, #ff0066, #00f0ff);
    background-size: 300% 100%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: gradientMove 4s linear infinite;
  }
  @keyframes gradientMove {
    0% { background-position: 0% 50%; }
    100% { background-position: 300% 50%; }
  }
  .subtitle {
    font-size: 14px;
    color: rgba(0, 240, 255, 0.6);
    margin-bottom: 30px;
    letter-spacing: 4px;
  }
  .message {
    font-size: 20px;
    line-height: 2;
    color: #e0e0ff;
    text-shadow: 0 0 10px rgba(0, 240, 255, 0.5);
  }
  .message .highlight {
    color: #00f0ff;
    font-weight: bold;
  }
  .footer {
    margin-top: 30px;
    font-size: 13px;
    color: rgba(180, 0, 255, 0.7);
    letter-spacing: 2px;
  }
  .code-line {
    font-size: 12px;
    color: rgba(0, 240, 255, 0.3);
    margin-top: 20px;
  }
</style>
</head>
<body>
<canvas id="particles"></canvas>
<div class="container">
  <div class="moon"></div>
  <div class="title">MID-AUTUMN BLESSING</div>
  <div class="subtitle">&lt; 计算机服务队 · 中秋特辑 /&gt;</div>
  <div class="message">
    祝<span class="highlight">没有回家的人们</span> 
    天天开心，万事顺意 🌕
  </div>
  <div class="footer">—— 来自计算机服务队的温暖 ——</div>
  <div class="code-line">console.log("Happy Mid-Autumn Festival!");</div>
</div>

<script>
  // 粒子动画
  const canvas = document.getElementById('particles');
  const ctx = canvas.getContext('2d');
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const particles = [];
  const count = 80;

  class Particle {
    constructor() {
      this.reset();
    }
    reset() {
      this.x = Math.random() * canvas.width;
      this.y = Math.random() * canvas.height;
      this.size = Math.random() * 2 + 0.5;
      this.speedX = (Math.random() - 0.5) * 0.5;
      this.speedY = (Math.random() - 0.5) * 0.5;
      this.alpha = Math.random() * 0.5 + 0.2;
      this.color = Math.random() > 0.5 ? '0, 240, 255' : '180, 0, 255';
    }
    update() {
      this.x += this.speedX;
      this.y += this.speedY;
      if (this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) {
        this.reset();
      }
    }
    draw() {
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
      ctx.fillStyle = `rgba(${this.color}, ${this.alpha})`;
      ctx.fill();
    }
  }

  for (let i = 0; i < count; i++) {
    particles.push(new Particle());
  }

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles.forEach(p => {
      p.update();
      p.draw();
    });
    // 连线效果
    for (let i = 0; i < particles.length; i++) {
      for (let j = i + 1; j < particles.length; j++) {
        const dx = particles[i].x - particles[j].x;
        const dy = particles[i].y - particles[j].y;
        const dist = Math.sqrt(dx * dx + dy * dy);
        if (dist < 120) {
          ctx.beginPath();
          ctx.moveTo(particles[i].x, particles[i].y);
          ctx.lineTo(particles[j].x, particles[j].y);
          ctx.strokeStyle = `rgba(0, 240, 255, ${0.08 * (1 - dist / 120)})`;
          ctx.stroke();
        }
      }
    }
    requestAnimationFrame(animate);
  }
  animate();

  window.addEventListener('resize', () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  });
</script>
</body>
</html>
