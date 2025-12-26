
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>X (Twitter) Mass Delete – README</title>
</head>
<body>

<h1>X (Twitter) Mass Delete – UI Automation (No Tokens Required)</h1>

<h2>Overview</h2>
<p>This script automates the deletion of tweets and undoing reposts directly through the X (Twitter) web interface. It mimics the manual steps you would take in the browser, requiring <strong>no API keys, tokens, or external tools</strong>. It works with your existing logged-in session.</p>

<h2>Why This Approach?</h2>
<p>I created this script because I was <strong>unable to download my Twitter archive</strong> due to a bug, which prevented me from using the other popular archive-based deletion method. This solution uses the same UI flows you would click manually, making it simple and accessible.</p>

<h2>Features</h2>
<ul>
    <li>Iterates through visible tweet cards on your <strong>Posts</strong> or <strong>Replies</strong> tab.</li>
    <li>Opens the overflow menu for each tweet.</li>
    <li>Clicks <strong>Delete</strong> and confirms, or attempts <strong>Undo repost</strong> if applicable.</li>
    <li>Scrolls to load more tweets and repeats until no more actionable items remain.</li>
</ul>

<h2>Important Notes</h2>
<ul>
    <li><strong>Irreversible:</strong> Deletions cannot be undone. If possible, export your archive first.</li>
    <li><strong>Rate Limits:</strong> Backend limits still apply (~50 deletes per 15 minutes; ~300 per 3 hours). <a href="ocs.x.com/x-api/posts/manage-tweets/introductionOfficial Docs</a></li>
    <li><strong>Fragile Selectors:</strong> X’s UI/DOM may change over time. You might need to tweak selectors. <a href="https://stackoverflow.com/questions/deleting-tweets-with-js-consoleCommunity Discussion</a></li>
</ul>

<h2>How to Use</h2>
<ol>
    <li>Open your X (Twitter) profile in a browser (Posts or Replies tab).</li>
    <li>Open the <strong>Developer Console</strong> (F12 → Console).</li>
    <li>Paste the script and press <strong>Enter</strong>.</li>
    <li>Keep the tab focused while the script runs.</li>
</ol>

<h2>Configuration</h2>
<p>You can adjust these constants to control pacing and reduce rate-limit errors:</p>
<pre><code>
const CLICK_DELAY_MS = 1200;   // Delay after clicks
const SCROLL_DELAY_MS = 1800;  // Wait after scrolling
const MAX_RETRIES = 3;         // Retries for menu actions
const SHORT_PAUSE_MS = 500;    // Small spacing between tweets
</code></pre>


<h2>References</h2>
<ul>
    <li>https://docs.x.com/x-api/posts/manage-tweets/introductionManage Posts – Official Docs</a></li>
    <li>https://stackoverflow.com/questions/64863099/deleting-tweets-with-js-consoleStackOverflow Discussion on UI Selectors</a></li>
    <li>https://chrissmith.xyz/blog/2024/bulk-deleting-tweets/Community Scripts &amp; Blog Posts</a></li>
    <li>https://gist.github.com/lucahammer/1aa16b4d3c1fb04035839da5ef699d65Gist Example</a></li>
</ul>


<h2>Disclaimer</h2>
<p>Use at your own risk. This script interacts with the live UI and may break if X updates its DOM structure.</p>

</body>
</html>
``
