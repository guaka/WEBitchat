# WEBitchat

A standalone real-time web-based visualizer for Bitchat activity over the Nostr protocol, displaying location-based messages on an interactive map.

**Note**: This is an independent project and is not officially part of the Bitchat project.

## Overview

WEBitchat is a single-page HTML application that connects to multiple Nostr relays to display Bitchat location channel messages (Kind 20000 events) in real-time. It provides both a map view and a chronological activity feed.

## Features

### Core Functionality
- **Real-time data**: Connects to multiple Nostr relays for live updates
- **Interactive map**: Displays messages with geohash coordinates on a Leaflet map
- **Activity feed**: Chronological list of all Bitchat messages
- **Geohash visualization**: Shows geohash areas as rectangles on the map
- **Filtering**: Filter by specific geohashes (e.g., "ey", "9q8yy")
- **9q exclusion**: Toggle to hide the very active 9q area
- **Load more**: Fetch historical messages from relays

### Map Features
- **Geohash rectangles**: Visual representation of geohash coverage areas
- **Message markers**: Pin markers for each message location
- **Popup details**: Click markers for message content and metadata
- **Auto-zoom**: Automatically focuses on filtered geohash areas
- **Real-time updates**: New messages appear instantly on the map

### Filtering & Search
- **Geohash filter**: Type any geohash to see only messages from that area
- **9q exclusion toggle**: Hide the very active 9q area to focus on other regions
- **Real-time filtering**: Updates both map and activity list instantly
- **Partial matching**: "ey" will match "ey", "9q8yy", etc.

## Technical Details

### Architecture
- **Single HTML file**: Self-contained with embedded CSS and JavaScript
- **No external dependencies**: Uses CDN for Leaflet map library
- **WebSocket connections**: Direct connections to Nostr relays
- **Client-side filtering**: All filtering happens in the browser

### Data Sources
- **Nostr relays**: Connects to 5 major Nostr relays
  - relay.damus.io
  - nos.lol
  - relay.primal.net
  - offchain.pub
  - nostr21.com
- **Event types**: Only processes Kind 20000 (ephemeral events) for location channels
- **Geohash tags**: Extracts location data from `g` tags in event metadata

### Geohash Support
- **Full geohash decoding**: Converts geohash strings to lat/lng coordinates
- **Bounding box calculation**: Shows exact coverage areas for each geohash
- **Multiple geohash lengths**: Supports 1-12 character geohashes
- **Visual rectangles**: Displays geohash areas as colored rectangles on map

## Usage

### Basic Usage
1. **Open the HTML file** in a web browser
2. **Wait for initial load** - connects to relays and fetches recent messages
3. **View on map** - messages appear as pin markers with geohash rectangles
4. **Browse activity feed** - chronological list on the right side

### Filtering
1. **Filter by geohash**: Type "ey" in the filter box to see only that area
2. **Exclude 9q area**: Check the toggle to hide the very active 9q region
3. **Load more data**: Click "Load More Notes" to fetch historical messages

### Map Interaction
- **Zoom and pan**: Use mouse wheel and drag to navigate
- **Click markers**: View message details in popups
- **Click rectangles**: See geohash area information
- **Auto-focus**: Map automatically zooms to filtered areas

## Configuration

### Relay Settings
The visualizer connects to these relays by default:
```javascript
this.relays = [
    'wss://relay.damus.io',
    'wss://nos.lol', 
    'wss://relay.primal.net',
    'wss://offchain.pub',
    'wss://nostr21.com'
];
```

### Load Limits
- **Initial load**: 10,000 events per relay
- **Load more**: 500 events per relay (1000 when 9q exclusion is active)
- **Memory limit**: 10,000 activities kept in memory

### Filtering Options
- **Geohash filter**: Partial matching (case-insensitive)
- **9q exclusion**: Hides all geohashes starting with "9q"
- **Combined filtering**: Both filters can be used together

## Deployment

### GitHub Pages
1. Create a GitHub repository
2. Upload the HTML file (rename to `index.html` for cleaner URL)
3. Enable GitHub Pages in repository settings
4. Access at `https://username.github.io/repository-name/`

### Other Options
- **Netlify**: Drag and drop deployment
- **Vercel**: Import from GitHub
- **Any static hosting**: Just upload the HTML file

## Browser Requirements

- **Modern browser**: Chrome, Firefox, Safari, Edge
- **WebSocket support**: Required for relay connections
- **HTTPS**: Required for WebSocket connections (GitHub Pages provides this)

## Troubleshooting

### Common Issues
- **No messages showing**: Check browser console for relay connection errors
- **Load more not working**: Check console for subscription errors
- **Map not loading**: Ensure Leaflet CDN is accessible
- **WebSocket errors**: May need HTTPS (try GitHub Pages)

### Debug Information
- **Console logging**: Detailed logs for all operations
- **Relay status**: Shows connection status for each relay
- **Activity counts**: Displays message counts per relay
- **Filter status**: Shows current filter settings

## Development

### File Structure
- **Single HTML file**: All code in one file for easy deployment
- **Embedded CSS**: Styles defined in `<style>` section
- **Embedded JavaScript**: All logic in `<script>` section
- **CDN dependencies**: Leaflet map library loaded from CDN

### Key Classes
- **WEBitchatVisualizer**: Main application class
- **WebSocket management**: Handles connections to multiple relays
- **Geohash utilities**: Converts geohashes to coordinates and bounds
- **Filtering system**: Client-side filtering of messages
- **Map integration**: Leaflet map with markers and rectangles

## Future Enhancements

### Potential Improvements
- **More relay options**: Allow users to add custom relays
- **Message search**: Full-text search within messages
- **Time range filtering**: Filter by date/time ranges
- **Export functionality**: Download message data
- **Mobile optimization**: Better mobile interface
- **Offline support**: Cache messages for offline viewing

### Performance Optimizations
- **Virtual scrolling**: For large message lists
- **Map clustering**: Group nearby markers
- **Lazy loading**: Load messages on demand
- **WebWorker**: Background processing for large datasets

## License

This project is released into the public domain under the Unlicense, following the same licensing approach as the Bitchat project. This allows for unrestricted use, modification, and distribution.

## Contributing

This is an independent project. To contribute to this visualizer:
1. Fork the repository
2. Make your changes to the HTML file
3. Test thoroughly with different geohash areas
4. Submit a pull request with your improvements

## Support

For issues or questions:
- Check the browser console for error messages
- Ensure you have a stable internet connection
- Try refreshing the page if relays seem disconnected
- Verify the HTML file is served over HTTPS

