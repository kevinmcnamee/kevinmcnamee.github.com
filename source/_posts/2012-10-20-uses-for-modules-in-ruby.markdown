---
layout: post
title: "Usage of Modules as Mixins in Ruby"
date: 2012-10-20 08:19
comments: true
categories: 
---

Modules are similar to classes except they don't have instances and don't have subclasses. In ruby, modules can provide value in a wide range of uses. Modules collect related methods and constants in one singular location to share  behavior across classes. Mixins allow for exactly this.

Without even writing a module, you are using mixins everyday throughout your ruby programs. You are most likely utilizing enumerables everyday. Enumerables are just modules built into ruby's standard library. Enumerables are a set of methods that are accessable across all classes in ruby. To visualize this, let's take a look at what we see if we check for the ancestors of the ```Array``` class in irb:
	>> Array.ancestors
	=> [Array, Enumerable, Object, Kernal, BasicObject]

You can see that ```Enumerable``` is mixed in to the object hierarchy of the ```Array``` class. The array is not a subclass of Enumerable, but rather inherits the behaviors and full set of methods from the enumerables. 

To show an example, we want to create two classes: a ```Movie``` class and a ```Song``` class. We want each class to have similar behavior in that instances of each class can be thumbed up or thumbed down. We wouldn't want to create a superclass in order share theses methods because we don't want any shared properties other than the ability to be thumbed up or thumbed down. In this case, we will create a module called ```Rankable```.

```ruby
module Rankable
	def thumbs_up
		self.rank += 1
		puts "#{self.title} got a thumbs up and now has a rank of #{self.rank}!"
	end

	def thumbs_down
		self.rank -= 1
		puts "#{self.title} got a thumbs down and now has a rank of #{self.rank}!"
	end
end
```

Now, we can create our two classes for Movies and Songs. By including the Rankable module in both the ```Movie``` class as well as the ```Song``` class, we are able to augment the behavior to vote our movies and songs up and down.

```ruby
require 'rankable'

class Movie
	include Rankable

	attr_accessor :title, :rank

	def initialize(title, rank=5)
		@title = title
		@rank = rank
	end

class Song
	include Rankable

	attr_accessor :title, :rank

	def initialize(title, rank=5)
		@title = title
		@rank = rank
	end
end
```

Let's now create a new movie instance and pass the ```thumbs_up``` method. You can see by mixing in the ```Rankable``` module, we have access to the thumbs_up method.

```ruby
movie1 = Movie.new("Argo")
movie1.thumbs_up
puts movie1.rank #=> "Argo got a thumbs up and now has a rank of 6!"
```
A similar method is accessible when we instantiate a new instance of the ```Song``` class.

```ruby
song1 = Song.new("Gangnam Style")
song1.thumbs_down
puts movie1.rank #=> "Gangnam Style got a thumbs down and now has a rank of 4!"
```

Just as we looked at the ancestor hierarchy of the Array class earlier, when we check the ancestors of ```Movie``` or ```Song``` we will see a similar output. The difference here is, instead of ```Enumerable``` which remember is a module built into the ruby library, we will see our custom module, ```Rankable``` between the ```Movie``` class and ```Object```.
	>> Movie.ancestors
	=> [Movie, Rankable, Object, Kernal, BasicObject]

When a method is passed to an instance of the ```Movie``` class, it will first look in the ```Movie``` class for the behavior of that method. If the the instance does not find that method in it's direct class, it will start going up the chain of superclasses to find the method behavior. Before checking the next direct superclass, the instance will check for a method in the direct module. If no module exists, the class instance will only then look in direct superclass. The image visualizes this action.

{% img [class] /images/modules.jpg %}

Mixins are great for abstracting behaviors from your classes and ensuring you do are not creating duplicate code in your programs. This is a basic overview of using modules as mixins. Modules can flex the power of your ruby code in much deeper ways including a replacement of monkey patching your code as well as namespacing. Look for more in depth posts on each of these topics in the future.
