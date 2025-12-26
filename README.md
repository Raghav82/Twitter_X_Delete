
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

<h2>Improvements &amp; Rate-Limit Handling</h2>

<p>This version improves reliability and reduces stalls by aligning the script’s pacing with X’s backend limits, while removing the tab-focus gate that caused unnecessary pauses.</p>

<h3>What’s improved</h3>
<ul>
    <li><strong>Rate-limit aware soft cap:</strong> Auto-pause after ~<strong>45 actions per 15 minutes</strong> to avoid hitting the documented <strong>50 deletes / 15 minutes</strong> user window.</li>
    <li><strong>Long-cap protection:</strong> Optional auto-pause near <strong>~290 actions per 3 hours</strong> to respect the ~<strong>300 actions / 3 hours</strong> backend cap.</li>
    <li><strong>Jittered timing:</strong> Adds small random jitter to delays so requests don’t look perfectly periodic (helps reduce anti-abuse triggers).</li>
    <li><strong>Lower retry pressure:</strong> <code>MAX_RETRIES = 2</code> plus a brief cooldown reduces burstiness when UI elements render slowly.</li>
    <li><strong>Failure-streak cool-off:</strong> If several actions fail back-to-back (likely 429s), the script pauses <strong>15 minutes</strong> and then resumes.</li>
    <li><strong>Focus gate removed:</strong> The previous <code>awaitFocus()</code> check is removed to prevent the script from stalling even when the tab is seemingly in focus.</li>
</ul>

<h3>Config knobs (defaults shown)</h3>
<pre><code>
const CLICK_DELAY_MS_BASE  = 2000;   // after each click (menu, confirm)
const SCROLL_DELAY_MS_BASE = 2400;   // after scroll to load more posts
const SHORT_PAUSE_MS_BASE  = 800;    // spacing between items
const JITTER_MAX_MS        = 500;    // random jitter added to all delays

const MAX_RETRIES          = 2;      // conservative to reduce burst pressure

const SOFT_CAP_PER_WINDOW  = 45;                 // ~50/15-min backend window
const WINDOW_RESET_MS      = 15 * 60 * 1000;     // 15 minutes

const LONG_CAP_PER_3H      = 290;                // ~300/3-hour backend cap
const LONG_RESET_MS        = 3 * 60 * 60 * 1000; // 3 hours

const FAILURE_STREAK_LIMIT = 7;                  // consecutive failures → cool-off
const FAILURE_COOLDOWN_MS  = 15 * 60 * 1000;     // 15 minutes
</code></pre>

<h3>Tips</h3>
 <li>Keep the tab foregrounded for smoother modal rendering (no longer required, but helps).</li>
 <li>If you still see stalls, increase delays (e.g., +300–500ms) or lower MAX_RETRIES=1.</li>
 <li>For large accounts, expect multi-window runs: the script will pause and resume as limits reset.</li>
<ul>


</body>
</html>

