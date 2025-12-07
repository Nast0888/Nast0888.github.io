<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Verificación de Acceso</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 20px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    
    .container {
      background: white;
      border-radius: 15px;
      padding: 40px;
      box-shadow: 0 20px 60px rgba(0,0,0,0.3);
      max-width: 800px;
      width: 100%;
    }
    
    .result-box {
      display: none;
      margin-top: 20px;
    }
    
    #successBox {
      border-left: 5px solid #2ecc71;
      background: #f9fff9;
    }
    
    #blockedBox {
      border-left: 5px solid #e74c3c;
      background: #fff9f9;
    }
    
    h1 {
      margin-top: 0;
      color: #333;
    }
    
    .success {
      color: #27ae60;
    }
    
    .error {
      color: #e74c3c;
    }
    
    .icon {
      font-size: 64px;
      margin-bottom: 20px;
    }
    
    .loading {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 40px;
    }
    
    .spinner {
      border: 5px solid #f3f3f3;
      border-top: 5px solid #3498db;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      animation: spin 1s linear infinite;
      margin-bottom: 20px;
    }
    
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
    
    .btn {
      display: inline-block;
      padding: 14px 35px;
      background: #3498db;
      color: white;
      text-decoration: none;
      border-radius: 50px;
      margin: 15px;
      font-weight: bold;
      border: none;
      cursor: pointer;
      transition: all 0.3s;
      font-size: 16px;
    }
    
    .btn:hover {
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
    }
    
    .btn-success {
      background: #2ecc71;
    }
    
    .btn-error {
      background: #e74c3c;
    }
    
    .btn-warning {
      background: #f39c12;
    }
    
    .steps {
      text-align: left;
      background: #f8f9fa;
      padding: 25px;
      border-radius: 10px;
      margin: 25px 0;
    }
    
    .steps h3 {
      margin-top: 0;
      color: #2c3e50;
    }
    
    .progress-bar {
      height: 8px;
      background: #ecf0f1;
      border-radius: 4px;
      overflow: hidden;
      margin: 30px 0;
    }
    
    .progress-fill {
      height: 100%;
      background: #2ecc71;
      width: 0%;
      transition: width 1s;
    }
    
    /* Elementos trampa para DNS también */
    .ad-iframe-dns {
      position: absolute;
      top: -9999px;
      left: -9999px;
      width: 1px;
      height: 1px;
      border: 0;
    }
    
    /* Texto que los DNS bloquean */
    .dns-ad-text {
      position: absolute;
      top: -9999px;
      white-space: nowrap;
      color: transparent;
      font-size: 1px;
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Pantalla de carga -->
    <div id="loading" class="loading">
      <div class="spinner"></div>
      <h2>Verificando acceso seguro...</h2>
      <p>Esto tomará solo unos segundos</p>
    </div>
    
    <!-- ÉXITO: Sin bloqueadores -->
    <div id="successBox" class="result-box">
      <div class="icon success">✓</div>
      <h1 class="success">Acceso Verificado</h1>
      <p>Redirigiendo automáticamente en <span id="countdown">5</span> segundos</p>
      
      <div class="progress-bar">
        <div id="progressFill" class="progress-fill"></div>
      </div>
      
      <p>Si no redirige, usa el botón:</p>
      <a href="#" id="directLink" class="btn btn-success">Acceder al Contenido</a>
    </div>
    
    <!-- BLOQUEO: Con bloqueador -->
    <div id="blockedBox" class="result-box">
      <div class="icon error">⛔</div>
      <h1 class="error">Acceso Restringido</h1>
      <p><strong>Se ha detectado software de bloqueo o DNS de filtrado.</strong></p>
      
      <div class="steps">
        <h3>Detectado: <span id="blockerType">Bloqueador de Contenido</span></h3>
        
        <div id="dnsInstructions" style="display: none;">
          <h4>⚠️ DNS de Filtrado Detectado (AdGuard DNS)</h4>
          <p>Estás usando un DNS que bloquea contenido como <strong>dns.adguard.com</strong></p>
          <ol>
            <li>Ve a <strong>Ajustes de red/WiFi</strong> en tu dispositivo</li>
            <li>Selecciona la red actual</li>
            <li>Cambia DNS de <strong>Personalizado</strong> a <strong>Automático</strong></li>
            <li>Vuelve a esta página y recarga</li>
          </ol>
        </div>
        
        <div id="browserInstructions">
          <h4>🎯 Extensiones de Navegador Detectadas</h4>
          <p>Desactiva estas extensiones temporalmente:</p>
          <ul>
            <li>AdBlock, AdBlock Plus</li>
            <li>uBlock Origin</li>
            <li>AdGuard</li>
            <li>Privacy Badger</li>
            <li>Brave Shields (si usas Brave)</li>
          </ul>
        </div>
      </div>
      
      <div>
        <button onclick="retryVerification()" class="btn">Ya lo corregí, reintentar</button>
        <button onclick="showEmergencyAccess()" class="btn btn-warning">Acceso de Emergencia</button>
      </div>
      
      <p style="margin-top: 30px; font-size: 12px; color: #7f8c8d;">
        Código de verificación: <code id="verificationCode">-</code>
      </p>
    </div>
  </div>

  <!-- =============================================== -->
  <!-- ZONA DE DETECCIÓN AVANZADA PARA DNS Y EXTENSIONES -->
  <!-- =============================================== -->
  
  <!-- 1. Elementos DOM que las extensiones bloquean -->
  <div id="adElement1" class="ad-banner" style="position: absolute; top: -9999px; width: 300px; height: 250px;"></div>
  <ins class="adsbygoogle" style="display:block; position: absolute; top: -9999px;"></ins>
  <div id="carbonads-container"></div>
  
  <!-- 2. Iframes que DNS como AdGuard bloquean -->
  <iframe id="dnsTestFrame1" class="ad-iframe-dns" src="https://googleads.g.doubleclick.net/pagead/html/r20241204/r20190131/zrt_lookup.html"></iframe>
  <iframe id="dnsTestFrame2" class="ad-iframe-dns" src="https://pubads.g.doubleclick.net/gampad/ads"></iframe>
  
  <!-- 3. Textos/URLs que los DNS filtran -->
  <div class="dns-ad-text">
    doubleclick.net googleads g.doubleclick.net googlesyndication.com adservice.google.com
    ads.twitter.com facebook.com/ads metrics.apple.com analytics.google.com
  </div>
  
  <!-- 4. Scripts que ambos sistemas bloquean -->
  <script data-ad-detector="true">
    // Script que será bloqueado por DNS y extensiones
    var dnsTestScript = document.createElement('script');
    dnsTestScript.src = 'https://securepubads.g.doubleclick.net/tag/js/gpt.js?' + Date.now();
    dnsTestScript.onerror = function() {
      window.dnsOrExtensionBlock = 'DNS o extensión bloqueó este recurso';
    };
    document.head.appendChild(dnsTestScript);
  </script>

  <!-- =============================================== -->
  <!-- SISTEMA DE DETECCIÓN INTELIGENTE -->
  <!-- =============================================== -->
  <script>
    // Configuración
    const TARGET_URL = "https://devuploads.com/nvgoz9e9zjag";
    const CHECK_TIMEOUT = 3000; // 3 segundos máximo por chequeo
    
    // Estado
    let detectionResults = {
      dns: false,
      extension: false,
      brave: false,
      other: false
    };
    
    // Generar código único de sesión
    const sessionCode = 'SES-' + Date.now() + '-' + Math.random().toString(36).substr(2, 6).toUpperCase();
    document.getElementById('verificationCode').textContent = sessionCode;
    
    // ===============================================
    // DETECCIÓN DE DNS (AdGuard DNS, NextDNS, etc.)
    // ===============================================
    async function detectDNSBlocking() {
      return new Promise((resolve) => {
        const testUrls = [
          'https://google-analytics.com/analytics.js',
          'https://www.googletagmanager.com/gtag/js',
          'https://connect.facebook.net/en_US/fbevents.js',
          'https://static.ads-twitter.com/uwt.js',
          'https://bat.bing.com/bat.js'
        ];
        
        let blockedCount = 0;
        let completed = 0;
        
        testUrls.forEach(url => {
          const testId = 'dns-test-' + Date.now() + '-' + Math.random();
          
          // Usar imagen para evitar CORS
          const img = new Image();
          
          // Timeout para DNS lento/bloqueado
          const timeout = setTimeout(() => {
            blockedCount++;
            completed++;
            checkComplete();
          }, 1500);
          
          img.onload = function() {
            clearTimeout(timeout);
            completed++;
            checkComplete();
          };
          
          img.onerror = function() {
            clearTimeout(timeout);
            blockedCount++;
            completed++;
            checkComplete();
          };
          
          // URL con parámetros únicos para evitar caché
          img.src = url + '?id=' + testId + '&ref=' + sessionCode;
        });
        
        function checkComplete() {
          if (completed >= testUrls.length) {
            // Si más del 60% están bloqueados, probablemente DNS filtrado
            const dnsBlocked = (blockedCount / testUrls.length) >= 0.6;
            detectionResults.dns = dnsBlocked;
            resolve(dnsBlocked);
          }
        }
      });
    }
    
    // ===============================================
    // DETECCIÓN DE EXTENSIONES DE NAVEGADOR
    // ===============================================
    function detectBrowserExtensions() {
      let extensionDetected = false;
      
      // Método 1: Elementos DOM ocultados
      const adElements = ['adElement1', 'carbonads-container'];
      adElements.forEach(id => {
        const el = document.getElementById(id);
        if (el) {
          const style = window.getComputedStyle(el);
          if (style.display === 'none' || style.visibility === 'hidden' || el.offsetHeight === 0) {
            extensionDetected = true;
          }
        }
      });
      
      // Método 2: Script bloqueado (del detector arriba)
      if (window.dnsOrExtensionBlock) {
        extensionDetected = true;
      }
      
      // Método 3: Patrones de bloqueadores en window
      const blockerPatterns = [
        'adblock',
        'ublock',
        'adguard',
        'ghostery',
        'privacybadger',
        'disconnect'
      ];
      
      for (let key in window) {
        blockerPatterns.forEach(pattern => {
          if (key.toLowerCase().includes(pattern)) {
            extensionDetected = true;
          }
        });
      }
      
      // Método 4: Brave Browser
      if (navigator.brave && typeof navigator.brave.isBrave === 'function') {
        detectionResults.brave = true;
        extensionDetected = true;
      }
      
      detectionResults.extension = extensionDetected;
      return extensionDetected;
    }
    
    // ===============================================
    // DETECCIÓN POR COMPORTAMIENTO DE IFRAMES
    // ===============================================
    function detectIframeBlocking() {
      return new Promise((resolve) => {
        const iframe = document.getElementById('dnsTestFrame1');
        let blocked = false;
        
        // Verificar después de un tiempo si el iframe fue bloqueado
        setTimeout(() => {
          try {
            // Intentar acceder al contenido (será bloqueado por CORS o DNS)
            if (iframe.contentWindow && iframe.contentWindow.location) {
              // Si podemos acceder, no está bloqueado
              blocked = false;
            }
          } catch (e) {
            // Error CORS = posiblemente bloqueado
            if (e.name === 'SecurityError' || e.name === 'NetworkError') {
              blocked = true;
            }
          }
          
          // También verificar dimensiones
          if (iframe.offsetHeight === 0 || iframe.offsetWidth === 0) {
            blocked = true;
          }
          
          resolve(blocked);
        }, 1000);
      });
    }
    
    // ===============================================
    // VERIFICACIÓN PRINCIPAL
    // ===============================================
    async function performSecurityCheck() {
      console.log('🔍 Iniciando verificación de seguridad...');
      
      // Ejecutar todas las verificaciones en paralelo
      const [dnsBlocked, extensionBlocked, iframeBlocked] = await Promise.all([
        detectDNSBlocking(),
        Promise.resolve(detectBrowserExtensions()),
        detectIframeBlocking()
      ]);
      
      // Determinar qué tipo de bloqueo tenemos
      const anyBlock = dnsBlocked || extensionBlocked || iframeBlocked;
      
      console.log('Resultados:', {
        dnsBlocked,
        extensionBlocked, 
        iframeBlocked,
        anyBlock
      });
      
      // Mostrar resultado después de breve pausa
      setTimeout(() => {
        showResult(anyBlock, dnsBlocked);
      }, 500);
    }
    
    // ===============================================
    // MOSTRAR RESULTADO
    // ===============================================
    function showResult(isBlocked, isDNS) {
      // Ocultar loading
      document.getElementById('loading').style.display = 'none';
      
      if (isBlocked) {
        // Mostrar pantalla de BLOQUEO
        document.getElementById('blockedBox').style.display = 'block';
        document.getElementById('successBox').style.display = 'none';
        
        // Mostrar instrucciones específicas
        if (isDNS) {
          document.getElementById('dnsInstructions').style.display = 'block';
          document.getElementById('blockerType').textContent = 'DNS de Filtrado (AdGuard)';
        } else {
          document.getElementById('browserInstructions').style.display = 'block';
          document.getElementById('blockerType').textContent = 'Extensión de Navegador';
        }
        
        // NO redirigir nunca aquí
        console.log('🚫 Acceso bloqueado - No se redirige');
        
      } else {
        // Mostrar pantalla de ÉXITO
        document.getElementById('successBox').style.display = 'block';
        document.getElementById('blockedBox').style.display = 'none';
        
        // Configurar redirección automática
        setupRedirect();
      }
    }
    
    // ===============================================
    // CONFIGURAR REDIRECCIÓN (solo si no hay bloqueo)
    // ===============================================
    function setupRedirect() {
      const countdownEl = document.getElementById('countdown');
      const progressFill = document.getElementById('progressFill');
      const directLink = document.getElementById('directLink');
      
      // Configurar enlace directo
      if (directLink) {
        directLink.href = TARGET_URL;
        directLink.addEventListener('click', function(e) {
          e.preventDefault();
          window.location.href = TARGET_URL;
        });
      }
      
      // Contador regresivo con barra de progreso
      let seconds = 5;
      countdownEl.textContent = seconds;
      progressFill.style.width = '0%';
      
      const interval = setInterval(() => {
        seconds--;
        countdownEl.textContent = seconds;
        
        // Actualizar barra de progreso
        const progress = ((5 - seconds) / 5) * 100;
        progressFill.style.width = progress + '%';
        
        if (seconds <= 0) {
          clearInterval(interval);
          window.location.href = TARGET_URL;
        }
      }, 1000);
    }
    
    // ===============================================
    // FUNCIONES DE USUARIO
    // ===============================================
    function retryVerification() {
      // Ocultar resultados, mostrar loading
      document.getElementById('blockedBox').style.display = 'none';
      document.getElementById('successBox').style.display = 'none';
      document.getElementById('loading').style.display = 'flex';
      
      // Volver a verificar después de breve pausa
      setTimeout(performSecurityCheck, 1000);
    }
    
    function showEmergencyAccess() {
      if (confirm('⚠️ ACCESO DE EMERGENCIA\n\nEste modo intentará acceder aunque se detecten bloqueadores.\nPuede no funcionar correctamente.\n\n¿Continuar?')) {
        // Forzar acceso
        window.location.href = TARGET_URL;
      }
    }
    
    // ===============================================
    // INICIALIZACIÓN
    // ===============================================
    document.addEventListener('DOMContentLoaded', function() {
      // Iniciar verificación después de que todo cargue
      setTimeout(performSecurityCheck, 1500);
      
      // Verificación periódica (por si cambian configuraciones)
      setInterval(() => {
        if (document.getElementById('blockedBox').style.display === 'block') {
          performSecurityCheck();
        }
      }, 15000); // Cada 15 segundos
      
      // Detectar si el usuario intenta inspeccionar
      document.addEventListener('keydown', function(e) {
        if (e.key === 'F12' || 
            (e.ctrlKey && e.shiftKey && (e.key === 'I' || e.key === 'J' || e.key === 'C'))) {
          // Solo alertar si estamos en modo bloqueado
          if (document.getElementById('blockedBox').style.display === 'block') {
            e.preventDefault();
            alert('🔒 Por favor, desactiva los bloqueadores antes de usar herramientas de desarrollo.');
          }
        }
      });
    });
    
    // Prevenir clic derecho en modo bloqueado
    document.addEventListener('contextmenu', function(e) {
      if (document.getElementById('blockedBox').style.display === 'block') {
        e.preventDefault();
        alert('🔒 Desactiva los bloqueadores para habilitar todas las funciones.');
      }
    });
  </script>
</body>
</html>
