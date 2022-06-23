# MPG: Multiplayer Party Game

## Preamble

Like most that join Commit, I came with the goal of learning something new. The hackathon onboarding project is the perfect sandbox for accommodating this goal with the practice and experience in building a software project from your own ideas.  

I’ve had an idea for a while now to build a certain kind of game, a multiplayer party game. 

There’s outrageous fun to be had playing social party games with friends, family, and colleagues. It’s awesome breaking the ice and forming closer bonds through silly (or not), entertaining games that let you be yourself (or something else).  

Some of my favorites, as examples: Table-top ones like Exploding Kittens, Codenames, and video game ones like Among Us, Ultimate Chicken Horse, or those in the Jackbox Party Packs.  

Most of these have something in common, there’s prerequisites like having a copy of the game, using something to play, hosting and teaching others the game.  

I am particularly fond of ones that let you onboard anyone, easily, without too many requirements or preparation. Where you can gather a group, pick up a game and have anyone learn while they play. 

Let us think about this and break things down before I get into my version of a game.  

[> TLDR: You may skip this preamble and jump to the … 

TLDR: Skip to my project, Greater Scope of the problem we are trying to solve.  

Skip the context, here’s the meat of the domain. The crux of my implementation] 

### Prerequisite #1: Using something to play 

What is something that everyone always carries that could play a game, connected with others? The answer to this is of course smartphones, or more formally, mobile computing with wireless networking.  

Going deeper and thinking of the details... Do these devices need an internet connection to network together? On cellular data or Wi-Fi? Same Wi-Fi network? Maybe forming an ad-hoc network or using Bluetooth?  

For all the above, I know of a game called [Spaceteam](https://spaceteam.ca/) that works out these concerns as different modes, it works through the internet, Wi-Fi, and Bluetooth. The creator of the game has a great [blog post](http://spaceteamadmirals.club/blog/the-spaceteam-networking-post/) explaining the networking and more behind-the-scenes technical details. 

### Prerequisite #2: Having a copy of the game 

How is the game software distributed to all the devices? 

My last example achieved success as an app distributed on the app stores, but that’s not the only approach. What’s something with less friction, doesn’t need an account, a download or installation? It could be a website hosting the game, where you at once start playing after entering a URL. As a web developer and advocate for web technologies, I like this approach the best.  

Both approaches at some point require an internet connection, where the latter could require more of an online connection, unless made available offline. Even better, as a [Progressive Web App](https://web.dev/learn/pwa/progressive-web-apps/), it could start as an on-demand site and later be installed like an app. 

Here's some scenarios to consider that relate to these two prerequisites so far:  

What if my group is camping out in the woods or travelling in a ferry? With no internet and no Wi-Fi access point? Also, everyone would need to have the game on their phone! What if that hasn’t happened in time, when the idea to play is spontaneous or a new party member wishes to join on the spot? (These are real situations I have faced as a social gamer living in Vancouver.) 

The ad-hoc network solution solves the first problem but distributing the game in an ad-hoc matter is problematic. It could be that a local website for the game is served, or an app-store application package could be shared and sideloaded somehow. 

There is also the [set-up of Jackbox Games](https://www.jackboxgames.com/how-to-play/) to consider: The host starts the game as an app on an internet connected console, casting to a screen for all to see. Each player connects and joins that game using a website on their phones, acting as personal input and output controllers. 

### Prerequisite #3: Learning how to play 

This one is up to the design of the game itself and can be made easier by having someone experienced teach the game. Ideally the game is simple and ends quickly enough to be understood without much effort. Spaceteam does this effectively through trial by fire, and Jackbox games usually have a quick tutorial video segment before the start of a game. I also think incorporating hints or subtle explanations on how to play into the regular flow of the game would work too. 

## Hackathon Onboarding Project (HOP)

### My setup of a multiplayer party game 

I decided to make my game in the style of Jackbox, but without the need for a central console and shared view. Instead, each player connects directly to a website, creates their own game sessions from there for others to join. Without a shared view, the action and gameplay would be happening exclusively on each participant's screen. This model simplifies the setup and makes the game accessible without prior download or installation of an application. All you need is a phone and an internet connection. 

### My goals for this project 

1. Learn a functional programming language 
2. Use a full-stack web application framework 
3. Reduce my dependence on JavaScript 
4. Play with distributed computing as building blocks 

As a JavaScript developer I use lambdas and higher-order functions like bread and butter. I also apply the concept of immutability to prevent unexpected side effects when possible. 

Yet since it’s multi-paradigm there are no guarantees in upholding functional programming. I just cannot seem to let go of [`Array.prototype.push()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push), so it’s fair to say I’m not a very disciplined functional programmer with JavaScript. 

Which is why to me, it has become interesting to learn and use a language specifically designed for this. 

In the past, like I suspect most others do, I started learning Haskell. Unfortunately, I found it hard to grasp from the very beginning. While it got me to appreciate the purely functional and mathematical nature of it, I felt like something else could be more approachable for me given the unfamiliar syntax, and the extra burden of using its static and strong [type system for lambda calculus](https://en.wikipedia.org/wiki/Hindley%E2%80%93Milner_type_system). 

I also know I’m best motivated to learn something if I get the satisfaction of creating something visual, interactive, and compelling in the end. Sorry Haskell, you might be too general purpose and academic for me right now and for my project. 

I looked towards other candidate languages, and I looked towards Elm. Great! It’s designed for functional programming and specific to the domain of front-end web development which works for me in learning by building something visual and interactive. 

Yet I had another goal in mind for my project, which disqualified Elm. I wanted something not general purpose, but also not domain specific, instead something that I could use across the stack. This led me towards Elixir and the Phoenix framework. 

With Elixir I can learn a functional programming language that’s approachable like Ruby. It’s dynamic and functional, and not statically typed nor purely functional like Haskell. There is still the issue of side effects, but the language is idiomatic in preventing that by promoting higher-order functions, and with data structures and values adhering to immutability. Plus, you get new ways of doing pattern matching that I haven’t experienced before, such as the [`=` operator](https://elixir-lang.org/getting-started/pattern-matching.html#the-match-operator) not assigning values, but instead matching on them. And as a huge plus, you inherit the concurrent and distributed powers of Erlang allowing you to use the concepts of distributed computing as basic building blocks allowing you to scale by taking advantage of multi-core systems. 

They say in JavaScript [everything is an object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#objects:~:text=everything%20(bar%20core%20types)%20in%20JavaScript%20is%20an%20object), well in Elixir there’s similar sayings that generalize some of its features such as: [everything runs inside a process](https://elixir-lang.org/getting-started/processes.html#:~:text=all%20code%20runs%20inside%20processes), [everything is an expression](https://elixirforum.com/t/how-does-implict-return-work-in-functions/32417/3), and [everything is immutable](https://elixir.bagwanpankaj.com/2014/02/25/introduction-to-elixir/#:~:text=8.)%20Immutability%3A-,Everything%20is%20immutable,-%2D%20more%20or%20less). The concept of a Process is key in organizing components out of functions that hold state. 

Everything is an expression speaks to Elixir being expression-oriented which means most expressions evaluate down to a value. In statement-oriented C derived languages (JavaScript included) if is a statement that does not return a value, whereas in Elixir if is an expression (like a function) that could return a value. 

```elixir
y = if is_number(1) do 
      "yes"
    else
      "no"
    end
```