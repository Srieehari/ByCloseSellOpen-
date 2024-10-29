# ByCloseSellOpen Algorithm

This algorithm implements a straightforward daily trading strategy, buying shares near the market close and liquidating them at the market open the following trading day. Initially, the algorithm was set up for SPY, but it has since been modified to trade AAPL or any stock of the users choice.

## Overview

- **Objective**: To buy AAPL stock near the market close and sell at the market open the next day.
- **Approach**: A Market-On-Close order is submitted shortly before market close, and all positions are liquidated at the market open the next day.

## Future Plans

- **Reinforcement Learning Model**: This algorithm is planned for further development with the integration of a reinforcement learning model. The RL model will eventually be used to optimize buy and sell decisions based on historical data and market patterns, adding an adaptive layer to the trading strategy.

## Algorithm Details

1. **Initialization**:
   - Sets the start and end dates for backtesting.
   - Sets an initial cash allocation of $1,000,000.
   - Selects AAPL for trading, with minute-level data resolution.
   - Configures the brokerage model to Interactive Brokers with a margin account.

2. **Scheduled Functions**:
   - `SellOpen()`: Scheduled to run one minute after the market opens. If any positions are held, it liquidates them immediately.

3. **OnData()**:
   - The algorithm checks at 15:44 (3:44 PM) if there are no open positions and no existing order to close. If conditions are met, it calculates the order quantity and places a Market-On-Close order for the entire portfolio.

## Key Variables

- `closingOrderSent`: A flag to track if a Market-On-Close order has already been submitted, preventing multiple orders on the same day.

## Usage

### Requirements

1. **QuantConnect Lean CLI**: Ensure QuantConnect Lean CLI is installed for dataset downloads.
2. **Brokerage Model**: Uses Interactive Brokers' margin account setup. Adjust if using another brokerage model.

### Functionality

- **Buy Signal**: When there are no open positions, and the time is close to the market close (15:44), a Market-On-Close order is placed.
- **Sell Signal**: The algorithm liquidates all holdings at the market open the following day.

### Limitations

This strategy assumes sufficient market liquidity and may not perform as expected in highly volatile conditions or illiquid markets. Backtesting results may vary based on market conditions and are not indicative of future performance.

## Code Annotations

- `self.set_start_date` and `self.set_end_date`: Define backtest duration.
- `self.Schedule.On`: Schedules the `SellOpen()` function to run one minute after the market opens each day.
- `MarketOnCloseOrder`: Places a market-on-close order near the trading day's end.
- `Liquidate()`: Sells all holdings at the market open the next day.

## Contributing

For customization, contributors can adjust the security, trading times, and risk management parameters based on personal strategies. This template can also be expanded to include other securities or trading rules as required.

