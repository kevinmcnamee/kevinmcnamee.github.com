---
layout: post
title: "Why You Don't Need has\_and\_belongs\_to\_many Relationships"
date: 2012-11-07 09:02
comments: true
categories: 
published: false
---


When mapping associations between models in your Rails application, you will inevitably come to a point when two models both 'has' and 'belongs\_to' each other. In this situation, you need to choose between a has\_many :through relationship and a has\_and\_belongs\_to\_many relationship.

Given the ease and minimal keystrokes needed, you might think a has\_and\_belongs\_to\_many relationship is the way to go. I mean, it is an association built into the ethers of Active Record, so it must be the path to choose right? Wrong. When creating associations between models, you almost never know how this relationship will blossom as your application grows. I want to show you how potentially dangerous a has\_and\_belongs\_to\_many relationship can turn out. By taking a few steps upfront to setup a solid has\_many :through relationship with an associated join table, you provide yourself with a huge amount of flexibility down the road.

Let's start by explaining the usage of these similar but distinctly exclusive association types. We will use the all too familiar association between cops and perpetrators:

### has\_and\_belongs\_to\_many

This script to setup this association is dangerously simple. I'll show a little later in this post how this can blow up in your face.

```ruby
class Cop < ActiveRecord::Base
  has_and_belongs_to_many :perps
end

class Perp < ActiveRecord::Base
  has_and_belongs_to_many :cops
end
```

### has\_many :through

A has\_many :through association is used to setup a many to many relationship with another model in your application. This assocation uses a join table to connect the models allowing each to both 'has' and 'belong\_to' each model. In this case, our cop can have many perps to bust and our perps can belong to the many cops who will inevitably violate them.

```ruby
class Cop < ActiveRecord::Base
  has_many :cop_perps
  has_many :perps, :through => :cop_perps
end

class Perp < ActiveRecord::Base
  has_many :cop_perps
  has_many :cops, :through => :cop_perps
end

class CopPerp < ActiveRecord::Base
  belongs_to :cop
  belongs_to :perps
end
```

This relationship now allows for extending the association within the join table. There are a few additional steps you need to take to setup this association that are not necessary for the previous example. First, you must create a migration for the perps table and insert belongs\_to associations for the other models. You also need to create an additional line of code on each ```Cop``` and ```Perp``` tables.

The extra 10 minutes you take to setup this association will potentially save you hours of work and headache if you decide you now need to extend the cop_perps table in the future.

### When to use has\_and\_belongs\_to\_many (hint: never)

[Rails Guides](http://guides.rubyonrails.org/association_basics.html#choosing-between-has_many-through-and-has_and_belongs_to_many) says that "You should use has_many :through if you need validations, callbacks, or extra attributes on the join model". As the great coding philosopher [Avi Flombaum](http://shitavisays.tumblr.com/) once eluded, how can you possibly know that your join model will not serve an additional purpose this early in the application process. No matter where you are in the development stage, you can never see so far in the future to know you will not need to extend the join table.

For instance, what if we want to add some more information to how a cop and his perp are associated? In the case of the has\_many :through association, we can change the name of CopPerp model to Tickets, add a migration to change the table name from cops_perps to tickets, and update the associations in the models. Now we can add information to the Tickets model such as time of arrest, court date, status, etc.

```ruby
class Cop < ActiveRecord::Base
  has_many :tickets
  has_many :perps, :through => :tickets
end

class Perp < ActiveRecord::Base
  has_many :tickets
  has_many :cops, :through => :tickets
end

class Ticket < ActiveRecord::Base
  belongs_to :cop
  belongs_to :perps
end
```

This task is much more difficult had we used the has\_and\_belongs\_to\_many association. We would have to go back and manually create the join table and has\_many :through associations. Otherwise, the only information we could ever access is that a cop belongs to a perp and a perp belongs to a cop.

What do you think of this theory? Can you offer a reason where you absolutely think using a has\_and\_belongs\_to\_many association is superior to has\_many :through?

And now I leave you with those immortal words from Eazy-E and the gang:

<iframe width="480" height="360" src="http://www.youtube.com/embed/WiX7GTelTPM" frameborder="0" allowfullscreen></iframe>