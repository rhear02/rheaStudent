---
layout: page
title: Calculator
description: A blog for ideas for Compsci
permalink: /calculator/

---
{% include nav/home.html %}

<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Smaller Calculator</title>
  <style>
    /* Calculator container */
    .calculator-container {
      display: grid;
      grid-template-columns: repeat(4, 1fr); /* 4 columns */
      grid-gap: 5px; /* Reduced gap between buttons */
      background-color: #333;
      padding: 10px; /* Reduced padding */
      border-radius: 10px; /* Smaller border radius */
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); /* Reduced shadow */
      max-width: 300px; /* Reduced width */
      margin: 30px auto; /* Adjusted top and bottom margin */
    }

    /* Calculator output style */
    .calculator-output {
      grid-column: span 4; /* Takes full width of the first row */
      border-radius: 5px; /* Smaller border radius */
      padding: 10px; /* Reduced padding */
      font-size: 20px; /* Smaller font size */
      background-color: #222;
      color: #fff;
      text-align: right;
      display: flex;
      justify-content: flex-end;
      align-items: center;
      box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.1); /* Reduced shadow */
    }

    /* Calculator number and operation buttons */
    .calculator-number, .calculator-operation, .calculator-equals, .calculator-clear {
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 18px; /* Smaller font size */
      background-color: #ff69b4;
      color: white;
      border: none;
      padding: 10px; /* Reduced padding */
      border-radius: 5px; /* Smaller border radius */
      cursor: pointer;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1); /* Reduced shadow */
      transition: background-color 0.3s, transform 0.2s;
    }

    /* Button hover and active effects */
    .calculator-number:hover, .calculator-operation:hover, .calculator-equals:hover, .calculator-clear:hover {
      background-color: #ff69b4;
    }

    .calculator-number:active, .calculator-operation:active, .calculator-equals:active, .calculator-clear:active {
      transform: scale(0.95);
    }

    /* Specific styles for operation buttons */
    .calculator-operation {
      background-color: #ff69b4;
    }

    .calculator-operation:hover {
      background-color: #ff69b4;
    }

    /* Style for the equals button */
    .calculator-equals {
      background-color: #ff69b4;
      grid-column: span 2; /* Make the equals button larger */
    }

    .calculator-equals:hover {
      background-color: #ff69b4;
    }

    /* Clear button style */
    .calculator-clear {
      background-color: #ff69b4;
      grid-column: span 2; /* Make the clear button larger */
    }

    .calculator-clear:hover {
      background-color: #ff69b4;
    }
  </style>
</head>
<body>

  <div class="calculator-container">
    <!-- result display -->
    <div class="calculator-output" id="output">0</div>
    
    <!-- row 1 -->
    <button class="calculator-number">1</button>
    <button class="calculator-number">2</button>
    <button class="calculator-number">3</button>
    <button class="calculator-operation">+</button>
    
    <!-- row 2 -->
    <button class="calculator-number">4</button>
    <button class="calculator-number">5</button>
    <button class="calculator-number">6</button>
    <button class="calculator-operation">-</button>
    
    <!-- row 3 -->
    <button class="calculator-number">7</button>
    <button class="calculator-number">8</button>
    <button class="calculator-number">9</button>
    <button class="calculator-operation">*</button>
    
    <!-- row 4 -->
    <button class="calculator-clear">A/C</button>
    <button class="calculator-number">0</button>
    <button class="calculator-number">.</button>
    <button class="calculator-operation">/</button>
    
    <!-- equals button -->
    <button class="calculator-equals">=</button>
  </div>

  <script>
    let firstNumber = '';
    let secondNumber = '';
    let operator = null;
    let shouldReset = false;

    const output = document.getElementById('output');
    const numberButtons = document.querySelectorAll('.calculator-number');
    const operationButtons = document.querySelectorAll('.calculator-operation');
    const equalsButton = document.querySelector('.calculator-equals');
    const clearButton = document.querySelector('.calculator-clear');

    numberButtons.forEach(button => {
      button.addEventListener('click', () => {
        if (shouldReset) {
          output.textContent = '';
          shouldReset = false;
        }
        if (output.textContent === '0') {
          output.textContent = button.textContent;
        } else {
          output.textContent += button.textContent;
        }
      });
    });

    operationButtons.forEach(button => {
      button.addEventListener('click', () => {
        firstNumber = output.textContent;
        operator = button.textContent;
        shouldReset = true;
      });
    });

    equalsButton.addEventListener('click', () => {
      secondNumber = output.textContent;
      const result = calculate(firstNumber, secondNumber, operator);
      output.textContent = result;
      shouldReset = true;
    });

    clearButton.addEventListener('click', () => {
      output.textContent = '0';
      firstNumber = '';
      secondNumber = '';
      operator = null;
      shouldReset = false;
    });

    function calculate(first, second, operator) {
      first = parseFloat(first);
      second = parseFloat(second);
      switch (operator) {
        case '+':
          return first + second;
        case '-':
          return first - second;
        case '*':
          return first * second;
        case '/':
          return first / second;
        default:
          return 0;
      }
    }
  </script>

</body>
</html>

<body style="background-color:pink;">