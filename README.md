[紫薇.index.html](https://github.com/user-attachments/files/25841477/index.html)
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZiWei Analytics | 现代命理分析模型</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&family=Noto+Sans+SC:wght@300;400;500;700&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    <script src="https://unpkg.com/iztro/dist/index.min.js"></script>

    <style>
        :root {
            --google-blue: #1A73E8;
            --google-blue-hover: #1557B0;
            --google-red: #EA4335;
            --bg-color: #F8F9FA;
            --surface-color: #FFFFFF;
            --text-primary: #202124;
            --text-secondary: #5F6368;
            --border-color: #DADCE0;
        }

        body {
            margin: 0;
            font-family: 'Roboto', 'Noto Sans SC', sans-serif;
            background-color: var(--bg-color);
            color: var(--text-primary);
            display: flex;
            flex-direction: column;
            min-height: 100vh;
        }

        /* 顶部导航 */
        header {
            background: var(--surface-color);
            padding: 16px 24px;
            box-shadow: 0 1px 2px 0 rgba(60,64,67,0.3);
            display: flex;
            align-items: center;
        }
        .logo {
            font-size: 22px;
            font-weight: 500;
            color: var(--text-primary);
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .logo span { color: var(--google-blue); }

        /* 首页居中搜索框容器 */
        #search-view {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        .search-card {
            background: var(--surface-color);
            padding: 40px;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 500px;
            text-align: center;
        }
        .search-card h1 {
            font-weight: 400;
            margin-bottom: 30px;
        }

        /* 表单样式 */
        .input-group {
            margin-bottom: 20px;
            text-align: left;
        }
        label {
            display: block;
            font-size: 14px;
            color: var(--text-secondary);
            margin-bottom: 8px;
        }
        input[type="date"], select, .radio-group {
            width: 100%;
            padding: 12px 16px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 16px;
            box-sizing: border-box;
            outline: none;
            transition: border 0.3s;
        }
        input:focus, select:focus {
            border-color: var(--google-blue);
            box-shadow: 0 0 0 2px rgba(26,115,232,0.2);
        }
        .radio-group { display: flex; gap: 20px; border: none; padding: 0; }
        
        .btn-primary {
            background: var(--google-blue);
            color: white;
            border: none;
            padding: 12px 32px;
            font-size: 16px;
            border-radius: 24px;
            cursor: pointer;
            font-weight: 500;
            transition: background 0.3s, box-shadow 0.3s;
            margin-top: 10px;
        }
        .btn-primary:hover {
            background: var(--google-blue-hover);
            box-shadow: 0 1px 3px rgba(0,0,0,0.2);
        }

        /* 命盘控制台容器 (隐藏) */
        #dashboard-view {
            display: none;
            padding: 24px;
            flex: 1;
            gap: 24px;
            max-width: 1400px;
            margin: 0 auto;
            width: 100%;
            box-sizing: border-box;
        }

        @media(min-width: 1024px) {
            #dashboard-view { flex-direction: row; }
        }

        /* 左侧：紫微命盘 12宫格 (Grid) */
        .chart-container {
            flex: 1.2;
            background: var(--surface-color);
            border-radius: 12px;
            padding: 16px;
            box-shadow: 0 1px 2px 0 rgba(60,64,67,0.3);
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            grid-template-rows: repeat(4, 1fr);
            gap: 8px;
            aspect-ratio: 1 / 1;
            max-height: 800px;
        }

        .palace {
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 8px;
            display: flex;
            flex-direction: column;
            cursor: pointer;
            transition: background 0.2s, box-shadow 0.2s;
            position: relative;
        }
        .palace:hover {
            box-shadow: 0 1px 3px rgba(0,0,0,0.2);
            border-color: var(--google-blue);
        }

        .palace-name {
            font-size: 12px;
            color: var(--text-secondary);
            position: absolute;
            bottom: 8px;
            right: 8px;
        }
        .stars-major { font-weight: 500; color: var(--google-red); font-size: 14px;}
        .stars-minor { font-size: 12px; color: var(--text-secondary); margin-top: 4px;}

        /* 定位 12 宫 (顺时针，寅起) */
        .p-yin { grid-area: 4 / 1 / 5 / 2; }
        .p-mao { grid-area: 3 / 1 / 4 / 2; }
        .p-chen { grid-area: 2 / 1 / 3 / 2; }
        .p-si { grid-area: 1 / 1 / 2 / 2; }
        .p-wu { grid-area: 1 / 2 / 2 / 3; }
        .p-wei { grid-area: 1 / 3 / 2 / 4; }
        .p-shen { grid-area: 1 / 4 / 2 / 5; }
        .p-you { grid-area: 2 / 4 / 3 / 5; }
        .p-xu { grid-area: 3 / 4 / 4 / 5; }
        .p-hai { grid-area: 4 / 4 / 5 / 5; }
        .p-zi { grid-area: 4 / 3 / 5 / 4; }
        .p-chou { grid-area: 4 / 2 / 5 / 3; }

        /* 中盘信息 */
        .center-info {
            grid-area: 2 / 2 / 4 / 4;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            background: var(--bg-color);
            border-radius: 8px;
        }

        /* 右侧：深度解析 */
        .analysis-container {
            flex: 1;
            background: var(--surface-color);
            border-radius: 12px;
            box-shadow: 0 1px 2px 0 rgba(60,64,67,0.3);
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .tabs {
            display: flex;
            border-bottom: 1px solid var(--border-color);
        }
        .tab {
            flex: 1;
            text-align: center;
            padding: 16px;
            cursor: pointer;
            font-weight: 500;
            color: var(--text-secondary);
            border-bottom: 2px solid transparent;
            transition: color 0.3s, border-color 0.3s;
        }
        .tab.active {
            color: var(--google-blue);
            border-bottom-color: var(--google-blue);
        }

        .tab-content { padding: 24px; overflow-y: auto; display: none; }
        .tab-content.active { display: block; }
        
        .info-card {
            background: #E8F0FE; /* Google light blue */
            border-radius: 8px;
            padding: 16px;
            margin-bottom: 16px;
        }
        .info-card h3 { margin: 0 0 8px 0; color: var(--google-blue); font-size: 16px;}
        .info-card p { margin: 0; font-size: 14px; line-height: 1.6; }

        .warning-card {
            background: #FCE8E6; /* Google light red */
            border-radius: 8px;
            padding: 16px;
            margin-bottom: 16px;
        }
        .warning-card h3 { margin: 0 0 8px 0; color: var(--google-red); font-size: 16px;}
    </style>
</head>
<body>

    <header>
        <div class="logo">
            <span class="material-icons">analytics</span>
            ZiWei <span>Analytics</span>
        </div>
        <div style="flex: 1;"></div>
        <button class="btn-primary" style="padding: 8px 16px; font-size: 14px; border-radius: 4px;" onclick="location.reload()">重新输入</button>
    </header>

    <div id="search-view">
        <div class="search-card">
            <h1>生成命运分析模型</h1>
            <p style="color: var(--text-secondary); margin-bottom: 24px; font-size: 14px;">基于《中州派初级讲义》与《紫微斗数精成》算法</p>
            
            <div class="input-group radio-group">
                <label><input type="radio" name="gender" value="M" checked> 男 (阳/阴)</label>
                <label><input type="radio" name="gender" value="F"> 女 (阴/阳)</label>
            </div>

            <div class="input-group">
                <label>公历出生日期</label>
                <input type="date" id="birthDate" value="1990-01-01">
            </div>

            <div class="input-group">
                <label>出生时辰</label>
                <select id="birthTime">
                    <option value="0">子时 (23:00 - 01:00)</option>
                    <option value="1">丑时 (01:00 - 03:00)</option>
                    <option value="2">寅时 (03:00 - 05:00)</option>
                    <option value="3">卯时 (05:00 - 07:00)</option>
                    <option value="4">辰时 (07:00 - 09:00)</option>
                    <option value="5">巳时 (09:00 - 11:00)</option>
                    <option value="6" selected>午时 (11:00 - 13:00)</option>
                    <option value="7">未时 (13:00 - 15:00)</option>
                    <option value="8">申时 (15:00 - 17:00)</option>
                    <option value="9">酉时 (17:00 - 19:00)</option>
                    <option value="10">戌时 (19:00 - 21:00)</option>
                    <option value="11">亥时 (21:00 - 23:00)</option>
                </select>
            </div>

            <button class="btn-primary" onclick="generateChart()">运行分析计算</button>
        </div>
    </div>

    <div id="dashboard-view">
        
        <div class="chart-container" id="astrolabe-grid">
            <div class="center-info" id="center-info">
                <h2>载入中...</h2>
            </div>
            
            </div>

        <div class="analysis-container">
            <div class="tabs">
                <div class="tab active" onclick="switchTab(0)">基础概览</div>
                <div class="tab" onclick="switchTab(1)">中州派推理</div>
                <div class="tab" onclick="switchTab(2)">大限流年</div>
            </div>

            <div class="tab-content active" id="tab-0">
                <h2 style="font-weight: 400; margin-top: 0;">性格与潜能分析</h2>
                <p style="color: var(--text-secondary); font-size: 14px;">参考《紫微斗数精成》星情查阅字典</p>
                <div id="basic-analysis">
                    </div>
            </div>

            <div class="tab-content" id="tab-1">
                <h2 style="font-weight: 400; margin-top: 0;">趋吉避凶指南</h2>
                <p style="color: var(--text-secondary); font-size: 14px;">参考《中州派紫微斗数初级讲义》非宿命论推理</p>
                
                <div class="info-card">
                    <h3><span class="material-icons" style="vertical-align: middle; font-size: 18px;">lightbulb</span> 星系互涉 (星曜互涉)</h3>
                    <p>中州派认为，星曜不可单看。您命盘中的 <strong>[主星组合]</strong> 显示出极强的开创力，但需注意在行运不佳时避免盲目投资。</p>
                </div>

                <div class="warning-card">
                    <h3><span class="material-icons" style="vertical-align: middle; font-size: 18px;">warning</span> 风险提示与化解</h3>
                    <p>斗数不主张宿命。若发现夫妻宫或财帛宫见 <strong>[擎羊/陀罗]</strong> 等煞曜，并不代表必定离婚或破产，而是提示“波折”。建议：聚少离多、或从事拿手术刀/利器相关职业以化解煞气。</p>
                </div>
            </div>

            <div class="tab-content" id="tab-2">
                <h2 style="font-weight: 400; margin-top: 0;">时光轴 (Timeline)</h2>
                <p>四化寻契机：大限如地，流年如人。以下为核心四化引发的生命转折点追踪（该模块需后续深度运算）。</p>
                <ul style="line-height: 2;">
                    <li><strong>生年四化</strong>：定一生基调。</li>
                    <li><strong>大限四化</strong>：定十年大势。</li>
                    <li><strong>流年四化</strong>：定当年吉凶。</li>
                </ul>
            </div>
        </div>
    </div>

    <script>
        // 宫位地支的 CSS class 映射 (从寅起，顺时针)
        const dzClassMap = [
            'p-yin', 'p-mao', 'p-chen', 'p-si', 
            'p-wu', 'p-wei', 'p-shen', 'p-you', 
            'p-xu', 'p-hai', 'p-zi', 'p-chou'
        ];

        function switchTab(index) {
            document.querySelectorAll('.tab').forEach((el, i) => {
                el.className = i === index ? 'tab active' : 'tab';
            });
            document.querySelectorAll('.tab-content').forEach((el, i) => {
                el.className = i === index ? 'tab-content active' : 'tab-content';
            });
        }

        function generateChart() {
            const dateStr = document.getElementById('birthDate').value;
            const timeIndex = document.getElementById('birthTime').value;
            const gender = document.querySelector('input[name="gender"]:checked').value;

            if (!dateStr) return alert("请输入出生日期");

            // 切换 UI 状态
            document.getElementById('search-view').style.display = 'none';
            document.getElementById('dashboard-view').style.display = 'flex';

            try {
                // 调用 iztro 库进行排盘
                // iztro 接受参数: solarDate (YYYY-MM-DD), timeIndex (0为子时), gender (M/F)
                const astrolabe = iztro.astrolabeBySolarDate(dateStr, parseInt(timeIndex), gender);
                
                renderChart(astrolabe);
                renderAnalysis(astrolabe);
            } catch (error) {
                console.error(error);
                alert("排盘库加载或计算出错，请刷新重试！");
            }
        }

        function renderChart(astrolabe) {
            const grid = document.getElementById('astrolabe-grid');
            
            // 清理之前的宫位（保留 center-info）
            const centerInfo = document.getElementById('center-info');
            grid.innerHTML = '';
            grid.appendChild(centerInfo);

            // 更新中盘信息
            centerInfo.innerHTML = `
                <h3 style="margin:0; color:var(--google-blue); font-weight:400;">${astrolabe.fiveElementsClass}</h3>
                <p style="margin:5px 0 0 0; font-size:14px; color:var(--text-secondary);">
                    ${astrolabe.gender === 'M' ? '乾造 (男)' : '坤造 (女)'}<br>
                    命主: ${astrolabe.soul}<br>
                    身主: ${astrolabe.body}
                </p>
            `;

            // 渲染 12 宫
            astrolabe.palaces.forEach((palace, index) => {
                const div = document.createElement('div');
                // 这里的 index 从寅(0)开始，与我们的 CSS 类严格对应
                div.className = `palace ${dzClassMap[index]}`;
                
                // 提取主星
                const majorStars = palace.majorStars.map(s => s.name).join(' ');
                // 提取吉凶辅星
                const minorStars = palace.minorStars.map(s => s.name).join(' ');

                div.innerHTML = `
                    <div class="stars-major">${majorStars || '无主星'}</div>
                    <div class="stars-minor">${minorStars}</div>
                    <div class="palace-name">${palace.name}</div>
                `;

                // 交互：点击高亮三方四正
                div.onclick = () => highlightSanFangSiZheng(index);

                grid.appendChild(div);
            });
        }

        function highlightSanFangSiZheng(targetIndex) {
            // 清除旧高亮
            document.querySelectorAll('.palace').forEach(el => {
                el.style.backgroundColor = 'transparent';
                el.style.borderColor = 'var(--border-color)';
            });

            // 计算三方四正的索引
            // 斗数中，三合为顺逆数第4个宫位（即 +4, +8 取余），对宫为相冲的第6个宫位（+6 取余）
            const sanFang = [
                targetIndex, 
                (targetIndex + 4) % 12, 
                (targetIndex + 8) % 12, 
                (targetIndex + 6) % 12
            ];

            const palaces = document.querySelectorAll('.palace');
            
            sanFang.forEach((idx, i) => {
                const el = palaces[idx];
                if(el) {
                    if (i === 0) {
                        el.style.backgroundColor = '#E8F0FE'; // 本宫浅蓝
                        el.style.borderColor = 'var(--google-blue)';
                    } else if (i === 3) {
                        el.style.backgroundColor = '#FCE8E6'; // 对宫浅红
                        el.style.borderColor = 'var(--google-red)';
                    } else {
                        el.style.backgroundColor = '#E6F4EA'; // 三合浅绿
                        el.style.borderColor = '#1E8E3E';
                    }
                }
            });
        }

        function renderAnalysis(astrolabe) {
            // 获取命宫数据
            const mingGong = astrolabe.palaces.find(p => p.name === '命宫');
            const stars = mingGong.majorStars.map(s => s.name).join('、');

            const container = document.getElementById('basic-analysis');
            container.innerHTML = `
                <div style="margin-bottom: 20px;">
                    <div style="font-size: 14px; color: var(--text-secondary);">核心命局</div>
                    <div style="font-size: 24px; color: var(--google-blue); font-weight: 500;">
                        命宫坐 【 ${stars || '无主星'} 】
                    </div>
                </div>
                <p style="font-size: 15px; line-height: 1.6;">
                    按《紫微斗数精成》所述，命宫是人生的枢纽。您的命宫状态决定了您一生的抗压能力与最高成就限额。
                </p>
                <div style="background: #f1f3f4; padding: 12px; border-radius: 8px; margin-top: 16px;">
                    <strong style="color: #202124;">《中州派》点拨：</strong><br>
                    <span style="font-size:14px; color: var(--text-secondary);">
                        面对星盘，中州派主张：若命宫无主星，需借对宫（迁移宫）星曜看。切勿死记硬背吉凶，见煞不一定凶，可能激发斗志；见吉不一定全美，可能滋生懒惰。
                    </span>
                </div>
            `;
            
            // 初始化点击一下命宫，高亮它的三方四正
            const mingIndex = astrolabe.palaces.findIndex(p => p.name === '命宫');
            highlightSanFangSiZheng(mingIndex);
        }
    </script>
</body>
</html>
