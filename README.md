# What is "Surviving C++"?
"Surviving C++" is my attempt to explain things I've learned about C++ that aren't taught in a class. This is meant to be the missing manual, a condensed can of "on the job training", and maybe some statements that are useful, even if they're not 100% true.

Consider this a survival guide: how to do things practically in C++ and actually get work done, so that readers can continue the learning process on their own.

## Who is this tutorial for?
This tutorial is primarily written for new or introductory software engineers. People who may have had some amount of instruction in software engineering concepts but have never done C++. I find many devs of this kind who have, for example, finished a computer science degree and have written production code in Java, but are unable or unwilling to take on any C++ work due to having no experience with the language. I am writing this guide specifically for those kinds of people.

I will be assuming that people reading this have some experience with software development and have preferably learned at least one other high-level programming language. Due to its popularity in schools, I'm going to assume many readers know Java, and may make occasional reference to how things work in Java. However, Java knowledge is not required. This guide is not "C++ for Java programmers," it's about helping everyone survive C++

### A note for experienced C/C++ programmers
Hello, experienced C/C++ programmers. You may have been linked to this guide by the author (me) or in the context of collecting materials to send to new devs. I want to be clear: this is not meant to be a reference manual or an explanation of every nuance of every decision. This is just meant to be a set of guidelines to get new devs up and writing code quickly so that they can start contributing to your projects. I've found that many developers learn best by doing, but that people are afraid to start "doing" with C++ because of all these complexities. 

Your domain is likely to have extra requirements that are beyond the scope of this guide. That information is up to you to communicate as an experienced engineer or mentor. I am here only to provide an introduction set of guidelines that should work for most cases, as well as to expose new devs to what C++ is capable of. Statements I make on what someone "should" do in a particular circumstance is meant to be a general guideline that can and should be broken when there is extra information. But new devs need to know the "rules" to know when to break them.

Also, some amount my suggestions will, by definition, be opinions. I will try and be fairly general, or at least explain why I think certain patterns are good.

## Assorted notes on this guide
- I will assume that we are compiling with at least C++11, sometimes C++17. I find that most projects with modern compilers will support C++11 at a minimum, and usually will support C++17 as well. C++20 at time of writing is a bit too new to assume it has widespread adoption. When relevant, I will call out if a specific code section requires a certain C++ revision. However, many of these concepts are applicable even to C++98 or even older C code.
- I am writing primiarly with the idea that the reader will be creating new C++ code. Not necessarily an entirely new project, but often to implement a task or code story, one will need to write some amount of new code. This will also help when refactoring existing leagcy code, as that is effectively transforming old code into a new, more readable and maintainble style. Programming in a legacy system has many caveats attached to it, and users may be required to make suboptimal implementation choices in the interest of matching the style. This is usually a good idea, but I unfortunately won't have context for every legacy system, so am unable to offer specific advice for that

# Surviving C++, Lesson 1: Guidelines for Writing Good Classes
One of the primary mistakes I see from people who are new to C++ is writing bad classes and types. C++ has much more flexibility in its design that allows you to be more expressive using the type system compared with, for example, Java. In Java, everything must be a capital-O Object, even if it doesn't make logical sense for it to be one. This lesson is primarily about unlearning that bad habit and putting good habits for writing classes in its place.

## Not everything must be a Class
As stated, the #1 thing I see developers mistakenly do in C++ is make everything into a class. I want to emphasize how C++ doesn't require this

## Struct vs Class
In C, there only existed `struct`: a struct was a useful bundle of fields with a name, where each field also has a name and a type. This meant that users could logically wrap pieces of data together if it was useful.

In C++, we now have the `class` keyword. Classes in C++ have many of the same benefits of any high-level programming language with classes and object orientation. However, the `struct` keyword still remains. Semantically, the only difference between a struct and a class is that data members in a struct are default public (to preserve behavior from C), and data members are default private.

However, it is useful to restrict ourselves to picking struct vs. class based on this assertion:

### Use a class if you have a Class Invariant
A "class invariant" is a statement of fact about a class that must always be true, and that the class will maintain by restricting access to its private members
