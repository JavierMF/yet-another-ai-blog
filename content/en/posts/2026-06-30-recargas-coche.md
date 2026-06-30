---
title: "Tracking EV charging the easy way"
date: 2026-06-30
type: post
categories: [Productivity]
tags: [Notion, Claude, Skills, Electric car, PDF]
images: ["/img/posts/recargas-notion.png"]
---

A few months ago we switched to a fully electric car, and the way we "refuel" changed completely. We don't have a charger at home, so we always charge at public stations. But with an EV the pattern is the opposite of what it was with combustion cars — instead of stopping when you're nearly empty to fill up, you do small, frequent top-ups whenever the car is parked: at a parking lot, at a shopping center, at the cinema, at a restaurant that has a charger.

The result was a pile of small charges from many different providers, each with their own app and pricing, and no clear picture of how much we'd spent in total that month.

## ⚡ A ridiculously simple solution

The solution I put together to track the spending is almost embarrassing in how simple it is. The full process:

1. Open the banking app, find the charge for the top-up, tap "share receipt" → generates a PDF.
2. Send it to Claude on my phone, attach the PDF, and write "Log this charge".
3. Done.

The skill that kicks in extracts the provider, date, and amount from the PDF, and adds it to a Notion database. From there I can easily see the monthly total, group by provider, compare months.

{{< figure src="/img/posts/recargas-notion.png" alt="EV charging log in Notion" width="70%" >}}

What surprised me was how straightforward the PDF extraction turned out to be. I expected to have to tweak the prompt, give it examples, provide some structure — but I didn't have to do anything. First try, Claude read the receipt and extracted exactly what I needed. I'm not sure if it's because bank receipts have a predictably consistent structure or if Claude is just very good at this, but it worked with zero special configuration.

## 🚗 Built from my phone

Something unusual about this project was the "development process", if you can even call it that. I was waiting at a doctor's office, bored, and the idea came to me. I started exploring in a Claude chat whether something like this would be possible: what fields the database would have, how it would extract data from the PDF, how it would connect with Notion.

Before I knew it we weren't just discussing the idea — Claude had created the database in Notion, processed a couple of test receipts, and written the skill to repeat it in the future. All in the time it took to wait for my appointment.

## 📊 What I've discovered

In case anyone's wondering: yes, I'm spending a bit more on charging than I used to spend on petrol. But not because electricity is expensive — per kilometre it's significantly cheaper — but because since getting the electric car we're driving a lot more. It's so comfortable and enjoyable that we've multiplied our day trips and car journeys. The numbers don't lie, but they don't tell the whole story either.
