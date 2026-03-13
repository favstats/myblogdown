+++
date = 2026-03-13
lastmod = 2026-03-13
draft = false
tags = ["microtargeting", "transparency", "google", "elections"]
title = "It's Not Just Meta: Political Parties in the Netherlands Are Advertising with Google Ads Despite Ban"
math = true
summary = """
Google, just like Meta, banned political ads in the EU in 2025. We found political ads from Dutch parties in Google's own Transparency Center. It gets worse: even more ads are being served on news websites through Google's infrastructure with no trace in their transparency tools at all.
"""

[header]
image = "headers/google_political_ads_collage.png"
caption = "Political ads from D66, DENK, GroenLinks, PvdA, JA21, Partij voor Ontwikkeling, and Partij voor de Dieren served via Google's ad infrastructure on at5.nl"

+++

<style>
.article-style figcaption:before {
  content: "" !important;
  counter-increment: none !important;
}
</style>

Last few days I talked a lot about Meta running political ads despite their ban, covered by [NOS](https://nos.nl/nieuwsuur/artikel/2605591-meta-s-verbod-op-politieke-reclame-werkt-niet-partijen-adverteren-gewoon-door) and the [AD](https://www.ad.nl/politiek/honderden-verboden-politieke-advertenties-overspoelen-sociale-media-gevaarlijk-dat-dit-kan~ac746b9f/). And it's not just here: the same problem has been found in [Belgium](https://www.vrt.be/vrtnws/nl/2026/03/04/politici-plaatsen-nog-steeds-politieke-advertenties-op-meta/), [Denmark](https://www.dr.dk/nyheder/politik/folketingsvalg/flere-sf-ere-taget-i-forbudt-reklame-paa-facebook), and [documented by Justice for Prosperity](https://justiceforprosperity.org/honderden-illegale-politieke-advertenties/). Your question might be: is this just Meta, or why the focus on that platform?

The answer is: it's not just Meta. Google, just like Meta, [announced in 2025](https://blog.google/around-the-globe/google-europe/political-advertising-in-eu/) that it would no longer carry political ads in the EU, in response to the [Transparency and Targeting of Political Advertising regulation](https://eur-lex.europa.eu/DE/legal-content/summary/transparency-and-targeting-of-political-advertising.html) (TTPA, Regulation (EU) 2024/900). I [wrote about this before](/post/israelads/) when I found Israel's Foreign Affairs Ministry running undisclosed ads on Google. And for all its flaws, Meta's Ad Library at least lets you search for ad content. Google's [Ads Transparency Center](https://adstransparency.google.com/) only lets you search by advertiser name or outgoing link, not by content, which makes finding political ads significantly harder.

## Political Ads in Google's Own Transparency Center

Google maintains an [Ads Transparency Center](https://adstransparency.google.com/) where anyone can look up what ads an advertiser is running. Despite Google's ban on political advertising in the EU, we found local political parties whose ads are visible right there, in Google's own transparency tool:

- [Leefbaar Almere](https://adstransparency.google.com/advertiser/AR17495549022557962241?region=NL&start-date=2026-01-01&end-date=2026-03-13)
- [Lokaal Zaans](https://adstransparency.google.com/advertiser/AR15845593140586086401?region=NL&start-date=2026-01-01&end-date=2026-03-13)
- [Frisse Wind 21](https://adstransparency.google.com/advertiser/AR06791428246664642561?region=NL&start-date=2026-01-01&end-date=2026-03-13)

{{< figure src="/img/google_ads/transparency_frisse_wind.jpg" caption="Frisse Wind 21 ads in Google's Ads Transparency Center" >}}

{{< figure src="/img/google_ads/transparency_lokaal_zaans.jpg" caption="Lokaal Zaans ads in Google's Ads Transparency Center" >}}

{{< figure src="/img/google_ads/transparency_leefbaar_almere.jpg" caption="Leefbaar Almere ads in Google's Ads Transparency Center" >}}

What makes it even harder to assess the scale: Google's Transparency Center does not show reach or impression data for these ads. Click on any of them and you'll see that this data won't be available until sometime in April 2026, a full month *after* the municipal elections on 18 March. By the time anyone can check how many people saw these ads, the votes will have been counted long ago.

{{< figure src="/img/google_ads/transparency_reach_unavailable.jpg" caption="Google's Transparency Center shows no reach data until April 2026, a month after elections" >}}

But at least these ads leave a trace. You can find them and document them using Google's own tools.

## It Gets Worse: Political Ads Served by Google with No Trace at All

While monitoring the Dutch municipal elections, we spotted something on [at5.nl](https://www.at5.nl), Amsterdam's local news outlet: display ads from political parties, appearing right alongside editorial election coverage. The ads carried the proper TTPA disclaimer ("Dit is een politieke reclameboodschap in het kader van de gemeenteraadsverkiezingen"). And the page itself showed "Advertentie weergegeven door Google" (Advertisement displayed by Google).

{{< figure src="/img/google_ads/at5_d66_fullpage.png" caption="D66 political ad displayed on the at5.nl homepage, served via Google's ad infrastructure" >}}

We built a scraper to systematically collect these ads. Over the course of several days, we captured political display ads from D66, DENK, PvdA, GroenLinks, JA21, Partij voor Ontwikkeling, and Partij voor de Dieren on at5.nl, all served through Google's ad infrastructure:

{{< figure src="/img/google_ads/denk.png" caption="DENK: \"Voorrang voor Amsterdammers bij een betaalbare woning\"" >}}

{{< figure src="/img/google_ads/d66.png" caption="D66: \"Het kan wél\"" >}}

{{< figure src="/img/google_ads/pvda_stem.png" caption="PvdA: \"Stem PvdA\"" >}}

{{< figure src="/img/google_ads/groenlinks.png" caption="GroenLinks: \"Stem 18 maart GroenLinks Amsterdam\"" >}}

{{< figure src="/img/google_ads/ja21.png" caption="JA21: \"Amsterdam weer van ons. Stem 18 maart\"" >}}

{{< figure src="/img/google_ads/pvda_kies.png" caption="PvdA: \"Kies 18 maart voor Amsterdam\"" >}}

{{< figure src="/img/google_ads/partij_voor_ontwikkeling.png" caption="Partij voor Ontwikkeling: \"Amsterdam van het slot af\"" >}}

{{< figure src="/img/google_ads/partij_voor_de_dieren.png" caption="Partij voor de Dieren: \"Stem 18 maart\"" >}}

Every single one of these ads carries the official `politiekereclame.nl` disclaimer, correctly self-identifying as political advertising for the municipal elections. And yet, when you search for these parties and their ads in Google's Ads Transparency Center, they don't show up. There is no public record that they ever ran. For researchers, journalists, and regulators, these ads are essentially invisible.

## How Does This Happen and Why It Matters

Google's enforcement apparently relies on a [self-declaration system](https://support.google.com/platformspolicy/answer/16411925?hl=en) where advertisers declare whether they intend to run political ads. If they say "No," the ads seemingly flow through unchecked, even when they use official party logos and political disclaimers. There is no indication that the system scans ad content or cross-references advertiser identities. This means that political ads end up on news sites right next to journalism about the very same elections, with no public record in Google's transparency tools that they ever ran.

On Tuesday, Laurens Dassen (Volt) [questioned the Minister of the Interior](https://www.tweedekamer.nl/kamerstukken/plenaire_verslagen/detail/2025-2026/49#1bc3b80d) about this enforcement failure in parliament. As I [wrote for Tech Policy Press](https://www.techpolicy.press/what-data-reveals-about-meta-and-googles-political-ad-ban-in-the-eu/), both Meta and Google shut down their old transparency tools when they introduced their bans, and the new EU-wide ad repository that is supposed to replace them won't be operational until October 2026 at the earliest. That means these elections are happening in a transparency vacuum, where political ads are running but nobody has the tools to properly monitor them.

This research is part of our work at [HEIO](http://heio.nl/) ([University of Amsterdam/ASCoR](https://ascor.uva.nl/), [AI Forensics](https://aiforensics.org/), [Trollrensics](https://www.trollrensics.com/), [Post-X Society](https://www.postxsociety.org/)). We're investigating further. More to come.
