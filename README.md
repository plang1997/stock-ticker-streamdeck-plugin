# stock-ticker-stream-deck-plugin

A stock ticker plugin for Stream Deck that uses modern Elgato CLI tools.

![StreamDeck_W1KAB8ful2](https://user-images.githubusercontent.com/46971999/60206582-cd1e8300-9808-11e9-9506-fe2e9bec466f.png)

## Prerequisites

- **Go** 1.16+ ([golang.org](https://golang.org))
- **Elgato Stream Deck CLI** - Install globally via npm:
  ```bash
  npm install -g @elgato/cli
  ```
  
For detailed CLI documentation, see [developer.elgato.com](https://developer.elgato.com/documentation/stream-deck)

## Building

### Development Build

Build the plugin and link it for testing:
```bash
cd cmd/stock_ticker_stream_deck_plugin
GOOS=darwin GOARCH=amd64 go build -o ../../com.exension.stocks.sdPlugin/sdplugin-stocks ./...
streamdeck link com.exension.stocks.sdPlugin
streamdeck restart com.exension.stocks
```

### Release Build

Build and package for distribution:
```bash
cd cmd/stock_ticker_stream_deck_plugin
GOOS=darwin GOARCH=amd64 go build -o ../../com.exension.stocks.sdPlugin/sdplugin-stocks ./...
GOOS=windows GOARCH=amd64 go build -o ../../com.exension.stocks.sdPlugin/sdplugin-stocks.exe ./...
mkdir -p release
streamdeck pack com.exension.stocks.sdPlugin --output release --force --no-update-check
```

The `.streamDeckPlugin` file will be in the `release/` folder.

## Installing

1. **Uninstall old version** (if present)
   - Open Stream Deck app
   - Right-click "Stocks" plugin
   - Click "Uninstall"

2. **Navigate to release package**
   ```bash
   open release/
   ```

3. **Install new version**
   - Double-click `com.exension.stocks.streamDeckPlugin`
   - Accept the installation prompt

The plugin will now persist across Stream Deck restarts and system reboots.
