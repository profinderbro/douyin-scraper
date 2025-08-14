# Douyin Scraper

A simple JavaScript tool to extract post links from Douyin (TikTok China) pages.

## Features

- Automatically scrolls through the page to load more posts
- Extracts all unique post links containing `/note/`
- Copies extracted links to clipboard
- Console logging for monitoring progress

## Usage

1. Navigate to a Douyin user profile or feed page in your browser
2. Open the browser's Developer Console (F12 → Console tab)
3. Copy and paste the contents of `app.js` into the console
4. Press Enter to execute

The script will:
- Auto-scroll for 10 seconds to load posts
- Extract all post links
- Display the count and links in console
- Copy all links to your clipboard

## Configuration

You can modify these settings in the script:

- **Scroll duration**: Change `10000` (10 seconds) to adjust loading time
- **Scroll interval**: Change `1000` (1 second) to adjust scroll speed
- **Link pattern**: Modify the selector `a[href*="/note/"]` for different link types

## Output

The script outputs:
- Console log showing number of links found
- Individual links printed to console
- All links copied to clipboard (newline-separated)

## Requirements

- Modern web browser with JavaScript enabled
- Access to Douyin website
- Developer Console access

## Notes

- Adjust the scroll duration based on your internet speed and page size
- The script filters out duplicate links automatically
- Works best on profile pages with multiple posts