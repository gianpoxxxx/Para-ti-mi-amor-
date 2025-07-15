<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Mi Amor QR - Rasga y Descubre</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Dancing+Script:wght@700&display=swap" rel="stylesheet" />
  <style>
    :root {
      --rosa-principal: #fa61d3;
      --lila-principal: #b721ff;
      --color-texto: #e94057;
    }
    html, body {
      height: 100%;
      margin: 0;
      padding: 0;
    }
    body {
      min-height: 100vh;
      font-family: 'Roboto', sans-serif;
      background: linear-gradient(135deg, var(--lila-principal) 0%, var(--rosa-principal) 100%);
      display: flex;
      align-items: center;
      justify-content: center;
      overflow-x: hidden;
      position: relative;
      box-sizing: border-box;
    }
    .fondo-corazones {
      position: fixed;
      width: 100vw;
      height: 100vh;
      z-index: 0;
      top: 0; left: 0;
      pointer-events: none;
    }
    .corazon-bg {
      position: absolute;
      opacity: 0.18;
      font-size: 3.5rem;
      animation: lovefloat 8s linear infinite;
    }
    .corazon-bg.c1 {left:10vw; top:4vh; animation-delay: 0s;}
    .corazon-bg.c2 {left:80vw; top:14vh; font-size:2.5rem; animation-delay: 3s;}
    .corazon-bg.c3 {left:26vw; top:70vh; font-size:2.9rem; animation-delay: 2s;}
    .corazon-bg.c4 {left:75vw; top:65vh; font-size:4rem; animation-delay: 5s;}
    .corazon-bg.c5 {left:45vw; top:15vh; font-size:3.2rem; animation-delay: 4s;}
    @keyframes lovefloat {
      0% { transform: translateY(0) scale(1);}
      50% { opacity: 0.26;}
      100% { transform: translateY(-60px) scale(1.09);}
    }

    /* LOGIN */
    .auth-container {
      background: rgba(255,255,255, 0.96);
      border-radius: 18px;
      box-shadow: 0 5px 32px rgba(50,9,77,0.16),0 1.5px 5px rgba(0,0,0,0.05);
      border: 2px solid var(--rosa-principal);
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      width: 100%;
      max-width: 375px;
      padding: 32px 8vw 38px 8vw;
      gap: 16px;
      position: relative;
      z-index: 1;
      animation: aparecer 0.75s;
      box-sizing: border-box;
    }
    .auth-container .pregunta {
      font-family: 'Dancing Script', cursive;
      font-size: 1.1rem;
      color: var(--color-texto);
      font-weight: bold;
      margin-bottom: 14px;
      margin-top: 2px;
      letter-spacing: 0.4px;
      text-shadow: 1px 1px 6px #fbc8e7bb;
    }
    .heart-input {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-bottom: 6px;
    }
    .corazon-input {
      position: relative;
      width: 66px; height: 60px;
      margin-top: 4px;
      max-width: 80vw;
    }
    .corazon-input svg {
      width: 100%; height: 100%;
      display: block;
    }
    .corazon-input input[type="password"] {
      position: absolute;
      top: 25px;
      left: 0;
      width: 100%;
      background: transparent;
      border: none;
      font-size: 1.08rem;
      font-weight: bold;
      color: var(--color-texto);
      text-align: center;
      outline: none;
      letter-spacing: 2px;
      z-index: 1;
      font-family: 'Roboto', sans-serif;
      filter: drop-shadow(1px 1.5px 3px #f67ac080);
    }
    .corazon-input input::placeholder {
      color: #e295c3aa;
    }
    .auth-container button {
      padding: 9px 36px;
      font-size: 1rem;
      font-weight: bold;
      border: none;
      border-radius: 24px;
      background: linear-gradient(90deg,var(--color-texto) , var(--rosa-principal) 96%);
      color: #fff;
      transition: background 0.18s;
      cursor: pointer;
      box-shadow: 0 2px 8px #ea91d185;
      letter-spacing: 1.1px;
      margin-top: 7px;
    }
    .auth-container button:active {
      background: linear-gradient(90deg,var(--rosa-principal) , var(--color-texto) 96%);
    }
    .auth-container .error {
      color: #c91d57;
      font-size: .98rem;
      font-weight: bold;
      min-height: 18px;
      margin-top: 0;
      letter-spacing: 0.5px;
    }

    /* CARTA Y QR */
    .card {
      display: none;
      flex-direction: column;
      background: #fff;
      border-radius: 18px;
      box-shadow: 0 5px 32px rgba(50,9,77,0.08),0 1.5px 5px rgba(0,0,0,0.05);
      padding: 21px 3vw 15px 3vw;
      width: 100%;
      max-width: 415px;
      margin: auto;
      position: relative;
      align-items: center;
      gap: 16px;
      border: 1.6px solid var(--rosa-principal);
      z-index: 2;
      animation: aparecer 0.8s;
      box-sizing: border-box;
    }
    .card-text {
      max-width: 100%;
      display: flex;
      flex-direction: column;
      gap: 10px;
      align-items: center;
    }
    .card-text h2 {
      margin: 0;
      font-size: 1.17rem;
      font-weight: 700;
      color: var(--color-texto);
    }
    .card-text p {
      margin: 0;
      color: #444;
      font-size: .99rem;
      line-height: 1.42;
      text-align: center;
      white-space: pre-line;
    }
    .card-text .firma {
      font-family: 'Dancing Script', cursive;
      font-size: 1.06rem;
      color: #bf126a;
      margin-top: 8px;
    }
    .scratch-qr-container {
      position: relative;
      width: 70vw;
      max-width: 240px;
      min-width: 120px;
      aspect-ratio: 1/1;
      margin: 10px auto 0 auto;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .scratch-qr-img {
      width: 100%;
      height: 100%;
      max-width: 240px;
      min-width: 120px;
      max-height: 240px;
      min-height: 120px;
      display: block;
      border-radius: 12px;
      background: #fff;
      box-shadow: 0 2px 13px #fbc8e77c;
      object-fit: contain;
    }
    .scratch-canvas {
      position: absolute;
      top: 0; left: 0;
      width: 100%;
      height: 100%;
      border-radius: 12px;
      box-shadow: 0 2px 13px #fbc8e74d;
      cursor: pointer;
      touch-action: none;
      background: none;
      transition: opacity 0.7s;
      z-index: 2;
    }
    .scratch-instruccion {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      color: #e94057;
      font-size: 1rem;
      font-weight: 700;
      font-family: 'Roboto', cursive;
      pointer-events: none;
      z-index: 3;
      user-select: none;
      text-shadow: 1px 1px 8px #fff, 0 0 12px #fff8;
      transition: opacity 0.7s;
      text-align: center;
      padding: 0 6%;
      box-sizing: border-box;
    }
    @keyframes aparecer {
      from { opacity: 0; transform: scale(0.97);}
      to { opacity: 1; transform: scale(1);}
    }
    @media (max-width: 430px) {
      .card, .auth-container {
        padding-left: 2vw;
        padding-right: 2vw;
      }
      .corazon-input {width:49px;height:44px;}
      .corazon-input input[type="password"] {font-size: .92rem; top:11px;}
      .card-text h2 {font-size: 1.04rem;}
      .card-text p {font-size: .95rem;}
      .card-text .firma {font-size: .93rem;}
    }
  </style>
</head>
<body>
  <div class="fondo-corazones" aria-hidden="true">
    <span class="corazon-bg c1">❤</span>
    <span class="corazon-bg c2">❤</span>
    <span class="corazon-bg c3">❤</span>
    <span class="corazon-bg c4">❤</span>
    <span class="corazon-bg c5">❤</span>
  </div>
  <!-- Pantalla de contraseña -->
  <div class="auth-container" id="authContainer">
    <div class="pregunta">Fecha de la primera llamada</div>
    <div class="heart-input">
      <div class="corazon-input">
        <svg viewBox="0 0 88 78">
          <path d="M44 72C44 72 7 49.7 7 27.5C7 12.2 19.1 2 32.5 2C39.6 2 45.3 7.3 47.7 14.4C50.1 7.3 55.9 2 63 2C76.4 2 88.5 12.2 88.5 27.5C88.5 49.7 44 72 44 72Z"
            fill="#ffe5f5" stroke="#fa61d3" stroke-width="3"/>
        </svg>
        <input type="password" maxlength="6" id="passwordInput" placeholder="______" autocomplete="off" inputmode="numeric" />
      </div>
    </div>
    <button id="submitPassword">Abrir</button>
    <div class="error" id="errorMsg"></div>
  </div>
  <!-- Carta romántica oculta -->
  <div class="card" id="cardContainer" style="display:none;">
    <div class="card-text">
      <h2>Mi Amor,</h2>
      <p>
Tanto tiempo, tantas cosas, tantas personas.<br>
Y pensar que todo este tiempo yo solo te buscaba a ti.<br>
Cuanto mas tiempo estoy contigo mas me gustas, a pesar de los problemas y todo lo que pasemos que no se te olvide lo mucho q te amo.... me pase de cursi poessss.
      </p>
      <div class="firma">
        Con todo mi amor. <span>❤</span>
      </div>
    </div>
    <div class="scratch-qr-container">
      <img src="https://storage2.me-qr.com/qr/227978633.png" alt="QR especial" class="scratch-qr-img" draggable="false" />
      <canvas class="scratch-canvas" id="scratchCanvas"></canvas>
      <div class="scratch-instruccion" id="scratchInstruc">✨ Rasga aquí para descubrir tu sorpresa ✨</div>
    </div>
  </div>
  <script>
    // Control de acceso
    const submitBtn = document.getElementById('submitPassword');
    const passwordInput = document.getElementById('passwordInput');
    const authContainer = document.getElementById('authContainer');
    const cardContainer = document.getElementById('cardContainer');
    const errorMsg = document.getElementById('errorMsg');

    function showCard() {
      authContainer.style.display = "none";
      cardContainer.style.display = "flex";
      setTimeout(initializeScratch, 250);
    }
    function checkPassword() {
      if (passwordInput.value.trim() === '140325') {
        showCard();
        passwordInput.value = '';
        errorMsg.textContent = '';
      } else {
        errorMsg.textContent = 'Ups... inténtalo otra vez, mi amor 🩷';
        passwordInput.value = '';
        passwordInput.focus();
      }
    }
    passwordInput.addEventListener('keypress', function(e) {
      if (e.key === 'Enter') { checkPassword(); }
    });
    submitBtn.addEventListener('click', checkPassword);
    window.onload = () => { passwordInput.focus(); };

    // Efecto de rasgado responsivo
    function initializeScratch(){
      const canvas = document.getElementById('scratchCanvas');
      const ctx = canvas.getContext('2d');

      function setCanvasSize() {
        let parent = canvas.parentElement;
        canvas.width = parent.offsetWidth;
        canvas.height = parent.offsetHeight;
        drawCover();
      }
      window.addEventListener('resize', setCanvasSize);
      setCanvasSize();

      function drawCover() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        const grad = ctx.createLinearGradient(0,0, canvas.width, canvas.height);
        grad.addColorStop(0, "#ffe5f5");
        grad.addColorStop(1, "#f1bae7");
        ctx.fillStyle = grad;
        ctx.fillRect(0, 0, canvas.width, canvas.height);
        ctx.font = `${Math.max(14,canvas.width/10)}px Dancing Script, cursive`;
        ctx.globalAlpha = 0.22;
        for(let i=0; i<18; i++){
          ctx.fillText("❤", Math.random()*canvas.width, Math.random()*canvas.height);
        }
        ctx.globalAlpha = 1;
        ctx.strokeStyle = "#fff";
        for(let i=0;i<3;i++){
          ctx.beginPath();
          ctx.moveTo(Math.random()*canvas.width,Math.random()*canvas.height);
          ctx.bezierCurveTo(Math.random()*canvas.width,Math.random()*canvas.height,Math.random()*canvas.width,Math.random()*canvas.height,Math.random()*canvas.width,Math.random()*canvas.height);
          ctx.stroke();
        }
      }

      let isDrawing = false, lastX = 0, lastY = 0;
      function getOffset(e) {
        const rect = canvas.getBoundingClientRect();
        let clientX, clientY;
        if(e.touches && e.touches.length > 0) {
          clientX = e.touches[0].clientX;
          clientY = e.touches[0].clientY;
        } else {
          clientX = e.clientX;
          clientY = e.clientY;
        }
        return { x: clientX - rect.left, y: clientY - rect.top }
      }
      function startDraw(e) {
        e.preventDefault();
        isDrawing = true;
        const pos = getOffset(e);
        lastX = pos.x;
        lastY = pos.y;
      }
      function draw(e) {
        if(!isDrawing) return;
        e.preventDefault();
        const pos = getOffset(e);
        ctx.globalCompositeOperation = "destination-out";
        ctx.lineWidth = Math.max(34,canvas.width/6);
        ctx.lineCap = "round";
        ctx.beginPath();
        ctx.moveTo(lastX, lastY);
        ctx.lineTo(pos.x, pos.y);
        ctx.stroke();
        lastX = pos.x;
        lastY = pos.y;
        ctx.globalCompositeOperation = "source-over";
      }
      function endDraw(e) {
        isDrawing = false;
        let imageData = ctx.getImageData(0, 0, canvas.width, canvas.height).data;
        let clearPixels = 0;
        for (let i = 3; i < imageData.length; i += 4) {
          if (imageData[i] === 0) clearPixels++;
        }
        let clearRatio = clearPixels / (canvas.width * canvas.height) * 100;
        if (clearRatio > 40) {
          canvas.style.opacity = 0;
          instrucDiv.style.opacity = 0;
          setTimeout(()=>{
            canvas.style.display="none";
            instrucDiv.style.display="none";
          },700);
        }
      }
      canvas.addEventListener('mousedown', startDraw);
      canvas.addEventListener('mousemove', draw);
      canvas.addEventListener('mouseup', endDraw);
      canvas.addEventListener('mouseleave', endDraw);
      canvas.addEventListener('touchstart', startDraw, {passive:false});
      canvas.addEventListener('touchmove', draw, {passive:false});
      canvas.addEventListener('touchend', endDraw);

      document.querySelector('.scratch-qr-img').ondragstart = e => e.preventDefault();
      const instrucDiv = document.getElementById('scratchInstruc');
      instrucDiv.style.opacity = 1;
      setInterval(()=> {
        instrucDiv.style.opacity = 0.7 + 0.3*Math.sin(Date.now()/950);
      },80);
    }
  </script>
</body>
</html>
