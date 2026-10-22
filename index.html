<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cyber Sphere 3D - Marble Runner</title>
  <!-- Carga de Three.js para renderizado 3D -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      user-select: none;
    }

    body, html {
      width: 100%;
      height: 100%;
      overflow: hidden;
      background-color: #050811;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      color: #fff;
    }

    #game-container {
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
    }

    /* HUD Superior */
    #hud {
      position: absolute;
      top: 20px;
      left: 20px;
      right: 20px;
      display: flex;
      justify-content: space-between;
      pointer-events: none;
      z-index: 10;
    }

    .hud-card {
      background: rgba(10, 15, 30, 0.75);
      border: 1px solid rgba(0, 240, 255, 0.3);
      padding: 10px 22px;
      border-radius: 12px;
      backdrop-filter: blur(8px);
      text-align: center;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.5);
    }

    .hud-card .title {
      font-size: 11px;
      color: #00f0ff;
      letter-spacing: 1.5px;
      font-weight: bold;
    }

    .hud-card .val {
      font-size: 26px;
      font-weight: 800;
      color: #ffffff;
      text-shadow: 0 0 10px rgba(0, 240, 255, 0.6);
    }

    /* Pantallas emergentes (Menú / Game Over) */
    .overlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(5, 8, 17, 0.88);
      backdrop-filter: blur(12px);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 100;
      text-align: center;
      padding: 20px;
    }

    .overlay h1 {
      font-size: 46px;
      color: #00f0ff;
      text-shadow: 0 0 25px rgba(0, 240, 255, 0.8);
      margin-bottom: 12px;
    }

    .overlay p {
      font-size: 17px;
      color: #94a3b8;
      max-width: 480px;
      margin-bottom: 28px;
      line-height: 1.5;
    }

    .overlay button {
      padding: 16px 42px;
      font-size: 18px;
      font-weight: bold;
      color: #050811;
      background: linear-gradient(135deg, #00f0ff, #7000ff);
      border: none;
      border-radius: 30px;
      cursor: pointer;
      box-shadow: 0 0 20px rgba(0, 240, 255, 0.5);
      transition: all 0.2s ease;
    }

    .overlay button:hover {
      transform: scale(1.06);
      box-shadow: 0 0 30px rgba(0, 240, 255, 0.9);
    }

    /* Controles en pantalla para móviles */
    #touch-controls {
      display: none;
      position: absolute;
      bottom: 25px;
      left: 20px;
      right: 20px;
      z-index: 50;
      justify-content: space-between;
      pointer-events: none;
    }

    .touch-btn {
      width: 65px;
      height: 65px;
      border-radius: 50%;
      background: rgba(0, 240, 255, 0.2);
      border: 2px solid rgba(0, 240, 255, 0.5);
      color: white;
      font-size: 20px;
      font-weight: bold;
      pointer-events: auto;
      backdrop-filter: blur(5px);
    }
  </style>
