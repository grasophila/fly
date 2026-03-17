<html lang="zh-CN">
<head>
    <meta charset="UTF-8<meta name="viewport" content="width=device-width, initial-scale=1.0">
   秦山草木
   <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #121215;
            background-image: url("https://www.transparenttextures.com/patterns/old-paper.png");
            background-blend-mode: overlay;
            font-family: "微软雅黑", "宋体", serif;
            padding: 20px;
            /* 背景微动动画 */
            animation: bgFloat 18s infinite ease-in-out;
        }

        /* 背景缓慢浮动动画 */
        @keyframes bgFloat {
            0%, 100% { background-position: 0 0; }
            50% { background-position: 6px 4px; }
        }

        .game-container {
            max-width: 750px;
            margin: 40px auto;
            padding: 40px;
            border: 2px solid #9a3820;
            background: rgba(0, 0, 0, 0.8);
            position: relative;
            border-radius: 6px;
            box-shadow: 0 0 30px rgba(154, 56, 32, 0.35);
            overflow: hidden;
        }

        /* 草木装饰浮动动画 */
        .plant-decoration {
            position: absolute;
            width: 50px;
            height: 50px;
            opacity: 0.25;
            z-index: -1;
            animation: plantSwing 10s infinite ease-in-out;
        }

        .plant1 { top: 25px; left: 30px; animation-delay: 0s; }
        .plant2 { top: 30px; right: 35px; animation-delay: 3s; }
        .plant3 { bottom: 45px; left: 40px; animation-delay: 5s; }
        .plant4 { bottom: 35px; right: 30px; animation-delay: 7s; }

        @keyframes plantSwing {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-6px) rotate(3deg); }
        }

        .game-title {
            text-align: center;
            font-size: 32px;
            letter-spacing: 10px;
            color: #d4af37;
            margin-bottom: 15px;
            text-shadow: 0 0 15px #9a3820;
            font-weight: normal;
        }

        .game-subtitle {
            text-align: center;
            font-size: 16px;
            color: #c0b298;
            margin-bottom: 40px;
            letter-spacing: 3px;
        }

        /* 分段文本框样式 */
        .story-section {
            margin-bottom: 22px;
            /* 竹简翻页渐入动画 */
            opacity: 0;
            transform: translateY(15px);
            animation: scrollFade 1s forwards ease-out;
        }

        @keyframes scrollFade {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .story-textarea {
            width: 100%;
            min-height: 70px;
            background: rgba(18, 14, 10, 0.7);
            border: 1px solid #8a724e;
            padding: 20px 25px;
            color: #e6d8b8;
            font-size: 17px;
            line-height: 1.9;
            outline: none;
            resize: vertical;
            border-radius: 4px;
            font-family: "微软雅黑", "宋体", serif;
            transition: all 0.3s ease;
        }

        .story-textarea:focus {
            border-color: #d4af37;
            box-shadow: 0 0 10px rgba(212, 175, 55, 0.25);
        }

        /* 选项框样式：上下排布，默认隐藏 */
        .choice-container {
            display: none;
            flex-direction: column;
            gap: 18px;
            margin-top: 30px;
            align-items: center;
        }

        .choice-btn {
            width: 280px;
            padding: 14px 0;
            background: #9a3820;
            color: #fff;
            border: none;
            font-size: 17px;
            letter-spacing: 2px;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: "微软雅黑", "宋体", serif;
        }

        .choice-btn:hover {
            background: #c44e2f;
            transform: translateX(5px);
            box-shadow: 0 0 12px rgba(196, 78, 47, 0.4);
        }

        /* 木系法术特效动画 */
        @keyframes vineEffect {
            0% { opacity: 0; transform: scale(0.8); }
            100% { opacity: 1; transform: scale(1); }
        }

        .vine-animate {
            animation: vineEffect 1.2s ease-out;
        }
    </style>
<body>
<div class="game<!-- 草木装饰 -->
        <div class="plant-decoration plant</div>
       <div class="plant-decoration</div>
<div class="plant</div><div class="</div<h1 class="game-title">秦</h1<p class="game-subtitle">春秋战国·秦地山林·木</p><!-- 剧情分段文本框 -->
        <div id="story-content"><!-- 选项按钮（上下排布）<div class="choice-container" id="choice-box">
            <button class="choice-btn" id="choiceA" onclick="selectOptionA()"><button class="choice-btn" id="choiceB" onclick="</button</div></div>

<script>
        // 剧情分段数据（按回车拆分，每段对应一个文本框）
        const storyData = [
            { type: 'text', content: '风停了，你看着躺在一片落叶丛里的"母亲"，轻声对她说晚安。' },
            { type: 'text', content: '于是世界又安静下来，你百无聊赖地躺在她身侧，像哺乳期的幼崽寻求着一个温暖的怀抱。' },
            { type: 'text', content: '抬起头数到第十六颗星星时，你听到山脚下传来躁动声，飞鸟掠过你头顶，你远远望去，看到与你长相相似的一群小动物经过。' },
            { type: 'choice', optionA: '去看看小动物们', optionB: '还是留在母亲身边吧' },
            { type: 'text', content: '【选择A】你再次回头看了一眼还在沉睡的"母亲"，轻手轻脚的飞掠下山，跟在那群小动物身后。' },
            { type: 'text', content: '【选择B】你盯着那张恬静的女子侧脸发呆，山脚下传来与此处格格不入的嘈杂声，你最后还是没按耐住好奇心，偷偷溜了下去。' },
            { type: 'text', content: '小动物们有些骑着马，有些装在结构复杂花纹精致的木头里，你一路上好奇地打量，边听边看，只用了半个夜晚便大致理解了他们的语言。' },
            { type: 'text', content: '原来是母亲之前提到的人类啊。你想。和我们真的长得很像呢。' },
            { type: 'text', content: '马上就要到宽阔的大路上了。也许我等他们离开树林后就得回到母亲身边了。你想。' },
            { type: 'text', content: '突然，破空声打破清晨的寂静，你听见撕心裂肺地叫喊，马嘶鸣着不安地在原地踱步，身穿黑衣面上有浓须的几个高头大马的人窜出来拦路，两拨人马相撞，血腥味迅速传到你身周。' },
            { type: 'choice', optionA: '跑出去试图阻止', optionB: '暗中帮帮他们' },
            { type: 'text', content: '【选择A】你只是轻轻一提气，便瞬间出现在两队人马之间，你努力回想着"母亲"身边流转的元素能量，靠着山林里充裕的木元素将刺客们用藤蔓抽飞。' },
            { type: 'text', content: '刺客们见情况不对，立马开始逃窜，身后马车旁的人想追，看见你神色淡淡地立在原地便也不敢再轻举妄动。' },
            { type: 'text', content: '【选择B】你伸手抚上旁边树木上垂下的叶片，刺客们被突然冒出的土墙挡住，惊诧之下对视一眼，迅速往后退去。' },
            { type: 'text', content: '马车旁的人一阵骚动后又安静下来，有一位看起来从容镇定的男子从马车里走出，对着前方道路拱手，高声喊到："感谢高人相助，可否一见？"' },
            { type: 'text', content: '你纠结的用手抠树皮，最后好奇心战胜了谨慎，你走了出去。' },
            { type: 'text', content: '一切尘埃落定后，你听见身后的马车里走出来一位穿着华贵的年轻男子，他朝你鞠躬拱手。' },
            { type: 'text', content: '男子冲你露出一个得体的笑容："我们几人是秦国的商贩，得仙人所救实乃大幸！不知仙人如何称呼？"' },
            { type: 'text', content: '你歪了歪脑袋，不知道他在说什么。对方自觉自己失礼，连忙赔罪，吩咐仆从递上一个古朴精致的饰品盒，打开瞬间你便被里面晶莹剔透的宝石与璀璨的金银晃了眼睛。' },
            { type: 'text', content: '男子双手奉上这份谢礼，看你迟迟不收，忐忑又小心翼翼的抬头。' },
            { type: 'text', content: '"你们要去哪？"你说。' },
            { type: 'text', content: '"回到秦国，仙人。"他恭敬回答，弯腰的姿势未变半分。' },
            { type: 'text', content: '"我可以跟你们一起吗？"蓝发的仙人俯视着面前渺小的，卑微的人类。' }
        ];

        const storyContent = document.getElementById('story-content');
        const choiceBox = document.getElementById('choice-box');
        const choiceA = document.getElementById('choiceA');
        const choiceB = document.getElementById('choiceB');
        let currentIndex = 0;
        let choiceFlag = false;

        // 渲染剧情内容
        function renderStory() {
            if (currentIndex >= storyData.length) return;
            const item = storyData[currentIndex];
            
            if (item.type === 'text') {
                // 渲染文本框
                const textDiv = document.createElement('div');
                textDiv.className = 'story-section';
                const textarea = document.createElement('textarea');
                textarea.className = 'story-textarea';
                textarea.value = item.content;
                textarea.readOnly = true;
                textDiv.appendChild(textarea);
                storyContent.appendChild(textDiv);
                currentIndex++;
                // 延迟加载下一段，模拟竹简翻页节奏
                setTimeout(() => renderStory(), 800);
            } else if (item.type === 'choice') {
                // 显示选项，暂停剧情加载
                choiceFlag = true;
                choiceA.innerText = item.optionA;
                choiceB.innerText = item.optionB;
                choiceBox.style.display = 'flex';
            }
        }

        // 选择选项A
        function selectOptionA() {
            choiceBox.style.display = 'none';
            choiceFlag = false;
            // 跳过对应选项B的剧情段
            currentIndex += (currentIndex === 3) ? 2 : 4;
            renderStory();
        }

        // 选择选项B
        function selectOptionB() {
            choiceBox.style.display = 'none';
            choiceFlag = false;
            // 跳过对应选项A的剧情段
            currentIndex += (currentIndex === 3) ? 1 : 3;
            renderStory();
        }

        // 初始化游戏
        window.onload = function() {
            renderStory();
        };
    </script>
</html>

