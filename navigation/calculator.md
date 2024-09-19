---
layout: page
title: Calculator
description: A blog for ideas for Compsci
permalink: /calculator/

---
{% include nav/home.html %}

<style>
  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr); /* 4 equal columns */
    gap: 10px; /* Gap between buttons */
    max-width: 250px; /* Adjust the width */
    margin: 0 auto; /* Center the calculator */
  }

  .calculator-output {
    grid-column: span 4; /* Take up the full width */
    padding: 10px;
    font-size: 24px;
    background-color: #DB7093;
    color: #fff;
    text-align: right;
  }

  .calculator-number, .calculator-operation, .calculator-equals, .calculator-clear { 
    font-size: 18px; /* Calculator buttons */
    background-color: #DB7093;
    color: #fff;
    text-align: center;
  }

  .calculator-clear { /* Clear button */
    grid-column: span 2;
    background-color: #DDA0DD;
  }

  .calculator-equals { /* Equals button */
    background-color: #DDA0DD;
  }

  .calculator-operation {   /* buttons for signs */
    background-color: #DDA0DD;
  }
</style>

<div class="calculator-container"> <!-- display  -->
  <div class="calculator-output" id="output">0</div>
  <div class="calculator-number">1</div>   <!-- row 1 -->
  <div class="calculator-number">2</div>
  <div class="calculator-number">3</div>
  <div class="calculator-operation">+</div>
  <div class="calculator-number">4</div>   <!-- row 2 -->
  <div class="calculator-number">5</div>
  <div class="calculator-number">6</div>
  <div class="calculator-operation">-</div>
  <div class="calculator-number">7</div>   <!-- row 3 -->
  <div class="calculator-number">8</div>
  <div class="calculator-number">9</div>
  <div class="calculator-operation">*</div>
  <div class="calculator-clear">A/C</div>   <!-- row 4 -->
  <div class="calculator-number">0</div>
  <div class="calculator-number">.</div>
  <div class="calculator-equals">=</div>
</div>