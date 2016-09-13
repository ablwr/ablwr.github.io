---
layout: post
title: "Form Helpers"
date: 2014-07-15 22:38:07 -0400
comments: true
categories: forms, form for more like form FOUR am I right
---

Forms are hard! Forms are confusing in real life as well as on (or behind) the web. One problem with building web forms in Rails for me was that there are too many options! There are three distinct ways to create forms. And it’s also hard to tell which options are optional and which ones are required. Additionally, the syntax isn't always the same, so it can be hard to remember three different ways to do the same thing without mixing them up, especially as a beginner.

![](/images/basic_form.png)

Here is the first form. This is the form that I think most people in my Ruby005 class would have written last week, before we learned about Rails form helpers. This is a form at its lowest level of abstraction while still being partially in Ruby, although it lacks Rails form helpers and form options helpers. This form just iterates through each ingredient and creates a checkbox. Checkboxes gives value of 1 if checked, 0 if not. And in the controller, we have to add ingredient_ids as an empty array in the params. It has to be called that or the whole thing won't work and all this code will be for naught. 

![](/images/form_tag.png)

Collection_check_boxes takes in five arguments, object, method, collection, value_method, text_method. Above, the recipe is the object, the ingredients_ids are the method, Ingredient.all is the collection, the :id is the value of the checkbox, and the name is the text to display with the checkbox. Best practice would be to abstract away the collection here so you are not calling a class in your View, and make a variable for Ingredient.all. Collection_check_boxes can look cumbersome with its five arguments, but its much cleaner than the previous code.

![](/images/form_for.png)

In form_for, it looks like collection_check_boxes only takes FOUR arguments. And when you’re in formland, that’s an easy way to remember. Form_FOR takes FOUR. It actually takes five arguments, but one has already been declared at the beginning of the form. It’s @recipe.

There's plenty more to learn about forms and form helpers, but I hope this little post can clear up some of the confusion surrounding usage.