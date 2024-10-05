<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stop-Watch</title>
</head>
<body>
    <div class="container">
        <label id="time-display">00:00:00</label>
        <div class="controls">
            <button id="start-stop">Start</button>
            <button id="lap-reset">Lap</button>
        </div>
        <ul id="lap-list"></ul>
    </div>
    <script>
let timerInterval;
let elapsedTime = 0; 
let isRunning = false;
const timeDisplay = document.getElementById("time-display");
const startStopBtn = document.getElementById("start-stop");
const lapResetBtn = document.getElementById("lap-reset");
const lapList = document.getElementById("lap-list");
function formatTime(ms) {
  let totalSeconds = Math.floor(ms / 1000);
  let minutes = Math.floor(totalSeconds / 60);
  let seconds = totalSeconds % 60;
  let milliseconds = Math.floor((ms % 1000) / 10);
  return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}:${String(milliseconds).padStart(2, '0')}`;
}
function updateTime() {
  timeDisplay.innerText = formatTime(elapsedTime);
}
startStopBtn.addEventListener("click", function() {
  if (isRunning) {
    clearInterval(timerInterval);
    startStopBtn.innerText = "Start";
    startStopBtn.classList.remove("stop");
    lapResetBtn.innerText = "Reset"; 
    isRunning = false;
  } 
  else {
      let startTime = Date.now() - elapsedTime;
    timerInterval = setInterval(function() {
      elapsedTime = Date.now() - startTime;
      updateTime();
    }, 10);
    startStopBtn.innerText = "Stop";
    startStopBtn.classList.add("stop");
    lapResetBtn.innerText = "Lap"; 
    isRunning = true;
  }
});
lapResetBtn.addEventListener("click", function() {
  if (isRunning) {
    const lapTime = document.createElement("li");
    lapTime.innerText = formatTime(elapsedTime);
    lapList.prepend(lapTime); 
  } 
  else {
    elapsedTime = 0;
    updateTime();
    lapList.innerHTML = ""; 
    lapResetBtn.innerText = "Lap"; 
  }
});
</script>
</body>
</html>
