# Portfolio Tracker - Cherri Implementation

A comprehensive stock portfolio tracking system built with **Cherri** (Siri Shortcuts programming language). Track your investments, monitor gains/losses, and display real-time portfolio data on your iOS/macOS home screen.

## Features

- **Add Holdings**: Add stocks with symbol, shares, and cost basis
- **Update Holdings**: Modify existing positions
- **Remove Holdings**: Delete holdings from your portfolio
- **View Portfolio**: See complete portfolio summary with current prices and gains/losses
- **Widget Support**: Real-time portfolio widget for iOS/macOS home screen
- **Auto-Refresh**: Optional daily automation to keep data current
- **Yahoo Finance Integration**: Live stock price data
- **CSV Storage**: Persistent, iCloud-synced CSV file storage

## Components

### Shortcuts (5)
1. **Portfolio - Add Holding** - Add new stock positions
2. **Portfolio - Update Holding** - Modify existing positions
3. **Portfolio - Remove Holding** - Delete positions
4. **Portfolio - View** - Display full portfolio summary
5. **Portfolio - Refresh Widget** - Update widget data cache

### Widget (1)
- **Portfolio Widget** (Scriptable) - Home screen widget displaying portfolio value, change, and top holdings

## Quick Start

See [SETUP.md](SETUP.md) for complete installation and setup instructions.

### Prerequisites
- iOS/iPadOS 15+ or macOS Sonoma+
- Scriptable (free app) - for widget functionality
- iCloud Drive enabled

### Installation Summary
1. Create `portfolio.csv` in `iCloud Drive/Shortcuts/` folder (see CSV Format below)
2. Install Scriptable from App Store (for widget functionality)
3. Download and install the 5 compiled `.shortcut` files
4. Copy `Portfolio_Widget.js` to Scriptable
5. Add Scriptable widget to home screen
6. Run "Portfolio - Add Holding" to add your first stock

### CSV Format
Create a file at `iCloud Drive/Shortcuts/portfolio.csv` with the following format:
```csv
symbol,shares,costBasis,dateAdded
AAPL,100,150.25,2024-01-15
GOOGL,50,135.00,2024-02-20
```

You can also use the provided `portfolio.csv` example file as a starting point.

## Usage

### Adding a Stock
1. Run "Portfolio - Add Holding"
2. Enter stock symbol (e.g., AAPL)
3. Enter number of shares
4. Enter cost basis per share

### Viewing Your Portfolio
1. Run "Portfolio - View" to see full details
2. Check your home screen widget for quick overview

### Updating the Widget
- Widget updates automatically when you add/update/remove holdings
- Run "Portfolio - Refresh Widget" manually for latest prices
- Set up automation for daily auto-refresh

## Architecture

### Data Storage
Uses **CSV file** stored in iCloud Drive for persistent, cross-device storage:

**Location**: `iCloud Drive/Shortcuts/portfolio.csv`

**Format**:
```csv
symbol,shares,costBasis,dateAdded
AAPL,100,150.25,2024-01-15
GOOGL,50,135.00,2024-02-20
```

The shortcuts read and write directly to this CSV file, which is automatically synced across all your devices via iCloud.

### Yahoo Finance API
Fetches real-time stock prices from:
```
https://query1.finance.yahoo.com/v8/finance/chart/{SYMBOL}
```

## Project Structure

```
portfolio-tracker/
├── src/
│   ├── lib/
│   │   ├── portfolio_csv.cherri     # CSV data access layer
│   │   ├── yahoo_api.cherri         # API integration
│   │   └── formatting.cherri        # Display utilities
│   └── shortcuts/
│       ├── add_holding.cherri
│       ├── update_holding.cherri
│       ├── remove_holding.cherri
│       ├── view_portfolio.cherri
│       └── refresh_widget.cherri
├── widget/
│   └── Portfolio_Widget.js          # Scriptable widget
├── compiled/                         # Compiled shortcuts
├── portfolio.csv                     # Example CSV file
├── SETUP.md                          # Setup instructions
└── README.md                         # This file
```

## Building from Source

### Requirements
- Cherri compiler (https://cherrilang.org)
- Git

### Compilation

```bash
cd portfolio-tracker/src

# Compile all shortcuts
cherri shortcuts/add_holding.cherri -o ../dist/Portfolio_Add_Holding.shortcut
cherri shortcuts/update_holding.cherri -o ../dist/Portfolio_Update_Holding.shortcut
cherri shortcuts/remove_holding.cherri -o ../dist/Portfolio_Remove_Holding.shortcut
cherri shortcuts/view_portfolio.cherri -o ../dist/Portfolio_View.shortcut
cherri shortcuts/refresh_widget.cherri -o ../dist/Portfolio_Refresh_Widget.shortcut
```

## Troubleshooting

### Widget Not Updating
- Ensure internet connection is active
- Run "Portfolio - Refresh Widget" manually
- Check that iCloud Drive is enabled and syncing

### Price Data Issues
- Yahoo Finance API may have temporary outages
- Some symbols may not be supported (try alternative exchanges)
- Rate limiting may occur with frequent requests

### CSV File Issues
- Ensure `portfolio.csv` exists in `iCloud Drive/Shortcuts/` folder
- Check CSV format matches the required structure (symbol,shares,costBasis,dateAdded)
- Ensure iCloud Drive is enabled and syncing across devices

## Limitations

- Yahoo Finance API is free but may have rate limits
- Widget refresh requires manual trigger or automation
- International stocks may require exchange suffix (e.g., AAPL.L)
- Historical data not stored (only current prices)

## Future Enhancements

- [ ] Support for cryptocurrency portfolios
- [ ] Historical performance charts
- [ ] Dividend tracking
- [ ] Multiple portfolio support
- [ ] Export to CSV
- [ ] Tax lot management

## License

MIT License - See LICENSE file for details

## Credits

- Built with [Cherri](https://cherrilang.org)
- Stock data from [Yahoo Finance](https://finance.yahoo.com)
- Widget powered by [Scriptable](https://scriptable.app)
- Data storage via iCloud Drive CSV files

## Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Check SETUP.md for common problems
- Review Cherri documentation at https://cherrilang.org

## Version

Current Version: **1.0.0**

---

Made with ❤️ using Cherri
