> * 原文作者：[@cscalfani](https://twitter.com/cscalfani)
> * 译者：[临书](https://github.com/tmpbook)
> * 校对者：

## So You Want to be a Functional Programmer (Part 1)

![01](src/assets/images/top-banner.png)

Taking that first step to understanding Functional Programming concepts is the most important and sometimes the most difficult step. But it doesn’t have to be. Not with the right perspective.

### Learning to Drive

![learn-to-drive](src/assets/images/learn-to-drive.png)

When we first learned to drive, we struggled. It sure looked easy when we saw other people doing it. But it turned out to be harder than we thought.

We practiced in our parent’s car and we really didn’t venture out on the highway until we had mastered the streets in our own neighborhood.

But through repeated practice and some panicky moments that our parents would like to forget, we learned to drive and we finally got our license.

With our license in hand, we’d take the car out any chance we could. With each trip, we got better and better and our confidence went up. Then came the day when we had to drive someone else’s car or our car finally gave up the ghost and we had to buy a new one.

What was it like that first time behind the wheel of a *different car*? Was it like the *very first time* behind the wheel? Not even close. The first time, it was all so foreign. We’ve been in a car before that, but only as a passenger. This time we were in the driver seat. The one with all the controls.

But when we drove our second car, we simply asked ourselves a few simple questions like, where does the key go, where are the lights, how do you use the turn signals and how do you adjust the side mirrors.

After that, it was pretty smooth sailing. But why was this time so easy compared to the first time?

That’s because the new car was pretty much like the old car. It had all the same basic things that a car needs and they were pretty much in the same place.

A few things were implemented differently and maybe it had a few additional features, but we didn’t use them the first time we drove or even the second. Eventually, we learned all the new features. At least the ones we cared about.

Well, learning programming languages is sort of like this. The first is the hardest. But once you have one under your belt, subsequent ones are easier.

When you first start a second language, you ask questions like, “How do I create a module? How do you search an array? What are the parameters of the substring function?”

You’re confident that you can learn to drive this new language because it reminds you of your old language with maybe a few new things to hopefully make your life easier.

### Your First Spaceship

![your-first-spaceship](src/assets/images/your-first-spaceship.png)

Whether you’ve been driving one car your whole life or dozens of cars, imagine that you’re about to get behind the wheel of a spaceship.

If you were going to fly a spaceship, you wouldn’t expect your driving ability on the road to help you much. You’d be starting over from square zero. (*We are programmers after all. We count starting at zero.*)

You would begin your training with the expectation that things are very different in space and that flying this contraption is very different than driving on the ground.

Physics hasn’t changed. Just the way you navigate within that same Universe.

And it’s the same with learning Functional Programming. You should expect that things will be very different. And that much of what you know about programming will *not* translate.

Programming is thinking and Functional Programming will teach you to think very differently. So much so, that you’ll probably never go back to the old way of thinking.

### Forget Everything You Know

![04](src/assets/images/Forget-Everything-You-Know.png)

People love saying this phrase, but it’s sort of true. *Learning functional programming is like starting from scratch*. Not completely, but effectively. There are lots of similar concepts but it’s best if you just expect that you have to *relearn everything*.

There are all kinds of things that you’re used to doing as a programmer that you cannot do any more with Functional Programming.

Just like in your car, you used to backup to get out of the driveway. But in a spaceship, there is no reverse. Now you may think, “WHAT? NO REVERSE?! HOW THE HELL AM I SUPPOSED TO DRIVE WITHOUT REVERSE?!”

Well, it turns out that you don’t need reverse in a spaceship because of its ability to maneuver in three dimensional space. Once you understand this, you’ll never miss reverse again. In fact, someday, you’ll think back at how limiting the car really was.

> Learning Functional Programming takes a while. So be patient.

So let’s exit the cold world of Imperative Programming and take a gentle dip into the hot springs of Functional Programming.

What follows in this multi-part article are Functional Programming Concepts that will help you before you dive into your first Functional Language. Or if you’ve already taken the plunge, this will help round out your understanding.

Please don’t rush. Take your time reading from this point forward and take the time to understand the coding examples. You may even want to stop reading after each section to let the ideas sink in. Then return later to finish.

The most important thing is that you *understand*.

### Purity

![05](src/assets/images/Purity.png)

When Functional Programmers talk of Purity, they are referring to Pure Functions.

Pure Functions are very simple functions. They only operate on their input parameters.

Here’s an example in Javascript of a Pure Function:

```javascript
var z = 10;
function add(x, y) {
    return x + y;
}
```

Notice that the *add* function does NOT touch the z variable. It doesn’t read from z and it doesn’t write to z. It only reads x and y, its inputs, and returns the result of adding them together.

That’s a pure function. If the *add* function did access z, it would no longer be pure.

Here’s another function to consider:

```javascript
function justTen() {
    return 10;
}
```

If the function, *justTen*, is pure, then it can only return a constant. Why?

Because we haven’t given it any inputs. And since, to be pure, it cannot access anything other than its own inputs, the only thing it can return is a constant.

Since pure functions that take no parameters do no work, they aren’t very useful. It would be better if *justTen* was defined as a constant.

> Most *useful* Pure Functions must take at least one parameter.

Consider this function:

```javascript
function addNoReturn(x, y) {
    var z = x + y
}
```

Notice how this function doesn’t return anything. It adds x and y and puts it into a variable z but doesn’t return it.

It’s a pure function since it only deals with its inputs. It does add, but since it doesn’t return the results, it’s useless.

> All *useful* Pure Functions must return something.

Let’s consider the first *add* function again:

```javascript
function add(x, y) {
    return x + y;
}
console.log(add(1, 2)); // prints 3
console.log(add(1, 2)); // still prints 3
console.log(add(1, 2)); // WILL ALWAYS print 3
```

Notice that *add(1, 2)* is always 3. Not a huge surprise but only because the function is pure. If the add function used some outside value, then you could never predict its behavior.

> Pure Functions will *always* produce the same output given the same inputs.

Since Pure Functions cannot change any external variables, all of the following functions are *impure*:

```javascript
writeFile(fileName);
updateDatabaseTable(sqlCmd);
sendAjaxRequest(ajaxRequest);
openSocket(ipAddress);
```

All of these function have what are called *Side Effects*. When you call them, they change files and database tables, send data to a server or call the OS to get a socket. They do more than just operate on their inputs and return outputs. Therefore, you can never predict what these functions will return.

> Pure functions have *no* side effects.

In Imperative Programming Languages such as Javascript, Java, and C#, Side Effects are *everywhere*. This makes debugging very difficult because a variable can be changed *anywhere* in your program. So when you have a bug because a variable is changed to the wrong value at the wrong time, where do you look? Everywhere? That’s not good.

At this point, you’re probably thinking, “HOW THE HELL DO I DO ANYTHING WITH *ONLY* PURE FUNCTIONS?!”

In Functional Programming, you don’t just write Pure Functions.

Functional Languages cannot eliminate Side Effects, they can only confine them. Since programs have to interface to the real world, some parts of every program must be impure. The goal is to minimize the amount of impure code and segregate it from the rest of our program.

### Immutability

![06](src/assets/images/Immutability.jpeg)

Do you remember when you first saw the following bit of code:

```javascript
var x = 1;
x = x + 1;
```

And whoever was teaching you told you to forget what you learned in math class? In math, x can never be equal to x + 1.

But in Imperative Programming, it means, take the current value of x add 1 to it and put that result back into x.

Well, in functional programming, x = x + 1 is illegal. So you have to *remember* what you *forgot* in math… Sort of.

> There are *no* variables in Functional Programming.

Stored values are still called variables because of history but they are constants, i.e. once x takes on a value, it’s that value for life.

Don’t worry, x is usually a local variable so its life is usually short. But while it’s alive, it can never change.

Here’s an example of constant variables in Elm, a Pure Functional Programming Language for Web Development:

```elm
addOneToSum y z =
    let
        x = 1
    in
        x + y + z
```

If you’re not familiar with ML-Style syntax, let me explain. addOneToSum is a function that takes 2 parameters, y and z.

Inside the let block, x is bound to the value of 1, i.e. it’s equal to 1 for the rest of its life. Its life is over when the function exits or more accurately when the let block is evaluated.

Inside the in block, the calculation can include values defined in the let block, viz. x. The result of the calculation x + y + z is returned or more accurately, 1 + y + z is returned since x = 1.

Once again, I can hear you ask “HOW THE HELL AM I SUPPOSED TO DO ANYTHING WITHOUT VARIABLES?!”

Let’s think about when we want to modify variables. There are 2 general cases that come to mind: multi-valued changes (e.g. changing a single value of an object or record) and single-valued changes (e.g. loop counters).

Functional Programming deals with changes to values in a record by making a copy of the record with the values changed. It does this efficiently without having to copy all parts of the record by using data structures that makes this possible.

Functional programming solves the single-valued change in exactly the same way, by making a copy of it.

Oh, yes and by not having loops.

“WHAT NO VARIABLES AND NOW NO LOOPS?! I HATE YOU!!!”

Hold on. It’s not like we can’t do loops (no pun intended), it’s just that there are no specific loop constructs like *for*, *while*, *do*, *repeat*, etc.

> Functional Programming uses recursion to do looping.

Here are two ways you can do loops in Javascript:

```javascript
// simple loop construct
var acc = 0;
for (var i = 1; i <= 10; ++i)
    acc += i;
console.log(acc); // prints 55
// without loop construct or variables (recursion)
function sumRange(start, end, acc) {
    if (start > end)
        return acc;
    return sumRange(start + 1, end, acc + start)
}
console.log(sumRange(1, 10, 0)); // prints 55
```

Notice how recursion, the functional approach, accomplishes the same as the for loop by calling itself with a new start (start + 1) and a new accumulator (acc + start). It doesn’t modify the old values. Instead it uses new values calculated from the old.

Unfortunately, this is hard to see in Javascript even if you spend a little time studying it, for two reasons. One, the syntax of Javascript is noisy and two, you’re probably not used to thinking recursively.

In Elm, it’s easier to read and, therefore, understand:

```elm
sumRange start end acc =
    if start > end then
        acc
    else
        sumRange (start + 1) end (acc + start) 
```

Here’s how it runs:

```
sumRange 1 10 0 =      -- sumRange (1 + 1)  10 (0 + 1)
sumRange 2 10 1 =      -- sumRange (2 + 1)  10 (1 + 2)
sumRange 3 10 3 =      -- sumRange (3 + 1)  10 (3 + 3)
sumRange 4 10 6 =      -- sumRange (4 + 1)  10 (6 + 4)
sumRange 5 10 10 =     -- sumRange (5 + 1)  10 (10 + 5)
sumRange 6 10 15 =     -- sumRange (6 + 1)  10 (15 + 6)
sumRange 7 10 21 =     -- sumRange (7 + 1)  10 (21 + 7)
sumRange 8 10 28 =     -- sumRange (8 + 1)  10 (28 + 8)
sumRange 9 10 36 =     -- sumRange (9 + 1)  10 (36 + 9)
sumRange 10 10 45 =    -- sumRange (10 + 1) 10 (45 + 10)
sumRange 11 10 55 =    -- 11 > 10 => 55
55
```

You’re probably thinking that *for* loops are easier to understand. While that’s debatable and more likely an issue of familiarity, non-recursive loops require Mutability, which is bad.

I haven’t entirely explained the benefits of Immutability here but check out the *Global Mutable State* section in [Why Programmers Need Limits](https://medium.com/@cscalfani/why-programmers-need-limits-3d96e1a0a6db) to learn more.

One obvious benefit is that if you have access to a value in your program, you only have read access, which means that no one else can change that value. Even you. So no accidental mutations.

Also, if your program is multi-threaded, then no other thread can pull the rug out from under you. That value is constant and if another thread wants to change it, it’ll have create a new value from the old one.

Back in the mid 90s, I wrote a Game Engine for Creature Crunch and the biggest source of bugs was multithreading issues. I wish I knew about immutability back then. But back then I was more worried about the difference between a 2x or 4x speed CD-ROM drives on game performance.

> Immutability creates simpler and safer code.

### My Brain!!!!

![07](src/assets/images/My-Brain!!!!.png)

Enough for now.

In subsequent parts of this article, I’ll talk about Higher-order Functions, Functional Composition, Currying and more.

Up Next: [Part 2](https://github.com/tmpbook)
