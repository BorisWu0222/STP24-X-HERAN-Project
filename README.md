<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>STP24 X 禾聯家電 專案成果Demo</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Microsoft JhengHei', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .header {
            text-align: center;
            margin-bottom: 30px;
            background: rgba(255, 255, 255, 0.95);
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }
        
        .header h1 {
            color: #2c3e50;
            font-size: 2.5em;
            margin-bottom: 10px;
        }
        
        .header p {
            color: #7f8c8d;
            font-size: 1.1em;
        }
        
        .upload-section {
            background: rgba(255, 255, 255, 0.95);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }
        
        .upload-section h2 {
            color: #2c3e50;
            margin-bottom: 20px;
            font-size: 1.5em;
        }
        
        .upload-row {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            align-items: center;
        }
        
        .upload-group {
            flex: 1;
        }
        
        .upload-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #34495e;
        }
        
        .file-input {
            width: 100%;
            padding: 12px;
            border: 2px dashed #3498db;
            border-radius: 8px;
            background: #f8f9fa;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .file-input:hover {
            border-color: #2980b9;
            background: #e3f2fd;
        }
        
        .btn {
            background: linear-gradient(45deg, #3498db, #2980b9);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
        }
        
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
        }
        
        .controls-section {
            background: rgba(255, 255, 255, 0.95);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }
        
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 3px solid #3498db;
        }
        
        .section-header h2 {
            color: #2c3e50;
            font-size: 1.8em;
            margin: 0;
        }
        
        .current-weights {
            display: flex;
            gap: 20px;
        }
        
        .weight-display {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9em;
        }
        
        .formula-display {
            background: #f8f9fa;
            border: 2px solid #e9ecef;
            border-radius: 12px;
            padding: 20px;
            margin-bottom: 25px;
        }
        
        .formula-display h4 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 1.2em;
        }
        
        .formula-text {
            background: #ffffff;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
            font-family: 'Courier New', monospace;
            font-size: 0.9em;
            line-height: 1.6;
            color: #495057;
            overflow-x: auto;
        }
        
        .bonus-rules {
            background: #ffffff;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 15px;
        }
        
        .rule-step {
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #e9ecef;
        }
        
        .rule-step:last-child {
            border-bottom: none;
            margin-bottom: 0;
        }
        
        .rule-step strong {
            color: #2c3e50;
            font-size: 1.1em;
            display: block;
            margin-bottom: 10px;
        }
        
        .rule-step ul {
            margin: 10px 0;
            padding-left: 20px;
        }
        
        .rule-step li {
            margin-bottom: 5px;
            color: #495057;
        }
        
        .rule-step p {
            margin: 8px 0;
            color: #495057;
        }
        
        .rule-step span {
            color: #e74c3c;
            font-weight: bold;
        }
        
        .controls-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        
        .control-group h3 {
            color: #2c3e50;
            margin-bottom: 20px;
            font-size: 1.3em;
        }
        
        .sub-weights {
            margin-left: 20px;
            padding-left: 20px;
            border-left: 3px solid #ecf0f1;
        }
        
        .slider-group {
            margin-bottom: 20px;
        }
        
        .slider-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #34495e;
        }
        
        .slider-container {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .slider {
            flex: 1;
            height: 6px;
            border-radius: 3px;
            background: #ddd;
            outline: none;
            -webkit-appearance: none;
        }
        
        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: #3498db;
            cursor: pointer;
        }
        
        .slider-value {
            min-width: 60px;
            text-align: center;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #34495e;
        }
        
        .input-group input {
            width: 100%;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 1em;
        }
        
        .input-row {
            display: flex;
            gap: 20px;
            align-items: flex-start;
        }
        
        .dashboard-summary {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
            border: 2px solid #ecf0f1;
        }
        
        .dashboard-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 15px;
            font-weight: bold;
        }
        
        .dashboard-label {
            color: #2c3e50;
        }
        
        .dashboard-value {
            color: #e74c3c;
            font-size: 1.2em;
        }
        
        .dashboard-chart {
            margin-top: 15px;
            width: 100%;
            max-width: 100%;
            height: 180px;
            overflow-x: auto;
        }
        
        .weight-warning {
            color: #e74c3c;
            font-weight: bold;
            margin-top: 20px;
            padding: 15px;
            background: #ffeaa7;
            border-radius: 8px;
            border: 1px solid #fdcb6e;
            text-align: center;
        }
        
        .results-section {
            background: rgba(255, 255, 255, 0.95);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 30px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }
        
        .summary-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .summary-card {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            border-radius: 12px;
            text-align: center;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }
        
        .summary-card h3 {
            font-size: 1.2em;
            margin-bottom: 10px;
        }
        
        .summary-card .value {
            font-size: 2em;
            font-weight: bold;
        }
        
        .charts-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 30px;
            max-width: 100%;
        }
        
        .chart-card {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            min-width: 0;
            max-width: 100%;
            height: 350px;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
        }

        .chart-card canvas {
            width: 100% !important;
            height: 260px !important;
            max-width: 100%;
            max-height: 260px;
            display: block;
            margin: 0 auto;
        }

        /* 限制 bonusStackChart 的最大高度 */
        #bonusStackChart {
            width: 100% !important;
            height: 150px !important;
            max-width: 100%;
            max-height: 150px;
            display: block;
            margin: 0 auto;
        }
        
        .chart-card h3 {
            text-align: center;
            margin-bottom: 20px;
            color: #2c3e50;
        }
        
        .table-container {
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            margin: 30px auto;
            max-width: 1400px;
        }
        
        .table-container h3 {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 20px;
            margin: 0;
            text-align: center;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
        }
        
        th, td {
            padding: 12px;
            text-align: center;
            border-bottom: 1px solid #eee;
        }
        
        th {
            background: #f8f9fa;
            font-weight: bold;
            color: #2c3e50;
        }
        
        tbody tr:hover {
            background: #f8f9fa;
        }
        
        .grade-s { color: #e74c3c; font-weight: bold; }
        .grade-a { color: #f39c12; font-weight: bold; }
        .grade-b { color: #3498db; font-weight: bold; }
        
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>STP24 X 禾聯家電 專案成果Demo</h1>
            <p>從數據到價值：AI 驅動的智能 KPI 洞察</p>
        </div>
        
        <div class="upload-section">
            <h2>📁 檔案上傳</h2>
            <div class="upload-row">
                <div class="upload-group">
                    <label for="salesFile">銷售單據檔案 (Excel)</label>
                    <input type="file" id="salesFile" class="file-input" accept=".xlsx,.xls" />
                </div>
                <div class="upload-group">
                    <label for="kpiFile">業務員KPI目標檔案 (Excel)</label>
                    <input type="file" id="kpiFile" class="file-input" accept=".xlsx,.xls" />
                </div>
            </div>
            <button class="btn" id="processBtn">🚀 開始分析</button>
        </div>
        
        <div class="controls-section">
            <div class="section-header">
                <h2>📊 KPI權重調整</h2>
                <div class="current-weights">
                    <span class="weight-display">策略型: <strong id="headerStrategyWeight">30%</strong></span>
                    <span class="weight-display">營運型: <strong id="headerOperationWeight">70%</strong></span>
                </div>
            </div>
            
            <div class="formula-display">
                <h4>📝 當前KPI計算公式：</h4>
                <div class="formula-text" id="kpiFormula">
                    (A產品銷售額比例達成率 × 45% + A產品客戶數達成率 × 55%) × 30% + (銷售額達成率 × 30% + 毛利率達成率 × 35% + 新客戶營收占比達成率 × 20% + 客戶服務滿意度達成率 × 15%) × 70%
                </div>
            </div>
            
            <div class="controls-grid">
                <div class="control-group">
                    <h3>📊 策略型KPI權重調整</h3>
                    <div class="slider-group">
                        <label>策略型KPI權重</label>
                        <div class="slider-container">
                            <input type="range" class="slider" id="strategyWeight" min="0" max="100" value="30">
                            <span class="slider-value" id="strategyWeightValue">30%</span>
                        </div>
                    </div>
                    <div class="sub-weights">
                        <div class="slider-group">
                            <label>A產品銷售額比例</label>
                            <div class="slider-container">
                                <input type="range" class="slider" id="aProductRatioWeight" min="0" max="100" value="45">
                                <span class="slider-value" id="aProductRatioWeightValue">45%</span>
                            </div>
                        </div>
                        <div class="slider-group">
                            <label>A產品客戶數</label>
                            <div class="slider-container">
                                <input type="range" class="slider" id="aProductCustomersWeight" min="0" max="100" value="55">
                                <span class="slider-value" id="aProductCustomersWeightValue">55%</span>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="control-group">
                    <h3>📈 營運型KPI權重調整</h3>
                    <div class="slider-group">
                        <label>營運型KPI權重</label>
                        <div class="slider-container">
                            <input type="range" class="slider" id="operationWeight" min="0" max="100" value="70">
                            <span class="slider-value" id="operationWeightValue">70%</span>
                        </div>
                    </div>
                    <div class="sub-weights">
                        <div class="slider-group">
                            <label>銷售額達成率</label>
                            <div class="slider-container">
                                <input type="range" class="slider" id="salesWeight" min="0" max="100" value="30">
                                <span class="slider-value" id="salesWeightValue">30%</span>
                            </div>
                        </div>
                        <div class="slider-group">
                            <label>毛利率達成率</label>
                            <div class="slider-container">
                                <input type="range" class="slider" id="profitWeight" min="0" max="100" value="35">
                                <span class="slider-value" id="profitWeightValue">35%</span>
                            </div>
                        </div>
                        <div class="slider-group">
                            <label>新客戶營收占比</label>
                            <div class="slider-container">
                                <input type="range" class="slider" id="newCustomerWeight" min="0" max="100" value="20">
                                <span class="slider-value" id="newCustomerWeightValue">20%</span>
                            </div>
                        </div>
                        <div class="slider-group">
                            <label>客戶服務滿意度</label>
                            <div class="slider-container">
                                <input type="range" class="slider" id="satisfactionWeight" min="0" max="100" value="15">
                                <span class="slider-value" id="satisfactionWeightValue">15%</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="weight-warning" id="weightWarning" style="display: none;">
                ⚠️ 總權重不等於100%，請調整！
            </div>
        </div>
        
        <div class="controls-section">
            <div class="section-header">
                <h2>💰 獎金設定</h2>
                <div class="current-weights">
                    <span class="weight-display">總預算: <strong id="headerTotalBudget">$5,000,000</strong></span>
                    <span class="weight-display">個人上限: <strong id="headerMaxBonus">$200,000</strong></span>
                </div>
            </div>
            
            <div class="formula-display">
                <h4>💰 獎金計算規則：</h4>
                <div class="bonus-rules">
                    <div class="rule-step">
                        <strong>第一關：最低門檻</strong>
                        <ul>
                            <li>A產品銷售額比例 ≥ 10%，否則獎金歸零</li>
                            <li>客戶服務滿意度 ≥ 70%，否則扣除10%獎金</li>
                        </ul>
                    </div>
                    
                    <div class="rule-step">
                        <strong>第二關：分級基礎</strong>
                        <div class="bonus-table">
                            <table style="width: 100%; border-collapse: collapse; margin: 15px 0;">
                                <thead>
                                    <tr style="background: #f8f9fa;">
                                        <th style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">等第組合</th>
                                        <th style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">說明</th>
                                        <th style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">權重</th>
                                        <th style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">基礎獎金</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center; font-weight: bold;">SS</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6;">頂尖表現者：策略型70+ 且 營運型70+</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">10.0</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;"><span id="bonusS" style="color:#e74c3c; font-weight:bold;">$100,000</span></td>
                                    </tr>
                                    <tr>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center; font-weight: bold;">SA/AS</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6;">優秀表現者：策略型70+, 營運型40-70 或相反</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">6.0</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;"><span id="bonusSA" style="color:#e74c3c; font-weight:bold;">$75,000</span></td>
                                    </tr>
                                    <tr>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center; font-weight: bold;">SB/BS</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6;">偏科表現者：策略型70+, 營運型≤40 或相反</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">4.5</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;"><span style="color:#e74c3c; font-weight:bold;">$60,000</span></td>
                                    </tr>
                                    <tr>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center; font-weight: bold;">AA</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6;">穩定表現者：策略型40-70 且 營運型40-70</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">3.0</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;"><span id="bonusAA" style="color:#e74c3c; font-weight:bold;">$60,000</span></td>
                                    </tr>
                                    <tr>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center; font-weight: bold;">AB/BA</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6;">一般表現者：策略型40-70, 營運型≤40 或相反</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">1.8</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;"><span id="bonusOther" style="color:#e74c3c; font-weight:bold;">$40,000</span></td>
                                    </tr>
                                    <tr>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center; font-weight: bold;">BB</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6;">待改進者：策略型≤40 且 營運型≤40</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;">1.0</td>
                                        <td style="padding: 10px; border: 1px solid #dee2e6; text-align: center;"><span id="bonusB" style="color:#e74c3c; font-weight:bold;">$20,000</span></td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    
                    <div class="rule-step">
                        <strong>第三關：個人Bonus (如果營運型KPI超過100)</strong>
                        <p style="margin: 10px 0; font-weight: bold;">(實際銷售額 - 目標銷售額) × 平均毛利率 × 分成率 (超過100越多分成率越高)</p>
                        
                        <div class="bonus-table">
                            <table style="width: 60%; border-collapse: collapse; margin: 15px 0;">
                                <thead>
                                    <tr style="background: #f8f9fa;">
                                        <th style="padding: 8px; border: 1px solid #dee2e6; text-align: center;">營運型KPI分數</th>
                                        <th style="padding: 8px; border: 1px solid #dee2e6; text-align: center;">分成率</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td style="padding: 8px; border: 1px solid #dee2e6; text-align: center;">100 < x ≤ 120</td>
                                        <td style="padding: 8px; border: 1px solid #dee2e6; text-align: center; color:#e74c3c; font-weight:bold;">15%</td>
                                    </tr>
                                    <tr>
                                        <td style="padding: 8px; border: 1px solid #dee2e6; text-align: center;">120 < x ≤ 130</td>
                                        <td style="padding: 8px; border: 1px solid #dee2e6; text-align: center; color:#e74c3c; font-weight:bold;">20%</td>
                                    </tr>
                                    <tr>
                                        <td style="padding: 8px; border: 1px solid #dee2e6; text-align: center;">130 < x ≤ 140</td>
                                        <td style="padding: 8px; border: 1px solid #dee2e6; text-align: center; color:#e74c3c; font-weight:bold;">28%</td>
                                    </tr>
                                </tbody>
                            </table>
                            <p style="margin: 10px 0; color: #666;">分成率隨超額分數指數增長，受個人上限 <span id="maxBonusDisplay">$200,000</span> 限制</p>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="controls-grid">
                <div class="control-group">
                    <h3>💰 獎金預算設定</h3>
                    <div class="input-row">
                        <div class="input-group" style="flex: 1; margin-right: 20px;">
                            <label>總獎金預算 (元)</label>
                            <input type="number" id="totalBudget" value="5000000">
                        </div>
                        <div class="input-group" style="flex: 1;">
                            <label>個人獎金上限 (元)</label>
                            <input type="number" id="maxBonus" value="200000">
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="control-group">
                <h3>📊 獎金儀表板</h3>
                <div class="dashboard-summary">
                    <div class="dashboard-item">
                        <span class="dashboard-label">預估實際發出獎金:</span>
                        <span class="dashboard-value" id="dashboardEstimatedPayout">$0</span>
                    </div>
                    <div class="dashboard-chart">
                        <canvas id="bonusStackChart" style="height: 150px;"></canvas>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="results-section hidden" id="resultsSection">
            <h2>📈 分析結果</h2>
            
            <div class="summary-cards">
                <div class="summary-card">
                    <h3>總獎金預算</h3>
                    <div class="value" id="totalBudgetDisplay">$5,000,000</div>
                </div>
                <div class="summary-card">
                    <h3>預估發放金額</h3>
                    <div class="value" id="estimatedPayout">$0</div>
                </div>
                <div class="summary-card">
                    <h3>參與人數</h3>
                    <div class="value" id="totalEmployees">0</div>
                </div>
                <div class="summary-card">
                    <h3>平均獎金</h3>
                    <div class="value" id="avgBonus">$0</div>
                </div>
            </div>
            
            <div class="charts-container">
                <div class="chart-card">
                    <h3>獎金分級分布</h3>
                    <canvas id="gradeChart"></canvas>
                </div>
                <div class="chart-card">
                    <h3>獎金金額分布</h3>
                    <canvas id="bonusChart"></canvas>
                </div>
            </div>
        </div>
        
    </div>

    <div class="table-container hidden" id="bonusTableSection">
        <h3>個人獎金明細</h3>
        <table id="bonusTable">
            <thead>
                <tr>
                    <th>業務員</th>
                    <th>策略型評分</th>
                    <th>營運型評分</th>
                    <th>總評分</th>
                    <th>等級</th>
                    <th>基礎獎金</th>
                    <th>績效獎金</th>
                    <th>總獎金</th>
                </tr>
            </thead>
            <tbody id="bonusTableBody">
            </tbody>
        </table>
    </div>
    </div>

    <script>
        // 全域變數
        let salesData = null;
        let kpiData = null;
        let bonusResults = [];
        let gradeChart = null;
        let bonusChart = null;
        let bonusStackChart = null;

        // 初始化
        document.addEventListener('DOMContentLoaded', function() {
            console.log('頁面載入完成');
            
            // 綁定事件
            document.getElementById('processBtn').addEventListener('click', processFiles);
            
            // 綁定滑桿事件
            document.getElementById('strategyWeight').addEventListener('input', function() { updateWeights('strategy'); });
            document.getElementById('operationWeight').addEventListener('input', function() { updateWeights('operation'); });
            document.getElementById('aProductRatioWeight').addEventListener('input', function() { updateSubWeights('strategy'); });
            document.getElementById('aProductCustomersWeight').addEventListener('input', function() { updateSubWeights('strategy'); });
            document.getElementById('salesWeight').addEventListener('input', function() { updateSubWeights('operation'); });
            document.getElementById('profitWeight').addEventListener('input', function() { updateSubWeights('operation'); });
            document.getElementById('newCustomerWeight').addEventListener('input', function() { updateSubWeights('operation'); });
            document.getElementById('satisfactionWeight').addEventListener('input', function() { updateSubWeights('operation'); });
            
            // 綁定輸入框事件
            document.getElementById('totalBudget').addEventListener('input', updateBonus);
            document.getElementById('maxBonus').addEventListener('input', updateBonus);
            
            // 初始化顯示
            updateWeightSummary();
            updateKPIFormula();
            updateBonusRules();
            updateBonusDashboard();
        });

        // 檔案處理
        async function processFiles() {
            console.log('開始處理檔案');
            
            const salesFile = document.getElementById('salesFile').files[0];
            const kpiFile = document.getElementById('kpiFile').files[0];
            
            if (!salesFile || !kpiFile) {
                alert('請選擇兩個檔案');
                return;
            }
            
            try {
                document.getElementById('processBtn').textContent = '處理中...';
                document.getElementById('processBtn').disabled = true;
                
                console.log('讀取銷售檔案...');
                salesData = await readExcel(salesFile);
                console.log('銷售數據:', salesData.length, '筆記錄');
                
                console.log('讀取KPI檔案...');
                kpiData = await readExcel(kpiFile);
                console.log('KPI數據:', kpiData.length, '筆記錄');
                
                console.log('開始計算獎金...');
                calculateBonus();
                displayResults();
                
                document.getElementById('processBtn').textContent = '✅ 分析完成';
                console.log('處理完成！');
                
            } catch (error) {
                console.error('檔案處理錯誤:', error);
                alert('檔案處理失敗: ' + error.message);
                document.getElementById('processBtn').textContent = '🚀 開始分析';
                document.getElementById('processBtn').disabled = false;
            }
        }

        // 讀取Excel檔案
        function readExcel(file) {
            return new Promise((resolve, reject) => {
                const reader = new FileReader();
                reader.onload = function(e) {
                    try {
                        const data = e.target.result;
                        const workbook = XLSX.read(data, { type: 'binary' });
                        const sheetName = workbook.SheetNames[0];
                        const worksheet = workbook.Sheets[sheetName];
                        const jsonData = XLSX.utils.sheet_to_json(worksheet);
                        resolve(jsonData);
                    } catch (error) {
                        reject(new Error('無法讀取Excel檔案: ' + error.message));
                    }
                };
                reader.onerror = function() {
                    reject(new Error('檔案讀取失敗'));
                };
                reader.readAsBinaryString(file);
            });
        }

        // 計算獎金
        function calculateBonus() {
            if (!salesData || !kpiData) {
                console.error('缺少必要的數據');
                return;
            }
            
            bonusResults = [];
            
            kpiData.forEach((employee, index) => {
                const employeeCode = employee['業務員編號'] || employee['員工編號'] || employee['編號'];
                const employeeName = employee['業務員姓名'] || employee['姓名'] || employee['員工姓名'];
                
                if (!employeeCode) {
                    console.warn('第', index + 1, '筆記錄缺少員工編號');
                    return;
                }
                
                const actualKPI = calculateActualKPI(employeeCode);
                const achievementRates = calculateAchievementRates(employee, actualKPI);
                const scores = calculateFinalScores(achievementRates);
                const bonus = calculateEmployeeBonus(scores, actualKPI, employee);
                
                bonusResults.push({
                    code: employeeCode,
                    name: employeeName || employeeCode,
                    strategyScore: scores.strategy,
                    operationScore: scores.operation,
                    totalScore: scores.total,
                    grade: bonus.grade,
                    baseBonus: bonus.base,
                    performanceBonus: bonus.performance,
                    totalBonus: bonus.total
                });
            });
            
            console.log('計算完成，共處理:', bonusResults.length, '筆記錄');
            adjustBonusForBudget();
        }

        // 計算實際KPI值
        function calculateActualKPI(employeeCode) {
            const employeeSales = salesData.filter(record => {
                const recordCode = record['業務員編號'] || record['員工編號'] || record['編號'];
                return recordCode === employeeCode;
            });
            
            if (employeeSales.length === 0) {
                return {
                    aProductRatio: Math.random() * 20,
                    aProductCustomers: Math.floor(Math.random() * 50),
                    totalSales: Math.random() * 1000000,
                    avgProfitMargin: Math.random() * 30,
                    newCustomerRatio: Math.random() * 15,
                    satisfaction: 70 + Math.random() * 25
                };
            }
            
            const totalSales = employeeSales.reduce((sum, record) => {
                const sales = parseFloat(record['銷售金額'] || record['銷售額'] || record['金額'] || 0);
                return sum + sales;
            }, 0);
            
            const aProductSales = employeeSales
                .filter(record => {
                    const productCode = record['銷貨品號'] || record['產品編號'] || '';
                    return productCode === '00E300076-00';
                })
                .reduce((sum, record) => {
                    const sales = parseFloat(record['銷售金額'] || record['銷售額'] || record['金額'] || 0);
                    return sum + sales;
                }, 0);
            
            const aProductCustomers = new Set(
                employeeSales
                    .filter(record => {
                        const productCode = record['銷貨品號'] || record['產品編號'] || '';
                        return productCode === '00E300076-00';
                    })
                    .map(record => record['客戶代號'] || record['客戶'])
            ).size;
            
            const totalProfit = employeeSales.reduce((sum, record) => {
                const profit = parseFloat(record['銷貨毛利'] || record['毛利'] || 0);
                const sales = parseFloat(record['銷售金額'] || record['銷售額'] || record['金額'] || 0);
                return sum + (profit * sales);
            }, 0);
            
            const avgProfitMargin = totalSales > 0 ? (totalProfit / totalSales) * 100 : 0;
            
            return {
                aProductRatio: totalSales > 0 ? (aProductSales / totalSales) * 100 : 0,
                aProductCustomers: aProductCustomers,
                totalSales: totalSales,
                avgProfitMargin: avgProfitMargin,
                newCustomerRatio: Math.random() * 20,
                satisfaction: 75 + Math.random() * 20
            };
        }

        // 計算達成率
        function calculateAchievementRates(employee, actualKPI) {
            const targets = {
                aProductRatio: parseFloat((employee['A產品佔總銷售額的比例'] || '20%').replace('%', '')),
                aProductCustomers: parseInt(employee['購買A產品的客戶數'] || '20'),
                totalSales: parseFloat(employee['總銷售額'] || '500000'),
                avgProfitMargin: parseFloat((employee['平均毛利率'] || '15%').replace('%', '')),
                newCustomerRatio: parseFloat((employee['新客户營收占比'] || '10%').replace('%', '')),
                satisfaction: parseFloat((employee['客戶服務滿意度'] || '80%').replace('%', ''))
            };
            
            return {
                aProductRatio: targets.aProductRatio > 0 ? (actualKPI.aProductRatio / targets.aProductRatio) * 100 : 0,
                aProductCustomers: targets.aProductCustomers > 0 ? (actualKPI.aProductCustomers / targets.aProductCustomers) * 100 : 0,
                totalSales: targets.totalSales > 0 ? (actualKPI.totalSales / targets.totalSales) * 100 : 0,
                avgProfitMargin: targets.avgProfitMargin > 0 ? (actualKPI.avgProfitMargin / targets.avgProfitMargin) * 100 : 0,
                newCustomerRatio: targets.newCustomerRatio > 0 ? (actualKPI.newCustomerRatio / targets.newCustomerRatio) * 100 : 0,
                satisfaction: targets.satisfaction > 0 ? (actualKPI.satisfaction / targets.satisfaction) * 100 : 0
            };
        }

        // 計算最終分數
        function calculateFinalScores(rates) {
            const strategyWeight = parseFloat(document.getElementById('strategyWeight').value) / 100;
            const operationWeight = parseFloat(document.getElementById('operationWeight').value) / 100;
            
            const aProductRatioWeight = parseFloat(document.getElementById('aProductRatioWeight').value) / 100;
            const aProductCustomersWeight = parseFloat(document.getElementById('aProductCustomersWeight').value) / 100;
            
            const salesWeight = parseFloat(document.getElementById('salesWeight').value) / 100;
            const profitWeight = parseFloat(document.getElementById('profitWeight').value) / 100;
            const newCustomerWeight = parseFloat(document.getElementById('newCustomerWeight').value) / 100;
            const satisfactionWeight = parseFloat(document.getElementById('satisfactionWeight').value) / 100;
            
            const strategyScore = (rates.aProductRatio * aProductRatioWeight + rates.aProductCustomers * aProductCustomersWeight);
            const operationScore = (rates.totalSales * salesWeight + rates.avgProfitMargin * profitWeight + rates.newCustomerRatio * newCustomerWeight + rates.satisfaction * satisfactionWeight);
            const totalScore = strategyScore * strategyWeight + operationScore * operationWeight;
            
            return {
                strategy: strategyScore,
                operation: operationScore,
                total: totalScore
            };
        }

        // 計算個人獎金
        function calculateEmployeeBonus(scores, actualKPI, employee) {
            if (actualKPI.aProductRatio < 10) {
                return { grade: 'FAIL', base: 0, performance: 0, total: 0 };
            }
            
            let penaltyRate = actualKPI.satisfaction < 70 ? 0.9 : 1;
            
            const getGrade = (score) => {
                if (score <= 40) return 'B';
                if (score <= 70) return 'A';
                return 'S';
            };
            
            const strategyGrade = getGrade(scores.strategy);
            const operationGrade = getGrade(scores.operation);
            const combinedGrade = strategyGrade + operationGrade;
            
            const baseAmounts = getDefaultBaseAmounts();
            const baseBonus = baseAmounts[combinedGrade] || 0;
            
            let performanceBonus = 0;
            if (scores.operation > 100) {
                const operationScore = scores.operation;
                let shareRate = 0;
                
                if (operationScore > 100 && operationScore <= 120) {
                    shareRate = 0.15;
                } else if (operationScore > 120 && operationScore <= 130) {
                    shareRate = 0.20;
                } else if (operationScore > 130 && operationScore <= 140) {
                    shareRate = 0.28;
                } else if (operationScore > 140) {
                    const excess = operationScore - 140;
                    shareRate = 0.28 + (excess / 100) * 0.1;
                    shareRate = Math.min(shareRate, 0.5);
                }
                
                const targetSales = parseFloat(employee['總銷售額'] || 200000);
                const excessSales = Math.max(0, actualKPI.totalSales - targetSales);
                performanceBonus = excessSales * (actualKPI.avgProfitMargin / 100) * shareRate;
            }
            
            const totalBonus = (baseBonus + performanceBonus) * penaltyRate;
            
            return {
                grade: combinedGrade,
                base: baseBonus * penaltyRate,
                performance: performanceBonus * penaltyRate,
                total: totalBonus
            };
        }

        // 獲取預設基礎獎金
        function getDefaultBaseAmounts() {
            return calculateDynamicBaseBonus();
        }

        // 動態計算基礎獎金分配
        function calculateDynamicBaseBonus() {
            const totalBudget = parseFloat(document.getElementById('totalBudget').value);
            
            let gradeDistribution = {};
            
            if (bonusResults.length > 0) {
                bonusResults.forEach(result => {
                    if (result.grade !== 'FAIL') {
                        gradeDistribution[result.grade] = (gradeDistribution[result.grade] || 0) + 1;
                    }
                });
            } else {
                gradeDistribution = getHistoricalGradeDistribution(10);
            }
            
            const gradeWeights = getStepUpWeights();
            
            let totalWeight = 0;
            Object.entries(gradeDistribution).forEach(([grade, count]) => {
                totalWeight += (gradeWeights[grade] || 1) * count;
            });
            
            const baseAmounts = {};
            const perWeightAmount = totalWeight > 0 ? totalBudget / totalWeight : 0;
            
            Object.keys(gradeWeights).forEach(grade => {
                baseAmounts[grade] = (gradeWeights[grade] || 1) * perWeightAmount;
            });
            
            return baseAmounts;
        }

        // 根據歷史數據估算等級分布
        function getHistoricalGradeDistribution(totalEmployees) {
            const distributionRatios = {
                'SS': 0.05, 'SA': 0.10, 'SB': 0.05, 'AS': 0.10, 'AA': 0.25,
                'AB': 0.25, 'BA': 0.10, 'BS': 0.05, 'BB': 0.05
            };
            
            const estimatedDistribution = {};
            Object.entries(distributionRatios).forEach(([grade, ratio]) => {
                estimatedDistribution[grade] = Math.max(1, Math.round(totalEmployees * ratio));
            });
            
            return estimatedDistribution;
        }

        // 階梯向上的權重設計
        function getStepUpWeights() {
            return {
                'SS': 10.0, 'SA': 6.0, 'SB': 4.5, 'AS': 6.0, 'AA': 3.0,
                'AB': 1.8, 'BA': 1.8, 'BS': 1.5, 'BB': 1.0, 'FAIL': 0
            };
        }

        // 調整獎金以符合預算
        function adjustBonusForBudget() {
            const totalBudget = parseFloat(document.getElementById('totalBudget').value);
            const maxBonus = parseFloat(document.getElementById('maxBonus').value);
            
            const dynamicBaseAmounts = calculateDynamicBaseBonus();
            
            bonusResults.forEach(result => {
                if (result.grade !== 'FAIL') {
                    const newBaseBonus = dynamicBaseAmounts[result.grade] || 0;
                    const currentPenaltyRate = result.baseBonus > 0 ? 
                        (result.baseBonus / getDefaultBaseAmounts()[result.grade]) : 0.9;
                    
                    result.baseBonus = newBaseBonus * Math.min(currentPenaltyRate || 0.9, 1);
                    result.totalBonus = result.baseBonus + result.performanceBonus;
                }
            });
            
            const currentTotal = bonusResults.reduce((sum, result) => sum + result.totalBonus, 0);
            
            if (currentTotal > totalBudget && bonusResults.length > 0) {
                const finalAdjustmentRatio = totalBudget / currentTotal;
                
                bonusResults.forEach(result => {
                    result.baseBonus *= finalAdjustmentRatio;
                    result.performanceBonus *= finalAdjustmentRatio;
                    result.totalBonus *= finalAdjustmentRatio;
                    
                    if (result.totalBonus > maxBonus) {
                        const excess = result.totalBonus - maxBonus;
                        result.totalBonus = maxBonus;
                        result.performanceBonus = Math.max(0, result.performanceBonus - excess);
                    }
                });
            }
        }

        // 顯示結果
        function displayResults() {
            document.getElementById('resultsSection').classList.remove('hidden');
            document.getElementById('bonusTableSection').classList.remove('hidden');
            updateSummaryCards();
            updateCharts();
            updateTable();
            updateBonusDashboard();
        }

        // 更新摘要卡片
        function updateSummaryCards() {
            const totalBudget = parseFloat(document.getElementById('totalBudget').value);
            const estimatedPayout = bonusResults.reduce((sum, result) => sum + result.totalBonus, 0);
            const totalEmployees = bonusResults.length;
            const avgBonus = totalEmployees > 0 ? estimatedPayout / totalEmployees : 0;
            
            document.getElementById('totalBudgetDisplay').textContent = '$' + totalBudget.toLocaleString();
            document.getElementById('estimatedPayout').textContent = '$' + Math.round(estimatedPayout).toLocaleString();
            document.getElementById('totalEmployees').textContent = totalEmployees;
            document.getElementById('avgBonus').textContent = '$' + Math.round(avgBonus).toLocaleString();
        }

        // 更新圖表
        function updateCharts() {
            updateGradeChart();
            updateBonusChart();
        }

        // 更新等級分布圖
        function updateGradeChart() {
            // 定義七種分級
            const gradeLabels = ['2S', '2A', '2B', 'SA', 'SB', 'AB', 'FAIL'];
            const gradeColors = {
                '2S': '#e74c3c',    // 紅
                '2A': '#f39c12',    // 橙
                '2B': '#3498db',    // 藍
                'SA': '#2ecc71',    // 綠
                'SB': '#9b59b6',    // 紫
                'AB': '#1abc9c',    // 青
                'FAIL': '#7f8c8d'   // 灰
            };

            // 統計分級人數
            const gradeCount = {
                '2S': 0,
                '2A': 0,
                '2B': 0,
                'SA': 0,
                'SB': 0,
                'AB': 0,
                'FAIL': 0
            };

            // 依據個人等級分類
            bonusResults.forEach(result => {
                let g = result.grade;
                if (g === 'FAIL') {
                    gradeCount['FAIL']++;
                } else {
                    // 轉換成七大類
                    // 2S: SS, 2A: AA, 2B: BB, SA: SA/AS, SB: SB/BS, AB: AB/BA
                    if (g === 'SS') gradeCount['2S']++;
                    else if (g === 'AA') gradeCount['2A']++;
                    else if (g === 'BB') gradeCount['2B']++;
                    else if (g === 'SA' || g === 'AS') gradeCount['SA']++;
                    else if (g === 'SB' || g === 'BS') gradeCount['SB']++;
                    else if (g === 'AB' || g === 'BA') gradeCount['AB']++;
                }
            });

            const ctx = document.getElementById('gradeChart').getContext('2d');
            if (gradeChart) {
                gradeChart.destroy();
            }
            gradeChart = new Chart(ctx, {
                type: 'doughnut',
                data: {
                    labels: gradeLabels,
                    datasets: [{
                        data: gradeLabels.map(l => gradeCount[l]),
                        backgroundColor: gradeLabels.map(l => gradeColors[l]),
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: true,
                            position: 'bottom',
                            labels: {
                                generateLabels: function(chart) {
                                    // 顯示人數
                                    const data = chart.data;
                                    return data.labels.map((label, i) => {
                                        return {
                                            text: label + ' (' + data.datasets[0].data[i] + '人)',
                                            fillStyle: data.datasets[0].backgroundColor[i],
                                            strokeStyle: data.datasets[0].backgroundColor[i],
                                            index: i
                                        };
                                    });
                                }
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    const label = context.label || '';
                                    const value = context.parsed || 0;
                                    return label + ': ' + value + '人';
                                }
                            }
                        }
                    }
                }
            });
        }

        // 更新獎金分布圖
        function updateBonusChart() {
            const bonusRanges = {
                '0-50K': 0,
                '50K-100K': 0,
                '100K-150K': 0,
                '150K+': 0
            };
            
            bonusResults.forEach(result => {
                if (result.totalBonus < 50000) bonusRanges['0-50K']++;
                else if (result.totalBonus < 100000) bonusRanges['50K-100K']++;
                else if (result.totalBonus < 150000) bonusRanges['100K-150K']++;
                else bonusRanges['150K+']++;
            });
            
            const ctx = document.getElementById('bonusChart').getContext('2d');
            
            if (bonusChart) {
                bonusChart.destroy();
            }
            
            bonusChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: Object.keys(bonusRanges),
                    datasets: [{
                        label: '人數',
                        data: Object.values(bonusRanges),
                        backgroundColor: 'rgba(52, 152, 219, 0.8)',
                        borderColor: 'rgba(52, 152, 219, 1)',
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            ticks: {
                                stepSize: 1
                            }
                        }
                    }
                }
            });
        }

        // 更新表格
        function updateTable() {
            const tbody = document.getElementById('bonusTableBody');
            tbody.innerHTML = '';
            
            bonusResults.forEach(result => {
                const row = document.createElement('tr');
                const gradeClass = result.grade.includes('S') ? 'grade-s' : 
                                  result.grade.includes('A') ? 'grade-a' : 'grade-b';
                
                row.innerHTML = `
                    <td>${result.name}</td>
                    <td>${Math.round(result.strategyScore)}</td>
                    <td>${Math.round(result.operationScore)}</td>
                    <td>${Math.round(result.totalScore)}</td>
                    <td class="${gradeClass}">${result.grade}</td>
                    <td>$${Math.round(result.baseBonus).toLocaleString()}</td>
                    <td>$${Math.round(result.performanceBonus).toLocaleString()}</td>
                    <td><strong>$${Math.round(result.totalBonus).toLocaleString()}</strong></td>
                `;
                
                tbody.appendChild(row);
            });
        }

        // 更新KPI公式顯示
        function updateKPIFormula() {
            const aProductRatio = document.getElementById('aProductRatioWeight').value;
            const aProductCustomers = document.getElementById('aProductCustomersWeight').value;
            const strategyWeight = document.getElementById('strategyWeight').value;
            const salesWeight = document.getElementById('salesWeight').value;
            const profitWeight = document.getElementById('profitWeight').value;
            const newCustomerWeight = document.getElementById('newCustomerWeight').value;
            const satisfactionWeight = document.getElementById('satisfactionWeight').value;
            const operationWeight = document.getElementById('operationWeight').value;
            
            const formula = `(A產品銷售額比例達成率 × ${aProductRatio}% + A產品客戶數達成率 × ${aProductCustomers}%) × ${strategyWeight}% + (銷售額達成率 × ${salesWeight}% + 毛利率達成率 × ${profitWeight}% + 新客戶營收占比達成率 × ${newCustomerWeight}% + 客戶服務滿意度達成率 × ${satisfactionWeight}%) × ${operationWeight}%`;
            
            document.getElementById('kpiFormula').textContent = formula;
        }

        // 更新獎金規則顯示
        function updateBonusRules() {
            const totalBudget = parseFloat(document.getElementById('totalBudget').value);
            const maxBonus = parseFloat(document.getElementById('maxBonus').value);
            const budgetRatio = totalBudget / 5000000;
            
            document.getElementById('bonusS').textContent = '$' + Math.round(100000 * budgetRatio).toLocaleString();
            document.getElementById('bonusSA').textContent = '$' + Math.round(75000 * budgetRatio).toLocaleString();
            document.getElementById('bonusAA').textContent = '$' + Math.round(60000 * budgetRatio).toLocaleString();
            document.getElementById('bonusOther').textContent = '$' + Math.round(40000 * budgetRatio).toLocaleString();
            document.getElementById('bonusB').textContent = '$' + Math.round(20000 * budgetRatio).toLocaleString();
            document.getElementById('maxBonusDisplay').textContent = '$' + maxBonus.toLocaleString();
        }

        // 權重更新函數
