---
layout: post
title:  "Menial: The Beginnings"
date:   2016-01-12
categories: thought
published: true
---

Menial is a project I started late 2015 as procrastination. It's already evolved so much since I started it around October so I'll break this down into a couple of posts. This is the initial idea.

I intended for Menial to be a virtual assistant. Somewhat like Siri or Google Now but programmed by the community. Each function of Menial is written in Python by users of the website and executed server-side. Users can choose to make their 'modules' public and can activate other peoples' modules on their own account. Each module needs to have an activation phrase so for the example below the activation phrase could be 'recycle'. Any query containing "recycle" will match with and execute the module below.

I'll run through a use case.

Wellington recycling collection is glass one week, cardboard/paper/plastic the next. It was always a hassle to look up what week we were on. This sounds like a job for Menial! I wrote a quick (messy) function on Menial that was pretty much as follows.

{% highlight ruby %}
def handle(text):
    # Get the current week of the year
    week = datetime.date.today().isocalendar()[1]

    if week % 2 != 0:
        print("Cardboard, paper and plastics.")
    else:
        print("Glass crates.")
{% endhighlight %}

<img src="{{ site.baseurl }}/images/menial-pebble.png" class="image right" width="150px">Pretty straight forward but how do you actually run a 'query' against your account on the website? Well, I made an API. I also made a Pebble app that uses the Pebble microphone and voice-to-text API so I can talk to my watch like a spy. At this stage I set up the Pebble Menial app using my API key so that Menial knows which account is being queried. So the process is as follows.

1. I can ask my watch "what do I recycle".
2. The Pebble app queries Menial.
3. Menial identifies the user account from the API key used and checks if any activated modules' phrases match the query. I have the above module active on my account with the phrase "recycle" and it matches the query so the script is executed and the output sent back.
3. The response is received on the watch "Glass crates".

Pretty basic.