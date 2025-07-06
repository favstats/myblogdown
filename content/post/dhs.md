+++
date = 2025-07-05
lastmod = 2025-07-05
draft = false
tags = ["microtargeting", "ad spending"]
title = "DHS Targeted Campaign Threatens Deportation on Meta and Google"
math = true
summary = """
In this post I briefly discuss the targeted campaign that Department of Homeland Security is running to threaten people with Latin American background with deportation.
"""

[header]
image = "headers/dhsads.jpg"
caption = "Spending and Targeting compared between Meta and Google"

+++

A [press release from the Department of Homeland Security](https://www.dhs.gov/news/2025/03/15/dhs-launches-international-ad-campaign-warning-illegal-aliens-self-deport-and-stay) issued earlier this year announced the launch of a "multimillion-dollar ad campaign" that would leverage ads that are "hyper-targeted, including through social media, text message and digital".

The goal, in their words, is to send a

> "warning [to] illegal aliens to not to come to America and break its laws or they will be hunted down and deported".

For this blog post, I will look into how "hyper-targeted" these ads are and how much money DHS is spending on them.

Using public data from the Meta Ad Library and Google's Ad Transparency Report, analyzed with the open-source tool [`metatargetr`](https://github.com/favstats/metatargetr), we can get a good picture of what is going on.

### The Ad Itself:

The ad features Homeland Security Secretary Kristi Noem delivering a threatening message. She states:

> "President Trump has a clear message for those of you who are here illegally: Leave now. If you don't, we will find you and we will deport you. You will never return."

<div align="center">
<a href="https://www.youtube.com/watch?v=hezXQvjzCkQ">
<img src="https://cdn.bsky.app/img/feed_fullsize/plain/did:plc:46yyakot3byghwqc6rhmqzqd/bafkreiasrcfymnds3k3p2zswzue5s7wscdmqf2dv6dknlr2pgh2qhid2wa@jpeg" alt="WARNING - Domestic">
</a>
</div>

### The Scale: Over $2.4 Million Spent Since March

First, the spending is massive. Between March 1st and July 5th of this year, DHS has poured over **$2.4 million** into digital ads on Google and Meta.

![](https://i.imgur.com/3QaJCQK.png)

### How Good is the "Hyper-Targeting"?

The DHS press release used the term "hyper-targeted," and the data shows what this means. The spending is geographically concentrated in U.S. counties with some of the largest Latino populations.

![Image: A scatter plot titled "Homeland Security advertising concentrated in U.S. counties with 25%+ Latino pop."](https://i.imgur.com/yiI0kWp.png)

As the plot shows, counties like Hidalgo, TX (over 90% Latino) and Miami-Dade, FL (over 70% Latino) are major targets and the vast majority of ads go to areas with a 25%+ Latino population. It is a clear strategic decision to aim this messaging at specific communities based on ethnicity.

Not convinced yet? Well, the use of "detailed" target audiences makes it very clear who the Trump administration is aiming to reach. The campaign targets users based on interests that are likely strongly correlated with the Latino demographic.

![Image: A bar chart titled "Most Used Detailed Targeting Criteria by DHS Digital Ads."](https://i.imgur.com/LcIbuy8.png)

Targeting users interested in "Regional Mexican," "Mexican pop music," and the "Spanish language" is a clear proxy for ethnicity. It also demonstrates how trivial it is to bypass Meta's supposed safeguards.

Because Meta *DOES* claim it has [**banned targeting by "race or ethnicity"**](https://www.facebook.com/business/news/removing-certain-ad-targeting-options-and-expanding-advertiser-controls), but anyone who is only slightly familiar with targeted ad campaigns knows how easy it is to find proxies for sensitive data categories.


### The "Hyper-Targeting" is Bad, Duh


Herein lies the central problem. The ad claims to focus on "illegal aliens" but the "hyper-targeting" method is, perhaps unsurprisingly, *quite indiscriminate*. Using broad cultural proxies like musical taste or language blankets entire communities with intimidating messages.

The result is that U.S. citizens, legal residents, and their families are served a threatening government message based on nothing more than their (likely) cultural background. Obviously, the issue is not that the targeting is imprecise though. It is that the tactic itself, subjecting a whole demographic to a message of intimidation, is fundamentally problematic. 

This approach just adds to the [widespread "climate of fear"](https://www.latimes.com/delos/newsletter/2025-06-27/ice-raids-latino-community-racial-profiling) caused by the Trump administration's promise of mass deportation. It becomes particularly worrisome when placed in the context of [well-documented cases](https://www.latimes.com/california/story/2025-07-02/federal-lawsuit-targets-trump-administration-immigration-raids), where U.S. citizens too have been swept up in enforcement actions. To the suprise of probably only few people, "hypertargeted" is just a poorly-hidden euphemism for digital racial profiling.
