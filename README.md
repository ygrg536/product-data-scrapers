# product data scraper: how to pick one for e-commerce price tracking, with real credit costs and plan prices compared

Most people searching for a product data scraper want the same thing: pull product names, prices, stock status and seller offers from retail sites on a schedule, without getting blocked or writing a parser for every site layout change. The short answer is that for most e-commerce tracking jobs, a managed scraping API is the practical route — you send a request, the service rotates IPs, renders JavaScript, clears CAPTCHAs, and returns structured JSON. One such option is ScraperAPI, which pairs a general-purpose API with dedicated structured endpoints for Amazon, Walmart, Target, Home Depot, Lowe's, eBay and Google Shopping.

This guide covers how these tools actually bill you (the part most comparison posts skip), what ScraperAPI's full plan list costs, where the hidden per-site credit multipliers change your math, and which situations call for a different tool entirely.

> **Quick pick:** If you're tracking Amazon or multi-retailer prices and need more than a few thousand requests a month, ScraperAPI's **Business plan at $299/month (3M credits, 100 concurrent requests, country-level geotargeting)** is the tier most price-monitoring teams land on. Smaller projects can start on the free plan — 1,000 credits/month, no credit card — and a 7-day trial with 5,000 credits to test at scale. 👉 [See all ScraperAPI plans and current prices](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## What a product data scraper actually has to do

A product data scraper is any tool that extracts structured fields — title, price, availability, seller, ratings, images — from product pages. The reason managed APIs exist is that the easy part (parsing HTML) is dwarfed by the hard part: most retail sites sit behind IP blocks, CAPTCHAs, and bot-detection systems like Cloudflare, Datadome and PerimeterX, and they change their layouts often enough that homegrown selectors break quietly.

A managed API handles that layer for you. In ScraperAPI's case, every plan includes JS rendering, premium residential and mobile IPs, rotating proxy pools, CAPTCHA and anti-bot detection, automatic retries, custom header and session support, and unlimited bandwidth with a 99.9% uptime guarantee. The credit system bundles all of that into one unit: one credit is the cost of a standard page request.

For e-commerce specifically, ScraperAPI also offers structured data endpoints. Instead of getting raw HTML back, you get a consistent JSON schema across six retailers plus Google Shopping: product details, variations, offer-level pricing from every seller on a listing (fulfilment type, shipping fees, delivery estimates), sponsored slot identification, search rankings, review data, and zip-code level availability. Amazon coverage runs deepest, including Buy Box detection, parent/child ASIN variations and FBA/FBM fulfilment data. The vendor claims up to 95% accuracy across 150+ countries — that's their own published figure, so treat it as a vendor claim, not an independent benchmark.

## ScraperAPI's full plan list and prices

Here is the complete plan lineup from the official pricing page. Annual billing saves 10%, shown as the per-month equivalent.

| Plan | Monthly price | Annual (per month) | Credits / month | Concurrency | Geo-targeting | Get it |
| --- | --- | --- | --- | --- | --- | --- |
| Free | $0 | — | 1,000 | 5 | — | [ Start free, no card](https://www.scraperapi.com/?fp_ref=coupons) |
| Hobby | $49 | $44.10 | 100,000 | 20 | US & EU only | [ Get Hobby](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | US & EU only | [ Get Startup](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | Country-level | [ Get Business](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Scaling | $475 | $427.50 | 5,000,000 | 200 | Country-level | [ Get Scaling](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | Country-level | [ Get Professional](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | Country-level | [ Get Advanced](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Enterprise | Custom | Custom | 22,000,000+ | 500+ | Country-level | [ Talk to sales](https://www.scraperapi.com/pricing/?fp_ref=coupons) |

Two things worth noting beyond the table. First, the documentation also lists a Student plan tier that isn't shown with a price in the standard plan comparison, so if that's you, check the pricing page directly. Second, Hobby and Startup are limited to US and EU geo-targeting and only 30 days of analytics history; country-level targeting and unlimited analytics start at Business. That's a real fork in the road if you need to see prices as shoppers in, say, Japan or Brazil see them.

## The credit cost nobody warns you about

The single most misunderstood part of credit-based scrapers is that "100,000 credits" rarely means 100,000 product pages. ScraperAPI charges different credit amounts per site: a standard page costs 1 credit, **Amazon costs 5**, Google and Bing (including subdomains) cost **25**, and LinkedIn costs **30**. Sites behind Cloudflare, Datadome or PerimeterX protection add 10 credits per request when the service bypasses them.

Run the numbers on the Hobby plan and the difference is stark. 100,000 credits buys you 100,000 standard pages, but only **20,000 Amazon product pages** — and if a target sits behind heavy bot protection, that figure shrinks further. A Google-heavy workload on Hobby gets you just 4,000 requests. This is why the "starting price" numbers you see in comparison articles can be misleading by a factor of five or more depending on what you're scraping.

Two safeguards make this manageable. The Domain Cost Estimator in your dashboard shows the exact credit cost for any URL before you commit, and you can set a `max_cost` parameter per scrape so no single request eats more credits than you intended. Both are worth using on day one, before you've burned a week's budget on one expensive domain.

## What happens when you run out of credits mid-month

Credits running out doesn't mean your pipeline dies, but the behaviour differs by plan, and it's buried in the documentation rather than the marketing pages.

By default, scraping pauses until your credits renew. From there:

1. **Auto-upgrade** (Hobby, Startup, Business, Scaling, Professional): opt in, and when credits hit zero your account automatically moves to the next plan tier, which usually has a better price-per-credit.
2. **Pay-as-you-go** (Scaling, Professional, Advanced, Enterprise): keep scraping past your limit at a fixed per-credit rate, capped by a monthly spending limit you set yourself. This is a spending cap, not a pre-charge — the service won't exceed it unless you change the setting in billing.
3. **Early annual renewal**: annual plans can renew before the term ends to get a fresh batch of credits.

One quirk to plan around: if you exceed your plan's concurrency limit, you get a 429 response and the request is turned away rather than queued. There's no extra charge, but your job simply doesn't run at that moment. If your scheduler fires 50 parallel requests on a Hobby plan (20 concurrent), 30 of them bounce. Throttling your workers to match your plan's concurrency is a config change that saves a lot of head-scratching.

On the risk side, the terms are unusually friendly. You can cancel anytime from the dashboard without charge, and there's a 7-day no-questions-asked refund policy if the service doesn't work for you. Combined with the free 5,000-credit trial week, you can validate real-world success rates on your actual target sites before spending anything. 👉 [Try the 7-day trial with 5,000 free credits](https://www.scraperapi.com/?fp_ref=coupons)

## Real cost: monthly vs annual billing

Annual billing drops each plan by 10%. On Hobby that's $44.10/month billed annually versus $49 monthly — $58.80 saved over a year. On Business, the difference is $29.90/month, or about $359 a year. The savings are real but modest; the stronger argument for annual is that it locks your rate and pairs with the early-renewal option if you scale mid-year.

If your request volume is spiky — a few quiet months, then a Prime Day or Black Friday push — monthly billing plus pay-as-you-go on Scaling and above is often cheaper overall than paying for a permanent high tier. ScraperAPI explicitly markets burst capacity for peak events, and customers reportedly run up to 200 million requests per month with onboarding-time custom concurrency limits.

## How it stacks up against the alternatives

Entry pricing across the major e-commerce scraping tools varies wildly, and — this is the part most listicles gloss over — the billing units are different, so the sticker prices aren't directly comparable. Here's what the documented numbers look like as of mid-2026:

| Tool | Starting price | Free tier | Bills by | Best for |
| --- | --- | --- | --- | --- |
| ChocoData | $19/mo (Vibe) | 1,000 requests/mo, no card | Credits/requests | Multi-site price scraping via one endpoint, lowest entry price |
| Oxylabs | $49/mo (Micro, up to 98,000 results) | 2,000 results, no card | Results | Deep parsed fields per retail page type |
| Bright Data | PAYG $1.50 per 1,000 records | 5,000 records/mo, no card | Delivered records | Bulk price datasets |
| ScrapingBee | $49/mo (Freelance) | 1,000 credits, no card | Credits | Simple credit-based API with Amazon and Google endpoints |
| Apify | $29/mo (Starter) | $5 usage/mo, no card | Platform dollars | Reusing prebuilt e-commerce actors |
| Zyte API | PAYG from ~$0.06 per 1,000 | $5 credit (30 days) | Per successful response, by site complexity | Mixed easy/hard targets |
| ScraperAPI | $0 free plan | 1,000 credits/mo + 5,000-credit trial | Credits | General API with structured retail endpoints |

A caveat on all of these figures: they come from vendor-published pricing gathered by third-party comparison sites, not from standardized independent benchmarks, and one of the main comparison sites openly discloses affiliate relationships with some vendors listed. Treat the numbers as directionally right and verify against each vendor's own pricing page before committing.

Where does ScraperAPI genuinely fit? ChocoData's $19 entry and Zyte's complexity-tiered PAYG are cheaper on-ramps for light or mixed workloads. Oxylabs and Bright Data offer deeper per-page parsing and per-record billing respectively, which some data teams prefer for bulk datasets. ScraperAPI's edge is the combination of a genuinely usable free tier, structured retail endpoints that eliminate selector maintenance, and mid-tier plans (Business at $299) that include country-level targeting without jumping straight to enterprise pricing. If you're mostly scraping Amazon product pages for price tracking, the 5-credit rate plus Amazon-specific fields (Buy Box, ASIN variations, FBA/FBM) is a strong fit.

## When a product data scraper is overkill

Honest limit-setting: if you need product data from one site, once, a browser extension or a one-off script beats any API subscription. And if your monthly volume is under a few thousand standard pages, ScraperAPI's free 1,000 credits may cover you indefinitely — upgrading before you've outgrown the free tier is money spent on nothing.

The tool starts earning its keep when at least one of these is true: you're tracking more than a handful of products on a schedule (hourly or nightly refreshes of thousands of ASINs are explicitly supported), you need offer-level data across multiple sellers, your targets have real bot protection, or you're building price monitoring into a product your own customers rely on. There's no bandwidth-based pricing and no way to buy individual proxy IPs — everything is request-credit based, which suits monitoring workloads but not bulk file downloads.

## FAQ

**How many products can I track per month on each plan?**
It depends entirely on the target site. Using Amazon's 5-credit rate: Hobby covers about 20,000 Amazon product fetches, Startup about 200,000, Business about 600,000. Standard 1-credit sites stretch those numbers fivefold. Check the Domain Cost Estimator for your actual targets.

**Do I need a credit card to try it?**
No. The 7-day trial with 5,000 credits requires no credit card, and the permanent free plan (1,000 credits/month) doesn't either.

**Can I get my money back?**
Yes — ScraperAPI offers a 7-day no-questions-asked refund, and you can cancel a subscription at any time from the dashboard without being charged.

**What happens if a site blocks my requests anyway?**
Sites behind Cloudflare, Datadome or PerimeterX cost an extra 10 credits per request when ScraperAPI bypasses them, and automatic retries are included on all plans. If a specific domain consistently fails, the Domain Cost Estimator and support can tell you before you waste volume on it.

**Can I scrape Google Shopping prices?**
Yes. Google Shopping is included in the structured retail endpoints alongside the six major retailers, and search ranking data is part of the returned schema.

## Which plan should you actually pick

A few rules of thumb, based on the verified numbers above:

- **Just validating an idea or scraping one competitor's catalogue occasionally** → stay on the free plan and the 7-day 5,000-credit trial. Don't pay yet.
- **Regular price tracking on Amazon or standard sites, up to ~20,000 Amazon fetches a month** → Hobby at $49/month is the entry point, but check the US/EU geo-targeting limit first.
- **A price-monitoring product with customers who expect country-specific prices** → Business at $299/month is where country-level geotargeting and unlimited analytics start; below that tier you're constrained to US and EU.
- **High-volume, spiky workloads around Prime Day or Black Friday** → Scaling ($475/month) or above, where pay-as-you-go with a self-set spending cap keeps workflows running through peaks without surprise bills.

Before you commit to anything, do two things: run your actual target URLs through the Domain Cost Estimator so you know your true credits-per-page, and confirm your concurrency needs fit the plan — a 429-heavy workload is a plan-mismatch problem, not a tool failure. Then start with the trial and measure success rates on your own targets rather than trusting anyone's benchmark, including this one. 👉 [Compare plans and start your free trial](https://www.scraperapi.com/pricing/?fp_ref=coupons)
