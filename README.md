# Douyin Scraper

Extracts Douyin post links and copies them to clipboard.

## Methode 01 [Using Browser Only]

1. Open Douyin profile/feed page
2. Open Developer option _(press F12)_ then `Console` tab, in Console type:
```
allow pasting
```
3. Paste the below code and press Enter wait for 10 sec 

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

## Methode 02 Using Python-Colab ([Try Now](https://colab.research.google.com/github/profinderbro/douyin-scraper/blob/main/scraper.ipynb))

1. Open the douyin profile in browser, press `F12` to open inspect then so to the network tab shown at top  and select `img` filter for images only and `media` for videos only

<img width="1152" height="605" alt="image" src="https://github.com/user-attachments/assets/a7708104-bf43-4078-849b-1aab50bf984e" />

2. Then hover and the cursore fasty to all the posts _(no need to open just hover fastly the network tab will cath that automatically)_
3. Now right the the file come in the netwok tab and right click on any and select `copy all urls` not `copy url`  as we want all at once

4. Now open Colab _(Google's Python NoteBook Free)_ , just paste this link to the broswer url box:
```
https://colab.research.google.com/github/profinderbro/douyin-scraper/blob/main/scraper.ipynb
```

<img width="638" height="428" alt="image" src="https://github.com/user-attachments/assets/1b880408-3ad6-4944-a16f-9a55f74eed1f" />

5. create a new file named `urls.txt` and paste all urls from the network tab (`copy all urls`) of browers's inspect mode
6. Hit the play button 
