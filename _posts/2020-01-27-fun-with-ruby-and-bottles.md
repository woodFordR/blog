---
layout: post
title: Fun with ruby & bottles
date: 2020-01-27
month: January
day: 27
year: 2020
categories: [ruby, OOP, polymorphism]
permalink: /:year/:month/:day/:title.html
---

I started my career in software development learning [ruby](https://www.ruby-lang.org/en/).  The language has a unique style & beauty for writing complex web applications or simple scripts.  During the last few weeks of 2019, I enjoyed reading [99 Bottles of OOP](https://www.sandimetz.com/99bottles).  Sandi Metz describes recipes for object oriented programming in great detail to make your code efficient and easy to change.  She discussed the _Liskov Substitution Principle_ and how we can use it to create the strategy _replace the conditional with polymorphism_. 
<br /><br />

### **Liskov Substitution Principle & Polymorphism**
Barbara Liskov was one of the first women to earn a computer science doctorate in 1968 at Stanford.  She gave the keynote presentation _Data Abstraction & Hierarchy_ at a conference in 1987, which first introduced behavioral subtyping.  It was later renamed as the _Liskov Substitution Principle_.  The _LSP_ states: if for each object of type **A** there is an object of type **B** such that when object of type **B** is substituted and replaced by object of type **A**, and the program's behavior remains unchanged, we can say **A** is a subtype of **B**.  Barbara Liskov would receive the Turing Award in 2008 for her contributions related to data abstraction.  
_Polymorphism_ is defined as the concept of 2 or more classes having the ability to respond to the same directive.  In _99 Bottles of OOP_, the strategy _replace the conditional with polymorphism_ demonstrates polymorphism while adhering to the LSP.  
<br /><br />

### **Replace the conditional with polymorphism**
  Dynamically typed languages like ruby rely on trust.  There are expectations for objects to respond appropriately to messages and presumptions about the message results.  In this example, I will create a simple program which lists the 9 main robots of *Mega Man 2*  which is an old video game for Nintendo 8-bit.  Maintaining the integrity of the program while providing a better experience for the developer are the goals as we change the code.

|MegaMan|BubbleMan|AirMan|QuickMan|HeatMan|WoodMan|MetalMan|FlashMan|CrashMan|
|----------|-------|---------|--------|--------|---------|---------|---------|
|![MegaMan](/assets/megaman2/megaman.png)|![BubbleMan](/assets/megaman2/bubbleman.gif)|![AirMan](/assets/megaman2/airman.jpg)|![QuickMan](/assets/megaman2/quickman.png)|![HeatMan](/assets/megaman2/heatman.png)|![WoodMan](/assets/megaman2/woodman.png)|![MetalMan](/assets/megaman2/metalman.jpg)|![FlashMan](/assets/megaman2/flashman.png)|![CrashMan](/assets/megaman2/crashman.png)|

<br />
{% highlight ruby %}
class MegaMan2GameTest < Minitest::Test
  def test_the_chracter_list
    expected = <<-GAME
The good Mega Man was created by Dr. Light.
The evil Metal Man was created by Dr. Wily.
The evil Flash Man was created by Dr. Wily.
The evil Crash Man was created by Dr. Wily.
The evil Heat Man was created by Dr. Wily.
The evil Wood Man was created by Dr. Wily.
The evil Bubble Man was created by Dr. Wily.
The evil Air Man was created by Dr. Wily.
The evil Quick Man was created by Dr. Wily.
      GAME
    assert_equal expected, MegaMan2Game.new.character_list
  end
end
{% endhighlight %}
<br />

{% highlight ruby %}
class MegaMan2Game
  def robot(name)
    robot = Robot.new(name)

    "The #{robot.morality} #{robot} was " \
      "created by #{robot.creator}.\n"
  end

  def character_list
    characters = ["Mega Man", "Metal Man", "Flash Man", "Crash Man", "Heat Man",
      "Wood Man", "Bubble Man", "Air Man", "Quick Man"]
    
    characters.collect {|x| robot(x)}.join("")
  end
end

class Robot
  attr_reader :name
  def initialize(name)
    @name = name
  end

  def creator
    if name == "Mega Man"
      "Dr. Light"
    else
      "Dr. Wily"
    end
  end

  def morality
    if name == "Mega Man"
      "good"
    else
      "evil"
    end
  end

  def health
    "20 HP"
  end

  def to_s
    "#{name}"
  end
end
{% endhighlight %}

<br/>
The test written first is our source of truth.  In _class Robot_ the name _Mega Man_ has a special meaning and is used a few times.  Let's create a subclass to stand in for this value and copy one of the methods which switch on it.  Then let's proceed to delete everything but the true branch of the conditional.
<br/><br/>

{% highlight ruby %}
class MegaManRobot < Robot
  def creator
    "Dr. Light"
  end
end
{% endhighlight %}

<br/>
Since we don't have a factory to create _MegaManRobot_ objects, we need to add one to the beginning of the _MegaMan2Game_ class.  Then we can use our new subclass in the factory.
<br/>

{% highlight ruby %}
class MegaMan2Game
  def robot(name)
    robot = robot_for(name)

    "The #{robot.morality} #{robot} was " \
      "created by #{robot.creator}.\n"
  end  
  
  def robot_for(name)
    if name == "Mega Man"
      MegaManRobot
    else
      Robot
    end.new(name)
  end

  # ...
end
{% endhighlight %}

<br/>
Now we can reduce the superclass' conditional branch to the false path.  
<br/>

{% highlight ruby %}
class Robot
  # ...

  def creator
    "Dr. Wily"
  end

  # ...
end
{% endhighlight %}

<br/>
We can repeat until all the methods that switch on this value are dispersed.  The goal is to iterate until there is a subclass for every different value upon which there is a switch.  The method _robot_for_ can be written into a case statement when we start creating more subclasses.  This starts becoming a pattern of the strategy _replace the conditional with polymorphism_.  It helps developers have a better time understanding and changing the code.
<br>

{% highlight ruby %}
class MegaMan2Game
  # ...
  
  def robot_for(name)
    case name
    when "Mega Man"
      MegaManRobot
    when "Metal Man"
      MetalManRobot
    when "Flash Man"
      FlashManRobot
    # ...
    else
      Robot
    end.new(name)
  end

  # ...
end
{% endhighlight %}

<br />
Finally, we can pull our factory method out and place a more appropriate _for_ class method in _Robot_.  The end result is to be more organized, especially when we start adding more attributes and features to our characters.  After we create our class method, we can alter the _robot_ method in our _MegaMan2Game_ class.  Polymorphism maintains the option of creating apps where the factories are substitutable.
<br />

{% highlight ruby %}
class MegaMan2Game
  def robot(name)
    robot = Robot.for(name)
    # ...
  end
  # ...
end

class Robot
  def self.for(name)
    case name
    when "Mega Man"
      MegaManRobot
    when "Metal Man"
      MetalManRobot
    when "Flash Man"
      FlashManRobot
    # ...
    else
      Robot
    end.new(name)
  end
  # ...
end
{% endhighlight %}
