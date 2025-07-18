<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>TradingView Chart with Watchlist</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #181818;
      color: #fff;
    }
    .container {
      display: flex;
      height: 100vh;
    }
    .chart-area {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #181818;
    }
    .watchlist {
      width: 220px;
      background: #23272a;
      padding: 20px 10px;
      box-sizing: border-box;
      border-left: 2px solid #111;
      overflow-y: auto;
    }
    .watchlist h2 {
      font-size: 1.2em;
      margin-bottom: 10px;
      color: #f9d923;
    }
    .symbol-list {
      list-style: none;
      padding: 0;
      margin: 0;
    }
    .symbol-list li {
      padding: 8px 12px;
      margin-bottom: 5px;
      border-radius: 4px;
      cursor: pointer;
      transition: background 0.2s;
    }
    .symbol-list li:hover, .symbol-list li.active {
      background: #32383e;
      color: #f9d923;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="chart-area">
      <div id="tradingview_chart"></div>
    </div>
    <div class="watchlist">
      <h2>Watchlist</h2>
      <ul class="symbol-list" id="symbolList">
        <!-- Symbols will be inserted here -->
      </ul>
    </div>
  </div>

  <!-- TradingView Widget Script -->
  <script src="https://s3.tradingview.com/tv.js"></script>
  <script>
    // Your watchlist symbols (add as many as you like)
    const symbols = [
      { code: "BINANCE:BTCUSDT", name: "BTC/USDT" },
      { code: "BINANCE:ETHUSDT", name: "ETH/USDT" },
      { code: "BINANCE:SOLUSDT", name: "SOL/USDT" },
      // Add more symbols as needed
    ];

    // Render the watchlist
    const symbolList = document.getElementById('symbolList');
    symbols.forEach((sym, idx) => {
      const li = document.createElement('li');
      li.textContent = sym.name;
      li.dataset.symbol = sym.code;
      if(idx === 0) li.classList.add('active');
      li.onclick = function() {
        document.querySelectorAll('.symbol-list li').forEach(li => li.classList.remove('active'));
        this.classList.add('active');
        loadTradingViewChart(this.dataset.symbol);
      };
      symbolList.appendChild(li);
    });

    // Function to load the TradingView chart
    let widget = null;
    function loadTradingViewChart(symbol) {
      if(widget) widget.remove();
      widget = new TradingView.widget({
        "container_id": "tradingview_chart",
        "width": 900,
        "height": 600,
        "symbol": symbol,
        "interval": "D",
        "timezone": "Etc/UTC",
        "theme": "dark",
        "style": "1",
        "locale": "en",
        "toolbar_bg": "#222",
        "enable_publishing": false,
        "allow_symbol_change": false,
        "hide_legend": false
      });
    }

    // Load the first chart on page load
    loadTradingViewChart(symbols[0].code);
  </script>
</body>
</html># nuevo
