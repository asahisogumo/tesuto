<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>2D アクションゲーム</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: #000;
      font-family: sans-serif;
    }
    #gameCanvas {
      display: block;
      background: #000;
    }
    /* スタートメニュー、Game Overメニュー、ランキング関連メニュー */
    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.8);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: #fff;
      z-index: 1000;
    }
    .overlay select, .overlay button, .overlay input {
      margin: 8px;
      padding: 8px;
      font-size: 16px;
    }
    .touch-controls {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      gap: 10px;
      z-index: 1001;
    }
    .touch-button {
      width: 60px;
      height: 60px;
      background: rgba(0, 0, 0, 0.3);
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      color: #fff;
      font-size: 24px;
      user-select: none;
      touch-action: none;
    }
    /* ホログラム風ボタン */
    .hologram-button {
      position: relative;
      padding: 12px 24px;
      font-size: 18px;
      color: #0ff;
      border: 2px solid #0ff;
      background: transparent;
      cursor: pointer;
      overflow: hidden;
      z-index: 1;
      border-radius: 8px;
    }
    .hologram-button:before {
      content: '';
      position: absolute;
      top: -50%;
      left: -50%;
      width: 200%;
      height: 200%;
      background: linear-gradient(45deg, #0ff, #f0f, #0ff, #f0, #0ff);
      animation: rotate 4s linear infinite;
      z-index: -2;
    }
    .hologram-button:after {
      content: '';
      position: absolute;
      inset: 0;
      background: rgba(255,255,255,0.1);
      mix-blend-mode: overlay;
      z-index: -1;
    }
    @keyframes rotate {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    /* ランキングリスト */
    #rankingList ul {
      list-style: none;
      padding: 0;
      margin: 0;
      width: 80%;
      max-width: 400px;
    }
    #rankingList li {
      padding: 4px 8px;
      border-bottom: 1px solid #555;
      display: flex;
      align-items: center;
    }
    #rankingList img {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      margin-right: 8px;
    }
  </style>
  <!-- Firebase SDK -->
  <!-- TODO: 以下のconfigを自分のFirebaseプロジェクトの設定に置き換えてください -->
  <script type="module">
    // Import the functions you need from the SDKs
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.2/firebase-app.js";
    import { getFirestore } from "https://www.gstatic.com/firebasejs/9.22.2/firebase-firestore.js";

    // Your web app's Firebase configuration
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_STORAGE_BUCKET",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    // Initialize Firebase
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    window.firebaseDB = db; // グローバルに参照できるように
  </script>
</head>
<body>
<canvas id="gameCanvas"></canvas>
<div id="startMenu" class="overlay">
  <h1>2D アクションゲーム</h1>
  <label>背景画像を選択:
    <select id="bgSelect">
      <option value="park-dot3.jpg">Park Background</option>
      <!-- 他の背景を使用する場合、フォルダに画像を置き、optionを追加 -->
    </select>
  </label>
  <label>モードを選択:
    <select id="modeSelect">
      <option value="normal">ノーマルモード</option>
      <option value="hard">ハードモード</option>
    </select>
  </label>
  <label>制限時間を選択:
    <select id="timeSelect">
      <option value="3">3分</option>
      <option value="5">5分</option>
      <option value="10">10分</option>
    </select>
  </label>
  <button id="startButton">ゲーム開始</button>
  <button id="viewRankingButton" class="hologram-button">ランキング確認</button>
  <p>操作: ←/A 移動左, →/D 移動右, Space: ジャンプ(2段)</p>
  <p>攻撃: 左クリック: 通常攻撃, 右クリック: ファイヤー攻撃</p>
  <p>目的: 時間内に敵を倒してスコアを稼ごう！</p>
  <p>ハードモード: 上空から敵が落ちてきます。空中攻撃可能。</p>
</div>
<div id="gameOverMenu" class="overlay" style="display:none;">
  <h1>Game Over</h1>
  <p id="finalScore"></p>
  <button id="retryButton">リトライ</button>
  <button id="backButton">タイトルに戻る</button>
