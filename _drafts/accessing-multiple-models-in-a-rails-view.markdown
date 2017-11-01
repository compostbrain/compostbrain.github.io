---
layout: "post"
title: "Accessing Multiple Models in a Rails View"
date: "2017-10-23 09:46"
categories: rails ruby
---
In my Go Tournament Manager app I need the display players for a round and games

In order to do that I am creating methods in my Round model for accessing these:

```ruby
class Round < ApplicationRecord
  belongs_to :tournament
  has_many :round_statuses
  has_many :players, through: :round_statuses
  has_many :games, dependent: :destroy
  validates :number, presence: true

  def games
    #code here...
  end

  def players
    #code here...
  end
end

```
