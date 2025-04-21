<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Angels in the Dark</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>Angels in the Dark</h1>
        <button id="menuToggle">☰ Menu</button>
    </header>

    <div id="sidebar">
        <h2>Emergency Contacts</h2>
        <div id="emergencyContacts"></div>

        <h2>Self-Defense Tips</h2>
        <div id="selfDefense"></div>
    </div>

    <main>
        <button id="sosButton">🚨 Send SOS</button>
        <p id="location">Location: Not Available</p>

        <div class="hidden-options">
            <button id="openCalculator">Open Calculator</button>
            <button id="openNotepad">Open Notepad</button>
        </div>

        <h3>Check Safe Route</h3>
        <input type="text" id="startLocation" placeholder="Start Location">
        <input type="text" id="endLocation" placeholder="Destination">
        <button id="checkSafety">Check Route</button>
    </main>

    <script src="script.js"></script>
</body>
</html>
document.getElementById('sosButton').addEventListener('click', function() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(position => {
            let latitude = position.coords.latitude;
            let longitude = position.coords.longitude;
            document.getElementById('location').innerText = `Location: ${latitude}, ${longitude}`;
            alert(`🚨 SOS Sent! Location: ${latitude}, ${longitude}`);
        }, () => alert('Unable to fetch location.'));
    } else {
        alert('Geolocation is not supported by this browser.');
    }
});

// Voice-Activated SOS (Say "Help me")
window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
const recognition = new SpeechRecognition();
recognition.continuous = true;
recognition.onresult = function(event) {
    let transcript = event.results[event.results.length - 1][0].transcript.toLowerCase();
    if (transcript.includes("help me")) {
        document.getElementById('sosButton').click();
    }
};
recognition.start();

// Sidebar Toggle
document.getElementById('menuToggle').addEventListener('click', function() {
    document.getElementById('sidebar').classList.toggle('active');
});

// Emergency Contacts
const emergencyContacts = {
    'Police': '112',
    'Ambulance': '100',
    'Women Helpline': '1091',
    'Child Helpline': '1098'
};

document.getElementById('emergencyContacts').innerHTML = Object.keys(emergencyContacts).map(contact => 
    `<p>${contact}: <a href="tel:${emergencyContacts[contact]}">${emergencyContacts[contact]}</a></p>`
).join('');

// Self-Defense Techniques
const selfDefenseTips = [
    'Aim for vulnerable spots like eyes, nose, throat, and groin.',
    'Use your keys as a weapon in case of emergency.',
    'Always be aware of your surroundings and trust your instincts.',
    'Carry a whistle or pepper spray for protection.',
    'Learn basic self-defense moves such as wrist escapes and palm strikes.'
];

document.getElementById('selfDefense').innerHTML = selfDefenseTips.map(tip => `<p>• ${tip}</p>`).join('');
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&display=swap');

body {
    background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
    color: #ffffff;
    font-family: 'Orbitron', sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
}

header {
    background: rgba(0, 0, 0, 0.8);
    padding: 15px;
    font-size: 24px;
    text-transform: uppercase;
    letter-spacing: 2px;
}

button {
    background: #ff007f;
    color: #ffffff;
    border: none;
    padding: 15px;
    font-size: 18px;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #ff3399;
    box-shadow: 0px 0px 10px #ff3399;
}

#sosButton {
    background: red;
    font-size: 20px;
    animation: pulse 1.5s infinite;
}

@keyframes pulse {
    0% { box-shadow: 0 0 10px red; }
    50% { box-shadow: 0 0 20px red; }
    100% { box-shadow: 0 0 10px red; }
}

#sidebar {
    position: fixed;
    left: -250px;
    top: 0;
    width: 250px;
    height: 100%;
    background: rgba(0, 0, 0, 0.9);
    transition: 0.5s;
    padding: 20px;
}

#sidebar.active {
    left: 0;
}

h2 {
    color: #00ffff;
}

.hidden-options {
    margin-top: 20px;
}

input {
    padding: 10px;
    margin: 5px;
    border-radius: 5px;
}

#menuToggle {
    position: absolute;
    top: 20px;
    left: 20px;
}

