<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jumbled Numbers Pattern</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f);
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 2rem;
            overflow-x: auto;
        }
        
        .container {
            max-width: 1400px;
            width: 100%;
            text-align: center;
        }
        
        h1 {
            font-size: 2.5rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        
        .subtitle {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }
        
        .pattern-explanation {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 1.5rem;
            margin-bottom: 2rem;
            text-align: left;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            display: none;
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease, padding 0.5s ease;
        }
        
        .pattern-explanation.visible {
            display: block;
            max-height: 500px;
            padding: 1.5rem;
        }
        
        .pattern-explanation h2 {
            margin-bottom: 1rem;
            color: #fdbb2d;
        }
        
        .pattern-explanation p {
            margin-bottom: 0.5rem;
            line-height: 1.5;
        }
        
        .circles-container {
            display: flex;
            justify-content: center;
            gap: 3rem;
            margin: 2rem 0;
            flex-wrap: wrap;
        }
        
        .circle-wrapper {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 1rem;
        }
        
        .circle-label {
            font-size: 1.5rem;
            font-weight: bold;
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            background: rgba(0, 0, 0, 0.6);
            padding: 0.5rem 1.5rem;
            border-radius: 25px;
            border: 2px solid rgba(255, 255, 255, 0.3);
        }
        
        .circle {
            width: 500px;
            height: 500px;
            border-radius: 50%;
            position: relative;
            border: 4px solid rgba(255, 255, 255, 0.7);
            overflow: hidden;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            background: rgba(255, 255, 255, 0.05);
            transition: all 0.5s ease;
        }
        
        .circle-1 {
            border-color: #ff4d4d;
        }
        
        .circle-2 {
            border-color: #4dff4d;
        }
        
        .circle-3 {
            border-color: #4d4dff;
        }
        
        .circle-4 {
            border-color: #ffff4d;
        }
        
        .number-item {
            width: 28px;
            height: 28px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 0.75rem;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.95);
            color: #1a2a6c;
            transition: all 0.3s ease;
            position: absolute;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(0, 0, 0, 0.1);
            cursor: pointer;
        }
        
        .number-item:hover {
            transform: scale(1.4);
            background: #fdbb2d;
            color: #1a2a6c;
            z-index: 5;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
        }
        
        .number-item.highlighted {
            transform: scale(1.6);
            background: #ff0000;
            color: white;
            z-index: 10;
            box-shadow: 0 0 15px rgba(255, 0, 0, 0.7);
            animation: pulse 1s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1.6); }
            50% { transform: scale(1.8); }
            100% { transform: scale(1.6); }
        }
        
        .pattern-sequence {
            margin-top: 2rem;
            padding: 1rem;
            background: rgba(255, 255, 255, 0.15);
            border-radius: 10px;
            font-size: 1.1rem;
            display: none;
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease, padding 0.5s ease;
        }
        
        .pattern-sequence.visible {
            display: block;
            max-height: 200px;
            padding: 1rem;
        }
        
        .highlight {
            color: #fdbb2d;
            font-weight: bold;
        }
        
        .controls {
            margin: 1rem 0;
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 1rem;
        }
        
        button {
            background: #fdbb2d;
            color: #1a2a6c;
            border: none;
            padding: 0.8rem 1.5rem;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        
        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.3);
        }
        
        .search-container {
            display: flex;
            justify-content: center;
            margin: 1rem 0;
            gap: 0.5rem;
        }
        
        input {
            padding: 0.8rem 1rem;
            border-radius: 50px;
            border: none;
            font-size: 1rem;
            width: 200px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        
        .stats {
            display: flex;
            justify-content: center;
            gap: 2rem;
            margin: 1rem 0;
            flex-wrap: wrap;
        }
        
        .stat-item {
            background: rgba(255, 255, 255, 0.1);
            padding: 1rem;
            border-radius: 10px;
            min-width: 150px;
        }
        
        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: #fdbb2d;
        }
        
        .revealed {
            border-width: 8px;
            box-shadow: 0 0 30px rgba(253, 187, 45, 0.7);
        }
        
        .hint {
            margin-top: 1rem;
            font-style: italic;
            opacity: 0.7;
        }
        
        @media (max-width: 1200px) {
            .circle {
                width: 450px;
                height: 450px;
            }
        }
        
        @media (max-width: 992px) {
            .circle {
                width: 400px;
                height: 400px;
            }
            
            .number-item {
                width: 24px;
                height: 24px;
                font-size: 0.7rem;
            }
            
            .circle-label {
                font-size: 1.3rem;
            }
        }
        
        @media (max-width: 768px) {
            .circle {
                width: 350px;
                height: 350px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .circles-container {
                gap: 2rem;
            }
            
            .circle-label {
                font-size: 1.2rem;
            }
        }
        
        @media (max-width: 576px) {
            .circle {
                width: 300px;
                height: 300px;
            }
            
            .number-item {
                width: 20px;
                height: 20px;
                font-size: 0.6rem;
            }
            
            .circle-label {
                font-size: 1.1rem;
                padding: 0.4rem 1.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Jumbled Numbers Pattern</h1>
        <p class="subtitle">Numbers 1-250 randomly placed within circles following a hidden pattern</p>
        
        <div class="pattern-explanation" id="patternExplanation">
            <h2>Hidden Pattern</h2>
            <p>Numbers appear jumbled, but they follow a specific distribution pattern:</p>
            <p>• <span class="highlight">Circle 1 (Red)</span>: Numbers where (number % 4) = 0 (4, 8, 12, 16, ...)</p>
            <p>• <span class="highlight">Circle 2 (Green)</span>: Numbers where (number % 4) = 1 (1, 5, 9, 13, ...)</p>
            <p>• <span class="highlight">Circle 3 (Blue)</span>: Numbers where (number % 4) = 2 (2, 6, 10, 14, ...)</p>
            <p>• <span class="highlight">Circle 4 (Yellow)</span>: Numbers where (number % 4) = 3 (3, 7, 11, 15, ...)</p>
        </div>
        
        <div class="search-container">
            <input type="number" id="searchInput" placeholder="Enter a number (1-250)" min="1" max="250">
            <button onclick="findNumber()">Find Number</button>
        </div>
        
        <div class="controls">
            <button onclick="jumbleNumbers()">Jumble Numbers Again</button>
            <button onclick="togglePattern()" id="patternToggle">Reveal Pattern</button>
            <button onclick="resetNumbers()">Reset Numbers</button>
        </div>
        
        <div class="stats">
            <div class="stat-item">
                <div>Circle 1 Count</div>
                <div class="stat-value" id="count1">0</div>
            </div>
            <div class="stat-item">
                <div>Circle 2 Count</div>
                <div class="stat-value" id="count2">0</div>
            </div>
            <div class="stat-item">
                <div>Circle 3 Count</div>
                <div class="stat-value" id="count3">0</div>
            </div>
            <div class="stat-item">
                <div>Circle 4 Count</div>
                <div class="stat-value" id="count4">0</div>
            </div>
        </div>
        
        <div class="circles-container">
            <div class="circle-wrapper">
                <div class="circle-label">Circle 1</div>
                <div class="circle circle-1" id="circle1"></div>
            </div>
            <div class="circle-wrapper">
                <div class="circle-label">Circle 2</div>
                <div class="circle circle-2" id="circle2"></div>
            </div>
            <div class="circle-wrapper">
                <div class="circle-label">Circle 3</div>
                <div class="circle circle-3" id="circle3"></div>
            </div>
            <div class="circle-wrapper">
                <div class="circle-label">Circle 4</div>
                <div class="circle circle-4" id="circle4"></div>
            </div>
        </div>
        
        <div class="pattern-sequence" id="patternSequence">
            <p><span class="highlight">Hidden Sequence:</span> 1→Circle 2, 2→Circle 3, 3→Circle 4, 4→Circle 1, 5→Circle 2, 6→Circle 3, ... continuing to 250</p>
            <p>Without knowing the pattern, finding specific numbers is very difficult!</p>
        </div>
        
        <p class="hint">Can you figure out the pattern? Try finding several numbers and see if you notice a relationship.</p>
    </div>

    <script>
        let currentNumbers = {
            circle1: [],
            circle2: [],
            circle3: [],
            circle4: []
        };
        
        let patternRevealed = false;
        
        function placeNumbersInGrid(circle, numbers, circleId) {
            const circleSize = 500;
            const itemSize = 28;
            const itemsPerRow = Math.floor(circleSize / itemSize);
            const totalRows = Math.ceil(numbers.length / itemsPerRow);
            
            // Calculate grid dimensions that fit within the circle
            const gridWidth = itemsPerRow * itemSize;
            const gridHeight = totalRows * itemSize;
            
            // Center the grid within the circle
            const startX = (circleSize - gridWidth) / 2;
            const startY = (circleSize - gridHeight) / 2;
            
            circle.innerHTML = '';
            
            numbers.forEach((number, index) => {
                const row = Math.floor(index / itemsPerRow);
                const col = index % itemsPerRow;
                
                const numberItem = document.createElement('div');
                numberItem.className = 'number-item';
                numberItem.textContent = number;
                numberItem.title = `Number ${number}`;
                numberItem.dataset.number = number;
                numberItem.dataset.circle = circleId;
                
                // Add slight random offset to make it look jumbled but still organized
                const randomOffsetX = (Math.random() - 0.5) * 10;
                const randomOffsetY = (Math.random() - 0.5) * 10;
                
                const x = startX + col * itemSize + randomOffsetX;
                const y = startY + row * itemSize + randomOffsetY;
                
                numberItem.style.left = `${x}px`;
                numberItem.style.top = `${y}px`;
                
                circle.appendChild(numberItem);
            });
            
            // Update stats
            updateStats();
        }
        
        function placeNumbers() {
            const circle1 = document.getElementById('circle1');
            const circle2 = document.getElementById('circle2');
            const circle3 = document.getElementById('circle3');
            const circle4 = document.getElementById('circle4');
            
            const numbers1 = []; // Numbers divisible by 4
            const numbers2 = []; // Numbers with remainder 1
            const numbers3 = []; // Numbers with remainder 2
            const numbers4 = []; // Numbers with remainder 3
            
            // Distribute numbers according to pattern
            for (let i = 1; i <= 250; i++) {
                const remainder = i % 4;
                
                if (remainder === 1) {
                    numbers2.push(i);
                } else if (remainder === 2) {
                    numbers3.push(i);
                } else if (remainder === 3) {
                    numbers4.push(i);
                } else {
                    numbers1.push(i);
                }
            }
            
            // Store current numbers
            currentNumbers.circle1 = [...numbers1];
            currentNumbers.circle2 = [...numbers2];
            currentNumbers.circle3 = [...numbers3];
            currentNumbers.circle4 = [...numbers4];
            
            // Shuffle each array to make them jumbled
            function shuffleArray(array) {
                for (let i = array.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [array[i], array[j]] = [array[j], array[i]];
                }
                return array;
            }
            
            // Place numbers in grid layout within each circle
            placeNumbersInGrid(circle1, shuffleArray([...numbers1]), 'circle1');
            placeNumbersInGrid(circle2, shuffleArray([...numbers2]), 'circle2');
            placeNumbersInGrid(circle3, shuffleArray([...numbers3]), 'circle3');
            placeNumbersInGrid(circle4, shuffleArray([...numbers4]), 'circle4');
        }
        
        function jumbleNumbers() {
            // Add animation effect
            const circles = document.querySelectorAll('.circle');
            circles.forEach(circle => {
                circle.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    circle.style.transform = 'scale(1)';
                }, 300);
            });
            
            // Jumble after a short delay for visual effect
            setTimeout(placeNumbers, 300);
        }
        
        function togglePattern() {
            const explanation = document.getElementById('patternExplanation');
            const sequence = document.getElementById('patternSequence');
            const toggleButton = document.getElementById('patternToggle');
            
            if (patternRevealed) {
                explanation.classList.remove('visible');
                sequence.classList.remove('visible');
                toggleButton.textContent = 'Reveal Pattern';
                patternRevealed = false;
                
                // Remove reveal effect from circles
                const circles = document.querySelectorAll('.circle');
                circles.forEach(circle => {
                    circle.classList.remove('revealed');
                });
            } else {
                explanation.classList.add('visible');
                sequence.classList.add('visible');
                toggleButton.textContent = 'Hide Pattern';
                patternRevealed = true;
                
                // Add reveal effect to circles
                const circles = document.querySelectorAll('.circle');
                circles.forEach(circle => {
                    circle.classList.add('revealed');
                });
            }
        }
        
        function resetNumbers() {
            // Remove any highlights
            const highlighted = document.querySelectorAll('.number-item.highlighted');
            highlighted.forEach(item => {
                item.classList.remove('highlighted');
            });
            
            // Hide pattern if it's visible
            if (patternRevealed) {
                togglePattern();
            }
            
            // Clear search input
            document.getElementById('searchInput').value = '';
            
            // Re-place numbers
            placeNumbers();
        }
        
        function findNumber() {
            const input = document.getElementById('searchInput');
            const number = parseInt(input.value);
            
            if (isNaN(number) || number < 1 || number > 250) {
                alert('Please enter a valid number between 1 and 250');
                return;
            }
            
            // Remove any previous highlights
            const highlighted = document.querySelectorAll('.number-item.highlighted');
            highlighted.forEach(item => {
                item.classList.remove('highlighted');
            });
            
            // Find and highlight the number
            const numberItems = document.querySelectorAll('.number-item');
            let found = false;
            
            numberItems.forEach(item => {
                if (parseInt(item.textContent) === number) {
                    item.classList.add('highlighted');
                    found = true;
                    
                    // Scroll the circle into view
                    const circle = item.closest('.circle');
                    circle.scrollIntoView({ behavior: 'smooth', block: 'center' });
                }
            });
            
            if (!found) {
                alert(`Number ${number} not found!`);
            }
        }
        
        function updateStats() {
            document.getElementById('count1').textContent = currentNumbers.circle1.length;
            document.getElementById('count2').textContent = currentNumbers.circle2.length;
            document.getElementById('count3').textContent = currentNumbers.circle3.length;
            document.getElementById('count4').textContent = currentNumbers.circle4.length;
        }
        
        // Initialize the visualization
        document.addEventListener('DOMContentLoaded', placeNumbers);
        
        // Add keyboard support for search
        document.getElementById('searchInput').addEventListener('keyup', function(event) {
            if (event.key === 'Enter') {
                findNumber();
            }
        });
    </script>
</body>
</html>
