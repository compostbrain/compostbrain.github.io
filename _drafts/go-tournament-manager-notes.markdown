---
layout: "post"
title: "Go Tournament Manager notes"
date: "2017-10-19 13:57"
categories: rails ruby
---

Seems like I need a method for determining the current round?

{% highlight ruby %}
Player.joins(
    :round_statuses,
  ).where(
    round_statuses: { status: 1 },
  ).where(id: players.map(&:id))
{% endhighlight %}


build vs create
