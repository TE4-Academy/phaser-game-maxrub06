# STEG-FÖR-STEG INSTRUKTIONER
JavaScript Phaser Basics - Upptäck och Lös Problem!

## Innan du börjar
1. Öppna `index.html` i webbläsaren
2. Öppna Developer Tools (F12) - Console-fliken
3. **Observera:** Du ser en blå fyrkant men kan inte röra dig, bara 2 mynt syns!

**Detta är meningen!** Du ska upptäcka och fixa problemen.

---

## PROBLEM 1: Spelaren rör sig inte! 🎮

**Testa:** Tryck på piltangenterna. Ingenting händer!

### Steg 1.1: Aktivera rörelse-funktionen
I `game.js`, i `update()`-funktionen, ta bort `//`:
```javascript
function update() {
    handlePlayerMovement();  // ← Ta bort // här!
    // updateDebug();        // Fixa senare
    // checkWinCondition();  // Fixa senare
}
```

### Steg 1.2: Skriv rörelse-funktionen
Ta bort `//` framför hela `handlePlayerMovement`-funktionen:
```javascript
function handlePlayerMovement() {
    // Nollställ hastighet
    player.body.setVelocity(0);
    
    // Kontrollera piltangenter
    if (cursors.left.isDown) {
        player.body.setVelocityX(-200);
    } else if (cursors.right.isDown) {
        player.body.setVelocityX(200);
    }
    
    if (cursors.up.isDown) {
        player.body.setVelocityY(-200);
    } else if (cursors.down.isDown) {
        player.body.setVelocityY(200);
    }
}
```

**Testa:** Nu ska spelaren röra sig med piltangenterna!

---

## PROBLEM 2: Spelaren försvinner utanför skärmen! 😱

**Testa:** Rör dig åt vänster länge. Spelaren försvinner!

### Steg 2.1: Aktivera world bounds
I `create()`-funktionen, ta bort `//`:
```javascript
// PROBLEM: Spelaren kan gå utanför skärmen!
player.body.setCollideWorldBounds(true);  // ← Ta bort // här!
```

**Testa:** Nu ska spelaren stanna vid kanten av skärmen!

---

## PROBLEM 3: Bara 2 mynt syns! 💰

**Observera:** Det ska finnas 5 mynt, men bara 2 syns.

### Steg 3.1: Lägg till fler mynt
I `create()`-funktionen, ta bort `//` framför de utkommenterade mynten:
```javascript
createCoin(this, 200, 150);
createCoin(this, 400, 300);
createCoin(this, 600, 200);  // ← Ta bort // här!
createCoin(this, 300, 450);  // ← Ta bort // här!
createCoin(this, 700, 400);  // ← Ta bort // här!
```

**Testa:** Nu ska 5 gula mynt synas på skärmen!

---

## PROBLEM 4: Kollision fungerar inte! 🤝

**Testa:** Rör dig över ett mynt. Ingenting händer!

### Steg 4.1: Aktivera kollisionsdetektering
I `create()`-funktionen, ta bort `//`:
```javascript
// PROBLEM: Kollision är inte uppsatt!
this.physics.add.overlap(player, coins, collectCoin, null, this);  // ← Ta bort // här!
```

### Steg 4.2: Skriv kollisions-funktionen
Ta bort `//` framför hela `collectCoin`-funktionen:
```javascript
function collectCoin(player, coin) {
    // Ta bort myntet
    coin.destroy();
    
    // Öka poäng
    score += 10;
    coinsCollected++;
    
    // Uppdatera UI
    updateScore();
    
    console.log('Mynt samlat! Poäng:', score);
}
```

### Steg 4.3: Skriv UI-uppdatering
Ta bort `//` framför `updateScore`-funktionen:
```javascript
function updateScore() {
    document.getElementById('score').textContent = score;
    document.getElementById('coins-left').textContent = (5 - coinsCollected);
}
```

**Testa:** Nu ska mynt försvinna när du rör dem och poängen ska öka!

---

## PROBLEM 5: Debug-info uppdateras inte! 🔍

### Steg 5.1: Aktivera debug-uppdatering
I `update()`-funktionen, ta bort `//`:
```javascript
function update() {
    handlePlayerMovement();
    updateDebug();          // ← Ta bort // här!
    // checkWinCondition();  // Fixa senare
}
```

**Testa:** Nu ska debug-området visa spelarens position och statistik!

---

## PROBLEM 6: Ingen win-condition! 🏆

