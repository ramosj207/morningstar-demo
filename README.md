# morningstar-demo

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>MorningStar | Mission Control</title>
<style>
:root {
  --bg: #0b1220;
  --panel: #172337;
  --border: #2b3a51;
  --text: #f2f6fc;
  --muted: #9aacc3;
  --gold: #f5bc61;
  --green: #7de0b2;
}
* { box-sizing: border-box; }
body {
  margin: 0;
  background: var(--bg);
  color: var(--text);
  font-family: -apple-system, BlinkMacSystemFont,
    "Segoe UI", sans-serif;
}
.container {
  max-width: 1100px;
  margin: auto;
  padding: 24px;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
  flex-wrap: wrap;
  padding: 16px 0 28px;
  border-bottom: 1px solid var(--border);
}
.logo { font-size: 23px; font-weight: 800; }
.logo span { color: var(--gold); }
.badge {
  background: #17382f;
  color: var(--green);
  padding: 8px 13px;
  border-radius: 30px;
  font-size: 12px;
}
h1 { font-size: clamp(28px, 5vw, 42px); }
h2 { font-size: 20px; }
p { color: var(--muted); }
.hero {
  margin: 30px 0;
  padding: 28px;
  border-radius: 16px;
  background: linear-gradient(120deg,
    #294766, #182a40);
  border: 1px solid #3b5974;
}
.hero h2 { font-size: 27px; margin: 12px 0; }
.eyebrow {
  color: var(--gold);
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1.5px;
}
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
  margin: 18px 0 35px;
}
.card, .task, .health {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 13px;
  padding: 20px;
}
.card { min-height: 150px; }
.card .emoji { font-size: 30px; }
.card h3 { margin: 12px 0 5px; }
.status { color: var(--green); font-size: 13px; }
.task {
  display: flex;
  align-items: center;
  gap: 15px;
  margin-bottom: 10px;
}
.task-number {
  color: var(--gold);
  font-weight: bold;
}
.task-info { flex: 1; }
.task-info strong { display: block; }
.task-info small { color: var(--muted); }
button {
  border: 1px solid #45617f;
  background: #2a4261;
  color: white;
  border-radius: 9px;
  padding: 10px 14px;
  cursor: pointer;
}
button:hover { background: #3b5879; }
.completed { opacity: .5; }
.completed strong { text-decoration: line-through; }
.health { margin-top: 35px; }
footer {
  margin: 35px 0;
  color: var(--muted);
  font-size: 12px;
}
@media(max-width: 750px) {
  .grid { grid-template-columns: repeat(2, 1fr); }
  .container { padding: 18px; }
}
</style>
</head>
<body>
<div class="container">

<header>
  <div class="logo"><span>✺</span> MORNINGSTAR</div>
  <div class="badge">● DEMO MODE</div>
</header>

<h1>Mission Control</h1>
<p>Your priorities. Your systems. One dashboard.</p>

<section class="hero">
  <div class="eyebrow">NEXT BEST ACTION</div>
  <h2 id="nextAction">Review career opportunities</h2>
  <p>Know exactly what to focus on next.</p>
</section>

<section>
  <h2>Priority Actions</h2>
  <div id="taskList"></div>
</section>

<section>
  <h2>Operating Systems</h2>
  <div class="grid">
    <div class="card">
      <div class="emoji">💼</div>
      <h3>Career OS</h3>
      <div class="status">● Demo Ready</div>
    </div>
    <div class="card">
      <div class="emoji">💰</div>
      <h3>Finance OS</h3>
      <div class="status">● Demo Ready</div>
    </div>
    <div class="card">
      <div class="emoji">⚖️</div>
      <h3>Legal OS</h3>
      <div class="status">● Demo Ready</div>
    </div>
    <div class="card">
      <div class="emoji">🏠</div>
      <h3>Asset OS</h3>
      <div class="status">● Demo Ready</div>
    </div>
  </div>
</section>

<section class="health">
  <div class="eyebrow">SYSTEM HEALTH</div>
  <h2>Interface Operational</h2>
  <p>
    Static demo running successfully.
    No live integrations or personal data.
  </p>
  <button onclick="resetTasks()">Reset Demo</button>
</section>

<footer>
  MorningStar v1.0 | Sample Data Only |
  Built with ChatGPT
</footer>

</div>

<script>
const tasks = [
  {
    title: "Review career opportunities",
    detail: "Career OS · High Priority"
  },
  {
    title: "Review legal follow-up",
    detail: "Legal OS · Sample Update"
  },
  {
    title: "Check property milestones",
    detail: "Asset OS · Sample Update"
  }
];

const completed = new Set();

function renderTasks() {
  const list = document.getElementById("taskList");
  list.innerHTML = "";

  tasks.forEach((task, index) => {
    const item = document.createElement("div");
    item.className = "task";

    if (completed.has(index)) {
      item.classList.add("completed");
    }

    const number = document.createElement("span");
    number.className = "task-number";
    number.textContent = String(index + 1).padStart(2, "0");

    const info = document.createElement("div");
    info.className = "task-info";

    const title = document.createElement("strong");
    title.textContent = task.title;

    const detail = document.createElement("small");
    detail.textContent = task.detail;

    info.append(title, detail);

    const button = document.createElement("button");
    button.textContent = completed.has(index)
      ? "Undo"
      : "Done";

    button.addEventListener("click", () => {
      if (completed.has(index)) {
        completed.delete(index);
      } else {
        completed.add(index);
      }
      renderTasks();
    });

    item.append(number, info, button);
    list.appendChild(item);
  });

  const next = tasks.find((_, i) => !completed.has(i));

  document.getElementById("nextAction").textContent =
    next ? next.title : "All sample tasks completed!";
}

function resetTasks() {
  completed.clear();
  renderTasks();
}

renderTasks();
</script>
</body>
</html>
