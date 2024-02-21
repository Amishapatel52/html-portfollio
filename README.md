<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer</title>
</head>
<style>
    body {
        padding: 0;
        margin: 0;
        font-family: verdana;
    }

    #timeDisplay {
        font-size: 100px;
        text-align: center;
        height: 150px;
    }

    .timeContainer {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100vh;
        background-color: rgb(0, 61, 0);
        color: white;
    }

    h1 {
        color: rgb(10, 238, 10);
        text-align: center;
    }

    .timerBtn {
        width: 100px;
        padding: 10px 15px;
        margin: 0px 20px;
        border-top-right-radius: 10px;
        border-bottom-left-radius: 10px;
        border-bottom-right-radius: 4px;
        border-top-left-radius: 4px;
        cursor: pointer;
        font-size: 20px;
        transition: 0.5s;
        color: white;
        font-weight: 500;
    }

    #startBtn {
        background-color: #009779;
    }

    #pauseBtn {
        background-color: #0e85fc;
    }

    #resetBtn {
        background-color: #c91400;
    }
</style>

<body>
    <div class="timeContainer">
        <h1>Stop Watch</h1>
        <div id="timeDisplay">00:00:00</div>
        <div class="container">
            <button class="timerBtn" id="startBtn">Start</button>
            <button class="timerBtn" id="pauseBtn">Pause</button>
            <button class="timerBtn" id="resetBtn">Reset</button>
        </div>
    </div>

    <script>
      const timeDisplay = document.querySelector("#timeDisplay");
const startBtn = document.querySelector("#startBtn");
const pauseBtn = document.querySelector("#pauseBtn");
const resetBtn = document.querySelector("#resetBtn");

let startTime = 0;
let elapsedTime = 0;
let currentTime = 0;
let paused = true;
let intervalId; // Timer ID to control the timer interval.
let hrs = 0;
let mins = 0;
let secs = 0;


// When the start button is clicked, it starts the timer
startBtn.addEventListener("click", () => {
    if (paused) {
        paused = false;
        startTime = Date.now() - elapsedTime;
        intervalId = setInterval(updateTime,1000); //  setInterval function and continuously updates the displayed time
    }
});

pauseBtn.addEventListener("click", () => {
    if (!paused) {
        paused = true;
        elapsedTime = Date.now() - startTime;
        clearInterval(intervalId); // clears the interval using clearInterval() by passing the interval id 
    }
});

// the reset button clears the time and resets all relevant variables
resetBtn.addEventListener("click", () => {
    paused = true;
    clearInterval(intervalId);
    elapsedTime = 0;
    startTime = 0;
    currentTime = 0;
    hrs = 0;
    mins = 0;
    secs = 0;
    timeDisplay.textContent = "00:00:00";
});

// updateTime function calculates the elapsed time
function updateTime() {
    elapsedTime = Date.now() - startTime; // difference between the current time and the start time

    // Calculate hours/minutes/seconds
    hrs = Math.floor((elapsedTime / (1000 * 60 * 60)) % 24);
    mins = Math.floor((elapsedTime / (1000 * 60)) % 60);
    secs = Math.floor((elapsedTime / 1000) % 60);

    // pad function adds leading zeros to single-digit hour/minute/second values for time display
    hrs = pad(hrs);
    mins = pad(mins);
    secs = pad(secs);

    timeDisplay.textContent = `${hrs}:${mins}:${secs}`;

    // these variables to ensure they are always at least two characters long
    function pad(unit) {
        return (("0") + unit).length > 2 ? unit : "0" + unit;
    }

    // document.getElementById('timeDisplay').value = '';
}
    </script>

</body>

</html>
