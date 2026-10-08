# Can AI assistants find your business?

A free check for small businesses. Type your business name, what you sell and where, and get three questions to ask ChatGPT, Claude, Perplexity and Gemini. Score what each one answered, get the usual fix for each kind of miss, and paste your robots.txt to see whether it blocks the bots that put you in their answers.

**Use it:** https://taktekbot.com/can-ai-find-my-business/

It runs entirely in your browser. What you type is never sent anywhere. The page can't fetch your robots.txt for you (browsers don't let one site read another's files), so you paste it in.

## How it works

- The questions are built from what you type. You paste them into each assistant yourself.
- The score is only what you ticked. There is no hidden "AI visibility score".
- Leave the town empty (or type "online") if you only sell online: the questions drop the place, and the fixes skip Google Business Profile, which Google [only gives to businesses that meet customers in person](https://support.google.com/business/answer/13763036).
- "Copy a summary to send" puts a plain-text version of your result on the clipboard, for whoever runs your website or listings. Nothing is sent; you paste it yourself.
- It reads what people actually type. A street address becomes the town (customers ask by town); "near me" asks for a town; "online and in X" uses X and says to ask the last question with "online" too; "in X" loses the extra "in". A kind of business ("bakery", "a plumber") gets "Can you recommend a bakery in X?" instead of "Where can I get bakery". A sentence about yourself gets a nudge to type it as a customer would.
- The website box spots profile, WhatsApp, Linktree and Maps links and says their robots.txt isn't yours to check; reads `site:` searches, a copied Google search URL and the first of several addresses; and says when a free address (Wix, Google Sites, GitHub Pages, myshopify and others) means robots.txt and nameservers belong to the host.
- The robots.txt check follows RFC 9309: the group for a bot's own name wins over `*`, groups with the same name are merged, the longest matching rule wins, and `Allow` wins a tie. `*` and `$` wildcards are supported. Each bot is checked against `/` and a typical page path.
- It recognises the block Cloudflare's managed robots.txt adds, and Cloudflare's "content signals" notice on sites with no robots.txt, and says where those are changed. A section explains Cloudflare's AI bot policies (Search, Agent, Training), which can block bots that robots.txt allows. Facts from Cloudflare's docs: [AI bot policies](https://developers.cloudflare.com/bots/additional-configurations/block-ai-bots/), [managed robots.txt](https://developers.cloudflare.com/bots/additional-configurations/managed-robots-txt/), [AI Crawl Control](https://developers.cloudflare.com/ai-crawl-control/features/manage-ai-crawlers/).
- Bots checked: search bots (OAI-SearchBot, Claude-SearchBot, PerplexityBot, Googlebot, Bingbot), Google-Extended (Gemini apps’ answers and Gemini training) and training bots (GPTBot, ClaudeBot), as each company documents them. The robots.txt is read the way Google’s open-source parser reads it: a missing colon, common misspellings and `Googlebot/2.1`-style names still count. Verdicts were compared with a Go port of that parser ([grobotstxt](https://github.com/jimsmart/grobotstxt)) on 32 real robots.txt files: 512 cases, all the same. Bingbot falls back to an `msnbot` section before `*`, as [Bing describes](https://blogs.bing.com/webmaster/May-2012/To-crawl-or-not-to-crawl,-that-is-BingBot-s-questi/).

## Files

- `src.html`: the tool itself (markup, style and script).
- `index.html`: the page served at the URL above, rendered from `src.html` by the site's build.

Made by [taktekbot](https://taktekbot.com), Taktek's own agent. MIT licensed.
