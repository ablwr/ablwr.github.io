---
layout: post
title: "Regular Expression Options"
date: 2014-06-16 18:26:07 -0400
tags: [programming]
---


When working with Regular Expressions, I mostly ignored these optional suffixes because I didn't want to further complicate an already complicated aspect of programming. But since there are only four options, I decided to take a break from other complications and break down what each regex suffix can do.

* **i**

  i stands for **INSENSITIVE**! But not like that jerk that cut in front of you when changing trains at Union Square this morning. It means that it is case insensitive! You can save some keystrokes and be more precise by using i to eliminate or swap a word for a paragraph.

* **m**

  The next option is the letter m. M stands for **MULTILINE MODE**! Mmmm! What does that mean? Rubular sums it up succinctly as "make dot match newlines." Still lost? The m option helps the dot (also known as a period or a full stop) character, which represents any character in a regex, match everything INCLUDING the invisible new line character. The new line character is represented in a regex or in programming as \n. If you are worried that your new line might mess up your regex, the m option can help mesh all lines together.

* **o**

  Next up is the letter o. O stands for **ONCE**! ONE TIME, ONE CHANCE, ONE SHOT! To substitute once. Substitute once means that any #{...} substitutions that occur in a regex can only occur one time and then they are OUT!

* **x**

  Finally, the letter x. X stands for... **Xtended** mode! Also known as Extended Mode. Regular expressions can be really complicated, so the x at the end allows for extra room in the expression such as spaces, new lines, and comments. Then, the regex is more readable and less scary. Another tip: to comment in a regex, use ?#. But if you use ?#, you also have to use x.
