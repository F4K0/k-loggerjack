# k-loggerjack

Our goal is to save space and be more efficient than the most common logging frameworks at the same time.

## Problem overview

LoggerJack is a tool which was created to chop down logs (hence the naming :) ).

Let's have a look at an example Spring application log:
![example_spring_log](https://user-images.githubusercontent.com/720608/123813947-34d2a180-d8ed-11eb-9c17-a793d7cc57a5.png)

Do you see any issues? Well maybe not, it's quite verbose and easy to track.
However if we have a closer look we can see that it is a bit too verbose and quite redundant:

![example_spring_dupes](https://user-images.githubusercontent.com/720608/123814123-592e7e00-d8ed-11eb-8f64-9c59b1a5a3dc.png)

Everything in red is duplicated at least two times. However the log level, for example, will be duplicated in every line.
This seems inefficient and quite resourceful. We are wasting storage space and precious time logging redundant data.

Let's see how LoggerJack would solve this issue.

## How LoggerJack works

First of all we are trying to reduce the amount of characters that we are logging. 
Why would we want to log `INFO` or `DEBUG` in every line if we could just simply replace it with a marker which is one character?
This is just the beginning. We are also marking re-occurrences of the same words and replacing it with a marker.
Let's see a LoggerJack log example:
![k-binlog-example](https://user-images.githubusercontent.com/720608/123814953-01dcdd80-d8ee-11eb-862b-b3c62f5520e0.png)

You might notice the first character in every line is an `i`. This means those lines are logged on an `INFO` level. 
Why should we write 4 characters when we can write just one, right?

In the second line we define two LoggerJack variables: a process ID (`p1`) and a thread name (`t1`) so we can use these in the third line instead of headlessly logging everything.

We are basically substituting variables in each line and trying to reduce the amount of characters we are logging. That's it, easy huh?
In these 8 lines we can easily save about 350 characters. Just imagine what we can do in a 1000+ lines of logs.

## LoggerJack readability

LoggerJack log files are readable but it's quite hard to understand them. However we are working on a CLI tool and a web UI as well to translate LoggerJack files into the same format as you are used to.

## LoggerJack efficiency 

Currently our main goal is to find a way to log super-fast. We are experimenting with binary logging and this is something we would like to implement in the future.
