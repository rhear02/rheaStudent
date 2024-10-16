---
layout: post
title: Team Teach blog
toc: True
comments: True
permalink: /teamTeachblog/
---

## 3.1 Variables and Assignments
- **Definition**: Variables store values that can be used and modified throughout your program.  
  Example: `x = 10` assigns the value `10` to variable `x`.
- **Reassigning Variables**: You can change the value of a variable at any time.  
  Example: `x = 20` changes `x` to `20`.
- **Interactive Challenge**:  
  **Task**: Create a variable `age` and assign it your current age. Now, reassign it with what your age will be in 10 years.

## 3.2 Data Abstraction
- **Definition**: Data abstraction hides complexity by allowing you to work with data without knowing the details.  
  Example: Arrays or lists abstract away how the data is stored in memory.
- **Purpose**: It simplifies the way you handle complex data, like files or databases.
- **Interactive Challenge**:  
  **Task**: Think of a complex concept (like a playlist of songs). Now abstract it into a simple list.  
  Example: `playlist = ["Song1", "Song2", "Song3"]`

## 3.3 Mathematical Expressions
- **Basic Operations**: Computers use operators like `+`, `-`, `*`, and `/` for calculations.  
  Example: `y = (5 + 3) * 2`
- **Order of Operations**: Use parentheses to control operation order.  
  Example: `result = (2 + 3) * 4` gives `20`.
- **Interactive Challenge**:  
  **Task**: Solve the expression `((8 - 3) * 2) / 5`. What is the result?

## 3.4 Strings
- **Definition**: Strings are sequences of characters enclosed in quotes.  
  Example: `greeting = "Hello, world!"`
- **String Concatenation**: Combine strings using `+`.  
  Example: `full_name = first_name + " " + last_name`
- **Interactive Challenge**:  
  **Task**: Create a variable called `favorite_food` and assign it your favorite food. Then, print: "I love `favorite_food`!"

## 3.5 Booleans
- **Definition**: Booleans represent `True` or `False` values.  
  Example: `is_sunny = True`
- **Logical Operators**: Use `and`, `or`, `not` to combine conditions.  
  Example: `is_warm = is_sunny and temperature > 70`
- **Interactive Challenge**:  
  **Task**: Set `is_tired` to `True` or `False` depending on how you feel. Then, print: "I am tired: `is_tired`."

## 3.6 Conditionals
- **Definition**: Conditionals allow your program to make decisions using `if`, `else`, and `elif`.  
  Example: `if x > 10: print("x is large")`
- **Comparison Operators**: Use `==`, `!=`, `>`, `<` for comparisons.  
  Example: `if age == 18: print("You're an adult!")`
- **Interactive Challenge**:  
  **Task**: Create a conditional that checks if your favorite number is greater than 10. Print an appropriate message.

## 3.7 Nested Conditionals
- **Definition**: Nested conditionals are `if` statements inside other `if` statements.  
  Example:  
  ```python
  if age > 18:
      if has_id:
          print("You can enter")

## 3.8 While Loops
- **Definition**: A `while` loop continues to run as long as its condition is `True`.  
  Example:  
  ```python
  count = 0
  while count < 5:
      print(count)
      count += 1

## 3.10 Lists
- **Definition**: A list is an ordered collection of items, which can be of any data type (numbers, strings, etc.).  
  Example: `fruits = ["apple", "banana", "cherry"]`
- **Accessing List Elements**: You can access items in a list using their index, starting from `0`.  
  Example: `print(fruits[0])  # Outputs: "apple"`
- **Interactive Challenge**:  
  **Task**: Create a list of your top three favorite hobbies and print each one in a new sentence.


<script src="https://utteranc.es/client.js"
        repo="rhear02/rheaStudent"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
