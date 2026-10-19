# Tutuorial
Students choose their class, subject, chapters, and total marks. The app generates a practice paper, and they can attempt it, check answers, and revise weak topics. Let's make it easy now. 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#5146d8">
<title>PaperPal | Class 8</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f4f5ff;color:#22243a}
header{background:#5146d8;color:white;padding:24px 18px;text-align:center}
header h1{margin:0;font-size:30px}
header p{margin-bottom:0}
main{max-width:680px;margin:22px auto;padding:0 14px}
.card{background:white;padding:20px;border-radius:16px;margin-bottom:16px;box-shadow:0 4px 16px #20205010}
label{display:block;font-weight:bold;margin:12px 0 6px}
select,button{width:100%;padding:12px;border-radius:9px;font-size:16px}
select{border:1px solid #ccc;background:white}
button{border:0;background:#5146d8;color:white;font-weight:bold;cursor:pointer;margin-top:12px}
button:disabled{opacity:.6}
.question{padding:14px 0;border-bottom:1px solid #eee}
.question p{font-weight:bold}
.question label{font-weight:normal;display:flex;gap:8px;align-items:flex-start}
.question input{margin-top:4px}
#result{font-weight:bold;margin-top:16px}
footer{text-align:center;padding:20px;color:#666;font-size:13px}
</style>
</head>
<body>
<header>
  <h1>📘 PaperPal</h1>
  <p>Practice today. Improve tomorrow.</p>
  <p>Class 8 • Free practice quizzes</p>
</header>

<main>
  <section class="card">
    <h2>Find your practice paper</h2>
    <label for="board">Choose your board</label>
    <select id="board">
      <option>CBSE</option>
      <option>Karnataka State Board</option>
    </select>
    <label for="subject">Choose a subject</label>
    <select id="subject">
      <option>Mathematics</option>
      <option>Science</option>
      <option>Social Science</option>
    </select>
    <button onclick="startQuiz()">Start practice</button>
    <p id="notice" aria-live="polite"></p>
  </section>

  <section class="card" id="quiz" hidden>
    <h2 id="quizTitle">Practice quiz</h2>
    <p>Sample questions • 1 mark each</p>
    <div id="questions"></div>
    <button onclick="checkAnswers()">Check answers</button>
    <p id="result" aria-live="polite"></p>
    <button onclick="startQuiz()">Try again</button>
  </section>
</main>

<footer>
  PaperPal is an independent learning project.
  Verify questions against your current textbook.
</footer>

<script>
const bank = {
  Mathematics: [
    {q:"What is 3/4 expressed as a percentage?",
     a:["25%","50%","75%","80%"], correct:2},
    {q:"What is the square of 12?",
     a:["24","124","144","122"], correct:2},
    {q:"How many degrees are in a straight angle?",
     a:["90°","180°","270°","360°"], correct:1}
  ],
  Science: [
    {q:"Which organ pumps blood around the human body?",
     a:["Lungs","Heart","Kidneys","Stomach"], correct:1},
    {q:"Which gas do plants absorb during photosynthesis?",
     a:["Oxygen","Nitrogen","Carbon dioxide","Hydrogen"], correct:2},
    {q:"What is the SI unit of force?",
     a:["Joule","Watt","Newton","Metre"], correct:2}
  ],
  "Social Science": [
    {q:"What is a constitution?",
     a:["A country's basic set of laws and principles",
        "A type of mountain","A weather report","A trade route"], correct:0},
    {q:"Which is a renewable source of energy?",
     a:["Coal","Petroleum","Solar energy","Natural gas"], correct:2},
    {q:"What does a map scale help us determine?",
     a:["Population only","Distance on the ground",
        "Temperature","Rainfall only"], correct:1}
  ]
};

function startQuiz(){
  const board = document.getElementById("board").value;
  const subject = document.getElementById("subject").value;
  document.getElementById("quizTitle").textContent =
    "Class 8 " + subject;
  document.getElementById("notice").textContent =
    board + " selected. These are general sample questions, " +
    "not yet verified against this board's syllabus.";
  document.getElementById("result").textContent = "";
  document.getElementById("questions").innerHTML =
    bank[subject].map((item,i) =>
      '<div class="question"><p>' + (i+1) + '. ' +
      item.q + '</p>' +
      item.a.map((choice,j) =>
        '<label><input type="radio" name="q' + i +
        '" value="' + j + '"> ' + choice + '</label>'
      ).join("") + '</div>'
    ).join("");
  document.getElementById("quiz").hidden = false;
  document.getElementById("quiz").scrollIntoView({behavior:"smooth"});
}

function checkAnswers(){
  let score = 0;
  bank[document.getElementById("subject").value].forEach((q,i)=>{
    const selected = document.querySelector(
      'input[name="q'+i+'"]:checked'
    );
    if(selected && Number(selected.value) === q.correct) score++;
  });
  document.getElementById("result").textContent =
    "Your score: " + score + " / 3. Keep practising!";
}
</script>
</body>
</html>