</div>
<!-- ユーザー名入力ダイアログ -->
<div id="rankingDialog" class="overlay" style="display:none;">
  <h2>ランキング登録</h2>
  <p>最終スコア: <span id="dialogScore"></span></p>
  <input type="text" id="playerNameInput" placeholder="あなたの名前" maxlength="20" />
  <label>アイコン選択:
    <select id="iconSelect">
      <option value="">なし</option>
      <option value="icons/icon1.png">アイコン1</option>
      <option value="icons/icon2.png">アイコン2</option>
      <option value="icons/icon3.png">アイコン3</option>
    </select>
  </label>
  <label>または画像アップロード:
    <input type="file" id="playerIconInput" accept="image/*" />
  </label>
  <button id="submitRankButton" class="hologram-button">登録</button>
</div>
<!-- ランキング表示 -->
<div id="rankingList" class="overlay" style="display:none;">
  <h2>ランキング</h2>
  <ul id="rankingUl"></ul>
  <button id="closeRankingButton" class="hologram-button">閉じる</button>
</div>
<div class="touch-controls">
  <div id="btn-left" class="touch-button">◀</div>
  <div id="btn-jump" class="touch-button">▲</div>
  <div id="btn-right" class="touch-button">▶</div>
  <div id="btn-attack" class="touch-button">✦</div>
  <div id="btn-fire" class="touch-button">🔥</div>
