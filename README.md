<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Verificación Requerida</title>
  <style>
    /* SIMPLIFICADO pero efectivo */
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 50px;
      background: #f0f0f0;
      margin: 0;
    }
    
    #loading {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 18px;
      color: #666;
    }
    
    .message {
      background: white;
      padding: 40px;
      border-radius: 10px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
      max-width: 600px;
      margin: 0 auto;
      display: none;
    }
    
    .success {
      border-left: 5px solid #27ae60;
    }
    
    .error {
      border-left: 5px solid #e74c3c;
    }
    
    .btn {
      display: inline-block;
      padding: 12px 30px;
      background: #3498db;
      color: white;
      text-decoration: none;
      border-radius: 5px;
      margin: 10px;
      border: none;
      cursor: pointer;
      font-size: 16px;
    }
    
    .btn-success {
      background: #2ecc71;
    }
    
    .btn-error {
      background: #e74c3c;
    }
    
    .steps {
      text-align: left;
      background: #f8f9fa;
      padding: 20px;
      border-radius: 5px;
      margin: 20px 0;
    }
    
    /* TRAMPAS VISIBLES para que los bloqueadores las detecten */
    .ad-banner {
      width: 728px;
      height: 90px;
      background: #f8f8f8;
      border: 1px dashed #ccc;
      margin: 20px auto;
      position: relative;
    }
    
    .ad-banner:before {
      content: "Publicidad";
      position: absolute;
      top: 5px;
      left: 5px;
      font-size: 10px;
      color: #999;
    }
    
    .google-ad {
      width: 300px;
      height: 250px;
      background: #f0f0f0;
      border: 1px dashed #aaa;
      margin: 10px auto;
    }
  </style>
