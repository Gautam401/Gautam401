<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>All-in-One Math Calculator</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }
    input[type="text"] {
      width: 300px;
      padding: 10px;
      margin-bottom: 10px;
      font-size: 16px;
    }
    select {
      padding: 10px;
      font-size: 16px;
    }
    button {
      padding: 10px 15px;
      font-size: 16px;
      margin-top: 10px;
    }
    #result {
      font-size: 18px;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <h1>All-in-One Math Calculator</h1>
  
  <label for="formula">Choose Formula:</label>
  <select id="formula">
    <option value="addition">Addition</option>
    <option value="subtraction">Subtraction</option>
    <option value="multiplication">Multiplication</option>
    <option value="division">Division</option>
    <option value="circleArea">Area of Circle</option>
    <option value="rectangleArea">Area of Rectangle</option>
    <option value="triangleArea">Area of Triangle</option>
    <option value="quadratic">Quadratic Equation</option>
  </select><br><br>

  <label for="input1">Enter First Value:</label>
  <input type="text" id="input1" placeholder="Enter value"><br><br>
  
  <label for="input2">Enter Second Value:</label>
  <input type="text" id="input2" placeholder="Enter value"><br><br>

  <button onclick="calculate()">Calculate</button>

  <div id="result"></div>

  <script>
    function calculate() {
      const formula = document.getElementById("formula").value;
      const value1 = parseFloat(document.getElementById("input1").value);
      const value2 = parseFloat(document.getElementById("input2").value);
      let result = "";
      
      if (isNaN(value1) || isNaN(value2)) {
        result = "Please enter valid numbers.";
      } else {
        switch (formula) {
          case "addition":
            result = `Result: ${value1 + value2}`;
            break;
          case "subtraction":
            result = `Result: ${value1 - value2}`;
            break;
          case "multiplication":
            result = `Result: ${value1 * value2}`;
            break;
          case "division":
            if (value2 !== 0) {
              result = `Result: ${value1 / value2}`;
            } else {
              result = "Error: Cannot divide by zero.";
            }
            break;
          case "circleArea":
            if (value1 > 0) {
              result = `Area of Circle: ${Math.PI * Math.pow(value1, 2)}`;
            } else {
              result = "Radius must be positive.";
            }
            break;
          case "rectangleArea":
            if (value1 > 0 && value2 > 0) {
              result = `Area of Rectangle: ${value1 * value2}`;
            } else {
              result = "Length and width must be positive.";
            }
            break;
          case "triangleArea":
            if (value1 > 0 && value2 > 0) {
              result = `Area of Triangle: ${(0.5 * value1 * value2)}`;
            } else {
              result = "Base and height must be positive.";
            }
            break;
          case "quadratic":
            if (value1 !== 0) {
              let discriminant = Math.pow(value2, 2) - 4 * value1 * value2;
              if (discriminant > 0) {
                let root1 = (-value2 + Math.sqrt(discriminant)) / (2 * value1);
                let root2 = (-value2 - Math.sqrt(discriminant)) / (2 * value1);
                result = `Roots: ${root1}, ${root2}`;
              } else if (discriminant === 0) {
                let root = -value2 / (2 * value1);
                result = `Single Root: ${root}`;
              } else {
                result = "No real roots.";
              }
            } else {
              result = "Coefficient a cannot be zero.";
            }
            break;
        }
      }
      
      document.getElementById("result").innerHTML = result;
    }
  </script>
  
</body>
</html>
