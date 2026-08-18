<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>浪花男子·出道之路</title>
    <style>
        :root { --naniwa-blue: #0077c2; --naniwa-pink: #f8a5c2; --bg: #f0f7ff; }
        body { font-family: 'PingFang SC', sans-serif; background-color: var(--bg); display: flex; justify-content: center; align-items: center; min-height: 100vh; margin: 0; }
        .game-box { width: 380px; height: 700px; background: white; border-radius: 30px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); overflow: hidden; display: flex; flex-direction: column; position: relative; }
        .header { background: linear-gradient(to right, var(--naniwa-blue), var(--naniwa-pink)); color: white; padding: 20px; text-align: center; font-weight: bold; }
        .content { flex: 1; padding: 20px; overflow-y: auto; }
        .stats { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; margin-bottom: 20px; font-size: 0.8rem; }
        .stat-card { background: #f8f9fa; padding: 10px; border-radius: 10px; text-align: center; border: 1px solid #eee; }
        .story { font-size: 1rem; line-height: 1.6; color: #333; margin-bottom: 20px; padding: 15px; background: #fff5f8; border-radius: 15px; border-left: 5px solid var(--naniwa-pink); }
        .choice-btn { width: 100%; padding: 12px; margin-bottom: 10px; border: none; border-radius: 20px; background: var(--naniwa-blue); color: white; cursor: pointer; font-size: 0.9rem; transition: 0.3s; }
        .choice-btn:hover { background: #005a92; }
        .hidden { display: none; }
    </style>
</head>
<body>

<div class="game-box">
    <div class="header" id="header">浪花男子·出道养成</div>
    <div class="content" id="game-ui">
        <!-- 初始界面 -->
        <div id="screen-start">
            <h3>创建练习生档案</h3>
            <input type="text" id="p-name" placeholder="输入姓名" style="width:100%; padding:10px; margin-bottom:10px;">
            <button class="choice-btn" onclick="startGame()">开始追梦之旅</button>
        </div>

        <!-- 游戏界面 -->
        <div id="screen-play" class="hidden">
            <div class="stats">
                <div class="stat-card">舞蹈<br><span id="s-dance">0</span></div>
                <div class="stat-card">综艺<br><span id="s-variety">0</span></div>
                <div class="stat-card">团魂<br><span id="s-bond">0</span></div>
            </div>
            <div class="story" id="story"></div>
            <div id="choices"></div>
        </div>
    </div>
</div>

<script>
    let player = { name: '', dance: 10, variety: 10, bond: 10, week: 1 };
    
    // 剧情脚本
    const script = [
        {
            text: "练习室里，西畑大吾正在教大家新舞步。你刚加入，动作有些跟不上，感到很沮丧。",
            choices: [
                { text: "请求大吾前辈再教一次", effect: { bond: 5, dance: 2 }, next: 1 },
                { text: "独自在镜子前拼命练习", effect: { dance: 10 }, next: 1 }
            ]
        },
        {
            text: "出道准备期，大桥和也提议大家一起去吃烤肉。这是增进团队感情的好机会。",
            choices: [
                { text: "和大家聊关西段子，气氛超好", effect: { variety: 10, bond: 5 }, next: 2 },
                { text: "默默负责烤肉，照顾大家", effect: { bond: 10 }, next: 2 }
            ]
        },
        {
            text: "距离出道发表还有最后一周，长尾谦杜和高桥恭平因为服装意见产生争执。你会怎么做？",
            choices: [
                { text: "充当和事佬，把大家聚在一起", effect: { bond: 15 }, next: 3 },
                { text: "专注于自己的走位，做到完美", effect: { dance: 10 }, next: 3 }
            ]
        },
        {
            text: "终于来到了那个决定命运的瞬间。事务所宣布出道成员，你站在舞台侧台，心跳加速。",
            choices: [
                { text: "坚定走上舞台", effect: { bond: 0 }, next: 4 }
            ]
        }
    ];

    function startGame() {
        const name = document.getElementById('p-name').value;
        if(!name) return alert('请先输入名字');
        player.name = name;
        document.getElementById('screen-start').classList.add('hidden');
        document.getElementById('screen-play').classList.remove('hidden');
        loadScene(0);
    }

    function loadScene(idx) {
        if(idx >= script.length) return endGame();
        
        const scene = script[idx];
        document.getElementById('story').innerText = scene.text;
        const container = document.getElementById('choices');
        container.innerHTML = '';
        
        scene.choices.forEach(c => {
            const btn = document.createElement('button');
            btn.className = 'choice-btn';
            btn.innerText = c.text;
            btn.onclick = () => {
                player.dance += c.effect.dance || 0;
                player.variety += c.effect.variety || 0;
                player.bond += c.effect.bond || 0;
                updateStats();
                loadScene(c.next);
            };
            container.appendChild(btn);
        });
    }

    function updateStats() {
        document.getElementById('s-dance').innerText = player.dance;
        document.getElementById('s-variety').innerText = player.variety;
        document.getElementById('s-bond').innerText = player.bond;
    }

    function endGame() {
        const total = player.dance + player.variety + player.bond;
        let result = "";
        if(total > 80) result = "恭喜你！你展现了完美的闪亮魅力，作为「浪花男子」的核心成员顺利出道！闪耀吧，Diamond Smile！";
        else result = "虽然暂时没有出道，但这段经历非常宝贵。粉丝们记住了你的努力，请继续加油！";
        
        document.getElementById('story').innerHTML = `<b>【最终评语】</b><br>${result}`;
        document.getElementById('choices').innerHTML = `<button class="choice-btn" onclick="location.reload()">重新开始追梦</button>`;
    }
</script>

</body>
</html>