</div>
<script type="module">
  // Firebase Firestore 参照
  import { collection, addDoc, query, orderBy, limit, getDocs, serverTimestamp } from "https://www.gstatic.com/firebasejs/9.22.2/firebase-firestore.js";
  const db = window.firebaseDB;

  const canvas = document.getElementById('gameCanvas');
  const ctx = canvas.getContext('2d');
  let width, height;

  // 背景画像
  let bgImage = new Image();
  let bgLoaded = false;
  function loadBackground(name) {
    bgLoaded = false;
    bgImage = new Image();
    bgImage.src = name;
    bgImage.onload = () => { bgLoaded = true; };
  }

  // メニュー要素
  const startMenu = document.getElementById('startMenu');
  const gameOverMenu = document.getElementById('gameOverMenu');
  const bgSelect = document.getElementById('bgSelect');
  const modeSelect = document.getElementById('modeSelect');
  const timeSelect = document.getElementById('timeSelect');
  const startButton = document.getElementById('startButton');
  const viewRankingButton = document.getElementById('viewRankingButton');
  const retryButton = document.getElementById('retryButton');
  const backButton = document.getElementById('backButton');
  const finalScoreEl = document.getElementById('finalScore');

  // ランキング関連要素
  const rankingDialog = document.getElementById('rankingDialog');
  const dialogScoreEl = document.getElementById('dialogScore');
  const playerNameInput = document.getElementById('playerNameInput');
  const iconSelect = document.getElementById('iconSelect');
  const playerIconInput = document.getElementById('playerIconInput');
  const submitRankButton = document.getElementById('submitRankButton');
  const rankingList = document.getElementById('rankingList');
  const rankingUl = document.getElementById('rankingUl');
  const closeRankingButton = document.getElementById('closeRankingButton');

  let gameStarted = false;
  let gameMode = 'normal';
  let gameEndTime = 0;
  let selectedTime = 3;
  let score = 0;

  startButton.addEventListener('click', () => {
    startMenu.style.display = 'none';
    beginGame();
  });
  viewRankingButton.addEventListener('click', () => {
    showRankingList();
  });
  retryButton.addEventListener('click', () => {
    gameOverMenu.style.display = 'none';
    beginGame(true);
  });
  backButton.addEventListener('click', () => {
    gameOverMenu.style.display = 'none';
    startMenu.style.display = 'flex';
  });
  closeRankingButton.addEventListener('click', () => {
    rankingList.style.display = 'none';
    startMenu.style.display = 'flex';
  });

  submitRankButton.addEventListener('click', async () => {
    const name = playerNameInput.value.trim() || '名無し';
    const selectedIconPath = iconSelect.value;
    const file = playerIconInput.files[0];
    let iconData = null;
    if (file) {
      iconData = await new Promise((resolve) => {
        const reader = new FileReader();
        reader.onload = (e) => resolve(e.target.result);
        reader.readAsDataURL(file);
      });
    } else if (selectedIconPath) {
      iconData = selectedIconPath;
    }
    // Firestore に保存
    try {
      await addDoc(collection(db, 'rankings'), {
        name: name,
        score: score,
        icon: iconData,
        timestamp: serverTimestamp()
      });
      playerNameInput.value = '';
      iconSelect.value = '';
      playerIconInput.value = '';
      rankingDialog.style.display = 'none';
      showRankingList();
    } catch (e) {
      console.error('ランキング保存エラー:', e);
      alert('ランキングの保存中にエラーが発生しました');
    }
  });

  async function showRankingList() {
    rankingUl.innerHTML = '';
    try {
      const q = query(collection(db, 'rankings'), orderBy('score', 'desc'), orderBy('timestamp', 'asc'), limit(10));
      const querySnapshot = await getDocs(q);
      if (querySnapshot.empty) {
        const li = document.createElement('li');
        li.textContent = 'まだランキングがありません。';
        rankingUl.appendChild(li);
      } else {
        let index = 1;
        querySnapshot.forEach((docSnap) => {
          const rec = docSnap.data();
          const li = document.createElement('li');
          if (rec.icon) {
            const img = document.createElement('img');
            img.src = rec.icon;
            li.appendChild(img);
          }
          const textSpan = document.createElement('span');
          textSpan.textContent = `${index}. ${rec.name} - ${rec.score}`;
          li.appendChild(textSpan);
          rankingUl.appendChild(li);
          index++;
        });
      }
    } catch (e) {
      console.error('ランキング取得エラー:', e);
      const li = document.createElement('li');
      li.textContent = 'ランキングの取得中にエラーが発生しました';
      rankingUl.appendChild(li);
    }
    startMenu.style.display = 'none';
    gameOverMenu.style.display = 'none';
    rankingDialog.style.display = 'none';
    rankingList.style.display = 'flex';
  }

  function beginGame(isRetry=false) {
    width = window.innerWidth;
    height = window.innerHeight;
    canvas.width = width;
    canvas.height = height;
    const bgName = bgSelect.value;
    loadBackground(bgName);
    gameMode = modeSelect.value;
    selectedTime = parseInt(timeSelect.value, 10);
    gameEndTime = Date.now() + selectedTime * 60000;
    gameStarted = true;
    initGame(isRetry);
    loop();
  }

  window.addEventListener('resize', () => {
    if (!gameStarted) return;
    width = window.innerWidth;
    height = window.innerHeight;
    canvas.width = width;
    canvas.height = height;
    createPlatforms();
    resetPlayer();
  });

  const gravity = 0.6;
  const player = { x:100, y:0, width:40, height:60, vx:0, vy:0, speed:4, jumpPower:12, onGround:false, facing:1, attackCooldown:0, jumpCount:0 };
  const keys = { left:false, right:false, up:false };
  const platforms = [];
  function createPlatforms() {
    platforms.length = 0;
    platforms.push({ x: 0, y: height - 40, width: width, height: 40 });
    platforms.push({ x: width * 0.5, y: height - 150, width: 120, height: 20 });
    platforms.push({ x: width * 0.75, y: height - 200, width: 120, height: 20 });
    platforms.push({ x: width * 0.9, y: height - 100, width: 100, height: 20 });
    platforms.push({ x: 100, y: height - 250, width: 100, height: 20 });
  }
  const enemies = [];
  function spawnEnemySide() {
    const fromRight = Math.random() < 0.5;
    const x = fromRight ? width + 50 : -50;
    const vx = fromRight ? -(2 + Math.random() * 2) : (2 + Math.random() * 2);
    enemies.push({ x: x, y: height - 100, width: 40, height: 40, vx: vx, vy: 0, onGround:false });
  }
  function spawnEnemyTop() {
    const x = Math.random() * (width - 40);
    const vy = 2 + Math.random() * 2;
    enemies.push({ x: x, y: -50, width: 40, height: 40, vx: 0, vy: vy, onGround:false });
  }
  const bullets = [];
  const fireballs = [];

  function initGame(isRetry) {
    createPlatforms();
    resetPlayer();
    score = isRetry ? score : 0;
    enemies.length = 0;
    bullets.length = 0;
    fireballs.length = 0;
    setupControls();
  }

  function update() {
    if (!gameStarted) return;
    const now = Date.now();
    if (now >= gameEndTime) { gameOver(); return; }
    if (keys.left) { player.vx = -player.speed; player.facing = -1; }
    else if (keys.right) { player.vx = player.speed; player.facing = 1; }
    else { player.vx = 0; }
    player.vy += gravity;
    player.x += player.vx;
    player.y += player.vy;
    if (player.x < 0 || player.x + player.width > width || player.y > height) { gameOver(); return; }
    let wasOnGround = player.onGround;
    player.onGround = false;
    platforms.forEach(p => {
      if (player.x < p.x + p.width && player.x + player.width > p.x && player.y + player.height < p.y + player.vy + gravity + 10 && player.y + player.height + player.vy >= p.y) {
        player.y = p.y - player.height;
        player.vy = 0;
        player.onGround = true;
        if (!wasOnGround) player.jumpCount = 0;
      }
    });
    if (player.attackCooldown > 0) player.attackCooldown--;
    bullets.forEach((b, idx) => {
      b.x += b.vx;
      b.y += b.vy;
      if (b.x < 0 || b.x > width || b.y < 0 || b.y > height) bullets.splice(idx,1);
      else enemies.forEach((e, eidx) => {
        if (b.x < e.x + e.width && b.x + b.width > e.x && b.y < e.y + e.height && b.y + b.height > e.y) {
          enemies.splice(eidx,1);
          bullets.splice(idx,1);
          score += 10;
        }
      });
    });
    fireballs.forEach((f, idx) => {
      f.x += f.vx;
      f.y += f.vy;
      if (f.x < 0 || f.x > width || f.y < 0 || f.y > height) fireballs.splice(idx,1);
      else enemies.forEach((e, eidx) => {
        if (f.x < e.x + e.width && f.x + f.width > e.x && f.y < e.y + e.height && f.y + f.height > e.y) {
          enemies.splice(eidx,1);
          fireballs.splice(idx,1);
          score += 20;
        }
      });
    });
    enemies.forEach((e, idx) => {
      e.vy += gravity;
      e.x += e.vx;
      e.y += e.vy;
      if (e.y + e.height > height - 40) { e.y = height - 40 - e.height; e.vy = 0; e.onGround=true; }
      if ((e.vx<0 && e.x+e.width<0) || (e.vx>0 && e.x>width) || e.y>height) enemies.splice(idx,1);
      if (player.x < e.x+e.width && player.x+player.width>e.x && player.y < e.y+e.height && player.y+player.height>e.y) { gameOver(); return; }
    });
    if (Math.random() < 0.02) spawnEnemySide();
    if (gameMode==='hard' && Math.random() < 0.01) spawnEnemyTop();
  }

  function draw() {
    if (!gameStarted) return;
    if (bgLoaded) ctx.drawImage(bgImage, 0, 0, width, height);
    else { ctx.fillStyle='#87CEEB'; ctx.fillRect(0,0,width,height); }
    ctx.fillStyle='white'; ctx.font='16px sans-serif';
    const rem = Math.max(0, gameEndTime - Date.now());
    const seconds = Math.ceil(rem/1000);
    const min = Math.floor(seconds/60);
    const sec = seconds % 60;
    const timeText = `残り時間: ${min}:${sec.toString().padStart(2,'0')}`;
    ctx.fillText(timeText, 10, 20);
    ctx.fillText('←/A, →/D: 移動, Space: ジャンプ(2段)', 10, 40);
    ctx.fillText('左クリック: 通常攻撃(+10), 右クリック: ファイヤー攻撃(+20)',10,60);
    ctx.fillText('スコア: '+score,10,80);
    ctx.fillText('モード: '+(gameMode==='normal'?'ノーマル':'ハード'),10,100);
    ctx.fillStyle='#4caf50'; ctx.fillRect(player.x,player.y,player.width,player.height);
    ctx.fillStyle='#795548'; platforms.forEach(p=>ctx.fillRect(p.x,p.y,p.width,p.height));
    ctx.fillStyle='#d32f2f'; enemies.forEach(e=>ctx.fillRect(e.x,e.y,e.width,e.height));
    ctx.fillStyle='#ffeb3b'; bullets.forEach(b=>ctx.fillRect(b.x,b.y,b.width,b.height));
    ctx.fillStyle='#ff4500'; fireballs.forEach(f=>ctx.fillRect(f.x,f.y,f.width,f.height));
  }

  function loop() { update(); draw(); if(gameStarted) requestAnimationFrame(loop); }

  function resetPlayer() { player.x=100; player.y=height-100; player.vx=0; player.vy=0; player.jumpCount=0; }
  function spawnBullet() {
    if (player.attackCooldown<=0) {
      let vx=0, vy=0;
      if (gameMode==='hard' && keys.up) { vx=0; vy=-8; }
      else { vx=player.facing*8; vy=0; }
      bullets.push({ x:player.x+player.width/2-4, y:player.y+player.height/2-4, width:8, height:8, vx:vx, vy:vy });
      player.attackCooldown=20;
    }
  }
  function spawnFireball() {
    if (player.attackCooldown<=0) {
      let vx=0, vy=0;
      if (gameMode==='hard' && keys.up) { vx=0; vy=-6; }
      else { vx=player.facing*6; vy=0; }
      fireballs.push({ x:player.x+player.width/2-8, y:player.y+player.height/2-8, width:16, height:16, vx:vx, vy:vy });
      player.attackCooldown=40;
    }
  }

  function gameOver() {
    gameStarted=false;
    finalScoreEl.textContent = '最終スコア: ' + score;
    gameOverMenu.style.display='flex';
    dialogScoreEl.textContent = score;
    playerNameInput.value = '';
    iconSelect.value = '';
    playerIconInput.value = '';
    rankingDialog.style.display = 'flex';
  }

  function setupControls() {
    window.addEventListener('keydown', e=>{
      if(e.code==='ArrowLeft'||e.code==='KeyA') keys.left=true;
      if(e.code==='ArrowRight'||e.code==='KeyD') keys.right=true;
      if(e.code==='ArrowUp') keys.up=true;
      if(e.code==='Space') { if(player.jumpCount<2) { player.vy=-player.jumpPower; player.jumpCount++; player.onGround=false; } }
    });
    window.addEventListener('keyup', e=>{
      if(e.code==='ArrowLeft'||e.code==='KeyA') keys.left=false;
      if(e.code==='ArrowRight'||e.code==='KeyD') keys.right=false;
      if(e.code==='ArrowUp') keys.up=false;
    });
    canvas.addEventListener('mousedown', e=>{
      if(!gameStarted) return;
      if(e.button===0) spawnBullet();
      else if(e.button===2) spawnFireball();
    });
    canvas.addEventListener('contextmenu', e=>e.preventDefault());
    const btnLeft=document.getElementById('btn-left');
    const btnRight=document.getElementById('btn-right');
    const btnJump=document.getElementById('btn-jump');
    const btnAttack=document.getElementById('btn-attack');
    const btnFire=document.getElementById('btn-fire');
    function setTouch(btn, action) {
      btn.addEventListener('touchstart', e=>{ e.preventDefault(); if(action==='left') keys.left=true; if(action==='right') keys.right=true; if(action==='jump'){ if(player.jumpCount<2){player.vy=-player.jumpPower;player.jumpCount++;player.onGround=false;}} if(action==='attack') spawnBullet(); if(action==='fire') spawnFireball(); });
      btn.addEventListener('touchend', e=>{ e.preventDefault(); if(action==='left') keys.left=false; if(action==='right') keys.right=false; });
    }
    setTouch(btnLeft,'left'); setTouch(btnRight,'right'); setTouch(btnJump,'jump'); setTouch(btnAttack,'attack'); setTouch(btnFire,'fire');
  }
</script>
</body>
</html>
