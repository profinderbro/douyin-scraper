# Douyin Scraper

Extracts Douyin post links and copies them to clipboard with improved user experience.

## Quick Start

Choose the method that works best for you:

- **Method 1**: Python-Colab approach - Best for extracting high-quality media URLs directly
- **Method 2**: Browser-only approach - Quick and requires no additional tools

---

## Method 01: Using Python-Colab ([Try Now](https://colab.research.google.com/github/profinderbro/douyin-scraper/blob/main/scraper.ipynb))

### When to use this method:
- You want the highest quality media URLs
- You need to process a large number of posts
- You prefer a more controlled extraction process

### Step-by-Step Instructions:

1. **Open the Douyin profile** in your browser
   - Navigate to the profile whose posts you want to scrape

2. **Open Developer Tools**
   - Press `F12` to open the Inspect panel
   - Click on the **Network** tab at the top
   - Select the appropriate filter:
     - `img` filter for images only
     - `media` filter for videos only
   
   *After pressing F12, it should look like this:*
   <img width="1152" height="605" alt="Developer Tools Network Tab" src="https://github.com/user-attachments/assets/a7708104-bf43-4078-849b-1aab50bf984e" />

3. **Capture post URLs**
   - Quickly hover your cursor over all the posts on the page
   - *Important: No need to click or open posts, just hover over them*
   - The Network tab will automatically capture the URLs

4. **Copy all URLs**
   - Right-click on any file that appeared in the Network tab
   - Select **"Copy all URLs"** (not "Copy URL" which only copies a single link)

5. **Open Google Colab**
   - Visit this link: [https://colab.research.google.com/github/profinderbro/douyin-scraper/blob/main/scraper.ipynb](https://colab.research.google.com/github/profinderbro/douyin-scraper/blob/main/scraper.ipynb)
   - This will open the Python notebook in your browser

6. **Create and populate the URLs file**
   - In Colab, create a new file named `urls.txt`
   - Paste all the URLs you copied from the Network tab
   
   *Your Colab interface should look like this:*
   
   <img width="638" height="428" alt="Colab Interface" src="https://github.com/user-attachments/assets/1b880408-3ad6-4944-a16f-9a55f74eed1f" />

8. **Run the script**
   - Click the play button to execute the notebook
   - Wait for the script to process all URLs

---

## Method 02: Using Browser Only

### When to use this method:
- You want a quick solution without additional tools
- You only need post links (not direct media URLs)
- You're comfortable running JavaScript in your browser console

### Step-by-Step Instructions:

1. **Open the Douyin profile/feed page** in your browser

2. **Open Developer Console**
   - Press `F12` to open Developer Tools
   - Navigate to the **Console** tab
   - Type `allow pasting` and press Enter (this enables pasting in the console)

3. **Run the extraction script**
   - Copy the entire code block below:
   ```javascript
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
   - Paste the code into the console and press Enter
   - Wait for 10 seconds while the script auto-scrolls and extracts links

4. **Retrieve your links**
   - The script will automatically copy all post links to your clipboard
   - You can also view the links in the console output

---

## Downloading Videos

### Option 1: Individual Downloads
1. Go to [dlpanda.com](https://dlpanda.com/)
2. Paste each link one by one
3. Download each video individually

### Option 2: Batch Downloads (Recommended for multiple videos)
If you have many videos to download, consider these alternatives:

1. **Using a download manager**:
   - Try tools like JDownloader 2 or Internet Download Manager
   - These can process multiple links simultaneously

2. **Using browser extensions**:
   - Install video download extensions like Video DownloadHelper
   - These can detect and download videos from supported sites

3. **Using command-line tools** (for advanced users):
   - Tools like `youtube-dl` or `yt-dlp` can be used with text files containing URLs
   - Example command: `yt-dlp -a urls.txt`

---

## Tips & Troubleshooting

### For Method 01:
- **Problem**: No URLs appear in the Network tab
  - **Solution**: Make sure you're hovering over posts, not just scrolling
  - **Solution**: Check that you've selected the correct filter (img/media)

- **Problem**: Colab shows errors
  - **Solution**: Make sure you've created the `urls.txt` file correctly
  - **Solution**: Check that all URLs are properly formatted (one per line)

### For Method 02:
- **Problem**: Script doesn't find any links
  - **Solution**: Make sure you're on a Douyin profile/feed page, not an individual post
  - **Solution**: Try increasing the timeout value (change `10000` to a higher number)

- **Problem**: Links aren't copied to clipboard
  - **Solution**: Some browsers block clipboard access. You can manually copy the links from the console output
  - **Solution**: Check browser permissions for clipboard access

### General Tips:
- For large profiles, consider running the script multiple times to capture all posts
- If you're having issues with one method, try the alternative method
- Both methods may require you to be logged in to Douyin to view certain content

---

## FAQ

**Q: Is this tool safe to use?**  
A: Yes, both methods only extract publicly available information from Douyin. However, be cautious about where you paste and store the extracted URLs.

**Q: Can I extract private profiles?**  
A: No, these methods only work for publicly accessible content.

**Q: Why are some videos not downloading?**  
A: Some videos may have regional restrictions or may have been removed after you extracted the links.

**Q: Can I automate the entire process?**  
A: While the scripts automate parts of the process, completely automated scraping may violate Douyin's terms of service.

**Q: How often should I use these tools?**  
A: Use responsibly and avoid excessive requests that might get your IP address temporarily blocked.