**Testa:** Samla alla 5 mynt. Händer något speciellt? Nej!

### Steg 6.1: Skriv win-condition
Ta bort `//` framför `checkWinCondition`-funktionen:
```javascript
function checkWinCondition() {
    if (coinsCollected >= 5 && gameState === 'playing') {
        gameState = 'won';
        console.log('Du vann!');
        // Visa win-meddelande
        alert('Grattis! Du samlade alla mynt!');  // ← Ta bort // här också!
    }
}
```

### Steg 6.2: Aktivera win-check
I `update()`-funktionen, ta bort `//`:
```javascript
function update() {
    handlePlayerMovement();
    updateDebug();
    checkWinCondition();    // ← Ta bort // här!
}
```

**Testa:** Samla alla mynt - du ska få en gratulationsruta!

---

## PROBLEM 7: Appen ser tråkig ut! 🎨

### Steg 7.1: Förbättra CSS
I `style.css`, förbättra stylingen:

```css
body {
    margin: 20px;                    /* Istället för 10px */
    background-color: #f5f5f5;       /* Istället för white */
}

.container {
    padding: 30px;                   /* Istället för 10px */
    background-color: white;         /* Lägg till */
    border-radius: 10px;             /* Lägg till */
    box-shadow: 0 2px 10px rgba(0,0,0,0.1); /* Lägg till */
}

h1 {
    text-align: center;              /* Istället för left */
    color: #333;                     /* Istället för black */
    margin-bottom: 20px;             /* Istället för 10px */
}

canvas {
    border: 3px solid #333;          /* Lägg till */
    border-radius: 5px;              /* Lägg till */
}

.stats {
    padding: 15px;                   /* Istället för 5px */
    font-size: 18px;                 /* Istället för 12px */
    border-radius: 5px;              /* Lägg till */
}

.stats span {
    color: #007acc;                  /* Istället för black */
}
```

---

## UTMANING: Lägg till fler funktioner! 🚀

### Timer-funktionalitet
Lägg till en timer som räknar ner:
```javascript
let timeLeft = 30;  // 30 sekunder

// I create():
gameTimer = this.time.addEvent({
    delay: 1000,
    callback: updateTimer,
    callbackScope: this,
    loop: true
});

function updateTimer() {
    timeLeft--;
    document.getElementById('timer').textContent = timeLeft;
    
    if (timeLeft <= 0) {
        gameState = 'lost';
        alert('Tiden är slut!');
    }
}
```

### Ljud-effekter
Lägg till ljud när mynt samlas:
```javascript
// I preload():
this.load.audio('coinSound', 'path/to/coin-sound.mp3');

// I collectCoin():
this.sound.play('coinSound');
```

### Power-ups
Skapa speciella mynt som ger extra poäng:
```javascript
function createPowerUp(scene, x, y) {
    const powerUp = scene.add.star(x, y, 5, 10, 20, 0xff0000);  // Röd stjärna
    scene.physics.add.existing(powerUp);
    powerUps.add(powerUp);
}
```

### High Score
Spara bästa resultat i localStorage:
```javascript
function saveHighScore() {
    const currentHigh = localStorage.getItem('highScore') || 0;
    if (score > currentHigh) {
        localStorage.setItem('highScore', score);
        alert('Nytt rekord!');
    }
}
```

---

## Nästa Nivå: Spelutvecklingskoncept 🤔

### 🎯 **Game Design-principer:**
- **Feedback:** Spelaren ska alltid veta vad som händer (ljud, animationer, poäng)
- **Progression:** Blir spelet svårare? Fler mynt? Snabbare rörelse?
- **Replay-value:** Varför skulle någon spela igen? High scores? Olika levels?

### 🏗️ **Tekniska utmaningar:**
- **Levels:** Olika banor med olika utmaningar
- **Animations:** Roterande mynt, hoppande spelare
- **Particle effects:** Stjärnor när mynt samlas
- **Mobile support:** Touch-kontroller för telefon

### 📱 **Optimering:**
- **Performance:** Vad händer med 100 mynt på skärmen?
- **Memory:** Städas sprites bort ordentligt?
- **Loading:** Stora bilder vs små geometriska former

Du har nu byggt ditt första riktiga spel! Du förstår:
- **Game loops** (update körs 60fps)
- **Physics** (kollision, hastighet, boundaries)
- **State management** (playing, won, lost)
- **UI-koppling** (spel ↔ HTML)

