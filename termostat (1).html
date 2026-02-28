<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Akıllı Termostat</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/paho-mqtt/1.0.1/mqttws31.min.js"></script>
<style>
  @import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@300;400;500&family=Syne:wght@400;700;800&display=swap');

  :root {
    --bg: #0d0f14; --card: #141720; --border: #1e2330;
    --accent: #e8663d; --accent2: #3d8fe8;
    --warm: #f0a050; --cool: #50b0f0;
    --text: #e8eaf0; --muted: #5a6080;
    --green: #4ecb8d; --red: #e85050;
  }

  * { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }

  body {
    background:var(--bg); color:var(--text);
    font-family:'DM Mono',monospace;
    min-height:100vh; overflow-x:hidden;
  }

  body::before {
    content:''; position:fixed; inset:0;
    background-image:
      radial-gradient(circle at 20% 20%,rgba(232,102,61,0.06) 0%,transparent 50%),
      radial-gradient(circle at 80% 80%,rgba(61,143,232,0.06) 0%,transparent 50%);
    pointer-events:none; z-index:0;
  }

  @keyframes fadeIn {
    from{opacity:0;transform:translateY(12px)}
    to{opacity:1;transform:translateY(0)}
  }

  /* ===== LOGIN ===== */
  #loginEkran {
    position:fixed; inset:0; z-index:999;
    background:var(--bg);
    display:flex; align-items:center; justify-content:center; padding:24px;
  }

  .login-box {
    background:var(--card); border:1px solid var(--border);
    border-radius:24px; padding:36px 28px;
    width:100%; max-width:360px;
    animation:fadeIn 0.4s ease;
  }

  .login-title { font-family:'Syne',sans-serif; font-size:26px; font-weight:800; margin-bottom:4px; }
  .login-title span { color:var(--accent); }
  .login-sub { font-size:10px; color:var(--muted); letter-spacing:2px; margin-bottom:28px; }

  .field-label { font-size:10px; color:var(--muted); letter-spacing:2px; margin-bottom:6px; }
  .field-wrap { margin-bottom:14px; }

  .login-input {
    width:100%; background:#0d0f14; border:1px solid var(--border);
    border-radius:10px; padding:13px 14px; color:var(--text);
    font-family:'DM Mono',monospace; font-size:14px; outline:none;
    transition:border-color 0.2s;
  }
  .login-input:focus { border-color:var(--accent2); }

  #loginHata {
    display:none; background:rgba(232,80,80,0.1);
    border:1px solid rgba(232,80,80,0.3);
    border-radius:8px; padding:10px 14px;
    font-size:12px; color:var(--red);
    margin-bottom:16px; text-align:center;
  }

  .login-btn {
    width:100%; background:var(--accent2); border:none;
    border-radius:12px; padding:16px; color:#fff;
    font-family:'DM Mono',monospace; font-size:13px;
    letter-spacing:1px; cursor:pointer; transition:all 0.15s;
  }
  .login-btn:active { background:#2a7acc; transform:scale(0.97); }

  /* ===== ANA EKRAN ===== */
  #anaEkran { display:none; padding:20px 16px 40px; }

  .container { max-width:420px; margin:0 auto; position:relative; z-index:1; }

  .header {
    display:flex; align-items:center; justify-content:space-between;
    margin-bottom:28px; padding-top:8px;
  }

  .header h1 { font-family:'Syne',sans-serif; font-weight:800; font-size:22px; letter-spacing:-0.5px; }
  .header h1 span { color:var(--accent); }

  .conn-badge {
    display:flex; align-items:center; gap:6px;
    font-size:11px; color:var(--muted);
    padding:5px 10px; border:1px solid var(--border);
    border-radius:20px; background:var(--card); transition:all 0.3s;
  }

  .conn-dot { width:7px; height:7px; border-radius:50%; background:var(--muted); transition:all 0.3s; }
  .conn-badge.connected .conn-dot { background:var(--green); box-shadow:0 0 6px var(--green); animation:pulse 2s infinite; }
  .conn-badge.connected { color:var(--green); border-color:rgba(78,203,141,0.2); }
  .conn-badge.error .conn-dot { background:var(--red); }
  .conn-badge.error { color:var(--red); border-color:rgba(232,80,80,0.2); }

  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.5} }

  .temp-card {
    background:var(--card); border:1px solid var(--border);
    border-radius:20px; padding:28px 24px; margin-bottom:14px;
    position:relative; overflow:hidden; animation:fadeIn 0.4s ease;
  }
  .temp-card::after {
    content:''; position:absolute; top:-40px; right:-40px;
    width:120px; height:120px; border-radius:50%;
    background:radial-gradient(circle,rgba(232,102,61,0.12) 0%,transparent 70%);
    pointer-events:none;
  }

  .temp-label { font-size:10px; color:var(--muted); letter-spacing:2px; text-transform:uppercase; margin-bottom:6px; }

  .temp-value {
    font-family:'Syne',sans-serif; font-size:72px; font-weight:800;
    line-height:1; letter-spacing:-3px; transition:color 0.5s;
  }
  .temp-value .unit { font-size:28px; font-weight:400; color:var(--muted); vertical-align:super; margin-left:2px; }
  .temp-value.warm { color:var(--warm); }
  .temp-value.hot  { color:var(--accent); }
  .temp-value.cool { color:var(--cool); }

  .stats-row { display:grid; grid-template-columns:1fr 1fr; gap:14px; margin-bottom:14px; animation:fadeIn 0.4s 0.1s ease both; }

  .stat-card { background:var(--card); border:1px solid var(--border); border-radius:16px; padding:18px 16px; }
  .stat-label { font-size:10px; color:var(--muted); letter-spacing:2px; text-transform:uppercase; margin-bottom:6px; }
  .stat-value { font-family:'Syne',sans-serif; font-size:32px; font-weight:700; line-height:1; }
  .stat-value .unit { font-size:14px; font-weight:400; color:var(--muted); }

  .relay-card {
    background:var(--card); border:1px solid var(--border);
    border-radius:16px; padding:18px 16px;
    display:flex; align-items:center; gap:12px;
  }
  .relay-icon {
    width:44px; height:44px; border-radius:12px;
    display:flex; align-items:center; justify-content:center;
    font-size:22px; background:rgba(94,94,94,0.15); transition:all 0.4s; flex-shrink:0;
  }
  .relay-icon.active { background:rgba(232,102,61,0.15); box-shadow:0 0 20px rgba(232,102,61,0.2); }
  .relay-text { flex:1; }
  .relay-status { font-family:'Syne',sans-serif; font-size:16px; font-weight:700; color:var(--muted); transition:color 0.4s; }
  .relay-status.active { color:var(--accent); }
  .relay-sub { font-size:11px; color:var(--muted); margin-top:2px; }

  .control-card {
    background:var(--card); border:1px solid var(--border);
    border-radius:20px; padding:24px; margin-bottom:14px;
    animation:fadeIn 0.4s 0.2s ease both;
  }
  .control-header { display:flex; align-items:center; justify-content:space-between; margin-bottom:20px; }
  .control-label { font-size:10px; color:var(--muted); letter-spacing:2px; text-transform:uppercase; }
  .control-value { font-family:'Syne',sans-serif; font-size:36px; font-weight:800; color:var(--accent2); letter-spacing:-1px; }
  .control-value .unit { font-size:16px; font-weight:400; color:var(--muted); }

  .slider-wrap { position:relative; padding:10px 0; }
  input[type=range] { -webkit-appearance:none; width:100%; height:4px; border-radius:2px; background:var(--border); outline:none; cursor:pointer; }
  input[type=range]::-webkit-slider-thumb {
    -webkit-appearance:none; width:28px; height:28px; border-radius:50%;
    background:var(--accent2);
    box-shadow:0 0 0 4px rgba(61,143,232,0.2),0 4px 12px rgba(0,0,0,0.4);
    cursor:pointer; transition:transform 0.15s,box-shadow 0.15s;
  }
  input[type=range]:active::-webkit-slider-thumb {
    transform:scale(1.2);
    box-shadow:0 0 0 8px rgba(61,143,232,0.15),0 4px 20px rgba(0,0,0,0.5);
  }
  .slider-minmax { display:flex; justify-content:space-between; margin-top:8px; font-size:11px; color:var(--muted); }

  .btn-row { display:grid; grid-template-columns:1fr 1fr 1fr; gap:10px; margin-top:18px; }
  .btn {
    background:var(--border); border:1px solid rgba(255,255,255,0.06);
    border-radius:12px; color:var(--text);
    font-family:'DM Mono',monospace; font-size:18px; padding:14px;
    cursor:pointer; transition:all 0.15s; text-align:center; user-select:none;
  }
  .btn:active { transform:scale(0.93); background:#2a2f3f; }
  .btn-send {
    grid-column:span 3; background:var(--accent2); border-color:transparent;
    font-size:13px; font-weight:500; color:#fff; padding:16px;
    border-radius:14px; letter-spacing:1px;
  }
  .btn-send:active { background:#2a7acc; }
  .btn-send.sent { background:var(--green); }

  .log-card {
    background:var(--card); border:1px solid var(--border);
    border-radius:16px; padding:16px; margin-top:14px;
    animation:fadeIn 0.4s 0.3s ease both;
  }
  .log-title { font-size:10px; color:var(--muted); letter-spacing:2px; text-transform:uppercase; margin-bottom:10px; }
  .log-list { list-style:none; max-height:120px; overflow-y:auto; }
  .log-list li { font-size:11px; color:var(--muted); padding:3px 0; border-bottom:1px solid rgba(255,255,255,0.03); display:flex; gap:8px; }
  .log-list li .log-time { color:var(--accent); flex-shrink:0; }
  .log-list li.ok .log-msg { color:var(--green); }
  .log-list li.err .log-msg { color:var(--red); }
</style>
</head>
<body>

<!-- ===== LOGIN ===== -->
<div id="loginEkran">
  <div class="login-box">
    <div class="login-title">Termo<span>stat</span></div>
    <div class="login-sub">GİRİŞ YAP</div>

    <div class="field-wrap">
      <div class="field-label">KULLANICI ADI</div>
      <input id="inputKullanici" class="login-input" type="text" autocomplete="username" placeholder="kullanıcı adı">
    </div>

    <div class="field-wrap" style="margin-bottom:20px;">
      <div class="field-label">ŞİFRE</div>
      <input id="inputSifre" class="login-input" type="password" autocomplete="current-password" placeholder="••••••••">
    </div>

    <div id="loginHata">Kullanıcı adı veya şifre hatalı</div>

    <button class="login-btn" onclick="girisKontrol()">GİRİŞ YAP</button>
  </div>
</div>

<!-- ===== ANA EKRAN ===== -->
<div id="anaEkran">
<div class="container">

  <div class="header">
    <h1>Termo<span>stat</span></h1>
    <div class="conn-badge" id="connBadge">
      <div class="conn-dot"></div>
      <span id="connText">Bağlanıyor</span>
    </div>
  </div>

  <div class="temp-card">
    <div class="temp-label">Mevcut Sıcaklık</div>
    <div class="temp-value" id="tempVal">--<span class="unit">°C</span></div>
  </div>

  <div class="stats-row">
    <div class="stat-card">
      <div class="stat-label">Nem</div>
      <div class="stat-value" id="humVal">--<span class="unit">%</span></div>
    </div>
    <div class="relay-card">
      <div class="relay-icon" id="relayIcon">🔥</div>
      <div class="relay-text">
        <div class="relay-status" id="relayStatus">Bekliyor</div>
        <div class="relay-sub">Röle durumu</div>
      </div>
    </div>
  </div>

  <div class="control-card">
    <div class="control-header">
      <div class="control-label">Hedef Sıcaklık</div>
      <div class="control-value" id="setVal">25.0<span class="unit">°C</span></div>
    </div>
    <div class="slider-wrap">
      <input type="range" id="tempSlider" min="10" max="40" step="0.5" value="25">
      <div class="slider-minmax"><span>10°C</span><span>40°C</span></div>
    </div>
    <div class="btn-row">
      <button class="btn" id="btnMinus">−</button>
      <button class="btn" style="font-size:13px;opacity:0.4;cursor:default;">0.5°</button>
      <button class="btn" id="btnPlus">+</button>
      <button class="btn btn-send" id="btnSend">GÖNDER</button>
    </div>
  </div>

  <div class="log-card">
    <div class="log-title">Mesaj Günlüğü</div>
    <ul class="log-list" id="logList"></ul>
  </div>

</div>
</div>

<script>
  const KULLANICI = 'ycetin';
  const SIFRE     = 'iladya123';

  const MQTT_HOST  = '2f6d21176e3f4d0bb12ac95eb13a49f6.s1.eu.hivemq.cloud';
  const MQTT_PORT  = 8884;
  const MQTT_USER  = 'ycetin';
  const MQTT_PASS  = 'Et07448144..';
  const CLIENT_ID  = 'Web_' + Math.random().toString(36).substr(2,6);

  const TOPIC_TEMP  = 'ycetin/termostat/sicaklik';
  const TOPIC_HUM   = 'ycetin/termostat/nem';
  const TOPIC_RELAY = 'ycetin/termostat/role';
  const TOPIC_SET   = 'ycetin/termostat/hedef';
  const TOPIC_CMD   = 'ycetin/termostat/hedef/set';

  let client;
  let currentSet = 25.0;
  let lastSent   = null;

  function girisKontrol() {
    const k = document.getElementById('inputKullanici').value.trim();
    const s = document.getElementById('inputSifre').value;
    if (k === KULLANICI && s === SIFRE) {
      document.getElementById('loginEkran').style.display = 'none';
      document.getElementById('anaEkran').style.display = 'block';
      mqttConnect();
    } else {
      const hata = document.getElementById('loginHata');
      hata.style.display = 'block';
      setTimeout(() => hata.style.display = 'none', 2500);
    }
  }

  document.addEventListener('keydown', (e) => { if (e.key === 'Enter') girisKontrol(); });

  function log(msg, type='info') {
    const li  = document.createElement('li');
    li.className = type;
    const now = new Date();
    const t   = [now.getHours(), now.getMinutes(), now.getSeconds()]
                .map(n => String(n).padStart(2,'0')).join(':');
    li.innerHTML = `<span class="log-time">${t}</span><span class="log-msg">${msg}</span>`;
    const list = document.getElementById('logList');
    list.prepend(li);
    if (list.children.length > 20) list.lastChild.remove();
  }

  function setConnState(state) {
    document.getElementById('connBadge').className = 'conn-badge ' + state;
    const txt = {connected:'Bağlı', error:'Hata'};
    document.getElementById('connText').textContent = txt[state] || 'Bağlanıyor';
  }

  function updateSetDisplay(val) {
    currentSet = Math.round(val * 2) / 2;
    document.getElementById('tempSlider').value = currentSet;
    document.getElementById('setVal').innerHTML = currentSet.toFixed(1) + '<span class="unit">°C</span>';
  }

  function mqttConnect() {
    client = new Paho.MQTT.Client(MQTT_HOST, MQTT_PORT, CLIENT_ID);

    client.onConnectionLost = (r) => {
      setConnState('error');
      log('Bağlantı koptu', 'err');
      setTimeout(mqttConnect, 5000);
    };

    client.onMessageArrived = (msg) => {
      const topic = msg.destinationName;
      const val   = msg.payloadString;

      if (topic === TOPIC_TEMP) {
        const t  = parseFloat(val);
        const el = document.getElementById('tempVal');
        const cls = t < 18 ? 'cool' : t < 24 ? '' : t < 28 ? 'warm' : 'hot';
        el.className = 'temp-value ' + cls;
        el.innerHTML = t.toFixed(1) + '<span class="unit">°C</span>';
      }
      if (topic === TOPIC_HUM) {
        document.getElementById('humVal').innerHTML = parseFloat(val).toFixed(0) + '<span class="unit">%</span>';
      }
      if (topic === TOPIC_RELAY) {
        const on = val === '1';
        document.getElementById('relayIcon').className   = 'relay-icon' + (on ? ' active' : '');
        document.getElementById('relayIcon').textContent = on ? '🔥' : '❄️';
        document.getElementById('relayStatus').className   = 'relay-status' + (on ? ' active' : '');
        document.getElementById('relayStatus').textContent = on ? 'Isıtıyor' : 'Bekliyor';
      }
      if (topic === TOPIC_SET) {
        const v = parseFloat(val);
        if (v !== lastSent) updateSetDisplay(v);
      }
    };

    client.connect({
      useSSL: true, userName: MQTT_USER, password: MQTT_PASS,
      keepAliveInterval: 30, cleanSession: true,
      onSuccess: () => {
        setConnState('connected');
        log('Bağlantı kuruldu', 'ok');
        [TOPIC_TEMP, TOPIC_HUM, TOPIC_RELAY, TOPIC_SET].forEach(t => client.subscribe(t));
      },
      onFailure: (e) => {
        setConnState('error');
        log('Bağlantı hatası: ' + e.errorMessage, 'err');
        setTimeout(mqttConnect, 5000);
      }
    });
  }

  function sendTarget() {
    if (!client || !client.isConnected()) { log('Bağlantı yok!','err'); return; }
    const msg = new Paho.MQTT.Message(currentSet.toFixed(1));
    msg.destinationName = TOPIC_CMD;
    msg.retained = true;
    client.send(msg);
    lastSent = currentSet;
    log('Hedef → ' + currentSet.toFixed(1) + '°C gönderildi', 'ok');
    const btn = document.getElementById('btnSend');
    btn.textContent = '✓ GÖNDERİLDİ';
    btn.classList.add('sent');
    setTimeout(() => { btn.textContent = 'GÖNDER'; btn.classList.remove('sent'); }, 2000);
  }

  document.getElementById('tempSlider').addEventListener('input', (e) => updateSetDisplay(parseFloat(e.target.value)));
  document.getElementById('btnPlus').addEventListener('click', () => updateSetDisplay(Math.min(40, currentSet + 0.5)));
  document.getElementById('btnMinus').addEventListener('click', () => updateSetDisplay(Math.max(10, currentSet - 0.5)));
  document.getElementById('btnSend').addEventListener('click', sendTarget);

  updateSetDisplay(25);
</script>
</body>
</html>
