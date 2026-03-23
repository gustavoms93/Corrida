<script>
const canvas = document.getElementById("gameCanvas");
const ctx = canvas.getContext("2d");

let gameActive = false, score = 0, speed = 7, fuel = 100, coins = 0;
let enemies = [], items = [], scenery = [], raf, isAccelerating = false;
let player = { lane: 1, x: 0, y: 0, w: 50, h: 85, targetX: 0 };

function resize() {
    canvas.width = Math.min(window.innerWidth, 450);
    canvas.height = window.innerHeight;
    player.y = canvas.height - 200;
    updateTargetX();
}
window.addEventListener('resize', resize);
resize();

// --- CONTROLES DE TECLADO (MELHORIA PC) ---
window.addEventListener("keydown", (e) => {
    if(!gameActive) return;
    if(["ArrowLeft", "ArrowRight", "ArrowUp", " ", "ArrowDown"].includes(e.key)) e.preventDefault(); // Evita scroll

    if(e.key === "ArrowLeft") movePlayer(-1);
    if(e.key === "ArrowRight") movePlayer(1);
    if(e.key === "ArrowUp" || e.key === " ") isAccelerating = true;
});

window.addEventListener("keyup", (e) => {
    if(e.key === "ArrowUp" || e.key === " ") isAccelerating = false;
});

// Eventos do Pedal (Mantido para Mobile/Mouse)
const gasPedal = document.getElementById("gas-pedal");
gasPedal.addEventListener("pointerdown", () => isAccelerating = true);
gasPedal.addEventListener("pointerup", () => isAccelerating = false);
gasPedal.addEventListener("pointerleave", () => isAccelerating = false);

// COMPARTILHAMENTO PERSONALIZADO v10.7
async function shareChallenge() {
    const gameUrl = "https://gustavoms93.github.io/Corrida/";
    const shareText = `🔥 DESAFIO ASPHALT ESCAPE 🔥\n\nFiz ${Math.floor(score)} pontos na rodovia… 🚗💨\nVocê consegue bater esse recorde? 😏\n\nEntre no jogo, acelere ao máximo e tente sobreviver ao tráfego!\n\n🎮 JOGUE AGORA:\n${gameUrl}\n\nCriado por Gustavo Moreira:`;

    if (navigator.share) {
        try { await navigator.share({ title: 'Asphalt Escape', text: shareText }); } catch (err) {}
    } else {
        window.open(`https://api.whatsapp.com/send?text=${encodeURIComponent(shareText)}`);
    }
}

function revive() {
    if(coins >= 300) {
        coins -= 300; document.getElementById("coin-txt").innerText = coins;
        fuel = 100; enemies = [];
        document.getElementById("menu-over").style.display = "none";
        document.getElementById("ui").style.display = "flex";
        gameActive = true; update();
    }
}

function loadRanking() {
    const ranks = JSON.parse(localStorage.getItem('gms_ranks') || "[]");
    document.getElementById("ranking-list").innerHTML = ranks.slice(0, 5).map((s, i) => `<li>${i+1}º - ${s} pts</li>`).join("");
}
loadRanking();

function updateTargetX() { player.targetX = (player.lane * (canvas.width / 3)) + (canvas.width / 6) - (player.w / 2); }
function movePlayer(dir) { if(!gameActive) return; player.lane = Math.max(0, Math.min(2, player.lane + dir)); updateTargetX(); }

function initGame() {
    score = 0; speed = 7; fuel = 100; coins = 0; enemies = []; items = []; scenery = []; isAccelerating = false;
    player.lane = 1; updateTargetX(); player.x = player.targetX;
    document.getElementById("coin-txt").innerText = "0";
    document.getElementById("menu-main").style.display = "none";
    document.getElementById("menu-over").style.display = "none";
    document.getElementById("ui").style.display = "flex";
    document.getElementById("game-ctrls").style.display = "flex";
    gameActive = true;
    if(raf) cancelAnimationFrame(raf);
    update();
}

function drawVehicle(v) {
    ctx.fillStyle = v.color || "#444";
    ctx.beginPath(); ctx.roundRect(v.x, v.y, v.w, v.h, 8); ctx.fill();
    if(v.isEasterEgg) {
        ctx.fillStyle = "white"; ctx.font = "bold 12px Arial";
        ctx.save(); ctx.translate(v.x+v.w-5, v.y+v.h-15); ctx.rotate(-Math.PI/2);
        ctx.fillText("GMS FLORESTAL", 0, 0); ctx.restore();
    }
    ctx.fillStyle = "rgba(0,0,0,0.5)"; ctx.fillRect(v.x+8, v.y+10, v.w-16, 22);
}

