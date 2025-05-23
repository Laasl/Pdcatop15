<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<title>Gestionnaire de tâches</title>
<style>
body {
font-family: Arial, sans-serif;
font-size: 18px;
line-height: 1.6;
padding: 20px;
background-color: #f5f5f5;
}
h2 {
margin-top: 40px;
}
form input, form button {
font-size: 18px;
padding: 10px;
margin: 5px 0;
width: 100%;
box-sizing: border-box;
}
.task {
border-radius: 10px;
border: 1px solid #ccc;
padding: 20px;
margin: 15px 0;
cursor: pointer;
transition: background-color 0.3s ease;
}
.task.non-commence {
background-color: #ffffff;
}
.task.en-cours {
background-color: #ffe4b3;
}
.task.termine {
background-color: #e0ffe0;
text-decoration: line-through;
}
.description {
font-size: 20px;
margin: 10px 0;
}
button {
padding: 12px 20px;
font-size: 18px;
margin-top: 10px;
}
</style>
</head>
<body>
<h2>Ajouter une tâche</h2>
<form id="taskForm">
<input type="text" id="title" placeholder="Titre" required><br>
<textarea id="description" placeholder="Description" required style="width:100%; height:80px; font-size:18px;"></textarea><br>
<input type="date" id="startDate" required>
<input type="date" id="endDate" required><br>
<button type="submit">Ajouter</button>
</form>

<h2>Liste des tâches</h2>
<div id="taskList"></div>
<button onclick="deleteCompleted()">Supprimer les tâches terminées</button>

<script>
const taskList = [];

document.getElementById('taskForm').addEventListener('submit', function(e) {
e.preventDefault();
const title = document.getElementById('title').value;
const desc = document.getElementById('description').value;
const start = document.getElementById('startDate').value;
const end = document.getElementById('endDate').value;
taskList.push({ title, desc, start, end, status: 'Non commencé' });
this.reset();
renderTasks();
});

function renderTasks() {
const container = document.getElementById('taskList');
container.innerHTML = '';
taskList.forEach((task, index) => {
const div = document.createElement('div');
const statusClass = task.status === 'Non commencé' ? 'non-commence'
: task.status === 'En cours' ? 'en-cours'
: 'termine';
div.className = `task ${statusClass}`;
div.innerHTML = `
<strong>${task.title}</strong><br>
<div class="description">${task.desc}</div>