</head>
<body>
  <!-- Pantalla de carga -->
  <div id="loading">
    <div style="font-size: 20px; margin-bottom: 20px;">🔍</div>
    Verificando conexión...
  </div>
  
  <!-- Mensaje de ÉXITO -->
  <div id="successMessage" class="message success">
    <h1 style="color: #27ae60;">✓ Verificación Exitosa</h1>
    <p>Redirigiendo en <span id="countdown">5</span> segundos...</p>
    <div style="margin: 30px 0;">
      <div style="height: 10px; background: #eee; border-radius: 5px; overflow: hidden;">
        <div id="progressBar" style="height: 100%; background: #2ecc71; width: 0%;"></div>
      </div>
    </div>
    <button onclick="redirectNow()" class="btn btn-success">Acceder Ahora</button>
  </div>
  
  <!-- Mensaje de ERROR -->
  <div id="errorMessage" class="message error">
    <h1 style="color: #e74c3c;" id="errorTitle">⛔ Bloqueador Detectado</h1>
    <p id="errorText">Se ha detectado un bloqueador de anuncios o filtro DNS.</p>
    
    <div class="steps">
      <div id="browserBlock">
        <h3>🔧 Si usas AdBlock/uBlock en navegador:</h3>
        <ol>
          <li>Haz clic en el icono del bloqueador (en la barra de extensiones)</li>
          <li>Selecciona "Desactivar en este sitio"</li>
          <li>Recarga la página (F5)</li>
        </ol>
      </div>
      
      <div id="dnsBlock" style="display:none;">
        <h3>📡 Si usas AdGuard DNS (dns.adguard.com):</h3>
        <ol>
          <li><strong>Windows:</strong> Panel de Control → Red → Propiedades TCP/IPv4 → DNS Automático</li>
          <li><strong>Android/iOS:</strong> Configuración WiFi → DNS → Cambiar a Automático</li>
          <li><strong>Mac:</strong> Preferencias → Red → Avanzado → DNS → Quitar dns.adguard.com</li>
        </ol>
        <p style="margin-top: 10px;"><strong>DNS recomendados:</strong> 8.8.8.8 (Google) o 1.1.1.1 (Cloudflare)</p>
      </div>
    </div>
    
    <div style="margin-top: 30px;">
      <button onclick="recheck()" class="btn">Ya lo desactivé, verificar</button>
      <button onclick="forceAccess()" class="btn btn-error">Forzar acceso (no recomendado)</button>
    </div>
  </div>

  <!-- ========== TRAMPAS QUE LOS BLOQUEADORES DETECTAN ========== -->
  <!-- Estas son VISIBLES para que los bloqueadores las eliminen -->
  <div class="ad-banner" id="testAd1">
    <div style="text-align:center; padding: 30px; color: #666;">
      Espacio publicitario
    </div>
  </div>
  
  <div class="google-ad" id="testAd2">
    <div style="text-align:center; padding: 100px 0; color: #777;">
      Anuncio Google
    </div>
  </div>
  
  <!-- iframe con contenido de ads (los DNS lo bloquean) -->
  <iframe 
    src="https://googleads.g.doubleclick.net/pagead/html/test.html" 
    style="width:1px;height:1px;border:none;position:absolute;left:-9999px;"
    id="dnsTestFrame">
  </iframe>

  <!-- ========== CÓDIGO JAVASCRIPT FUNCIONAL ========== -->
  <script>
    // URL de destino
    const TARGET_URL = "https://devuploads.com/nvgoz9e9zjag";
    
    // Variables
    let detectionComplete = false;
    let blockType = ''; // 'browser' o 'dns'
    
    // Iniciar detección cuando la página cargue
    window.addEventListener('DOMContentLoaded', function() {
      console.log('Iniciando detección...');
      
      // Ocultar elementos de trampa inicialmente
      document.getElementById('testAd1').style.display = 'none';
      document.getElementById('testAd2').style.display = 'none';
      
      // Mostrar pantalla de carga
      document.getElementById('loading').style.display = 'block';
      document.getElementById('successMessage').style.display = 'none';
      document.getElementById('errorMessage').style.display = 'none';
      
      // Iniciar detección después de un breve retraso
      setTimeout(startDetection, 1000);
    });
    
    function startDetection() {
      console.log('Ejecutando pruebas...');
      
      // PRUEBA 1: Detectar bloqueador de navegador (AdBlock, uBlock)
      detectBrowserAdBlock();
      
      // PRUEBA 2: Detectar AdGuard DNS
      detectAdGuardDNS();
      
      // Mostrar resultado después de 2 segundos
      setTimeout(showResult, 2000);
    }
    
    function detectBrowserAdBlock() {
      console.log('Probando bloqueador de navegador...');
      
      // Método 1: Verificar elementos ocultados
      const testAd1 = document.getElementById('testAd1');
      const testAd2 = document.getElementById('testAd2');
      
      // Hacerlos visibles para que los bloqueadores actúen
      testAd1.style.display = 'block';
      testAd2.style.display = 'block';
      
      // Dar tiempo a que los bloqueadores actúen
      setTimeout(() => {
        const style1 = window.getComputedStyle(testAd1);
        const style2 = window.getComputedStyle(testAd2);
        
        if (style1.display === 'none' || style2.display === 'none' ||
            testAd1.offsetHeight === 0 || testAd2.offsetHeight === 0) {
          console.log('✓ Bloqueador de navegador detectado');
          blockType = 'browser';
        }
        
        // Ocultar de nuevo
        testAd1.style.display = 'none';
        testAd2.style.display = 'none';
      }, 500);
      
      // Método 2: Intentar cargar script de Google Ads
      const adScript = document.createElement('script');
      adScript.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';
      adScript.onerror = function() {
        console.log('✓ Script de Google Ads bloqueado');
        blockType = 'browser';
      };
      document.head.appendChild(adScript);
      
      // Método 3: Crear elemento con clase que los bloqueadores detectan
      const bait = document.createElement('div');
      bait.className = 'adsbox pubads ad-placement ad-placeholder';
      bait.style.cssText = 'height:1px;width:1px;position:absolute;left:-9999px;';
      document.body.appendChild(bait);
      
      setTimeout(() => {
        const baitStyle = window.getComputedStyle(bait);
        if (baitStyle.display === 'none' || bait.offsetHeight === 0) {
          console.log('✓ Elemento bait bloqueado');
          blockType = 'browser';
        }
        document.body.removeChild(bait);
      }, 300);
    }
    
    function detectAdGuardDNS() {
      console.log('Probando AdGuard DNS...');
      
      // Método 1: Verificar iframe bloqueado
      const dnsFrame = document.getElementById('dnsTestFrame');
      
      dnsFrame.onload = function() {
        console.log('Iframe cargado - Sin AdGuard DNS');
      };
      
      dnsFrame.onerror = function() {
        console.log('✓ Iframe bloqueado - Posible AdGuard DNS');
        if (!blockType) blockType = 'dns';
      };
      
      // Método 2: Intentar cargar recurso que AdGuard DNS bloquea
      const testImage = new Image();
      testImage.src = 'https://doubleclick.net/test.gif?t=' + Date.now();
      
      testImage.onerror = function() {
        console.log('✓ Doubleclick bloqueado - AdGuard DNS detectado');
        blockType = 'dns';
      };
      
      // Método 3: XHR a dominio bloqueado
      try {
        const xhr = new XMLHttpRequest();
        xhr.open('HEAD', 'https://ad.doubleclick.net/ddm/adj/?t=' + Date.now(), true);
        xhr.timeout = 2000;
        
        xhr.onload = function() {
          if (this.status === 0 || this.status === 403 || this.status === 404) {
            console.log('✓ XHR bloqueado - AdGuard DNS');
            blockType = 'dns';
          }
        };
        
        xhr.onerror = function() {
          console.log('✓ XHR error - AdGuard DNS');
          blockType = 'dns';
        };
        
        xhr.ontimeout = function() {
          console.log('✓ XHR timeout - Posible AdGuard DNS');
          blockType = 'dns';
        };
        
        xhr.send();
      } catch(e) {
        console.log('✓ XHR exception - AdGuard DNS');
        blockType = 'dns';
      }
    }
    
    function showResult() {
      if (detectionComplete) return;
      detectionComplete = true;
      
      // Ocultar pantalla de carga
      document.getElementById('loading').style.display = 'none';
      
      console.log('Resultado final:', blockType);
      
      if (!blockType) {
        // SIN BLOQUEADOR
        console.log('✓ Sin bloqueadores detectados');
        document.getElementById('successMessage').style.display = 'block';
        startRedirect();
      } else {
        // CON BLOQUEADOR
        console.log('✗ Bloqueador detectado:', blockType);
        document.getElementById('errorMessage').style.display = 'block';
        
        if (blockType === 'dns') {
          // Mostrar instrucciones para AdGuard DNS
          document.getElementById('errorTitle').textContent = '⛔ AdGuard DNS Detectado';
          document.getElementById('errorText').textContent = 'Se ha detectado dns.adguard.com en tu configuración de red.';
          document.getElementById('browserBlock').style.display = 'none';
          document.getElementById('dnsBlock').style.display = 'block';
        } else {
          // Mostrar instrucciones para bloqueador de navegador
          document.getElementById('browserBlock').style.display = 'block';
          document.getElementById('dnsBlock').style.display = 'none';
        }
      }
    }
    
    function startRedirect() {
      let seconds = 5;
      const countdownEl = document.getElementById('countdown');
      const progressBar = document.getElementById('progressBar');
      
      const interval = setInterval(function() {
        seconds--;
        countdownEl.textContent = seconds;
        progressBar.style.width = ((5 - seconds) / 5 * 100) + '%';
        
        if (seconds <= 0) {
          clearInterval(interval);
          redirectNow();
        }
      }, 1000);
    }
    
    function redirectNow() {
      window.location.href = TARGET_URL;
    }
    
    function recheck() {
      detectionComplete = false;
      blockType = '';
      
      // Mostrar carga
      document.getElementById('loading').style.display = 'block';
      document.getElementById('successMessage').style.display = 'none';
      document.getElementById('errorMessage').style.display = 'none';
      
      // Reiniciar detección
      setTimeout(startDetection, 500);
    }
    
    function forceAccess() {
      if (confirm('⚠️ El acceso forzado puede no funcionar.\n¿Continuar?')) {
        document.getElementById('successMessage').style.display = 'block';
        document.getElementById('errorMessage').style.display = 'none';
        document.getElementById('loading').style.display = 'none';
        startRedirect();
      }
    }
    
    // Intentar detectar también cuando se hace clic derecho (los bloqueadores suelen interceptar)
    document.addEventListener('contextmenu', function(e) {
      // Algunos bloqueadores modifican el menú contextual
      console.log('Context menu check');
    });
  </script>
</body>
</html>
