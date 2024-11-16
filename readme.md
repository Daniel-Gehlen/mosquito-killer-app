### Fly-Swatting Game Code Review and Explanation

This is a simple game where the player must click on flying mosquitos before they disappear, while managing lives and time. It includes features for varying difficulty levels and ensures a responsive layout.

![](movie.gif)

---

## How the Game Works

1. **Game Setup**:
   - The game adjusts to the browser window's size using `ajustaTamanhoPalcoJogo()`.
   - Difficulty is set based on the `nivel` parameter from the URL (`normal`, `dificil`, `chucknorris`) and adjusts the mosquito spawn interval.

2. **Mosquito Creation**:
   - Mosquitos appear at random positions within the game area (`posicaoRandomica()`).
   - If a mosquito isn't clicked in time, the player loses a life.

3. **Lives and Game Over**:
   - Players have three lives, displayed as full hearts (`coracao_cheio.png`).
   - Each missed mosquito replaces a full heart with an empty heart (`coracao_vazio.png`).
   - Losing all lives redirects the player to a "game over" page (`fim_de_jogo.html`).

4. **Timer**:
   - A countdown timer decrements each second, ending the game in victory if the player survives (`vitoria.html`).

---

## Key Features in the Code

### 1. **Responsive Gameplay Area**
```javascript
function ajustaTamanhoPalcoJogo() {
	altura = window.innerHeight;
	largura = window.innerWidth;
}
```
- Ensures that mosquitos spawn within the visible screen area.

### 2. **Dynamic Mosquito Creation**
```javascript
var mosquito = document.createElement('img');
mosquito.src = 'imagens/mosquito.png';
mosquito.className = tamanhoAleatorio() + ' ' + ladoAleatorio();
mosquito.style.left = posicaoX + 'px';
mosquito.style.top = posicaoY + 'px';
mosquito.style.position = 'absolute';
mosquito.id = 'mosquito';
mosquito.onclick = function() { this.remove(); };
document.body.appendChild(mosquito);
```
- A mosquito is dynamically created and positioned randomly on the screen. Clicking it removes the mosquito, simulating a "swat."

### 3. **Difficulty Levels**
```javascript
if(nivel === 'normal') {
	criaMosquitoTempo = 1500; // 1.5 seconds
} else if(nivel === 'dificil') {
	criaMosquitoTempo = 1000; // 1 second
} else if (nivel === 'chucknorris') {
	criaMosquitoTempo = 750; // 0.75 seconds
}
```
- The spawn time interval (`criaMosquitoTempo`) decreases with increasing difficulty.

### 4. **Game Over and Victory Conditions**
- **Victory**: Triggered when the timer reaches `0`:
  ```javascript
  if (tempo < 0) {
      clearInterval(cronometro);
      clearInterval(criaMosca);
      window.location.href = 'vitoria.html';
  }
  ```
- **Game Over**: Triggered when all three lives are lost:
  ```javascript
  if(vidas > 3) {
      window.location.href = 'fim_de_jogo.html';
  }
  ```

### 5. **Randomized Mosquito Size and Orientation**
- Mosquitos can appear in three sizes:
  ```javascript
  function tamanhoAleatorio() {
      var classe = Math.floor(Math.random() * 3);
      switch (classe) {
          case 0: return 'mosquito1';
          case 1: return 'mosquito2';
          case 2: return 'mosquito3';
      }
  }
  ```
- And two orientations (facing left or right):
  ```javascript
  function ladoAleatorio() {
      var classe = Math.floor(Math.random() * 2);
      switch (classe) {
          case 0: return 'ladoA';
          case 1: return 'ladoB';
      }
  }
  ```

---

## Areas for Enhancement

1. **Mobile Optimization**:
   - Add touch events for better gameplay on mobile devices.

2. **Sound Effects**:
   - Play a sound when a mosquito is clicked or when a life is lost.

3. **Scoring System**:
   - Introduce a score based on mosquitos swatted.

4. **Pause/Resume Functionality**:
   - Allow players to pause the game and resume later.

5. **Visual Feedback**:
   - Add animations or effects when mosquitos are swatted.

6. **Improved Styling**:
   - Add a more polished design with CSS.

---

This code demonstrates a fun and interactive browser-based game with a clear structure and engaging mechanics. It’s an excellent project for practicing JavaScript DOM manipulation, event handling, and responsive design.