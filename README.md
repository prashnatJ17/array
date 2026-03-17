# array
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JavaScript Array Assignments</title>
    <style>
        body { font-family: sans-serif; padding: 20px; background-color: #f4f4f9; color: #333; }
        .container { max-width: 800px; margin: auto; background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); }
        section { border-bottom: 2px solid #eee; padding-bottom: 20px; margin-bottom: 20px; }
        h2 { color: #2c3e50; font-size: 1.2rem; }
        input { padding: 8px; border: 1px solid #ccc; border-radius: 4px; margin-right: 5px; }
        button { padding: 8px 12px; background-color: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer; transition: 0.3s; }
        button:hover { background-color: #0056b3; }
        .display-box { margin-top: 10px; padding: 10px; background: #f9f9f9; border: 1px solid #ddd; border-radius: 4px; min-height: 20px; }
        
        /* Specific Styles for Assignments */
        ul { list-style: none; padding: 0; }
        li { padding: 8px; border-bottom: 1px solid #eee; display: flex; justify-content: space-between; align-items: center; }
        li:nth-child(even) { background-color: #fafafa; } /* Alternating colors for Assignment 5 */
        li:hover { background-color: #f1f1f1; } /* Hover effect */
        .delete-btn { background-color: #dc3545; font-size: 12px; }
        .highlight { background-color: yellow; font-weight: bold; padding: 2px 5px; }
    </style>
</head>
<body>

<div class="container">

    <section>
        <h2>1. To-Do List Manager</h2>
        <input type="text" id="todoInput" placeholder="Enter a task">
        <button onclick="addTask()">Add Task</button>
        <button onclick="clearTasks()" style="background:#6c757d">Clear All</button>
        <ul id="todoList" class="display-box"></ul>
    </section>

    <section>
        <h2>2. Student Marks Calculator</h2>
        <input type="number" id="markInput" placeholder="Enter mark">
        <button onclick="addMark()">Add Mark</button>
        <button onclick="calculateMarks()" style="background:#28a745">Calculate</button>
        <button onclick="resetMarks()" style="background:#6c757d">Reset</button>
        <div id="marksResult" class="display-box">Results will appear here...</div>
    </section>

    <section>
        <h2>3. Search in an Array</h2>
        <p><small>Database: Audi, BMW, Tesla, Mercedes, Toyota</small></p>
        <input type="text" id="searchInput" placeholder="Search for a car...">
        <button onclick="searchArray()">Search</button>
        <div id="searchResult" class="display-box"></div>
    </section>

    <section>
        <h2>4. Filter Even and Odd Numbers</h2>
        <input type="number" id="numInput" placeholder="Add a number">
        <button onclick="addNumber()">Add Number</button>
        <button onclick="filterNumbers('even')">Show Even</button>
        <button onclick="filterNumbers('odd')">Show Odd</button>
        <button onclick="clearNumbers()" style="background:#6c757d">Clear</button>
        <div class="display-box">
            <strong>Even:</strong> <span id="evenDisp"></span><br>
            <strong>Odd:</strong> <span id="oddDisp"></span>
        </div>
    </section>

    <section>
        <h2>5. Sort Names Alphabetically</h2>
        <input type="text" id="nameInput" placeholder="Enter name">
        <button onclick="addName()">Add Name</button>
        <button onclick="sortNames()" style="background:#17a2b8">Sort</button>
        <button onclick="resetNames()" style="background:#6c757d">Reset</button>
        <ul id="nameList" class="display-box"></ul>
    </section>

</div>

<script>
    // --- 1. To-Do Logic ---
    let tasks = [];
    function addTask() {
        const val = document.getElementById('todoInput').value;
        if(val) { tasks.push(val); document.getElementById('todoInput').value = ''; renderTodos(); }
    }
    function removeTask(i) { tasks.splice(i, 1); renderTodos(); }
    function clearTasks() { tasks = []; renderTodos(); }
    function renderTodos() {
        document.getElementById('todoList').innerHTML = tasks.map((t, i) => 
            `<li>${t} <button class="delete-btn" onclick="removeTask(${i})">Delete</button></li>`).join('');
    }

    // --- 2. Marks Logic ---
    let marks = [];
    function addMark() {
        const m = parseFloat(document.getElementById('markInput').value);
        if(!isNaN(m)) { marks.push(m); document.getElementById('markInput').value = ''; }
    }
    function calculateMarks() {
        if(!marks.length) return;
        const total = marks.reduce((a, b) => a + b, 0);
        const max = Math.max(...marks);
        const min = Math.min(...marks);
        document.getElementById('marksResult').innerHTML = `Total: ${total} | Avg: ${(total/marks.length).toFixed(2)} | Max: ${max} | Min: ${min}`;
    }
    function resetMarks() { marks = []; document.getElementById('marksResult').innerText = 'Cleared'; }

    // --- 3. Search Logic ---
    const carArray = ["Audi", "BMW", "Tesla", "Mercedes", "Toyota"];
    function searchArray() {
        const query = document.getElementById('searchInput').value.toLowerCase();
        const found = carArray.find(c => c.toLowerCase() === query);
        document.getElementById('searchResult').innerHTML = found ? `<span class="highlight">${found}</span>` : "Not Found";
    }

    // --- 4. Numbers Logic ---
    let numArr = [];
    function addNumber() {
        const n = parseInt(document.getElementById('numInput').value);
        if(!isNaN(n)) { numArr.push(n); document.getElementById('numInput').value = ''; }
    }
    function filterNumbers(type) {
        const result = type === 'even' ? numArr.filter(x => x % 2 === 0) : numArr.filter(x => x % 2 !== 0);
        document.getElementById(type === 'even' ? 'evenDisp' : 'oddDisp').innerText = result.join(', ');
    }
    function clearNumbers() { numArr = []; document.getElementById('evenDisp').innerText = ''; document.getElementById('oddDisp').innerText = ''; }

    // --- 5. Sort Logic ---
    let namesArr = [];
    function addName() {
        const n = document.getElementById('nameInput').value;
        if(n) { namesArr.push(n); document.getElementById('nameInput').value = ''; renderNames(); }
    }
    function sortNames() { namesArr.sort((a,b) => a.localeCompare(b)); renderNames(); }
    function resetNames() { namesArr = []; renderNames(); }
    function renderNames() {
        document.getElementById('nameList').innerHTML = namesArr.map(n => `<li>${n}</li>`).join('');
    }
</script>

</body>
</html>
