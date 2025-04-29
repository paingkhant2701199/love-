‎<!DOCTYPE html>
‎<html>
‎<head>
‎    <title>ရွှေစင်ဦးနဲ့ပိုင်ခန့်လင်းအတွက် Special Love</title>
‎    <meta charset="UTF-8">
‎    <style>
‎        @import url('https://fonts.googleapis.com/css2?family=Padauk&display=swap');
‎        
‎        body {
‎            margin: 0;
‎            height: 100vh;
‎            display: flex;
‎            justify-content: center;
‎            align-items: center;
‎            background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
‎            overflow: hidden;
‎            font-family: 'Padauk', sans-serif;
‎            cursor: pointer;
‎            user-select: none;
‎        }
‎        
‎        .message-box {
‎            position: absolute;
‎            text-align: center;
‎            color: #fff;
‎            z-index: 100;
‎            background: rgba(231, 84, 128, 0.8);
‎            padding: 20px;
‎            border-radius: 15px;
‎            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
‎            max-width: 80%;
‎            animation: floatUp 8s ease-in-out infinite;
‎        }
‎        
‎        .message {
‎            font-size: 2rem;
‎            font-weight: bold;
‎            margin-bottom: 10px;
‎            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
‎        }
‎        
‎        .sub-message {
‎            font-size: 1.2rem;
‎            opacity: 0.9;
‎        }
‎        
‎        .heart {
‎            position: absolute;
‎            pointer-events: none;
‎            animation: float 4s ease-in-out infinite;
‎            opacity: 0;
‎            filter: drop-shadow(0 0 5px rgba(255,255,255,0.7));
‎        }
‎        
‎        @keyframes float {
‎            0% {
‎                transform: translate(-50%, -50%) scale(0.3) rotate(0deg);
‎                opacity: 0;
‎            }
‎            20% {
‎                opacity: 1;
‎            }
‎            80% {
‎                opacity: 1;
‎            }
‎            100% {
‎                transform: translate(-50%, -180%) scale(1) rotate(360deg);
‎                opacity: 0;
‎            }
‎        }
‎        
‎        @keyframes floatUp {
‎            0%, 100% {
‎                transform: translateY(0);
‎            }
‎            50% {
‎                transform: translateY(-20px);
‎            }
‎        }
‎        
‎        .firework {
‎            position: absolute;
‎            width: 5px;
‎            height: 5px;
‎            border-radius: 50%;
‎            box-shadow: 0 0 10px 5px rgba(255,255,255,0.8);
‎            animation: explode 1s ease-out forwards;
‎            opacity: 0;
‎        }
‎        
‎        @keyframes explode {
‎            0% {
‎                transform: scale(0.1);
‎                opacity: 0;
‎            }
‎            50% {
‎                opacity: 1;
‎            }
‎            100% {
‎                transform: scale(1.5);
‎                opacity: 0;
‎            }
‎        }
‎        
‎        .hidden {
‎            display: none;
‎        }
‎        
‎        .couple-names {
‎            font-size: 1.5rem;
‎            margin-bottom: 15px;
‎            color: #fffacd;
‎            text-shadow: 1px 1px 3px rgba(0,0,0,0.5);
‎        }
‎    </style>
‎</head>
‎<body>
‎    <div class="message-box">
‎        <div class="couple-names">ပိုင်ခန့်လင်း ❤️ ရွှေစင်ဦး</div>
‎        <div class="message">ရွှေစင်ဦးရေ...</div>
‎        <div class="sub-message">မင်းကိုကြည့်တိုင်း နှလုံးသားကခုန်ချင်နေတယ် ❤️</div>
‎    </div>
‎    
‎    <audio id="heartSound" src="https://assets.mixkit.co/sfx/preview/mixkit-romantic-heart-beat-1490.mp3" preload="auto"></audio>
‎    <audio id="sparkleSound" src="https://assets.mixkit.co/sfx/preview/mixkit-magic-sparkle-902.mp3" preload="auto"></audio>
‎    
‎    <script>
‎        const messages = [
‎            "မင်းမျက်လုံးတွေက ကြယ်တွေထက်လှတယ် ✨",
‎            "ငါတို့အတူရှိရင် အချိန်တွေက ပျံ့လွင့်သွားတယ်",
‎            "မင်းနဲ့အတူနေရတာ အရမ်းပျော်တယ်",
‎            "ရွှေစင်ဦးရဲ့အပြုံးက ငါ့အတွက်နေ့တိုင်းလိုအပ်နေတယ်","I Love You 3000 💖",
‎            "ပိုင်ခန့်လင်းရဲ့အချစ်က ရွှေစင်ဦးအတွက် အမြဲတမ်း",
‎            "ကိုတို့နှစ်ယောက် တူတူပျော်ရွှင်ကြမယ်",
‎            "နေ့တိုင်းမင်းနဲ့အတူနေဖြစ်ချင်တယ်"
‎        ];
‎        
‎        const colors = ["#ff6b6b", "#ff9e7d", "#ffd166", "#06d6a0", "#118ab2", "#ef476f", "#ffd166", "#ff85a1", "#a0e7e5"];
‎        
‎        // Sound effects
‎        const heartSound = document.getElementById('heartSound');
‎        const sparkleSound = document.getElementById('sparkleSound');
‎        
‎        // Create hearts
‎        function createHeart(x, y) {
‎            const heart = document.createElement('div');
‎            heart.className = 'heart';
‎            
‎            const size = Math.random() * 30 + 20;
‎            const duration = Math.random() * 3 + 2;
‎            const delay = Math.random() * 2;
‎            const color = colors[Math.floor(Math.random() * colors.length)];
‎            
‎            heart.innerHTML = 
‎                <svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="${color}">
‎                    <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
‎                </svg>
‎            ;
‎            
‎            heart.style.left = ${x}px;
‎            heart.style.top = ${y}px;
‎            heart.style.width = ${size}px;
‎            heart.style.height = ${size}px;
‎            heart.style.animationDuration = ${duration}s;
‎            heart.style.animationDelay = ${delay}s;
‎            
‎            document.body.appendChild(heart);
‎            
‎            setTimeout(() => {
‎                heart.remove();
‎            }, duration * 1000);
‎        }
‎        
‎        // Create fireworks
‎        function createFirework(x, y) {
‎            const particles = 30;
‎            for (let i = 0; i < particles; i++) {
‎                const firework = document.createElement('div');
‎                firework.className = 'firework';
‎                
‎                const angle = (Math.PI * 2) * (i / particles);
‎                const distance = Math.random() * 100 + 50;
‎                const duration = Math.random() * 0.5 + 0.5;
‎                const color = colors[Math.floor(Math.random() * colors.length)];
‎                
‎                firework.style.left = ${x}px;
‎                firework.style.top = ${y}px;
‎                firework.style.backgroundColor = color;
‎                firework.style.animationDuration = ${duration}s;
‎                
‎                document.body.appendChild(firework);
‎                
‎                setTimeout(() => {
‎                    firework.style.transform = translate(${Math.cos(angle) * distance}px, ${Math.sin(angle) * distance}px);
‎                }, 10);
‎                
‎                setTimeout(() => {
‎                    firework.remove();
‎                }, duration * 1000);
‎            }
‎        }
‎        
‎        // Change message periodically
‎        function changeMessage() {
‎            const messageBox = document.querySelector('.message-box');
‎            const message = document.querySelector('.message');
‎            const subMessage = document.querySelector('.sub-message');
‎            
‎            messageBox.classList.add('hidden');
‎            
‎            setTimeout(() => {
‎                const randomMsg = messages[Math.floor(Math.random() * messages.length)];
‎                message.textContent = Math.random() > 0.5 ? "ရွှေစင်ဦးရေ..." : "ပိုင်ခန့်လင်းရေ...";
‎                subMessage.textContent = randomMsg;
‎                messageBox.classList.remove('hidden');
‎                
‎                // Create heart explosion
‎                const rect = messageBox.getBoundingClientRect();const x = rect.left + rect.width / 2;
‎                const y = rect.top + rect.height / 2;
‎                
‎                for (let i = 0; i < 15; i++) {
‎                    setTimeout(() => {
‎                        createHeart(x, y);
‎                    }, i * 100);
‎                }
‎                
‎                sparkleSound.currentTime = 0;
‎                sparkleSound.play();
‎                
‎            }, 500);
‎        }
‎        
‎        // Click/touch event
‎        document.body.addEventListener('click', function(e) {
‎            createHeart(e.clientX, e.clientY);
‎            createFirework(e.clientX, e.clientY);
‎            
‎            heartSound.currentTime = 0;
‎            heartSound.play();
‎            
‎            // Change message every 3rd click
‎            if (Math.random() > 0.7) {
‎                changeMessage();
‎            }
‎        });
‎        
‎        // Initial setup
‎        function init() {
‎            // Initial hearts
‎            for (let i = 0; i < 20; i++) {
‎                setTimeout(() => {
‎                    const x = Math.random() * window.innerWidth;
‎                    const y = Math.random() * window.innerHeight;
‎                    createHeart(x, y);
‎                }, i * 200);
‎            }
‎            
‎            // Change message every 10 seconds
‎            setInterval(changeMessage, 10000);
‎        }
‎        
‎        init();
‎    </script>
‎</body>
‎</html>
‎
