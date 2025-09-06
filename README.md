# saurbh_1
this html code
program code:
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Attendance (Small)</title>
  <style>
    body{font-family:system-ui,Arial;margin:20px;background:#f8fafc}
    input,button{padding:6px 8px;margin-right:6px}
    table{width:100%;border-collapse:collapse;margin-top:10px}
    th,td{padding:6px;border:1px solid #e6eef6;text-align:left}
    .p{color:#065f46;font-weight:600}
    .a{color:#7f1d1d;font-weight:600}
  </style>
</head>
<body>
  <h3>Simple Attendance</h3>
  <input id="name" placeholder="Student name">
  <button id="add">Add</button>
  <button id="save">Save</button>
  <button id="load">Load</button>

  <table>
    <thead><tr><th>#</th><th>Name</th><th>Status</th></tr></thead>
    <tbody id="list"></tbody>
  </table>

<script>
  const listEl = document.getElementById('list');
  let students = [];
  function render(){
    listEl.innerHTML='';
    students.forEach((s,i)=>{
      const tr = document.createElement('tr');
      tr.innerHTML = `<td>${i+1}</td><td>${s.name}</td><td><button data-i="${i}">${s.status}</button></td>`;
      listEl.appendChild(tr);
    });
    listEl.querySelectorAll('button[data-i]').forEach(b=> b.addEventListener('click', e=>{
      const i = +e.target.dataset.i;
      students[i].status = students[i].status === 'Present' ? 'Absent' : 'Present';
      render();
    }));
  }
  document.getElementById('add').addEventListener('click', ()=>{
    const name = document.getElementById('name').value.trim(); if(!name) return;
    students.push({name, status:'Absent'}); document.getElementById('name').value=''; render();
  });
  document.getElementById('save').addEventListener('click', ()=>{
    localStorage.setItem('att_small', JSON.stringify(students)); alert('Saved');
  });
  document.getElementById('load').addEventListener('click', ()=>{
    const raw = localStorage.getItem('att_small'); if(raw) students = JSON.parse(raw); render();
  });
  // init
  render();
</script>
</body>
</html>