</head>
<body>

  <div id="game-container"></div>

  <!-- Interfaz de juego -->
  <div id="hud">
    <div class="hud-card">
      <div class="title">PUNTOS</div>
      <div id="score-display" class="val">0</div>
    </div>
    <div class="hud-card">
      <div class="title">GEMS</div>
      <div id="gems-display" class="val">0</div>
    </div>
    <div class="hud-card">
      <div class="title">DISTANCIA</div>
      <div id="dist-display" class="val">0m</div>
    </div>
  </div>

  <!-- Menú Principal / Fin de Juego -->
  <div id="overlay" class="overlay">
    <h1 id="menu-title">CYBER SPHERE 3D</h1>
    <p id="menu-desc">Controla la esfera neón. Esquiva las sierras giratorias, salta sobre las plataformas y recolecta cristales.</p>
    <button id="start-btn">¡INICIAR JUEGO!</button>
  </div>

  <script>
    // --- ESTADO Y VARIABLES GLOBALES ---
    let scene, camera, renderer;
    let sphere, sphereBody;
    let isPlaying = false;
    let score = 0, gemsCollected = 0, distance = 0;
    
    // Físicas simples
    const pos = { x: 0, y: 1, z: 0 };
    const vel = { x: 0, y: 0, z: -0.25 };
    const isGrounded = true;
    
    const obstacles = [];
    const gems = [];
    const platforms = [];

    // Estado de teclas
    const keys = { left: false, right: false, up: false, down: false, jump: false };

    // --- SINTETIZADOR DE SONIDO (Web Audio API) ---
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    
    function playSound(type) {
      if (audioCtx.state === 'suspended') audioCtx.resume();
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.connect(gain);
      gain.connect(audioCtx.destination);

      const now = audioCtx.currentTime;

      if (type === 'gem') {
        osc.type = 'sine';
        osc.frequency.setValueAtTime(587.33, now); // D5
        osc.frequency.exponentialRampToValueAtTime(1174.66, now + 0.15); // D6
        gain.gain.setValueAtTime(0.2, now);
        gain.gain.exponentialRampToValueAtTime(0.01, now + 0.15);
        osc.start(now);
        osc.stop(now + 0.15);
      } else if (type === 'jump') {
        osc.type = 'triangle';
        osc.frequency.setValueAtTime(150, now);
        osc.frequency.exponentialRampToValueAtTime(400, now + 0.2);
        gain.gain.setValueAtTime(0.3, now);
        gain.gain.exponentialRampToValueAtTime(0.01, now + 0.2);
        osc.start(now);
        osc.stop(now + 0.2);
      } else if (type === 'crash') {
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(120, now);
        osc.frequency.exponentialRampToValueAtTime(30, now + 0.3);
        gain.gain.setValueAtTime(0.4, now);
        gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
        osc.start(now);
        osc.stop(now + 0.3);
      }
    }

    // --- INICIALIZACIÓN DE THREE.JS ---
    function init() {
      // 1. Escena & Niebla
      scene = new THREE.Scene();
      scene.background = new THREE.Color(0x050811);
      scene.fog = new THREE.FogExp2(0x050811, 0.015);

      // 2. Cámara
      camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);

      // 3. Renderizador
      renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setSize(window.innerWidth, window.innerHeight);
      renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
      document.getElementById('game-container').appendChild(renderer.domElement);

      // 4. Luces
      const ambientLight = new THREE.AmbientLight(0xffffff, 0.5);
      scene.add(ambientLight);

      const dirLight = new THREE.DirectionalLight(0x00f0ff, 1.2);
      dirLight.position.set(20, 40, 20);
      scene.add(dirLight);

      // 5. Esfera del Jugador
      const sphereGeo = new THREE.SphereGeometry(1, 32, 32);
      const sphereMat = new THREE.MeshStandardMaterial({
        color: 0x00f0ff,
        wireframe: true,
        emissive: 0x0088ff,
        emissiveIntensity: 0.5
      });
      sphere = new THREE.Mesh(sphereGeo, sphereMat);
      scene.add(sphere);

      // Generar pista inicial
      buildTrack();

      // Eventos
      window.addEventListener('keydown', (e) => handleKey(e, true));
      window.addEventListener('keyup', (e) => handleKey(e, false));
      window.addEventListener('resize', onWindowResize);

      document.getElementById('start-btn').addEventListener('click', startGame);

      animate();
    }

    // --- GENERACIÓN PROCEDURAL DE PISTA ---
    function buildTrack() {
      // Crear tramos de pista y obstáculos
      for (let z = 0; z > -400; z -= 20) {
        // Plataforma
        const platGeo = new THREE.BoxGeometry(12, 1, 18);
        const platMat = new THREE.MeshStandardMaterial({ color: 0x0f172a, roughness: 0.8 });
        const plat = new THREE.Mesh(platGeo, platMat);
        plat.position.set(0, -0.5, z);
        scene.add(plat);
        platforms.push(plat);

        // Borde brillante
        const grid = new THREE.GridHelper(12, 6, 0x00f0ff, 0x1e293b);
        grid.position.set(0, 0.01, z);
        scene.add(grid);

        // Obstáculos (Cubos/Sierras) en tramos lejanos
        if (z < -30 && Math.random() > 0.3) {
          const obsGeo = new THREE.BoxGeometry(2, 2, 2);
          const obsMat = new THREE.MeshStandardMaterial({ color: 0xff0055, emissive: 0xff0033 });
          const obs = new THREE.Mesh(obsGeo, obsMat);
          obs.position.set((Math.random() - 0.5) * 8, 1, z);
          scene.add(obs);
          obstacles.push(obs);
        }

        // Cristales / Gemas
        if (z < -20 && Math.random() > 0.4) {
          const gemGeo = new THREE.OctahedronGeometry(0.8);
          const gemMat = new THREE.MeshStandardMaterial({ color: 0x00ff88, emissive: 0x00ff88 });
          const gem = new THREE.Mesh(gemGeo, gemMat);
          gem.position.set((Math.random() - 0.5) * 8, 1.2, z);
          scene.add(gem);
          gems.push(gem);
        }
      }
    }

    function handleKey(e, isDown) {
      if (e.key === 'ArrowLeft' || e.key === 'a' || e.key === 'A') keys.left = isDown;
      if (e.key === 'ArrowRight' || e.key === 'd' || e.key === 'D') keys.right = isDown;
      if (e.key === 'ArrowUp' || e.key === 'w' || e.key === 'W') keys.up = isDown;
      if (e.key === 'ArrowDown' || e.key === 's' || e.key === 'S') keys.down = isDown;
      if (e.key === ' ' && isDown && pos.y <= 1.05) {
        vel.y = 0.25;
        playSound('jump');
      }
    }

    function startGame() {
      document.getElementById('overlay').style.display = 'none';
      pos.x = 0; pos.y = 1; pos.z = 0;
      vel.x = 0; vel.y = 0; vel.z = -0.3;
      score = 0; gemsCollected = 0; distance = 0;
      isPlaying = true;
    }

    function gameOver() {
      isPlaying = false;
      playSound('crash');
      document.getElementById('overlay').style.display = 'flex';
      document.getElementById('menu-title').innerText = '¡GAME OVER!';
      document.getElementById('menu-desc').innerHTML = `Puntuación Total: <b>${Math.floor(score)}</b><br>Cristales Recolectados: <b>${gemsCollected}</b>`;
      document.getElementById('start-btn').innerText = 'REINTENTAR';
    }

    // --- BUCLE DE ANIMACIÓN Y FÍSICAS ---
    function animate() {
      requestAnimationFrame(animate);

      if (isPlaying) {
        // Controles laterales
        if (keys.left && pos.x > -5) vel.x -= 0.015;
        if (keys.right && pos.x < 5) vel.x += 0.015;
        
        // Aceleración / Freno
        if (keys.up) vel.z = Math.max(vel.z - 0.005, -0.6);
        else if (keys.down) vel.z = Math.min(vel.z + 0.005, -0.15);

        // Rozamiento lateral
        vel.x *= 0.9;

        // Gravedad
        pos.y += vel.y;
        if (pos.y > 1) {
          vel.y -= 0.012; // Fuerza de gravedad
        } else {
          pos.y = 1;
          vel.y = 0;
        }

        // Actualizar Posición
        pos.x += vel.x;
        pos.z += vel.z;

        sphere.position.set(pos.x, pos.y, pos.z);
        
        // Rotación visual de la esfera al rodar
        sphere.rotation.x += vel.z;
        sphere.rotation.z -= vel.x;

        // Caída fuera de la pista
        if (Math.abs(pos.x) > 6.5 && pos.y <= 1) {
          gameOver();
        }

        // Reciclaje procedural de objetos
        obstacles.forEach((obs) => {
          // Rotación de obstáculo
          obs.rotation.x += 0.02;
          obs.rotation.y += 0.02;

          // Colisión con obstáculo
          if (sphere.position.distanceTo(obs.position) < 1.6) {
            gameOver();
          }

          // Reposicionar al quedar atrás
          if (obs.position.z > sphere.position.z + 10) {
            obs.position.z = sphere.position.z - 350 - Math.random() * 50;
            obs.position.x = (Math.random() - 0.5) * 8;
          }
        });

        gems.forEach((gem) => {
          gem.rotation.y += 0.04;

          // Colisión con cristales
          if (sphere.position.distanceTo(gem.position) < 1.5) {
            playSound('gem');
            gemsCollected++;
            score += 100;
            gem.position.z = sphere.position.z - 350 - Math.random() * 50;
            gem.position.x = (Math.random() - 0.5) * 8;
          }

          // Reposicionar
          if (gem.position.z > sphere.position.z + 10) {
            gem.position.z = sphere.position.z - 350 - Math.random() * 50;
            gem.position.x = (Math.random() - 0.5) * 8;
          }
        });

        // Reposicionar plataformas para efecto infinito
        platforms.forEach((plat) => {
          if (plat.position.z > sphere.position.z + 20) {
            plat.position.z -= 400;
          }
        });

        // Puntuación
        distance = Math.floor(-pos.z);
        score += 0.2;

        // Actualizar HUD
        document.getElementById('score-display').innerText = Math.floor(score);
        document.getElementById('gems-display').innerText = gemsCollected;
        document.getElementById('dist-display').innerText = `${distance}m`;
      }

      // Cámara suave siguiendo a la esfera
      camera.position.x = sphere.position.x * 0.5;
      camera.position.y = sphere.position.y + 4;
      camera.position.z = sphere.position.z + 10;
      camera.lookAt(sphere.position.x, sphere.position.y + 0.5, sphere.position.z - 5);

      renderer.render(scene, camera);
    }

    function onWindowResize() {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    }

    window.onload = init;
  </script>
</body>
</html>
