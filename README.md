<!DOCTYPE html>
<html>

<head>

<meta charset="UTF-8">
<title>Wound Care EMR</title>

<style>

body{
font-family:Arial;
margin:0;
background:#f4f6fa;
}

.navbar{
background:#1f3a5f;
color:white;
padding:15px 30px;
display:flex;
justify-content:space-between;
}

.menu a{
color:white;
margin-left:20px;
cursor:pointer;
text-decoration:none;
}

.container{
padding:30px;
}

.card{
background:white;
padding:25px;
border-radius:8px;
box-shadow:0 2px 10px rgba(0,0,0,0.1);
margin-bottom:25px;
}

input,select{
width:100%;
padding:10px;
margin:6px 0;
border:1px solid #ccc;
border-radius:5px;
}

button{
background:#1f3a5f;
color:white;
border:none;
padding:10px 15px;
border-radius:5px;
cursor:pointer;
}

button:disabled{
background:#999;
}

table{
width:100%;
border-collapse:collapse;
}

th,td{
padding:10px;
border-bottom:1px solid #ddd;
text-align:left;
}

.section{
display:none;
}

.active{
display:block;
}

#loadingBar{
width:0%;
height:4px;
background:#1f3a5f;
transition:width 0.4s;
}

</style>

</head>


<body>


<div id="loadingBar"></div>


<div class="navbar">

<div>
<b>Wound Care EMR</b><br>
<small>Ns. Oki Hartono, S.Tr.Kep., CCWC</small>
</div>

<div class="menu">
<a onclick="showSection('dashboard')">Dashboard</a>
<a onclick="showSection('patients')">Patients</a>
</div>

</div>



<div class="container">


<div id="dashboard" class="section active">

<div class="card">

<h2>Dashboard</h2>

Total Patients :
<b id="totalPatients">0</b>

</div>

</div>



<div id="patients" class="section">


<div class="card">

<h2>Add Patient</h2>

<form id="patientForm">

<input id="Name" placeholder="Patient Name" required>

<input id="Date_of_Birth" type="date" required>

<select id="Gender" required>
<option value="">Gender</option>
<option>Male</option>
<option>Female</option>
</select>

<input id="Address" placeholder="Address">

<input id="Phone" placeholder="Phone">

<button id="saveBtn">Save Patient</button>

</form>

</div>



<div class="card">

<h2>Patient Database</h2>

<table id="patientTable">

<thead>

<tr>
<th>MRN</th>
<th>Name</th>
<th>Date of Birth</th>
<th>Gender</th>
<th>Address</th>
<th>Phone</th>
</tr>

</thead>

<tbody></tbody>

</table>

</div>

</div>

</div>



<script>

const API="https://script.google.com/macros/s/AKfycbx_Vcuo_p7fSYCrBIMkztQgYtk9norBOzvE8etwGkhfIjvcuaHtuGLGjMOrdaFFuhEQ/exec";



function loadingStart(){

document.getElementById("loadingBar").style.width="60%";

}



function loadingFinish(){

document.getElementById("loadingBar").style.width="100%";

setTimeout(()=>{
document.getElementById("loadingBar").style.width="0%";
},400);

}



function showSection(id){

document.querySelectorAll(".section").forEach(sec=>{
sec.classList.remove("active");
});

document.getElementById(id).classList.add("active");

}



function generateMRN(total){

let num=total+1;

return "GV"+num.toString().padStart(3,"0");

}



function loadPatients(){

loadingStart();

fetch(API)

.then(res=>res.json())

.then(data=>{

let table=document.querySelector("#patientTable tbody");

table.innerHTML="";

data.slice(1).forEach(row=>{

let tr=document.createElement("tr");

row.forEach(cell=>{

let td=document.createElement("td");

td.innerText=cell;

tr.appendChild(td);

});

table.appendChild(tr);

});

document.getElementById("totalPatients").innerText=data.length-1;

loadingFinish();

});

}



document.getElementById("patientForm").addEventListener("submit",function(e){

e.preventDefault();

loadingStart();

fetch(API)

.then(res=>res.json())

.then(data=>{

let MRN=generateMRN(data.length-1);

let patient={

MRN:MRN,
Name:document.getElementById("Name").value,
Date_of_Birth:document.getElementById("Date_of_Birth").value,
Gender:document.getElementById("Gender").value,
Address:document.getElementById("Address").value,
Phone:document.getElementById("Phone").value

};

fetch(API,{
method:"POST",
body:new URLSearchParams(patient)
})

.then(res=>res.text())

.then(()=>{

document.getElementById("patientForm").reset();

loadPatients();

});

});

});



window.onload=function(){

loadPatients();

setInterval(loadPatients,5000);

}

</script>

</body>
</html>
