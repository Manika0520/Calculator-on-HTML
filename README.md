# Calculator-on-HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        .calculator {
            width: 300px;
            margin: 50px auto;
            border: 1px solid #ccc;
            border-radius: 5px;
            overflow: hidden;
            box-shadow: 2px 2px 5px #888888;
        }

        .display {
            background-color: #f0f0f0;
            padding: 15px;
            text-align: right;
            font-size: 24px;
            border-bottom: 1px solid #ccc;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
        }

        button {
            padding: 20px;
            font-size: 18px;
            border: none;
            background-color: #eee;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #ddd;
        }

        .operator {
            background-color: #f5a623;
            color: white;
        }

        .operator:hover {
            background-color: #e0951a;
        }

        .equal {
            grid-column: span 2;
            background-color: #5cb85c;
            color: white;
        }

        .equal:hover {
            background-color: #4cae4c;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display">0</div>
        <div class="buttons">
            <button onclick="clearDisplay()">C</button>
            <button onclick="deleteLast()">DEL</button>
            <button onclick="appendOperator('/')" class="operator">/</button>
            <button onclick="appendOperator('*')" class="operator">*</button>
            <button onclick="appendNumber('7')">7</button>
            <button onclick="appendNumber('8')">8</button>
            <button onclick="appendNumber('9')">9</button>
            <button onclick="appendOperator('-')" class="operator">-</button>
            <button onclick="appendNumber('4')">4</button>
            <button onclick="appendNumber('5')">5</button>
            <button onclick="appendNumber('6')">6</button>
            <button onclick="appendOperator('+')" class="operator">+</button>
            <button onclick="appendNumber('1')">1</button>
            <button onclick="appendNumber('2')">2</button>
            <button onclick="appendNumber('3')">3</button>
            <button onclick="calculate()" class="equal">=</button>
            <button onclick="appendNumber('0')">0</button>
            <button onclick="appendDecimal()">.</button>
        </div>
    </div>

    <script>
        let display = document.querySelector('.display');
        let currentInput = '';
        let operator = null;
        let firstOperand = null;

        function updateDisplay() {
            display.textContent = currentInput || '0';
        }

        function appendNumber(number) {
            if (currentInput === '0') {
                currentInput = number;
            } else {
                currentInput += number;
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (currentInput === '' && firstOperand === null) return;

            if (firstOperand !== null) {
                calculate();
            }

            firstOperand = parseFloat(currentInput);
            operator = op;
            currentInput = '';
        }

        function appendDecimal() {
            if (!currentInput.includes('.')) {
                currentInput += '.';
                updateDisplay();
            }
        }

        function clearDisplay() {
            currentInput = '';
            operator = null;
            firstOperand = null;
            updateDisplay();
        }

        function deleteLast() {
            currentInput = currentInput.slice(0, -1);
            updateDisplay();
        }

        function calculate() {
            if (operator === null || firstOperand === null || currentInput === '') return;

            const secondOperand = parseFloat(currentInput);
            let result;

            switch (operator) {
                case '+':
                    result = firstOperand + secondOperand;
                    break;
                case '-':
                    result = firstOperand - secondOperand;
                    break;
                case '*':
                    result = firstOperand * secondOperand;
                    break;
                case '/':
                    if (secondOperand === 0) {
                        result = 'Error';
                    } else {
                        result = firstOperand / secondOperand;
                    }
                    break;
                default:
                    return;
            }

            currentInput = String(result);
            operator = null;
            firstOperand = null;
            updateDisplay();
        }

        updateDisplay(); // Initial display update
    </script>
</body>
</html>