function update() {
    if(!gameActive) return;
    ctx.fillStyle = "#222"; ctx.fillRect(0,0,canvas.width, canvas.height);
    
    if(Math.random() < 0.05) scenery.push({ x: Math.random() < 0.5 ? 5 : canvas.width - 25, y: -50, type: Math.random() > 0.5 ? '🌵' : '🌳' });
    scenery.forEach((s, i) => {
        s.y += speed; ctx.font = "20px Arial"; ctx.fillText(s.type, s.x, s.y);
        if(s.y > canvas.height) scenery.splice(i, 1);
    });

    ctx.strokeStyle = "rgba(255,255,255,0.2)"; ctx.setLineDash([40, 60]);
    ctx.lineDashOffset = -(score * 10);
    for(let i=1; i<3; i++) {
        ctx.beginPath(); ctx.moveTo(i*(canvas.width/3), 0); ctx.lineTo(i*(canvas.width/3), canvas.height); ctx.stroke();
    }

    player.x += (player.targetX - player.x) * 0.25; // Suavização um pouco mais rápida no PC
    drawVehicle({...player, color: "#e74c3c"});

    if(Math.random() < 0.03) items.push({ type: Math.random() > 0.8 ? 'gas' : 'coin', x: (Math.floor(Math.random()*3) * (canvas.width/3)) + (canvas.width/6), y: -50 });
    items.forEach((it, i) => {
        it.y += speed; ctx.font = "20px Arial"; ctx.fillText(it.type === 'coin' ? '🪙' : '⛽', it.x-10, it.y);
        if(Math.hypot(player.x+25 - it.x, player.y+40 - it.y) < 40) {
            if(it.type === 'coin') { coins += 10; document.getElementById("coin-txt").innerText = coins; }
            else fuel = Math.min(100, fuel + 35);
            items.splice(i, 1);
        }
    });

    if(Math.random() < 0.02 + (score/100000)) {
        let lane = Math.floor(Math.random()*3);
        let topEnemies = enemies.filter(e => e.y < 350);
        if(!enemies.some(e => e.lane === lane && e.y < 450) && topEnemies.length < 2) {
            let isEE = Math.random() < 0.02;
            enemies.push({
                lane, x: (lane * (canvas.width / 3)) + (canvas.width / 6) - 25,
                y: -200, w: 50, h: isEE ? 160 : 85,
                color: isEE ? "#1b5e20" : "#2980b9", isEasterEgg: isEE, speed: 2 + Math.random()*2, done: false
            });
        }
    }

    enemies.forEach((e, i) => {
        e.y += e.speed + (speed * 0.4); drawVehicle(e);
        if(player.x+10 < e.x+e.w-10 && player.x+player.w-10 > e.x+10 && player.y+10 < e.y+e.h-10 && player.y+player.h-10 > e.y+10) {
            gameActive = false; gameOver();
        }
        if(e.isEasterEgg && e.y > player.y && !e.done) {
            score += 50; e.done = true;
            const msg = document.getElementById("msg-box");
            msg.style.display = "block";
            setTimeout(() => { msg.style.display = "none"; }, 3000);
        }
        if(e.y > canvas.height) enemies.splice(i, 1);
    });

    if(gameActive) {
        let accel = isAccelerating ? 2 : 1;
        score += 1 * accel;
        fuel -= 0.035 * accel;
        speed = (7 + (score/6000)) * (isAccelerating ? 1.4 : 1);
        document.getElementById("fuel-fill").style.width = fuel + "%";
        document.getElementById("score-txt").innerText = Math.floor(score);
        document.getElementById("km-txt").innerText = Math.floor(speed * 15) + " KM/H";
        if(fuel <= 0) { gameActive = false; gameOver(); }
    }
    raf = requestAnimationFrame(update);
}

function gameOver() {
    document.getElementById("menu-over").style.display = "flex";
    document.getElementById("final-score-val").innerText = Math.floor(score);
    let ranks = JSON.parse(localStorage.getItem('gms_ranks') || "[]");
    ranks.push(Math.floor(score)); ranks.sort((a,b) => b-a);
    localStorage.setItem('gms_ranks', JSON.stringify(ranks.slice(0, 10)));
    loadRanking();
    document.getElementById("btn-revive").style.display = (coins >= 300) ? "block" : "none";
}
</script>
