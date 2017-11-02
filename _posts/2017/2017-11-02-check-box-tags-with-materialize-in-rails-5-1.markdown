---
layout: post
title: Check-box tags with materialize in rails 5.1
date: '2017-11-02 10:53'
categories: rails ruby
---

Getting checkboxes set up in Rails when using [Materialize CSS][Materialize CSS] can be tricky.  You need to place the label tag after the checkbox tag and they must have the exact same name.  Here is a slim code snippet that works:

{% highlight slim linenos %}
.row.margin
  .col.s12
    h6 Active in:
    - @tournament.rounds.each do |r|
      .col.s3
        = check_box_tag "round_status[#{ r.number }]", "active", true
        = label_tag "round_status[#{ r.number }]", "Round #{ r.number }"
{% endhighlight%}

This will generate the following HTML code:
{% highlight html linenos %}
<div class="col s12">
  <h6>Active in:</h6>
  <div class="col s3">
    <input type="checkbox" name="round_status[1]" id="round_status_1" value="active" checked="checked">
    <label for="round_status_1">Round 1</label>
  </div>
  <div class="col s3">
    <input type="checkbox" name="round_status[2]" id="round_status_2" value="active" checked="checked">
    <label for="round_status_2">Round 2</label>
  </div>
  <div class="col s3">
    <input type="checkbox" name="round_status[3]" id="round_status_3" value="active" checked="checked">
    <label for="round_status_3">Round 3</label>
  </div>
  <div class="col s3">
    <input type="checkbox" name="round_status[4]" id="round_status_4" value="active" checked="checked">
    <label for="round_status_4">Round 4</label>
  </div>
</div>
{% endhighlight %}

The checkboxes are checked by default in this example due to the third argument set to true in the check_box_tag.

Notice how in each input tag ```id="round_status_*"``` matches the label tag ```for="round_status_*"```.  These must be the same in order for this to work properly. If all four checkboxes are left in the default checked state the params will include:
```
"round_status"=>{"1"=>"active", "2"=>"active", "3"=>"active", "4"=>"active"}
```

If the user un-checks the first checkbox and submits the form the params will include"
```
 "round_status"=>{"2"=>"active", "3"=>"active", "4"=>"active"}
```
Take this into account when setting up the controller action...

[Materialize CSS]: http://materializecss.com/
