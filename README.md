<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>生日快乐！</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#FF6B8B',
                        secondary: '#FFD700',
                        accent: '#FF6B6B',
                    },
                    fontFamily: {
                        happy: ['"Comic Sans MS"', '"Marker Felt"', 'cursive'],
                    },
                    animation: {
                        'float': 'float 3s ease-in-out infinite',
                        'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                        'bounce-slow': 'bounce 3s infinite',
                        'fade-in': 'fadeIn 0.8s ease-out forwards',
                        'slide-up': 'slideUp 0.6s ease-out forwards',
                        'scale-in': 'scaleIn 0.5s ease-out forwards',
                        'spin-slow': 'spin 15s linear infinite',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-10px)' },
                        },
                        fadeIn: {
                            '0%': { opacity: '0' },
                            '100%': { opacity: '1' },
                        },
                        slideUp: {
                            '0%': { transform: 'translateY(20px)', opacity: '0' },
                            '100%': { transform: 'translateY(0)', opacity: '1' },
                        },
                        scaleIn: {
                            '0%': { transform: 'scale(0)', opacity: '0' },
                            '100%': { transform: 'scale(1)', opacity: '1' },
                        }
                    }
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .text-shadow {
                text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            }
            .text-shadow-glow {
                text-shadow: 0 0 10px rgba(255, 215, 0, 0.8), 0 0 20px rgba(255, 215, 0, 0.5);
            }
            .page {
                position: absolute;
                width: 100%;
                height: 100%;
                transition: transform 0.8s cubic-bezier(0.645, 0.045, 0.355, 1.000);
                transform-origin: left center;
                backface-visibility: hidden;
                overflow: hidden;
            }
            .page.flipped {
                transform: rotateY(-180deg);
            }
            .cake-layer {
                border-radius: 15px 15px 0 0;
            }
            .candle {
                position: relative;
            }
            .flame {
                position: absolute;
                width: 8px;
                height: 16px;
                background: #FF9F1C;
                border-radius: 50% 50% 20% 20%;
                top: -16px;
                left: 50%;
                transform: translateX(-50%);
                box-shadow: 0 0 15px 5px rgba(255, 159, 28, 0.5);
                animation: flicker 0.5s infinite alternate;
            }
            @keyframes flicker {
                0% { transform: translateX(-50%) scale(1); opacity: 0.8; }
                100% { transform: translateX(-50%) scale(1.1); opacity: 1; }
            }
            .confetti {
                position: absolute;
                width: 10px;
                height: 10px;
                opacity: 0;
                animation: confetti-fall 3s ease-in-out forwards;
            }
            @keyframes confetti-fall {
                0% { transform: translateY(-100vh) rotate(0deg); opacity: 1; }
                100% { transform: translateY(100vh) rotate(360deg); opacity: 0; }
            }
            .virtues-scroll {
                display: flex;
                flex-direction: column;
                gap: 1rem;
                width: max-content;
                animation: scrollVirtues 60s linear infinite;
            }
            .virtue-row {
                display: flex;
                gap: 0.5rem 1.5rem;
            }
            .virtue-item {
                display: inline-block;
                background: white;
                padding: 0.5rem 1rem;
                border-radius: 20px;
                box-shadow: 0 3px 6px rgba(0,0,0,0.1);
                white-space: nowrap;
                transform: translateY(0);
                transition: all 0.3s ease;
            }
            .virtue-item:hover {
                transform: translateY(-5px) scale(1.05);
                box-shadow: 0 5px 15px rgba(255,107,139,0.3);
            }
            @keyframes scrollVirtues {
                0% { transform: translateX(0); }
                100% { transform: translateX(-50%); }
            }
            .scroll-container {
                overflow-x: hidden;
                position: relative;
                width: 100%;
                padding: 2rem 0;
            }
            .message-popup {
                position: fixed;
                top: 50%;
                left: 50%;
                transform: translate(-50%, -50%) scale(0);
                background: white;
                padding: 2rem;
                border-radius: 15px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.2);
                z-index: 100;
                transition: transform 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            }
            .message-popup.show {
                transform: translate(-50%, -50%) scale(1);
            }
            .firework {
                position: absolute;
                border-radius: 50%;
                opacity: 0;
                transform: scale(0);
            }
            .firework-burst {
                animation: burst 1.5s ease-out forwards;
            }
            @keyframes burst {
                0% { opacity: 1; transform: scale(0); }
                50% { opacity: 1; }
                100% { opacity: 0; transform: scale(1); }
            }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-pink-100 to-yellow-100 min-h-screen overflow-hidden font-happy relative">
    <!-- 贺卡容器 -->
    <div id="card-container" class="relative w-full h-screen max-w-4xl mx-auto perspective-1000">
        <!-- 第1页：封面 -->
        <div class="page bg-gradient-to-br from-primary to-pink-400 flex flex-col items-center justify-center p-8 z-40" data-page="1">
            <div class="absolute top-0 left-0 w-full h-full overflow-hidden">
                <div id="cover-sparkles" class="w-full h-full"></div>
            </div>
            
            <h1 class="text-[clamp(2rem,6vw,4rem)] font-bold text-white text-center mb-8 tracking-wider text-shadow-glow animate-fade-in">
                新岁平安顺意！
            </h1>
            
            <div class="bg-white/20 backdrop-blur-sm rounded-xl p-8 max-w-lg w-full text-white text-center text-lg leading-relaxed animate-slide-up" style="animation-delay: 0.3s">
                <p class="mb-4">亲爱的，20岁生日快乐！！！</p>
                <p class="mb-4">今天是你的生日，</p>
                <p class="mb-4">我在这里祝你生日快乐！</p>
                <p class="mb-6">这是我给你做的专属计算机的电子生日礼物，</p>
                <p>请你打开看看吧！</p>
            </div>
            
            <div class="w-20 h-20 rounded-full bg-secondary flex items-center justify-center cursor-pointer transform transition-transform duration-300 hover:scale-110 shadow-lg mt-10 animate-slide-up" style="animation-delay: 0.6s" id="start-btn">
                <i class="fa fa-arrow-right text-primary text-3xl"></i>
            </div>
        </div>
        
        <!-- 第2页：100个优点 -->
        <div class="page bg-gradient-to-br from-yellow-50 to-orange-100 p-6 z-30" data-page="2">
            <h2 class="text-[clamp(1.5rem,4vw,2.5rem)] text-accent text-center mb-6 font-bold sticky top-4 bg-yellow-50/80 backdrop-blur-sm py-2 rounded-lg shadow-md">
                亲爱的朋友，你有100个优点
            </h2>
            
            <div class="scroll-container flex-1 flex items-center justify-center h-[70vh]">
                <div class="virtues-scroll" id="virtues-container">
                    <!-- 100个优点将通过JS动态生成 -->
                </div>
                <!-- 复制一份用于无缝滚动 -->
                <div class="virtues-scroll" id="virtues-container-clone">
                    <!-- 100个优点将通过JS动态生成 -->
                </div>
            </div>
            
            <div class="absolute bottom-8 right-8 w-16 h-16 rounded-full bg-primary flex items-center justify-center cursor-pointer transform transition-transform duration-300 hover:scale-110 shadow-md next-btn z-10">
                <i class="fa fa-arrow-right text-white text-2xl"></i>
            </div>
            
            <div class="text-center text-orange-500 mb-4">
                <i class="fa fa-angle-double-left scroll-indicator"></i> 
                <span class="mx-2">左右滚动查看</span>
                <i class="fa fa-angle-double-right scroll-indicator"></i>
            </div>
        </div>
        
        <!-- 第3页：蛋糕页 -->
        <div class="page bg-gradient-to-br from-green-50 to-teal-100 p-8 z-20" data-page="3">
            <h2 class="text-[clamp(1.8rem,5vw,3rem)] text-green-600 text-center mb-6 font-bold">
                生日快乐！
            </h2>
            
            <div class="flex flex-col items-center justify-center h-[70vh]">
                <!-- 美味蛋糕 -->
                <div class="cake relative mb-10 transform hover:scale-105 transition-transform duration-500">
                    <!-- 蛋糕底 -->
                    <div class="cake-layer w-72 h-16 bg-pink-400 relative">
                        <div class="absolute bottom-0 left-0 w-full h-3 bg-pink-500"></div>
                        <div class="absolute top-1/2 left-10 w-2 h-6 bg-white rounded-full transform -translate-y-1/2"></div>
                        <div class="absolute top-1/2 left-20 w-2 h-8 bg-white rounded-full transform -translate-y-1/2"></div>
                        <div class="absolute top-1/2 left-30 w-2 h-5 bg-white rounded-full transform -translate-y-1/2"></div>
                        <div class="absolute top-1/2 left-40 w-2 h-7 bg-white rounded-full transform -translate-y-1/2"></div>
                        <div class="absolute top-1/2 left-50 w-2 h-6 bg-white rounded-full transform -translate-y-1/2"></div>
                    </div>
                    <!-- 蛋糕中间 -->
                    <div class="cake-layer w-64 h-14 bg-pink-300 mx-auto -mt-2 relative">
                        <div class="absolute bottom-0 left-0 w-full h-3 bg-pink-400"></div>
                        <div class="absolute top-1/2 left-8 w-3 h-5 bg-secondary rounded-full transform -translate-y-1/2"></div>
                        <div class="absolute top-1/2 left-20 w-3 h-7 bg-secondary rounded-full transform -translate-y-1/2"></div>
                        <div class="absolute top-1/2 left-32 w-3 h-5 bg-secondary rounded-full transform -translate-y-1/2"></div>
                        <div class="absolute top-1/2 left-44 w-3 h-6 bg-secondary rounded-full transform -translate-y-1/2"></div>
                    </div>
                    <!-- 蛋糕顶 -->
                    <div class="cake-layer w-56 h-12 bg-pink-200 mx-auto -mt-2 relative">
                        <div class="absolute bottom-0 left-0 w-full h-3 bg-pink-300"></div>
                    </div>
                    
                    <!-- 奶油装饰 -->
                    <div class="absolute top-0 left-1/2 transform -translate-x-1/2 w-48 h-8 bg-white rounded-full -mt-4 relative overflow-hidden">
                        <div class="absolute top-1 left-5 w-3 h-3 bg-primary rounded-full"></div>
                        <div class="absolute top-2 left-15 w-4 h-4 bg-secondary rounded-full"></div>
                        <div class="absolute top-1 left-25 w-3 h-3 bg-purple-400 rounded-full"></div>
                        <div class="absolute top-3 left-35 w-3 h-3 bg-green-400 rounded-full"></div>
                    </div>
                    
                    <!-- 水果装饰 -->
                    <div class="absolute top-[-10px] left-[35%] w-8 h-8 bg-red-500 rounded-full shadow-md"></div>
                    <div class="absolute top-[-15px] left-[45%] w-10 h-10 bg-yellow-300 rounded-full shadow-md"></div>
                    <div class="absolute top-[-8px] left-[55%] w-8 h-8 bg-purple-500 rounded-full shadow-md"></div>
                    
                    <!-- 8根蜡烛 -->
                    <div class="candles flex justify-center gap-4 absolute top-0 left-1/2 transform -translate-x-1/2 -mt-18">
                        <div class="candle w-3 h-16 bg-secondary">
                            <div class="flame"></div>
                        </div>
                        <div class="candle w-3 h-14 bg-secondary">
                            <div class="flame"></div>
                        </div>
                        <div class="candle w-3 h-18 bg-secondary">
                            <div class="flame"></div>
                        </div>
                        <div class="candle w-3 h-15 bg-secondary">
                            <div class="flame"></div>
                        </div>
                        <div class="candle w-3 h-17 bg-secondary">
                            <div class="flame"></div>
                        </div>
                        <div class="candle w-3 h-13 bg-secondary">
                            <div class="flame"></div>
                        </div>
                        <div class="candle w-3 h-16 bg-secondary">
                            <div class="flame"></div>
                        </div>
                        <div class="candle w-3 h-14 bg-secondary">
                            <div class="flame"></div>
                        </div>
                    </div>
                </div>
                
                <div class="text-center">
                    <p class="text-dark text-xl mb-6">吹蜡烛许愿吧！这8根蜡烛祝你越来越发！</p>
                    <button id="blow-candle" class="bg-primary hover:bg-pink-600 text-white font-bold py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 shadow-lg">
                        吹灭蜡烛 <i class="fa fa-birthday-cake ml-2"></i>
                    </button>
                </div>
            </div>
            
            <div id="fireworks-container-cake" class="absolute top-0 left-0 w-full h-full pointer-events-none"></div>
            
            <div class="absolute bottom-8 right-8 w-16 h-16 rounded-full bg-primary flex items-center justify-center cursor-pointer transform transition-transform duration-300 hover:scale-110 shadow-md next-btn" style="display: none;">
                <i class="fa fa-arrow-right text-white text-2xl"></i>
            </div>
        </div>
        
        <!-- 第4页：祝福页 -->
        <div class="page bg-gradient-to-br from-indigo-900 to-purple-900 p-8 z-10" data-page="4">
            <div id="fireworks-container-final" class="absolute top-0 left-0 w-full h-full pointer-events-none"></div>
            
            <h2 class="text-[clamp(1.8rem,5vw,3rem)] text-yellow-300 text-center mb-10 font-bold text-shadow-glow">
                给我最好的朋友
            </h2>
            
            <div class="bg-white/10 backdrop-blur-sm rounded-xl p-8 max-w-2xl mx-auto text-white text-center text-lg leading-relaxed">
                <!-- 这里是可以自定义的祝福内容 -->
                <p class="mb-4">亲爱的朋友，</p>
                <p class="mb-4">在你20岁这个特别的日子里，</p>
                <p class="mb-4">我想对你说：</p>
                <p class="mb-4">认识你可能是我目前运气最好的时候吧，</p>
                <p class="mb-4">和你在一起的每一天都充满欢乐，</p>
                <p class="mb-4">愿你未来的日子里：</p>
                <p class="mb-4">笑口常开，好运连连，</p>
                <p class="mb-4">梦想成真，万事顺意，</p>
                <p class="mb-4">最重要的是永远保持这份纯真与快乐！</p>
                <p class="text-2xl font-bold text-yellow-200 mt-8 animate-pulse">生日快乐！永乐！</p>
            </div>
            
            <div class="absolute bottom-8 left-1/2 transform -translate-x-1/2">
                <button id="close-btn" class="bg-yellow-400 hover:bg-yellow-300 text-purple-900 font-bold py-3 px-8 rounded-full transition-all duration-300 transform hover:scale-105 shadow-lg">
                    保存这份祝福 <i class="fa fa-heart ml-2"></i>
                </button>
            </div>
        </div>
        
        <!-- 吹蜡烛后的弹窗消息 -->
        <div class="message-popup" id="age-message">
            <p class="text-2xl font-bold text-primary text-center">虽然年龄20，但是内心永远18！</p>
        </div>
    </div>
    
    <script>
        // 当前页码
        let currentPage = 1;
        const totalPages = 4;
        
        // 100个优点列表
        const virtues = [
            "善良", "乐观", "真诚", "聪明", "幽默", "体贴", "勇敢", "慷慨", "有耐心", "负责任",
            "有创意", "积极", "热情", "诚实", "可靠", "友善", "智慧", "有爱心", "勤奋", "有毅力",
            "开朗", "温柔", "坚强", "自信", "谦虚", "包容", "果断", "细心", "有活力", "有担当",
            "善解人意", "乐于助人", "有同理心", "有条理", "有远见", "有魅力", "有才华", "有品味", "有风度", "有正义感",
            "乐观向上", "坚持不懈", "勇于尝试", "善于沟通", "懂得倾听", "尊重他人", "热爱生活", "积极进取", "心地善良", "为人正直",
            "做事认真", "待人诚恳", "学习能力强", "适应能力强", "团队合作好", "独立思考", "创新精神", "时间管理好", "情绪稳定", "不是很挑食",
            "笑容甜美", "声音好听", "心灵手巧", "审美独特", "文笔优美", "口才出众", "你就是很好", "观察力强", "记忆力好", "分析能力强",
            "解决问题能力强", "善于鼓励他人", "懂得感恩", "知足常乐", "勇于承认错误", "不断自我提升", "珍惜友谊", "重视情感", "爱猫人士", "保护环境",
            "品味生活", "享受当下", "不畏挑战", "敢于突破", "保持初心", "坚守原则", "灵活变通", "坚持梦想", "传递正能量", "温暖如阳光",
            "冷静沉着", "风趣幽默", "纯真可爱", "成熟稳重", "天真烂漫", "优雅大方", "简单纯粹", "活力四射", "魅力无限", "独一无二"
        ];
        
        // DOM 元素
        const pages = document.querySelectorAll('.page');
        const startBtn = document.getElementById('start-btn');
        const nextBtns = document.querySelectorAll('.next-btn');
        const blowCandleBtn = document.getElementById('blow-candle');
        const flames = document.querySelectorAll('.flame');
        const fireworksContainerCake = document.getElementById('fireworks-container-cake');
        const fireworksContainerFinal = document.getElementById('fireworks-container-final');
        const coverSparkles = document.getElementById('cover-sparkles');
        const virtuesContainer = document.getElementById('virtues-container');
        const virtuesContainerClone = document.getElementById('virtues-container-clone');
        const ageMessage = document.getElementById('age-message');
        const closeBtn = document.getElementById('close-btn');
        
        // 初始化100个优点 - 5行20列，带错乱效果
        function initVirtues() {
            // 打乱优点顺序
            const shuffledVirtues = [...virtues].sort(() => Math.random() - 0.5);
            
            // 创建5行，每行20个优点
            for (let row = 0; row < 5; row++) {
                const virtueRow = document.createElement('div');
                virtueRow.className = 'virtue-row';
                
                // 为每行创建20个优点
                for (let i = 0; i < 20; i++) {
                    const index = row * 20 + i;
                    const virtueElement = document.createElement('div');
                    virtueElement.className = 'virtue-item';
                    
                    // 添加随机样式变化，创建错乱效果
                    const randomSize = 0.9 + Math.random() * 0.2; // 0.9-1.1倍大小
                    const randomY = -5 + Math.random() * 10; // -5到5px的Y偏移
                    const randomRotate = -3 + Math.random() * 6; // -3到3度的旋转
                    
                    virtueElement.style.transform = `scale(${randomSize}) translateY(${randomY}px) rotate(${randomRotate}deg)`;
                    virtueElement.style.backgroundColor = getRandomPastelColor();
                    
                    virtueElement.textContent = shuffledVirtues[index];
                    virtueRow.appendChild(virtueElement);
                }
                
                virtuesContainer.appendChild(virtueRow);
            }
            
            // 克隆一份用于无缝滚动
            virtuesContainerClone.innerHTML = virtuesContainer.innerHTML;
        }
        
        // 生成随机柔和的颜色
        function getRandomPastelColor() {
            const hue = Math.floor(Math.random() * 360);
            return `hsl(${hue}, 70%, 90%)`;
        }
        
        // 初始化封面闪光效果
        function createSparkles() {
            for (let i = 0; i < 80; i++) {
                const sparkle = document.createElement('div');
                sparkle.className = 'absolute rounded-full bg-white/70';
                sparkle.style.width = `${Math.random() * 4 + 1}px`;
                sparkle.style.height = sparkle.style.width;
                sparkle.style.left = `${Math.random() * 100}%`;
                sparkle.style.top = `${Math.random() * 100}%`;
                sparkle.style.boxShadow = '0 0 10px 2px rgba(255,255,255,0.8)';
                sparkle.style.animation = `float ${Math.random() * 3 + 2}s ease-in-out infinite`;
                sparkle.style.animationDelay = `${Math.random() * 3}s`;
                sparkle.style.opacity = Math.random() * 0.5 + 0.2;
                coverSparkles.appendChild(sparkle);
            }
        }
        
        // 翻页函数
        function goToPage(pageNum) {
            if (pageNum < 1 || pageNum > totalPages) return;
            
            // 隐藏当前页，显示目标页
            pages.forEach(page => {
                const pageId = parseInt(page.dataset.page);
                if (pageId < pageNum) {
                    page.classList.add('flipped');
                } else {
                    page.classList.remove('flipped');
                }
            });
            
            currentPage = pageNum;
            
            // 如果是最后一页，开始烟花效果
            if (pageNum === totalPages) {
                startFinalFireworks();
            }
        }
        
        // 吹蜡烛效果
        function blowCandle() {
            // 所有火焰同时熄灭
            flames.forEach(flame => {
                flame.style.animation = 'none';
                flame.style.transform = 'translateX(-50%) scale(0)';
                flame.style.opacity = '0';
            });
            
            // 创建彩色纸屑
            createConfetti(200);
            
            // 禁用按钮
            blowCandleBtn.disabled = true;
            blowCandleBtn.textContent = '蜡烛已吹灭！';
            
            // 播放蜡烛熄灭时的小烟花
            for (let i = 0; i < 8; i++) {
                setTimeout(() => {
                    createSmallFirework(i);
                }, i * 150);
            }
            
            // 2秒后播放大烟花
            setTimeout(() => {
                for (let i = 0; i < 5; i++) {
                    setTimeout(() => {
                        createBigFirework();
                    }, i * 1000);
                }
                
                // 显示消息
                setTimeout(() => {
                    ageMessage.classList.add('show');
                    
                    // 3秒后隐藏消息并显示下一页按钮
                    setTimeout(() => {
                        ageMessage.classList.remove('show');
                        document.querySelector('[data-page="3"] .next-btn').style.display = 'flex';
                    }, 3000);
                }, 1000);
            }, 1000);
        }
        
        // 创建彩色纸屑
        function createConfetti(count) {
            const colors = ['#FF6B6B', '#FFD700', '#4ECDC4', '#45B7D1', '#FFA07A', '#98D8C8', '#9370DB', '#8FBC8F'];
            
            for (let i = 0; i < count; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.left = `${Math.random() * 100}%`;
                confetti.style.width = `${Math.random() * 10 + 5}px`;
                confetti.style.height = `${Math.random() * 10 + 5}px`;
                confetti.style.animationDuration = `${Math.random() * 3 + 2}s`;
                confetti.style.animationDelay = `${Math.random() * 2}s`;
                
                // 随机旋转
                confetti.style.transform = `rotate(${Math.random() * 360}deg)`;
                
                document.querySelector('[data-page="3"]').appendChild(confetti);
                
                // 动画结束后移除
                setTimeout(() => {
                    confetti.remove();
                }, 5000);
            }
        }
        
        // 创建蜡烛熄灭时的小烟花
        function createSmallFirework(index) {
            const candle = flames[index].closest('.candle');
            const rect = candle.getBoundingClientRect();
            const cardRect = document.querySelector('[data-page="3"]').getBoundingClientRect();
            
            // 烟花位置在蜡烛顶部
            const x = rect.left + rect.width/2 - cardRect.left;
            const y = rect.top - cardRect.top;
            
            // 创建小型烟花
            const firework = document.createElement('div');
            firework.className = 'firework firework-burst';
            
            // 随机颜色
            const hue = Math.random() * 360;
            firework.style.backgroundColor = `hsl(${hue}, 80%, 60%)`;
            firework.style.boxShadow = `0 0 20px 10px hsl(${hue}, 80%, 60%, 0.5)`;
            
            // 位置和大小
            firework.style.left = `${x}px`;
            firework.style.top = `${y}px`;
            firework.style.width = '60px';
            firework.style.height = '60px';
            
            fireworksContainerCake.appendChild(firework);
            
            // 动画结束后移除
            setTimeout(() => {
                firework.remove();
            }, 1500);
        }
        
        // 创建大烟花
        function createBigFirework() {
            // 随机位置
            const x = Math.random() * 80 + 10; // 10%-90%
            const y = Math.random() * 50 + 10; // 10%-60%
            
            // 随机颜色
            const hue = Math.random() * 360;
            
            // 创建大型整体烟花
            const firework = document.createElement('div');
            firework.className = 'firework firework-burst';
            firework.style.backgroundColor = `hsl(${hue}, 80%, 60%, 0.7)`;
            firework.style.boxShadow = `0 0 60px 30px hsl(${hue}, 80%, 60%, 0.5), 0 0 100px 50px hsl(${hue}, 80%, 60%, 0.3)`;
            
            // 位置和大小
            firework.style.left = `${x}%`;
            firework.style.top = `${y}%`;
            firework.style.width = '200px';
            firework.style.height = '200px';
            
            fireworksContainerCake.appendChild(firework);
            
            // 添加一些点缀的小粒子
            for (let i = 0; i < 20; i++) {
                const particle = document.createElement('div');
                particle.className = 'firework firework-burst';
                particle.style.backgroundColor = `hsl(${hue + Math.random() * 30}, 80%, 70%)`;
                particle.style.left = `${x}%`;
                particle.style.top = `${y}%`;
                particle.style.width = `${5 + Math.random() * 10}px`;
                particle.style.height = `${5 + Math.random() * 10}px`;
                particle.style.animationDelay = `${Math.random() * 0.5}s`;
                
                fireworksContainerCake.appendChild(particle);
                
                setTimeout(() => {
                    particle.remove();
                }, 1500);
            }
            
            // 动画结束后移除
            setTimeout(() => {
                firework.remove();
            }, 1500);
        }
        
        // 最后一页的烟花效果
        function createFinalFirework() {
            // 随机位置
            const x = Math.random() * 80 + 10; // 10%-90%
            const y = Math.random() * 50 + 10; // 10%-60%
            
            // 随机颜色
            const hue = Math.random() * 360;
            
            // 创建大型整体烟花
            const firework = document.createElement('div');
            firework.className = 'firework firework-burst';
            firework.style.backgroundColor = `hsl(${hue}, 80%, 60%, 0.7)`;
            firework.style.boxShadow = `0 0 80px 40px hsl(${hue}, 80%, 60%, 0.5), 0 0 120px 60px hsl(${hue}, 80%, 60%, 0.3)`;
            
            // 位置和大小
            firework.style.left = `${x}%`;
            firework.style.top = `${y}%`;
            firework.style.width = '250px';
            firework.style.height = '250px';
            
            fireworksContainerFinal.appendChild(firework);
            
            // 添加点缀粒子
            for (let i = 0; i < 30; i++) {
                const particle = document.createElement('div');
                particle.className = 'firework firework-burst';
                particle.style.backgroundColor = `hsl(${hue + Math.random() * 30}, 80%, 70%)`;
                particle.style.left = `${x}%`;
                particle.style.top = `${y}%`;
                particle.style.width = `${5 + Math.random() * 10}px`;
                particle.style.height = `${5 + Math.random() * 10}px`;
                particle.style.animationDelay = `${Math.random() * 0.5}s`;
                
                fireworksContainerFinal.appendChild(particle);
                
                setTimeout(() => {
                    particle.remove();
                }, 1500);
            }
            
            // 动画结束后移除
            setTimeout(() => {
                firework.remove();
            }, 1500);
        }
        
        // 最后一页烟花表演
        function startFinalFireworks() {
            // 定时发射烟花
            const interval = setInterval(createFinalFirework, 1500);
            
            // 20秒后停止
            setTimeout(() => {
                clearInterval(interval);
            }, 20000);
        }
        
        // 事件监听
        startBtn.addEventListener('click', () => goToPage(2));
        
        nextBtns.forEach(btn => {
            btn.addEventListener('click', () => goToPage(currentPage + 1));
        });
        
        blowCandleBtn.addEventListener('click', blowCandle);
        
        closeBtn.addEventListener('click', () => {
            alert('希望你喜欢这份生日祝福！生日快乐！');
        });
        
        // 初始化
        window.addEventListener('DOMContentLoaded', () => {
            createSparkles();
            initVirtues();
            
            // 允许通过点击页面空白处翻页（除了按钮）
            pages.forEach(page => {
                page.addEventListener('click', (e) => {
                    // 检查是否点击了按钮
                    if (!e.target.closest('button') && !e.target.closest('.next-btn') && !e.target.closest('#start-btn')) {
                        if (currentPage < totalPages) {
                            // 第三页需要吹蜡烛后才能翻页
                            if (currentPage === 3) {
                                if (document.querySelector('[data-page="3"] .next-btn').style.display !== 'none') {
                                    goToPage(currentPage + 1);
                                }
                            } else {
                                goToPage(currentPage + 1);
                            }
                        }
                    }
                });
            });
        });
    </script>
</body>
</html>
