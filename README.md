# Douyin Scraper ([Try Now](https://colab.research.google.com/github/profinderbro/douyin-scraper/blob/main/scraper.ipynb))

Extracts Douyin post links and copies them to clipboard.

## Usage

1. Open Douyin profile/feed page
2. Open Developer option _(press F12)_ then `Console` tab, in Console type:
```
allow pasting
```
3. Paste `app.js` or the below code and press Enter wait for 10 sec 

```
(function() {
  // Scroll to load all posts (optional, comment out if you manually scroll)
  let scrollInterval = setInterval(() => {
    window.scrollTo(0, document.body.scrollHeight);
  }, 1000);

  // Stop scrolling after 10 seconds (adjust as needed)
  setTimeout(() => {
    clearInterval(scrollInterval);
    
    // Grab all <a> tags that look like post links
    const postLinks = Array.from(document.querySelectorAll('a[href*="/note/"]'))
      .map(link => link.href)
      .filter((href, index, self) => 
        href.includes('douyin.com/note/') && self.indexOf(href) === index
      );

    // Output the links to console
    console.log('Found ' + postLinks.length + ' post links:');
    postLinks.forEach(link => console.log(link));

    // Optional: Copy links to clipboard as a single string
    const linksText = postLinks.join('\n');
    navigator.clipboard.writeText(linksText).then(() => {
      console.log('Links copied to clipboard!');
    }).catch(err => {
      console.error('Failed to copy to clipboard:', err);
    });

  }, 10000); // Adjust delay based on how long it takes to load all posts
})();
```

4. Script auto-scrolls for 10 seconds, extracts links, copies to clipboard

## Download Videos

1. Go to [dlpanda.com](https://dlpanda.com/)
2. Paste links one by one
3. Download each video

## Config

- Scroll time: Change `10000` (10 seconds)
- Scroll speed: Change `1000` (1 second)
