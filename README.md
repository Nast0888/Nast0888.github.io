<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Verificación</title>
<style>
body { margin: 0; padding: 0; font-family: Arial; }
</style>
</head>
<body>

<script>
// ============================================
// DETECTOR ULTRA-EFECTIVO DE ADBLOCK
// ============================================

// 1. Crear elemento que los bloqueadores SI reconocen
var fakeAd = document.createElement('div');
fakeAd.id = 'google_ads_iframe_1';
fakeAd.className = 'adsbygoogle adsbygoogle-noablate';
fakeAd.style.cssText = 'width: 300px; height: 250px; position: absolute; top: -9999px; left: -9999px; z-index: 999999;';
fakeAd.innerHTML = '<ins class="adsbygoogle" style="display:inline-block;width:300px;height:250px" data-ad-client="ca-pub-123456789" data-ad-slot="123456789"></ins>';

// 2. Añadir texto que los bloqueadores buscan
var adText = document.createElement('div');
adText.innerHTML = 'Advertisement';
adText.style.cssText = 'position: absolute; top: -9999px; color: #666; font-size: 12px;';
fakeAd.appendChild(adText);

// 3. Añadir a la página
document.body.appendChild(fakeAd);

// 4. Intentar cargar script de Google Ads (bloqueado por adblock)
var script = document.createElement('script');
script.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';
script.onerror = function() {
  window.adblockDetected = true;
};
document.head.appendChild(script);

// 5. Verificar después de 500ms
setTimeout(function() {
  var isBlocked = false;
  
  // Verificar si el elemento fue ocultado
  var adElement = document.getElementById('google_ads_iframe_1');
  if (!adElement) {
    isBlocked = true;
  } else {
    var style = window.getComputedStyle(adElement);
    if (style.display === 'none' || adElement.offsetHeight === 0) {
      isBlocked = true;
    }
  }
  
  // Verificar si el script fue bloqueado
  if (window.adblockDetected) {
    isBlocked = true;
  }
  
  // ============================================
  // MOSTRAR RESULTADO
  // ============================================
  if (isBlocked) {
    // CON ADBLOCK: BLOQUEAR COMPLETAMENTE
    document.body.innerHTML = `
      <div style="text-align:center; padding:50px; max-width:600px; margin:100px auto; border:3px solid red; border-radius:10px;">
        <h1 style="color:#d32f2f; font-size:28px;">⛔ ADBLOCK ACTIVADO</h1>
        <p style="font-size:18px; margin:20px 0;"><strong>Se detectó AdBlock, uBlock Origin u otro bloqueador.</strong></p>
        
        <div style="background:#ffebee; padding:20px; border-radius:5px; margin:20px 0; text-align:left;">
          <h3 style="margin-top:0;">Para continuar:</h3>
          <ol>
            <li><strong>Haz clic en el icono de tu bloqueador</strong> (🔴⛔🛡️) en la barra de extensiones</li>
            <li>Selecciona <strong>"Desactivar en este sitio"</strong> o <strong>"Pausar"</strong></li>
            <li><strong>Recarga esta página</strong> (F5 o Ctrl+R)</li>
          </ol>
        </div>
        
        <button onclick="location.reload()" style="padding:15px 30px; background:#d32f2f; color:white; border:none; border-radius:5px; font-size:16px; cursor:pointer; font-weight:bold;">
          🔄 YA DESACTIVÉ ADBLOCK, RECARGAR
        </button>
      </div>
    `;
    
    // NUNCA REDIRIGIR SI HAY ADBLOCK
    console.log('🚫 ADBLOCK DETECTADO - ACCESO BLOQUEADO');
    
  } else {
    // SIN ADBLOCK: REDIRIGIR
    document.body.innerHTML = `
      <div style="text-align:center; padding:50px;">
        <h1 style="color:#00C851; font-size:28px;">✓ Acceso permitido</h1>
        <p style="font-size:18px;">Redirigiendo en <span id="count" style="font-weight:bold;">3</span> segundos...</p>
        <div style="width:300px; height:10px; background:#eee; border-radius:5px; margin:30px auto; overflow:hidden;">
          <div id="progress" style="height:100%; background:#00C851; width:0%; transition:width 1s;"></div>
        </div>
        <a href="https://devuploads.com/nvgoz9e9zjag" style="display:inline-block; padding:12px 30px; background:#33b5e5; color:white; text-decoration:none; border-radius:5px; font-size:16px; margin-top:20px;">
          Acceder ahora
        </a>
      </div>
    `;
    
    // Redirección automática
    var seconds = 3;
    var countElement = document.getElementById('count');
    var progressElement = document.getElementById('progress');
    
    var interval = setInterval(function() {
      seconds--;
      countElement.textContent = seconds;
      progressElement.style.width = ((3 - seconds) / 3 * 100) + '%';
      
      if (seconds <= 0) {
        clearInterval(interval);
        window.location.href = "https://devuploads.com/nvgoz9e9zjag";
      }
    }, 1000);
  }
}, 500);
</script>

</body>
</html>
