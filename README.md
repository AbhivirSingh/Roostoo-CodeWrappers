# Roostoo Trading Bot

## Overview
The Roostoo Trading Bot is an automated cryptocurrency trading simulation tool that integrates with the Roostoo mock API (https://mock-api.roostoo.com). It allows users to practice trading strategies in a risk-free environment using real-time market data. The bot supports multiple technical indicators (RSI, MACD, Bollinger Bands, Stochastic Oscillator) and implements autonomous trading strategies for coin selection and risk management. Built with Python, it fetches historical data via `yfinance` and uses `TA-Lib` for technical analysis.

## Features
- **Mock Trading with Roostoo API**: Simulates trades using the Roostoo mock API, providing a risk-free environment to test strategies.
- **Multiple Trading Strategies**:
  - Mean Reversion
  - MACD Crossover
  - RSI and Stochastic Oscillator
  - Bollinger Bands
  - Combined Strategy (combines signals from multiple indicators)
- **Coin Selection**: Dynamically selects coins to trade based on historical performance, volatility, and technical signals.
- **Technical Indicators**: Uses RSI, MACD, Bollinger Bands, and Stochastic Oscillator for signal generation.
- **Risk Management**: Implements stop-loss (3%), take-profit (6%), and position sizing (5% of portfolio per trade).
- **Historical Data Analysis**: Fetches 1 year of historical data via `yfinance` for long-term metrics.
- **Logging and Trade Reports**: Logs trades and saves detailed trade logs to files for analysis.
- **Customizable Parameters**: Adjust trading intervals, risk levels, and indicator settings in `trading_bot.py`.

## Prerequisites
- Python 3.8 or higher
- pip for installing dependencies
- Roostoo mock API keys (available from roostoo.com)
- Internet connection for fetching market data via the Roostoo API and historical data via `yfinance`

## Installation
1. **Clone the Repository**
   ```bash
   git clone https://github.com/AbhivirSingh/Roostoo-Trading-Bot.git
   cd Roostoo-Trading-Bot
   ```

2. **Set Up a Virtual Environment** (Recommended)
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**
   The `requirements.txt` file lists the necessary Python libraries:
   - requests>=2.28.0
   - pandas>=1.5.0
   - numpy>=1.23.0
   - yfinance>=0.2.0
   - TA-Lib>=0.4.24

   Install them using:
   ```bash
   pip install -r requirements.txt
   ```

   **Note on TA-Lib**: `TA-Lib` may require additional setup depending on your operating system. Refer to the [TA-Lib documentation](https://github.com/TA-Lib/ta-lib-python) for installation instructions.

4. **Configure API Keys**
   - Sign up at [roostoo.com](https://roostoo.com) to obtain mock API keys.
   - Edit the `config.py` file with your API keys:
     ```python
     API_KEY = "your_api_key"
     SECRET_KEY = "your_secret_key"
     ```

## Usage
1. **Run the Bot**
   The bot runs a continuous simulation, fetching market data every 10 seconds and making trading decisions every 20 seconds.
   ```bash
   python trading_bot.py
   ```
   The bot will:
   - Connect to the Roostoo mock API.
   - Select coins to trade based on predefined criteria.
   - Execute trades using the chosen strategy.
   - Log trades and portfolio updates.

2. **Monitor Logs**
   - Console logs provide real-time updates on coin selection, signals, trades, and portfolio value.
   - Detailed trade logs are saved as `trade_log_YYYYMMDD_HHMMSS.txt` files in the project directory.

3. **Stop the Bot**
   - Press `Ctrl+C` to stop the simulation.
   - The bot will close all open positions and generate a final trade log with a summary, including portfolio value, win rate, and trade details.

## Project Structure
```
Roostoo-Trading-Bot/
├── config.py             # API key configuration
├── requirements.txt      # Python dependencies
├── trading_bot.py        # Main trading bot script
├── LICENSE               # License file (not provided)
├── README.md             # Project documentation
```

## Configuration Parameters
Key parameters in `trading_bot.py` can be adjusted:
- `FETCH_INTERVAL`: 10 seconds (time between market data fetches)
- `TRADING_INTERVAL`: 20 seconds (time between trading decisions)
- `POSITION_SIZE_PCT`: 0.05 (5% of portfolio per trade)
- `STOP_LOSS_PCT`: 0.03 (3% stop loss)
- `TAKE_PROFIT_PCT`: 0.06 (6% take profit)
- `MAX_COINS`: 5 (maximum number of coins to trade simultaneously)
- `YF_HISTORICAL_PERIOD`: "1y" (1 year of historical data for analysis)
- Indicator settings: RSI, MACD, Bollinger Bands, and Stochastic Oscillator periods

## Supported Coins
The bot fetches available trading pairs from the Roostoo mock API (`/v3/exchangeInfo`). Default pairs include:
- BTC/USD
- ETH/USD
- LTC/USD
Additional pairs can be mapped in the `ticker_mapping` dictionary in `trading_bot.py` for historical data retrieval via `yfinance`.

## Trading Strategies
The bot supports the following strategies, selectable dynamically based on performance:
- **Mean Reversion**: Buys when the price is below the mean, sells when above.
- **MACD Crossover**: Uses MACD and signal line crossovers with RSI confirmation.
- **RSI Strategy**: Combines RSI and Stochastic Oscillator for overbought/oversold signals.
- **Bollinger Bands**: Trades based on price breakouts from Bollinger Bands with RSI confirmation.
- **Combined**: Requires agreement from at least two of MACD, RSI, and Bollinger Bands strategies.

## Risk Management
- **Position Sizing**: Limits each trade to 5% of the portfolio, adjusted based on the number of active positions.
- **Stop Loss/Take Profit**: Automatically sets stop-loss (3%) and take-profit (6%) levels for each trade.
- **Maximum Positions**: Limits the number of concurrent trades to 5 coins.

## Limitations
- The bot uses a mock API, so no real money is involved; it’s for simulation only.
- Historical data fetching via `yfinance` may fail for some pairs if not supported.
- The bot assumes the mock API is always available; downtime may cause errors.

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Make your changes and commit (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a Pull Request.

## Disclaimer
This bot is for educational and simulation purposes only. It uses the Roostoo mock API and does not involve real cryptocurrency trading. Cryptocurrency trading carries significant financial risks when done with real funds. The developers are not responsible for any financial losses incurred if this code is adapted for real trading.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact
For questions or support, open an issue on GitHub or visit [roostoo.com](https://roostoo.com) for more information about the Roostoo platform.