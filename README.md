# calculator-project1
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
  <title>Simple Calculator</title>
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #80ea66, #764ba2);
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      padding: 20px;
    }
    .calculator {
      background: rgba(255, 255, 255, 0.1);
      border-radius: 16px;
      padding: 24px 32px;
      width: 320px;
      max-width: 100%;
      box-shadow: 0 8px 24px rgba(0,0,0,0.3);
      display: flex;
      flex-direction: column;
      gap: 20px;
    }
    h1 {
      text-align: center;
      font-weight: 700;
      margin: 0 0 8px;
      font-size: 1.8rem;
      letter-spacing: 1px;
    }
    label {
      display: block;
      font-weight: 600;
      margin-bottom: 6px;
      font-size: 0.9rem;
    }
    input[type="number"] {
      width: 100%;
      padding: 12px 14px;
      font-size: 1.2rem;
      border-radius: 12px;
      border: none;
      outline: none;
      background: rgba(255,255,255,0.15);
      color: #fff;
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.3);
      transition: background 0.3s ease;
    }
    input[type="number"]:focus {
      background: rgba(255,255,255,0.3);
    }
    select {
      width: 100%;
      padding: 12px 14px;
      font-size: 1.3rem;
      border-radius: 12px;
      border: none;
      outline: none;
      background: rgba(255,255,255,0.15);
      color: #fff;
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.3);
      cursor: pointer;
      transition: background 0.3s ease;
      appearance: none;
      -webkit-appearance: none;
      -moz-appearance: none;
      text-align-last: center;
    }
    select:focus {
      background: rgba(255,255,255,0.3);
    }
    .result {
      background: rgba(255,255,255,0.15);
      border-radius: 12px;
      padding: 16px 20px;
      font-size: 1.6rem;
      font-weight: 700;
      text-align: center;
      box-shadow: inset 0 2px 5px rgba(0,0,0,0.3);
      min-height: 48px;
      user-select: text;
    }
    @media (max-width: 400px) {
      .calculator {
        width: 100%;
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="calculator" role="main" aria-label="Simple Calculator">
    <h1>Simple Calculator</h1>
    <div>
      <label for="num1">First Number</label>
      <input type="number" id="num1" inputmode="decimal" aria-describedby="num1-desc" placeholder="Enter first number" />
    </div>
    <div>
      <label for="num2">Second Number</label>
      <input type="number" id="num2" inputmode="decimal" aria-describedby="num2-desc" placeholder="Enter second number" />
    </div>
    <div>
      <label for="operation">Operation</label>
      <select id="operation" aria-label="Select operation">
        <option value="add">Addition (+)</option>
        <option value="subtract">Subtraction (−)</option>
        <option value="multiply">Multiplication (×)</option>
        <option value="divide">Division (÷)</option>
      </select>
    </div>
    <div class="result" id="result" aria-live="polite" role="status">
      Result will appear here
    </div>
  </div>

  <script>
    (function() {
      const num1Input = document.getElementById('num1');
      const num2Input = document.getElementById('num2');
      const operationSelect = document.getElementById('operation');
      const resultDisplay = document.getElementById('result');

      function calculate() {
        const val1 = parseFloat(num1Input.value);
        const val2 = parseFloat(num2Input.value);
        const op = operationSelect.value;
        if (isNaN(val1) || isNaN(val2)) {
          resultDisplay.textContent = 'Please enter valid numbers.';
          return;
        }

        let res;
        switch(op) {
          case 'add':
            res = val1 + val2;
            break;
          case 'subtract':
            res = val1 - val2;
            break;
          case 'multiply':
            res = val1 * val2;
            break;
          case 'divide':
            if (val2 === 0) {
              resultDisplay.textContent = 'Error: Division by zero';
              return;
            }
            res = val1 / val2;
            break;
          default:
            resultDisplay.textContent = 'Unknown operation';
            return;
        }
        if (Number.isInteger(res)) {
          resultDisplay.textContent = res;
        } else {
          resultDisplay.textContent = res.toFixed(6).replace(/\.?0+$/, '');
        }
      }

      num1Input.addEventListener('input', calculate);
      num2Input.addEventListener('input', calculate);
      operationSelect.addEventListener('change', calculate);
      resultDisplay.textContent = 'Please enter numbers and select operation.';
    })();
  </script>
</body>
</html>
