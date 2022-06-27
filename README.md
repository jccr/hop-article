# MPG: Multiplayer Party Game

Like most that join Commit, I came with the goal of learning something new. The [Hackathon Onboarding Project](https://docs.commit.dev/eps/ep-hop) is the perfect sandbox for accommodating this by building a software project from your own ideas.  

For a while now I've held on to the idea of building a certain kind of game, a multiplayer party game. 

There’s outrageous fun playing social party games with friends and colleagues. You break the ice and form closer bonds through silly (or not), entertaining games that let you be yourself (or something else).  

Here are my favorites: Table-top ones like Exploding Kittens, Codenames, and video game ones like Among Us, Ultimate Chicken Horse, or those in the Jackbox Party Packs.  

Most of these have something in common, there’s prerequisites like having a copy of the game, using something to play, hosting and teaching others the game. 

I am particularly fond of ones that let you onboard anyone, easily, without too many requirements or preparation. Where you can gather a group, pick up a game and have anyone learn while they play. 

Let's tackle the design and infrastructure for the version of my game by breaking down these prerequisites.

### Using something to play 

What is something that everyone always carries that could play a game, connected with others? The answer to this is of course a smartphone.

Going deeper and thinking of the details... Will these devices require an internet connection? Ad-hoc network (same WiFi) where internet doesn't matter? Maybe using Bluetooth instead?

For all the above, I know of a game called [Spaceteam](https://spaceteam.ca/) that works out these concerns as different modes, it works through the internet, Wi-Fi, or Bluetooth as explained in this great [networking blog post](http://spaceteamadmirals.club/blog/the-spaceteam-networking-post/) from the creator of the game.

Popping back up a level, all of this adds complexity to my project.
I'll simplify this to just using an internet connection, which will work well for the purposes of demonstrating my game remotely.

### Having a copy of the game 

How's the game software distributed to all the player's devices? 

My last example was an app distributed on the app stores. If I'm looking for something with less friction, without a download and installation step, I'd go for a website hosting the game allowing players to start after loading the URL. As a web developer and advocate for web technologies, I like this approach the best. Even better, as a [Progressive Web App](https://web.dev/learn/pwa/progressive-web-apps/), it could begin as an on-demand site and later be installed like an app. 

I can't help but think of some real world situations I have faced as a social gamer living in Vancouver:
What if my group is camping out in the woods or travelling in a ferry? With no internet and no Wi-Fi access points? Also, everyone would need to have the game on their phone! What if the idea to play happened spontaneously or a new party member wishes to join on the spot?

The ad-hoc network solves the first part, yet distributing the game in the same matter is problematic. It could be that a website for the game is served locally from a device, or an app-store application package is shared and sideloaded offline somehow. The former is doable and a potential idea for the future, but the latter less so given the closed nature of mobile phone platforms. (Though, I recently learned that [Android's Nearby Share works with apps](https://www.techrepublic.com/article/how-to-share-apps-with-androids-new-nearby-share/).)

There is also the popular [set-up of Jackbox Games](https://www.jackboxgames.com/how-to-play/) to consider: The host starts the game as an app on an internet connected console, casting to a screen for all to see. Each player connects and joins that game using a website on their phones, acting as personal input and output controllers. 

For the sake of simplicity the setup for my game should be similar but without a central console or shared view. Instead each player visits a website and creates a game for others to join, and without a shared view the action appears exclusively on each participant's screen.

### Learning how to play 

This one is up to the design of the game and could be solved by having someone experienced teach the game. 

Ideally though the game is simple and ends quickly enough to be understood by anyone new without much effort. Spaceteam does this effectively through trial by ~~error~~ fire, and Jackbox games usually have a quick and engaging tutorial video before the start of a game. 

I also think incorporating hints or subtle explanations into the regular flow of the game would work too. 

I'll try to use a mix of these ideas for my game (maybe not the video production, but I wish).

## The goals for my project

Now that I have the initial design let's establish some goals:

1. Learn a functional programming language.
2. Use a full-stack web application framework.
3. Reduce my dependence on JavaScript for app development.
4. Play with distributed computing as building blocks.

As a JavaScript developer I use lambdas and higher-order functions like bread and butter. I also apply the concept of immutability to prevent unexpected side effects when possible. 

Yet since it’s multi-paradigm there are no guarantees in upholding functional programming. I just cannot seem to let go of [`Array.prototype.push()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)! Which is why I'm interested in learning a language specifically designed for this. 

In the past, like I suspect others do, I started with Haskell. Unfortunately, I found it hard to grasp given the unfamiliar syntax, and the extra burden of using its static and strong [type system for lambda calculus](https://en.wikipedia.org/wiki/Hindley%E2%80%93Milner_type_system). While it got me to appreciate the purely functional and mathematical nature of it, I felt like it could be more approachable. 

I also know I’m best motivated in learning something if I get the satisfaction of creating something visual and interactive in the end. Sorry Haskell, you might be too general purpose and academic for me and my prpject right now. 

I looked towards other candidates, and I looked towards Elm. Great! It’s designed for functional programming and specific to the domain of front-end web development which works for building something visual and interactive. 

Yet I had another goal in mind for my project, which disqualified Elm. I wanted something not general purpose, but also not domain specific, instead something that I could use across the stack. This led me towards Elixir and the Phoenix framework. 

### Enter Elixir

With Elixir I can learn a functional programming language that’s approachable like Ruby. It’s dynamic and functional, and not statically typed nor purely functional like Haskell. You'd still need to manage side effects, but that's eased by promoting higher-order functions and with data structures adhering to immutability. Plus, you get new ways of doing pattern matching that I haven’t experienced before, such as the [`=` operator](https://elixir-lang.org/getting-started/pattern-matching.html#the-match-operator) not assigning values, but instead matching on them. And as a huge plus, you inherit the concurrent and distributed powers of Erlang allowing you to use the concepts of distributed computing as basic building blocks and allowing you to scale by taking advantage of multi-core systems. 

They say in JavaScript [everything is an object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#objects:~:text=everything%20(bar%20core%20types)%20in%20JavaScript%20is%20an%20object), well in Elixir there’s similar sayings that generalize some features, such as: [everything runs inside a process](https://elixir-lang.org/getting-started/processes.html#:~:text=all%20code%20runs%20inside%20processes), [everything is an expression](https://elixirforum.com/t/how-does-implict-return-work-in-functions/32417/3), and [everything is immutable](https://elixir.bagwanpankaj.com/2014/02/25/introduction-to-elixir/#:~:text=Everything%20is%20immutable). I found that the concept of a Process is key in organizing components out of functions that hold state. 

Everything is an expression speaks to Elixir being expression-oriented which means most expressions evaluate down to a value. In statement-oriented C derived languages (JavaScript included) `if` is a statement that does not return a value, whereas in Elixir `if` is an expression (like a function) that returns a value. 

```elixir
y = if is_number(1) do 
      "yes"
    else
      "no"
    end
```

