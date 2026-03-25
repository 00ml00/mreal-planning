#   
<!DOCTYPE html>  
<html>  
<head>  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<title>Mreal Planning</title>  
  
<style>  
body {margin:0;font-family:Arial;background:#121212;color:white;}  
.header {text-align:center;padding:15px;font-size:22px;border-bottom:2px solid red;background:#000;}  
.container {padding:15px;}  
.card {background:#1e1e1e;border:1px solid red;border-radius:10px;padding:12px;margin-bottom:12px;}  
button {background:red;color:white;border:none;padding:8px;margin-top:8px;border-radius:6px;}  
input {width:100%;padding:8px;margin-top:5px;border-radius:6px;border:none;}  
.small {font-size:12px;color:#aaa;}  
</style>  
</head>  
  
<body>  
  
<div class="header">Mreal Planning</div>  
  
<div class="container">  
  
<div class="card">  
<h3>Day <span id="day"></span></h3>  
<p class="small">2-week rotation active</p>  
</div>  
  
<div id="schedule"></div>  
  
<div class="card">  
<h3>Weight</h3>  
<input id="weight" placeholder="Enter weight">  
<button onclick="saveWeight()">Save</button>  
</div>  
  
<div class="card">  
<h3>Add Meal</h3>  
<input id="meal" placeholder="Extra meal">  
<button onclick="addMeal()">Add</button>  
<div id="meals"></div>  
</div>  
  
<div class="card">  
<h3>Peptide Log</h3>  
<button onclick="logPeptide()">Quick Log</button>  
<div id="log"></div>  
</div>  
  
<div class="card">  
<h3>Grocery List</h3>  
<ul>  
<li>Beef / Chuck Roast</li>  
<li>Chicken</li>  
<li>Eggs</li>  
<li>Rice / Oats / Tortillas</li>  
<li>Bone Broth / Tomato Sauce</li>  
<li>Onions / Jalapeños / Tomatoes</li>  
<li>Oranges / Apples</li>  
<li>Jerky / Almonds</li>  
<li>Electrolytes / Creatine / Magnesium</li>  
</ul>  
</div>  
  
</div>  
  
<script>  
  
// SAFE DATE CALCULATION (fixed error)  
let today = new Date();  
let start = new Date("2024-01-01");  
let diff = Math.floor((today - start) / (1000*60*60*24));  
let dayIndex = diff % 14;  
  
document.getElementById("day").innerText = dayIndex + 1;  
  
let schedules = [  
["5:30 AM Electrolytes","5:35 AM Peptides","6:00 Workout","7:15 Chile Verde","1:00 Enchiladas","7:00 Light Dinner","10:30 Peptides"],  
["5:30 AM Electrolytes","5:35 AM Peptides","6:00 Workout","7:15 Beef + Eggs","1:00 Chicken Bowl","7:00 Light Dinner","10:30 Peptides"]  
];  
  
let scheduleDiv = document.getElementById("schedule");  
  
schedules[dayIndex % 2].forEach(function(item){  
    let div = document.createElement("div");  
    div.className="card";  
    div.innerHTML = item + "<br><button onclick='done(this)'>Done</button>";  
    scheduleDiv.appendChild(div);  
});  
  
function done(btn){  
    btn.innerText="Done ✔";  
}  
  
function logPeptide(){  
    let time = new Date().toLocaleTimeString();  
    document.getElementById("log").innerHTML += "<br>"+time;  
}  
  
function saveWeight(){  
    let w = document.getElementById("weight").value;  
    localStorage.setItem("weight", w);  
    alert("Saved");  
}  
  
function addMeal(){  
    let meal = document.getElementById("meal").value;  
    document.getElementById("meals").innerHTML += "<br>"+meal;  
}  
  
</script>  
  
</body>  
</html>  
