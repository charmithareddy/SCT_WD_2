# SCT_WD_2
stop watch web application
let startTime = 0;
let elapsedTime = 0;
let intervalId = null;
let isRunning = false;

const display = document.getElementById("display");
const lapsList = document.getElementById("laps");

function formatTime(time) {
  const minutes = Math.floor(time / 60000);
  const seconds = Math.floor((time % 60000) / 1000);
  const milliseconds = Math.floor((time % 1000) / 10);

  return (
    String(minutes).padStart(2, "0") + ":" +
    String(seconds).padStart(2, "0") + ":" +
    String(milliseconds).padStart(2, "0")
  );
}

function start() {
  if (!isRunning) {
    isRunning = true;
    startTime = Date.now() - elapsedTime;

    intervalId = setInterval(() => {
      elapsedTime = Date.now() - startTime;
      display.textContent = formatTime(elapsedTime);
    }, 10);
  }
}

function pause() {
  if (isRunning) {
    clearInterval(intervalId);
    isRunning = false;
  }
}

function reset() {
  clearInterval(intervalId);
  isRunning = false;
  elapsedTime = 0;
  display.textContent = "00:00:00";
  lapsList.innerHTML = "";
}

function lap() {
  if (isRunning) {
    const lapItem = document.createElement("li");
    lapItem.textContent = display.textContent;
    lapsList.appendChild(lapItem);
  }
}
