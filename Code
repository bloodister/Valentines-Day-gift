<!DOCTYPE html>
<html>
<head>
    <title>情人节快乐</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: #000;
        }
        #canvas {
            position: fixed;
            top: 0;
            left: 0;
        }
        .love-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: #fff;
            font-size: 2.5em;
            text-align: center;
            text-shadow: 0 0 10px #ff0066;
            font-family: 'Microsoft Yahei', cursive;
            z-index: 100;
            animation: glow 2s ease-in-out infinite;
        }
        @keyframes glow {
            0%, 100% { opacity: 0.8; }
            50% { opacity: 1; text-shadow: 0 0 20px #ff0066; }
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <div class="love-text" id="loveText"></div>

    <script>
        // 烟花粒子类
        class Particle {
            constructor(x, y, color) {
                this.x = x;
                this.y = y;
                this.color = color;
                this.radius = 2;
                this.velocity = {
                    x: (Math.random() - 0.5) * 5,
                    y: (Math.random() - 0.5) * 5
                };
                this.alpha = 1;
            }

            draw() {
                ctx.globalAlpha = this.alpha;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
                ctx.fillStyle = this.color;
                ctx.fill();
            }

            update() {
                this.draw();
                this.velocity.x *= 0.99;
                this.velocity.y *= 0.99;
                this.x += this.velocity.x;
                this.y += this.velocity.y;
                this.alpha -= 0.005;
            }
        }

        // 烟花类
        class Firework {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = canvas.height;
                this.targetY = Math.random() * canvas.height/2;
                this.color = `hsl(${Math.random() * 360}, 50%, 50%)`;
                this.particles = [];
                this.velocity = { x: 0, y: -8 };
                this.exploded = false;
            }

            draw() {
                if (!this.exploded) {
                    ctx.globalAlpha = 1;
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, 3, 0, Math.PI * 2);
                    ctx.fillStyle = this.color;
                    ctx.fill();
                }
            }

            update() {
                this.draw();
                
                if (!this.exploded) {
                    this.y += this.velocity.y;
                    if (this.y <= this.targetY) {
                        this.explode();
                    }
                } else {
                    this.particles.forEach((particle, index) => {
                        if (particle.alpha <= 0) {
                            this.particles.splice(index, 1);
                        } else {
                            particle.update();
                        }
                    });
                }
            }

            explode() {
                this.exploded = true;
                for (let i = 0; i < 100; i++) {
                    this.particles.push(new Particle(this.x, this.y, this.color));
                }
            }
        }

        // 初始化
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        const texts = [
            "你是我的今天和所有的明天",
            "遇见你，是一切美好的开始",
            "我想把全世界的彩虹都放进你心里",
            "和你在一起的每一秒都是情人节",
            "你是我灵魂的倒影",
            "我的宇宙里为你藏了无数个温柔星球"
        ];
        
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        const fireworks = [];
        let fireworkTimer = 0;

        // 文字切换
        const loveText = document.getElementById('loveText');
        let textIndex = 0;
        setInterval(() => {
            loveText.style.opacity = 0;
            setTimeout(() => {
                textIndex = (textIndex + 1) % texts.length;
                loveText.textContent = texts[textIndex];
                loveText.style.opacity = 1;
            }, 500);
        }, 3000);

        // 动画循环
        function animate() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            fireworks.forEach((firework, index) => {
                firework.update();
                if (firework.exploded && firework.particles.length === 0) {
                    fireworks.splice(index, 1);
                }
            });

            if (fireworkTimer % 50 === 0) {
                fireworks.push(new Firework());
            }
            fireworkTimer++;

            requestAnimationFrame(animate);
        }

        // 窗口调整
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // 开始动画
        animate();
        loveText.textContent = texts[0];
    </script>
</body>
</html>
