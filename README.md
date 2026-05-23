[index.html](https://github.com/user-attachments/files/28175826/index.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>公考一战成公·通关舱</title>
    <style>
        :root {
            --primary: #c2410c; /* 沉稳的公考红 */
            --secondary: #ea580c;
            --xc-color: #0284c7; /* 行测蓝 */
            --sl-color: #0d9488; /* 申论青 */
            --bg: #f8fafc;
            --card-bg: #ffffff;
            --text: #1e293b;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background-color: var(--bg);
            color: var(--text);
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 900px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            padding: 25px 0;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border-radius: 16px;
            margin-bottom: 25px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        header h1 { margin: 0; font-size: 2.2rem; letter-spacing: 2px; }
        header p { margin: 8px 0 0 0; opacity: 0.9; font-size: 1rem; }

        .grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 20px;
            margin-bottom: 25px;
        }

        @media(min-width: 768px) {
            .grid { grid-template-columns: repeat(2, 1fr); }
            .full-width { grid-column: span 2; }
        }

        .card {
            background: var(--card-bg);
            padding: 20px;
            border-radius: 16px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
            border: 1px solid #e2e8f0;
        }

        .card h2 {
            margin-top: 0;
            font-size: 1.3rem;
            color: #0f172a;
            border-bottom: 2px solid #f1f5f9;
            padding-bottom: 8px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* 科目专属标签 */
        .badge-xc { background: #e0f2fe; color: var(--xc-color); padding: 2px 8px; border-radius: 4px; font-size: 0.8rem; }
        .badge-sl { background: #ccfbf1; color: var(--sl-color); padding: 2px 8px; border-radius: 4px; font-size: 0.8rem; }

        /* 进度条 */
        .progress-box {
            background: #f1f5f9;
            border-radius: 8px;
            height: 12px;
            margin: 15px 0;
            overflow: hidden;
        }
        .progress-bar {
            background: linear-gradient(90deg, var(--secondary), var(--primary));
            height: 100%;
            width: 0%;
            transition: width 0.3s;
        }

        /* 学习清单样式 */
        .task-group { margin-bottom: 15px; }
        .task-title { font-weight: bold; font-size: 1rem; margin-bottom: 8px; color: #334155; }
        .todo-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px 10px;
            background: #f8fafc;
            border-radius: 8px;
            margin-bottom: 6px;
            border-left: 4px solid #cbd5e1;
        }
        .todo-item.xc-style { border-left-color: var(--xc-color); }
        .todo-item.sl-style { border-left-color: var(--sl-color); }
        
        .todo-item input[type="checkbox"] { width: 18px; height: 18px; cursor: pointer; }
        .todo-item label { cursor: pointer; flex-grow: 1; }

        /* 按钮 */
        button {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            width: 100%;
            transition: opacity 0.2s;
        }
        button:hover { opacity: 0.9; }

        /* 番茄钟 */
        .timer-container { text-align: center; padding: 10px 0; }
        .timer-display { font-size: 3.5rem; font-weight: bold; color: #dc2626; font-family: monospace; margin: 10px 0; }

        /* 背诵卡片 */
        .recite-box {
            background: #fff7ed;
            border: 1px dashed #fed7aa;
            padding: 15px;
            border-radius: 12px;
            margin-top: 10px;
        }
        .recite-tips { font-size: 0.9rem; color: #7c2d12; margin-bottom: 10px; }

        /* 错题本 */
        textarea {
            width: 100%; height: 70px; padding: 10px; border-radius: 8px;
            border: 1px solid #cbd5e1; box-sizing: border-box; margin-bottom: 10px; resize: none;
        }
        .note-list { max-height: 120px; overflow-y: auto; background: #f1f5f9; padding: 10px; border-radius: 8px; font-size: 0.9rem; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>公考一战成公 · 通关舱</h1>
        <p>听课夯实基础，刷题总结错题，今日事今日毕！</p>
    </header>

    <!-- 总体进度条舱 -->
    <div class="card full-width">
        <h2>📊 今日通关总进度</h2>
        <div class="progress-box">
            <div class="progress-bar" id="totalProgress"></div>
        </div>
        <p style="margin: 0; text-align: right; font-size: 0.9rem; color: #64748b;" id="progressText">今日任务完成度：0%</p>
    </div>

    <div class="grid">
        <!-- 行测规划 -->
        <div class="card">
            <h2>🧩 《行测》核心通关步阀 <span class="badge-xc">行测</span></h2>
            
            <div class="task-group">
                <div class="task-title">① 言语理解与表达</div>
                <div class="todo-item xc-style"><input type="checkbox" class="task-check" id="xc1"><label for="xc1">📺 听课：主旨概括/逻辑填空技巧</label></div>
                <div class="todo-item xc-style"><input type="checkbox" class="task-check" id="xc2"><label for="xc2">✍️ 刷题：言语模块精练20题</label></div>
            </div>

            <div class="task-group">
                <div class="task-title">② 判断推理</div>
                <div class="todo-item xc-style"><input type="checkbox" class="task-check" id="xc3"><label for="xc3">📺 听课：图形推理/逻辑判断逻辑</label></div>
                <div class="todo-item xc-style"><input type="checkbox" class="task-check" id="xc4"><label for="xc4">✍️ 刷题：判断推理精练20题</label></div>
            </div>

            <div class="task-group">
                <div class="task-title">③ 资料分析（重中之重）</div>
                <div class="todo-item xc-style"><input type="checkbox" class="task-check" id="xc5"><label for="xc5">📺 听课：速算技巧与公式熟记</label></div>
                <div class="todo-item xc-style"><input type="checkbox" class="task-check" id="xc6"><label for="xc6">✍️ 刷题：资料分析牢记错题4篇</label></div>
            </div>
        </div>

        <!-- 申论规划 -->
        <div class="card">
            <h2>✍️ 《申论》要素攻坚步阀 <span class="badge-sl">申论</span></h2>

            <div class="task-group">
                <div class="task-title">① 单一题 / 综合分析</div>
                <div class="todo-item sl-style"><input type="checkbox" class="task-check" id="sl1"><label for="sl1">📺 听课：归纳概括核心要素找点法</label></div>
                <div class="todo-item sl-style"><input type="checkbox" class="task-check" id="sl2"><label for="sl2">✍️ 刷题：真题小题精练与格子手写</label></div>
            </div>

            <div class="task-group">
                <div class="task-title">② 公文写作 / 大作文</div>
                <div class="todo-item sl-style"><input type="checkbox" class="task-check" id="sl3"><label for="sl3">📺 听课：公文格式与大作文框架逻辑</label></div>
                <div class="todo-item sl-style"><input type="checkbox" class="task-check" id="sl4"><label for="sl4">✍️ 刷题：完整梳理1篇大作文/公文</label></div>
            </div>
            
            <div class="task-group">
                <div class="task-title">③ 常识积累</div>
                <div class="todo-item sl-style"><input type="checkbox" class="task-check" id="sl5"><label for="sl5">📺 听课：时政热点/法律常识梳理</label></div>
            </div>
        </div>

        <!-- 番茄工作法 -->
        <div class="card">
            <h2>⏱️ 专注时间：番茄计时器</h2>
            <p style="margin: 0; color: #64748b; font-size: 0.9rem;">每听课或刷题25分钟，强制休息5分钟，保持头脑清醒。</p>
            <div class="timer-container">
                <div class="timer-display" id="timer">25:00</div>
                <button id="startBtn" onclick="toggleTimer()">开启专注时间</button>
            </div>
        </div>

        <!-- 主动回忆背诵法 -->
        <div class="card">
            <h2>🧠 对应联动：主动回忆背诵舱</h2>
            <div class="recite-box">
                <div class="recite-tips"><strong>💡 记忆黄金法则（对应今日规划）：</strong></div>
                <p style="margin: 5px 0; font-size: 0.95rem; color: #431407;">
                    1. <strong>行测资料：</strong>合上书，默写出增长率、比重、平均数的公式。<br>
                    2. <strong>申论常识：</strong>闭上眼，尝试复述今天听课学到的申论金句或时政金句。
                </p>
                <button style="background-color: #ea580c; margin-top: 10px;" onclick="startReciteChallenge()">开始“合书”背诵挑战</button>
            </div>
        </div>

        <!-- 错题整理法 -->
        <div class="card full-width">
            <h2>📓 每日复盘：行测错题与申论失分点记录</h2>
            <p style="margin: 0 0 10px 0; color: #64748b; font-size: 0.9rem;">刷题不是目的，弄懂错题才是！写下今天错题的“死因”及避坑第一反应。</p>
            <textarea id="wrongQuestion" placeholder="例子：资料分析又漏看了“比上年同期”！或者是申论找点漏掉了第三段的关键词..."></textarea>
            <button onclick="saveNote()">把这道错题锁进保险箱</button>
            <p></p>
            <div class="note-list" id="notesContainer">目前还没有记录错题，继续保持！</div>
        </div>
    </div>
</div>

<script>
    // 进度条联动逻辑
    const checkboxes = document.querySelectorAll('.task-check');
    checkboxes.forEach(box => {
        box.addEventListener('change', calculateProgress);
    });

    function calculateProgress() {
        const total = checkboxes.length;
        const checked = document.querySelectorAll('.task-check:checked').length;
        const percentage = Math.round((checked / total) * 100);
        
        document.getElementById('totalProgress').style.width = percentage + '%';
        document.getElementById('progressText').textContent = `今日任务完成度：${percentage}%`;
    }

    // 番茄钟逻辑
    let timeLeft = 25 * 60;
    let timerId = null;
    let isRunning = false;

    function updateDisplay() {
        const minutes = Math.floor(timeLeft / 60);
        const seconds = timeLeft % 60;
        document.getElementById('timer').textContent = 
            `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
    }

    function toggleTimer() {
        const btn = document.getElementById('startBtn');
        if (isRunning) {
            clearInterval(timerId);
            btn.textContent = '开启专注时间';
            btn.style.backgroundColor = '#c2410c';
        } else {
            btn.textContent = '暂停';
            btn.style.backgroundColor = '#e2e8f0';
            btn.style.color = '#1e293b';
            timerId = setInterval(() => {
                if (timeLeft > 0) {
                    timeLeft--;
                    updateDisplay();
                } else {
                    clearInterval(timerId);
                    alert('🎉 一个公考番茄钟完成！快闭眼休息5分钟，然后进行“主动回忆”！');
                    timeLeft = 25 * 60;
                    updateDisplay();
                    btn.textContent = '开启专注时间';
                    btn.style.backgroundColor = '#c2410c';
                    btn.style.color = '#fff';
                }
            }, 1000);
        }
        isRunning = !isRunning;
    }

    // 主动回忆挑战
    function startReciteChallenge() {
        alert('🔥 【主动回忆高能挑战】\n\n请立刻闭上眼睛！\n\n尝试在脑海中死磕：刚刚听课或刷题时，最容易错的那个公式或申论核心词是什么？\n\n（撑过30秒再睁眼看书，效果翻倍！）');
    }

    // 错题记录
    let notes = [];
    function saveNote() {
        const input = document.getElementById('wrongQuestion');
        if(!input.value.trim()) return;
        notes.push(input.value);
        input.value = '';
        
        const container = document.getElementById('notesContainer');
        container.innerHTML = notes.map((note, index) => `<div style="margin-bottom:6px; padding-bottom:6px; border-bottom:1px dashed #cbd5e1;">📍 <b>记录 ${index+1}：</b>${note}</div>`).join('');
    }
</script>

</body>
</html>
