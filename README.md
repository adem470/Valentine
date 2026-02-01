# Valentine
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Be My Valentine?</title>

<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background: #ffd6e0;
        height: 100vh;
        overflow: hidden;
        display: flex;
        justify-content: center;
        align-items: center;
        text-align: center;
    }

    .box {
        background: white;
        padding: 40px;
        border-radius: 20px;
        box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        position: relative;
        z-index: 2;
    }

    h1 { color: #ff4d88; }

    button {
        padding: 12px 25px;
        font-size: 18px;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        margin: 10px;
    }

    #yesBtn { background: #ff4d88; color: white; }
    #noBtn {
        background: #aaa;
        color: white;
        position: absolute;
    }

    #bear {
        display: none;
        margin-top: 20px;
        animation: pop 0.5s ease;
    }

    #bear img { width: 180px; margin-top: 10px; }

    @keyframes pop {
        from { transform: scale(0); }
        to { transform: scale(1); }
    }

    .heart {
        position: absolute;
        bottom: -20px;
        font-size: 20px;
        animation: floatUp 6s linear infinite;
        z-index: 1;
    }

    @keyframes floatUp {
        0% { transform: translateY(0) scale(1); opacity: 1; }
        100% { transform: translateY(-110vh) scale(1.5); opacity: 0; }
    }
</style>
</head>

<body>

<!-- 🎵 Background Music -->
<audio id="music" loop>
  <source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_5c3a1b87b7.mp3" type="audio/mp3">
</audio>

<div class="box" id="mainBox">
    <h1>Will you be my Valentine? 💖</h1>
    <button id="yesBtn">Yes 🥰</button>
    <button id="noBtn">No 😢</button>

    <div id="bear">
        <h2>YAY!!! You said YES 💕</h2>
        <img src="https://images.unsplash.com/photo-1601758123927-1969a0b7f6f1" alt="Teddy Bear">
    </div>
</div>

<script>
const noBtn = document.getElementById("noBtn");
const yesBtn = document.getElementById("yesBtn");
const bear = document.getElementById("bear");
const box = document.getElementById("mainBox");
const music = document.getElementById("music");

// Start music on first click (browser rule)
document.body.addEventListener("click", () => {
    music.play().catch(()=>{});
}, { once: true });

// Move NO button
function moveButton() {
    const boxRect = box.getBoundingClientRect();
    const maxX = boxRect.width - noBtn.offsetWidth;
    const maxY = boxRect.height - noBtn.offsetHeight;

    noBtn.style.left = Math.random() * maxX + "px";
    noBtn.style.top = Math.random() * maxY + "px";
}

noBtn.addEventListener("mouseover", moveButton);
noBtn.addEventListener("click", moveButton);

// YES button
yesBtn.addEventListener("click", () => {
    bear.style.display = "block";
    yesBtn.style.display = "none";
    noBtn.style.display = "none";
    document.querySelector("h1").textContent = "I knew it 😌💘";
});

// Floating hearts
function createHeart() {
    const heart = document.createElement("div");
    heart.classList.add("heart");
    heart.innerHTML = "💖";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = Math.random() * 20 + 15 + "px";
    heart.style.animationDuration = Math.random() * 3 + 3 + "s";
    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 6000);
}

setInterval(createHeart, 300);
</script>

</body>
</html>
