<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CryptoEarn - Earn Free Crypto Daily</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            color: #333;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 3rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }

        .stat-card {
            background: rgba(255,255,255,0.95);
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-10px);
        }

        .stat-icon {
            font-size: 3rem;
            margin-bottom: 15px;
        }

        .btc { color: #f7931a; }
        .eth { color: #627eea; }
        .usdt { color: #26a17b; }
        .total { color: #667eea; }

        .stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            margin-bottom: 5px;
        }

        .earn-section {
            background: rgba(255,255,255,0.95);
            border-radius: 20px;
            padding: 40px;
            margin-bottom: 40px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }

        .earn-buttons {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .earn-btn {
            padding: 20px;
            border: none;
            border-radius: 15px;
            font-size: 1.2rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .earn-btn:hover {
            transform: scale(1.05);
        }

        .daily { background: linear-gradient(45deg, #ff6b6b, #ff8e8e); color: white; }
        .watch { background: linear-gradient(45deg, #4ecdc4, #44a08d); color: white; }
        .tasks { background: linear-gradient(45deg, #45b7d1, #96c93d); color: white; }
        .refer { background: linear-gradient(45deg, #feca57, #ff9ff3); color: white; }

        .progress-bar {
            width: 100%;
            height: 10px;
            background: #e0e0e0;
            border-radius: 5px;
            overflow: hidden;
            margin-top: 20px;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            width: 0%;
            transition: width 0.5s ease;
            border-radius: 5px;
        }

        .wallet-section {
            background: rgba(255,255,255,0.95);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }

        .wallet-address {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            font-family: monospace;
            font-size: 0.9rem;
            word-break: break-all;
            margin: 20px 0;
        }

        .withdraw-btn {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            border: none;
            padding: 15px 40px;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .withdraw-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(255,107,107,0.4);
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #4ecdc4;
            color: white;
            padding: 15px 20px;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            transform: translateX(400px);
            transition: transform 0.3s ease;
        }

        .notification.show {
            transform: translateX(0);
        }

        @media (max-width: 768px) {
            .header h1 { font-size: 2rem; }
            .stat-number { font-size: 2rem; }
            .earn-buttons { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-coins"></i> CryptoEarn</h1>
            <p>Earn Free Crypto Daily - Watch Videos, Complete Tasks & Get Rewards!</p>
        </div>

        <div class="stats-grid">
            <div class="stat-card">
                <div class="stat-icon btc"><i class="fab fa-bitcoin"></i></div>
                <div class="stat-number" id="btcBalance">0.000125</div>
                <div>BTC Balance</div>
            </div>
            <div class="stat-card">
                <div class="stat-icon eth"><i class="fab fa-ethereum"></i></div>
                <div class="stat-number" id="ethBalance">0.045</div>
                <div>ETH Balance</div>
            </div>
            <div class="stat-card">
                <div class="stat-icon usdt"><i class="fas fa-dollar-sign"></i></div>
                <div class="stat-number" id="usdtBalance">$12.50</div>
                <div>USDT Balance</div>
            </div>
            <div class="stat-card">
                <div class="stat-icon total"><i class="fas fa-wallet"></i></div>
                <div class="stat-number" id="totalBalance">$45.20</div>
                <div>Total Earnings</div>
            </div>
        </div>

        <div class="earn-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #333;">
                <i class="fas fa-play-circle"></i> Choose How to Earn
            </h2>
            <div class="earn-buttons">
                <button class="earn-btn daily" onclick="claimDaily()">
                    <i class="fas fa-calendar-day"></i>
                    Daily Bonus
                    <span style="font-size: 1.5rem;">+0.001 BTC</span>
                </button>
                <button class="earn-btn watch" onclick="watchVideo()">
                    <i class="fas fa-video"></i>
                    Watch Video
                    <span style="font-size: 1.5rem;">+0.0005 BTC</span>
                </button>
                <button class="earn-btn tasks" onclick="completeTask()">
                    <i class="fas fa-tasks"></i>
                    Complete Tasks
                    <span style="font-size: 1.5rem;">+$5 USDT</span>
                </button>
                <button class="earn-btn refer" onclick="showReferral()">
                    <i class="fas fa-users"></i>
                    Refer Friends
                    <span style="font-size: 1.5rem;">+10% Bonus</span>
                </button>
            </div>
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
            <p style="text-align: center; margin-top: 10px; color: #666;">
                Daily Progress: <span id="progressText">0%</span>
            </p>
        </div>

        <div class="wallet-section">
            <h2><i class="fas fa-wallet"></i> Your Wallet</h2>
            <div class="wallet-address" id="walletAddress">
                bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh
            </div>
            <button class="withdraw-btn" onclick="withdraw()">
                <i class="fas fa-download"></i> Withdraw Earnings
            </button>
            <p style="margin-top: 20px; color: #666; font-size: 0.9rem;">
                Minimum Withdrawal: $10 | Instant Payout
            </p>
        </div>
    </div>

    <div class="notification" id="notification">
        <i class="fas fa-check-circle"></i> 
        <span id="notificationText"></span>
    </div>

    <script>
        let balances = {
            btc: 0.000125,
            eth: 0.045,
            usdt: 12.50,
            total: 45.20
        };

        let dailyProgress = 0;

        function updateBalances() {
            document.getElementById('btcBalance').textContent = balances.btc.toFixed(6);
            document.getElementById('ethBalance').textContent = balances.eth.toFixed(3);
            document.getElementById('usdtBalance').textContent = `$${balances.usdt.toFixed(2)}`;
            document.getElementById('totalBalance').textContent = `$${balances.total.toFixed(2)}`;
        }

        function showNotification(message) {
            const notification = document.getElementById('notification');
            const text = document.getElementById('notificationText');
            text.textContent = message;
            notification.classList.add('show');
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        function updateProgress() {
            const progress = document.getElementById('progressFill');
            const text = document.getElementById('progressText');
            progress.style.width = dailyProgress + '%';
            text.textContent = dailyProgress + '%';
        }

        function claimDaily() {
            balances.btc += 0.001;
            balances.total += 2.50;
            dailyProgress = Math.min(100, dailyProgress + 25);
            updateBalances();
            updateProgress();
            showNotification('Daily Bonus Claimed! +0.001 BTC');
        }

        function watchVideo() {
            balances.btc += 0.0005;
            balances.total += 1.25;
            dailyProgress = Math.min(100, dailyProgress + 15);
            updateBalances();
            updateProgress();
            showNotification('Video Watched! +0.0005 BTC');
        }

        function completeTask() {
            balances.usdt += 5;
            balances.total += 5;
            dailyProgress = Math.min(100, dailyProgress + 30);
            updateBalances();
            updateProgress();
            showNotification('Task Completed! +$5 USDT');
        }

        function showReferral() {
            const refLink = 'https://cryptoearn.com/ref/yourusername';
            navigator.clipboard.writeText(refLink);
            showNotification('Referral link copied! Share & earn 10% bonus');
        }

        function withdraw() {
            if (balances.total >= 10) {
                showNotification('Withdrawal Requested! Processing in 24hrs');
                // Reset demo balances
                setTimeout(() => {
                    balances = { btc: 0.000125, eth: 0.045, usdt: 12.50, total: 45.20 };
                    dailyProgress = 0;
                    updateBalances();
                    updateProgress();
                }, 2000);
            } else {
                showNotification('Minimum $10 required for withdrawal');
            }
        }

        // Auto-update balances every 10 seconds (demo)
        setInterval(() => {
            if (Math.random() > 0.7) {
                balances.total += 0.10;
                updateBalances();
            }
        }, 10000);

        // Initialize
        updateBalances();
        updateProgress();
    </script>
</body>
</html>
