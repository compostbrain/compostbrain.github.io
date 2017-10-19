---
layout: post
title:  "Has Many Through"
date:   2017-10-11 21:56:25 -0400
categories: jekyll update
---

This will document how to set up a join table using has_many through in rails.

### Step 1

- Create a model for the join table with references to the mdoels being joined

```terminal
bin/rails g model round_status player:references round:references status:integer
```
### Step 2

- Set Any Defaults

the migration file might look like this:
```ruby
class CreateRoundStatuses < ActiveRecord::Migration[5.1]
  def change
    create_table :round_statuses do |t|
      t.references :player, foreign_key: true
      t.references :round, foreign_key: true
      t.integer :status, default: 1

      t.timestamps
    end
  end
end
```

the models may look like this:
```ruby
class RoundStatus < ApplicationRecord
  belongs_to :player
  belongs_to :round
  enum status: { active: 1, bye: 2}
end

class Round < ApplicationRecord
  belongs_to :tournament
  has_many :round_statuses
  has_many :players, through: :round_statuses
  has_many :games, dependent: :destroy
  validates :number, presence: true
end

class Player < ApplicationRecord
  has_many :tournament_registrations
  has_many :tournaments, through: :tournament_registrations
  has_many :round_statuses
  has_many :rounds, through: :round_statuses
  ```



- Run  the migration
bin/rails db:migrate