function updateWeights(changed) {
    let strategyWeight = parseFloat(document.getElementById('strategyWeight').value);
    let operationWeight = parseFloat(document.getElementById('operationWeight').value);

    if (changed === 'strategy') {
        // 當策略型變動時，營運型自動補足
        operationWeight = 100 - strategyWeight;
        document.getElementById('operationWeight').value = operationWeight;
        document.getElementById('operationWeightValue').textContent = operationWeight + '%';
    } else if (changed === 'operation') {
        // 當營運型變動時，策略型自動補足
        strategyWeight = 100 - operationWeight;
        document.getElementById('strategyWeight').value = strategyWeight;
        document.getElementById('strategyWeightValue').textContent = strategyWeight + '%';
    }

    // 更新顯示
    document.getElementById('strategyWeightValue').textContent = strategyWeight + '%';
    document.getElementById('operationWeightValue').textContent = operationWeight + '%';

    updateWeightSummary();
    updateKPIFormula();

    if (bonusResults.length > 0) {
        calculateBonus();
        displayResults();
    }
}

        // 子權重更新函數
        function updateSubWeights(category) {
            if (category === 'strategy') {
                const aProductRatio = parseFloat(document.getElementById('aProductRatioWeight').value);
                const aProductCustomers = parseFloat(document.getElementById('aProductCustomersWeight').value);
                
                if (aProductRatio + aProductCustomers !== 100) {
                    document.getElementById('aProductCustomersWeight').value = 100 - aProductRatio;
                    document.getElementById('aProductCustomersWeightValue').textContent = (100 - aProductRatio) + '%';
                }
                
                document.getElementById('aProductRatioWeightValue').textContent = aProductRatio + '%';
                document.getElementById('aProductCustomersWeightValue').textContent = aProductCustomers + '%';
                
            } else if (category === 'operation') {
                const sales = parseFloat(document.getElementById('salesWeight').value);
                const profit = parseFloat(document.getElementById('profitWeight').value);
                const newCustomer = parseFloat(document.getElementById('newCustomerWeight').value);
                const satisfaction = parseFloat(document.getElementById('satisfactionWeight').value);
                
                document.getElementById('salesWeightValue').textContent = sales + '%';
                document.getElementById('profitWeightValue').textContent = profit + '%';
                document.getElementById('newCustomerWeightValue').textContent = newCustomer + '%';
                document.getElementById('satisfactionWeightValue').textContent = satisfaction + '%';
                
                const total = sales + profit + newCustomer + satisfaction;
                if (total !== 100) {
                    document.getElementById('weightWarning').style.display = 'block';
                    document.getElementById('weightWarning').textContent = `⚠️ 營運型KPI權重總和為${total}%，請調整為100%！`;
                } else {
                    document.getElementById('weightWarning').style.display = 'none';
                }
            }
            
            updateWeightSummary();
            updateKPIFormula();
            
            if (bonusResults.length > 0) {
                calculateBonus();
                displayResults();
            }
        }

        // 更新權重總覽
        function updateWeightSummary() {
            const strategyWeight = parseFloat(document.getElementById('strategyWeight').value);
            const operationWeight = parseFloat(document.getElementById('operationWeight').value);
            
            document.getElementById('headerStrategyWeight').textContent = strategyWeight + '%';
            document.getElementById('headerOperationWeight').textContent = operationWeight + '%';
            
            const totalBudget = parseFloat(document.getElementById('totalBudget').value);
            const maxBonus = parseFloat(document.getElementById('maxBonus').value);
            document.getElementById('headerTotalBudget').textContent = '$' + totalBudget.toLocaleString();
            document.getElementById('headerMaxBonus').textContent = '$' + maxBonus.toLocaleString();
        }

        // 獎金更新函數
        function updateBonus() {
            updateWeightSummary();
            updateBonusRules();
            
            if (bonusResults.length > 0) {
                adjustBonusForBudget();
                displayResults();
            }
        }

        // 更新獎金儀表板
        function updateBonusDashboard() {
            const estimatedPayout = bonusResults.reduce((sum, result) => sum + result.totalBonus, 0);
            document.getElementById('dashboardEstimatedPayout').textContent = '$' + Math.round(estimatedPayout).toLocaleString();
            
            updateBonusStackChart();
        }

        // 更新累積堆疊圖
        function updateBonusStackChart() {
            if (bonusResults.length === 0) return;
            
            const employeeNames = bonusResults.map(result => result.name || result.code);
            const baseBonus = bonusResults.map(result => result.baseBonus);
            const performanceBonus = bonusResults.map(result => result.performanceBonus);
            
            const ctx = document.getElementById('bonusStackChart').getContext('2d');
            
            if (bonusStackChart) {
                bonusStackChart.destroy();
            }
            
            bonusStackChart = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: employeeNames,
                    datasets: [
                        {
                            label: '基礎獎金',
                            data: baseBonus,
                            backgroundColor: 'rgba(52, 152, 219, 0.8)',
                            borderColor: 'rgba(52, 152, 219, 1)',
                            borderWidth: 1
                        },
                        {
                            label: '績效獎金',
                            data: performanceBonus,
                            backgroundColor: 'rgba(231, 76, 60, 0.8)',
                            borderColor: 'rgba(231, 76, 60, 1)',
                            borderWidth: 1
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: {
                            stacked: true,
                            ticks: {
                                maxRotation: 45,
                                minRotation: 45
                            }
                        },
                        y: {
                            stacked: true,
                            beginAtZero: true,
                            ticks: {
                                callback: function(value) {
                                    return '$' + value.toLocaleString();
                                }
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'top'
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return context.dataset.label + ': $' + Math.round(context.parsed.y).toLocaleString();
                                },
                                footer: function(tooltipItems) {
                                    let total = 0;
                                    tooltipItems.forEach(item => {
                                        total += bonusResults[item.dataIndex].totalBonus;
                                    });
                                    return '總獎金: $' + Math.round(total).toLocaleString();
                                }
                            }
                        }
                    }
                }
            });
        }
    </script>
</body>
</html>
