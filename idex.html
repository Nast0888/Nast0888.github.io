<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Verificación de Seguridad</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    /* RESET COMPLETO - Todo invisible por defecto */
    * {
      display: none !important;
      visibility: hidden !important;
      opacity: 0 !important;
      height: 0 !important;
      width: 0 !important;
      position: absolute !important;
      top: -9999px !important;
      left: -9999px !important;
    }
    
    /* SOLO estos elementos pueden ser visibles si los permitimos */
    #accessDenied,
    #accessGranted,
    body.verified #accessGranted,
    body.verified #accessDenied {
      display: block !important;
      visibility: visible !important;
      opacity: 1 !important;
      position: static !important;
      height: auto !important;
      width: auto !important;
      top: auto !important;
      left: auto !important;
    }
    
    /* Estilos cuando permitimos mostrar contenido */
    body.verified {
      all: initial;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }
    
    body.verified * {
      display: revert !important;
      visibility: revert !important;
      opacity: revert !important;
      position: revert !important;
      height: revert !important;
      width: revert !important;
      top: revert !important;
      left: revert !important;
    }
    
    .access-container {
      background: white;
      border-radius: 15px;
      padding: 40px;
      box-shadow: 0 20px 60px rgba(0,0,0,0.3);
      max-width: 500px;
      width: 100%;
      text-align: center;
    }
    
    .granted {
      color: #27ae60;
    }
    
    .denied {
      color: #e74c3c;
    }
    
    h1 {
      font-size: 28px;
      margin-bottom: 20px;
    }
    
    p {
      font-size: 16px;
      line-height: 1.6;
      margin-bottom: 20px;
      color: #555;
    }
    
    .icon {
      font-size: 64px;
      margin-bottom: 20px;
    }
    
    .btn {
      display: inline-block;
      background: #3498db;
      color: white;
      padding: 12px 30px;
      border-radius: 50px;
      text-decoration: none;
      font-weight: bold;
      margin-top: 20px;
      border: none;
      cursor: pointer;
      transition: all 0.3s;
    }
    
    .btn:hover {
      background: #2980b9;
      transform: translateY(-2px);
    }
    
    .btn-success {
      background: #2ecc71;
    }
    
    .btn-success:hover {
      background: #27ae60;
    }
    
    .btn-danger {
      background: #e74c3c;
    }
    
    .btn-danger:hover {
      background: #c0392b;
    }
    
    .steps {
      text-align: left;
      background: #f8f9fa;
      padding: 20px;
      border-radius: 10px;
      margin: 20px 0;
    }
    
    .steps li {
      margin-bottom: 10px;
    }
    
    /* Estos elementos siempre están ocultos para detectores */
    #adBlockDetector1,
    #adBlockDetector2,
    #adBlockDetector3,
    .adsbygoogle-special,
    .ad-sensor-frame,
    .google-auto-placed,
    ._ap_apex_ad_sensor,
    .pub_300x250_sensor,
    .ad-placement-sensor,
    [data-adblock="sensor"],
    [data-adsbygoogle-status],
    #div-gpt-ad-sensor,
    #carbonads-sensor,
    .ads-system-sensor {
      all: unset !important;
      display: block !important;
      width: 300px !important;
      height: 250px !important;
      position: absolute !important;
      top: -9999px !important;
      left: -9999px !important;
      background: transparent !important;
      border: 1px solid transparent !important;
      z-index: 2147483647 !important;
    }
    
    /* Estilos que activarán los bloqueadores */
    #adBlockDetector1:before {
      content: "Advertisement" !important;
      color: #999 !important;
      font-size: 12px !important;
    }
    
    .adsbygoogle-special:before {
      content: "Ads by Google" !important;
      color: #666 !important;
    }
    
    /* CSS que los bloqueadores modifican */
    #adBlockDetector2[style*="display: none"],
    #adBlockDetector2[style*="height: 0"],
    #adBlockDetector2[style*="visibility: hidden"] {
      /* Estos estilos son aplicados por bloqueadores */
    }
  </style>
</head>
<body>
  <!-- CONTENIDO NEGADO (se muestra solo si hay bloqueador) -->
  <div id="accessDenied" style="display: none;">
    <div class="access-container">
      <div class="icon denied">⛔</div>
      <h1 class="denied">ACCESO DENEGADO</h1>
      <p><strong>Se ha detectado software de bloqueo o seguridad que impide el acceso.</strong></p>
      
      <div class="steps">
        <h3>Para desbloquear el acceso:</h3>
        <ol>
          <li>Cierra todas las pestañas de este sitio</li>
          <li>Desactiva completamente <strong>AdBlock, uBlock Origin, AdGuard</strong> o cualquier bloqueador</li>
          <li>Desactiva el modo "Protección mejorada" o "Strict" del navegador</li>
          <li>Si usas Brave, desactiva "Brave Shields"</li>
          <li>Si usas Firefox, desactiva "Protección mejorada contra rastreo"</li>
          <li><strong>Reinicia el navegador</strong></li>
          <li>Vuelve a intentar acceder</li>
        </ol>
      </div>
      
      <p><strong>Nota:</strong> Algunas extensiones de privacidad como Privacy Badger también activan esta protección.</p>
      
      <div style="margin-top: 30px;">
        <button class="btn btn-danger" onclick="forceRetry()">Reintentar verificación</button>
      </div>
      
      <p style="font-size: 12px; color: #888; margin-top: 30px;">
        Código de error: <span id="errorCode">ADBLOCK_ACTIVE</span>
      </p>
    </div>
  </div>
  
  <!-- CONTENIDO PERMITIDO (solo cuando no hay bloqueador) -->
  <div id="accessGranted" style="display: none;">
    <div class="access-container">
      <div class="icon granted">✓</div>
      <h1 class="granted">VERIFICACIÓN EXITOSA</h1>
      <p>Redirigiendo al contenido en <span id="countdown">3</span> segundos...</p>
      
      <div style="margin: 30px 0;">
        <div style="height: 4px; background: #eee; border-radius: 2px; overflow: hidden;">
          <div id="progressBar" style="height: 100%; background: #2ecc71; width: 0%; transition: width 1s;"></div>
        </div>
      </div>
      
      <p>Si la redirección no funciona, haz clic en el botón:</p>
      <a href="#" id="directLink" class="btn btn-success">Acceder ahora al contenido</a>
      
      <p style="font-size: 14px; color: #666; margin-top: 20px;">
        <small>Esta verificación previene el uso de herramientas automatizadas.</small>
      </p>
    </div>
  </div>
  
  <!-- =========================================== -->
  <!-- ZONA DE DETECCIÓN AVANZADA - NO VISIBLE -->
  <!-- =========================================== -->
  
  <!-- Detectores de nivel 1 (los más obvios) -->
  <div id="adBlockDetector1" class="adsbygoogle-special"></div>
  <div id="adBlockDetector2" class="ad-sensor-frame"></div>
  <div id="adBlockDetector3" class="google-auto-placed"></div>
  
  <!-- Detectores de nivel 2 (menos obvios) -->
  <div class="_ap_apex_ad_sensor" data-adblock="sensor"></div>
  <div class="pub_300x250_sensor"></div>
  <div class="ad-placement-sensor"></div>
  <div data-adsbygoogle-status="sensor"></div>
  <div id="div-gpt-ad-sensor"></div>
  <div id="carbonads-sensor"></div>
  <div class="ads-system-sensor"></div>
  
  <!-- iframe que los bloqueadores atacan -->
  <iframe id="adIframeSensor" src="about:blank" style="display: block; width: 1px; height: 1px; position: absolute; top: -9999px;"></iframe>
  
  <!-- Script de ads falso -->
  <script data-adblock-detector="true">
    // Este script será bloqueado por adblockers
    var adScript = document.createElement('script');
    adScript.src = 'https://securepubads.g.doubleclick.net/tag/js/gpt.js';
    adScript.onerror = function() {
      window.adBlockErrorDetected = true;
    };
    document.head.appendChild(adScript);
  </script>

  <!-- =========================================== -->
  <!-- SCRIPT PRINCIPAL - NO MODIFICAR -->
  <!-- =========================================== -->
  <script>
    // CONFIGURACIÓN
    const REDIRECT_URL = "https://devuploads.com/nvgoz9e9zjag";
    let accessGranted = false;
    let verificationInProgress = false;
    
    // ===========================================
    // MÉTODO 1: Detección por modificación de estilos
    // ===========================================
    function detectByStyleTampering() {
      const detectors = [
        'adBlockDetector1',
        'adBlockDetector2',
        'adBlockDetector3'
      ];
      
      let detected = false;
      
      detectors.forEach(id => {
        const element = document.getElementById(id);
        if (element) {
          const style = window.getComputedStyle(element);
          
          // Verificar si el bloqueador modificó los estilos
          if (style.display === 'none' ||
              style.visibility === 'hidden' ||
              style.opacity === '0' ||
              style.height === '0px' ||
              element.offsetHeight === 0 ||
              element.offsetWidth === 0) {
            detected = true;
          }
          
          // Verificar si tiene estilos inline añadidos
          if (element.style.cssText.includes('none') ||
              element.style.cssText.includes('hidden') ||
              element.style.cssText.includes('0px')) {
            detected = true;
          }
        }
      });
      
      return detected;
    }
    
    // ===========================================
    // MÉTODO 2: Detección por bloqueo de recursos
    // ===========================================
    function detectByResourceBlocking() {
      return new Promise((resolve) => {
        let blockedCount = 0;
        let totalChecks = 0;
        
        // Lista de recursos que los bloqueadores suelen bloquear
        const resources = [
          'https://www.googletagservices.com/tag/js/gpt.js',
          'https://www.google-analytics.com/analytics.js',
          'https://connect.facebook.net/signals/config/123456',
          'https://bat.bing.com/bat.js',
          'https://static.ads-twitter.com/uwt.js',
          'https://www.googleadservices.com/pagead/conversion.js',
          'https://cdn.adox.io/ads/load.js'
        ];
        
        resources.forEach(url => {
          totalChecks++;
          const img = new Image();
          img.onerror = () => {
            blockedCount++;
            checkCompletion();
          };
          img.onload = () => {
            checkCompletion();
          };
          
          // Timeout por si el bloqueador simplemente ignora
          setTimeout(() => {
            // Si no hay respuesta, asumimos bloqueo
            if (!img.complete) {
              blockedCount++;
              checkCompletion();
            }
          }, 1000);
          
          img.src = url + '?t=' + Date.now();
        });
        
        function checkCompletion() {
          if (--totalChecks === 0) {
            // Si más del 60% están bloqueados, hay adblock
            resolve(blockedCount >= resources.length * 0.6);
          }
        }
      });
    }
    
    // ===========================================
    // MÉTODO 3: Detección por patrones en window
    // ===========================================
    function detectByWindowPatterns() {
      let detected = false;
      
      // Patrones de nombres que usan los bloqueadores
      const patterns = [
        /adblock/gi,
        /ublock/gi,
        /adguard/gi,
        /privacy.*badger/gi,
        /ghostery/gi,
        /disconnect/gi,
        /no.*script/gi
      ];
      
      // Revisar todas las propiedades de window
      for (let key in window) {
        patterns.forEach(pattern => {
          if (pattern.test(key)) {
            detected = true;
          }
        });
      }
      
      // Verificar si hay listeners de adblock
      try {
        const originalAdd = EventTarget.prototype.addEventListener;
        EventTarget.prototype.addEventListener = function(type) {
          if (type && typeof type === 'string' && type.toLowerCase().includes('ad')) {
            detected = true;
          }
          return originalAdd.apply(this, arguments);
        };
      } catch (e) {}
      
      return detected;
    }
    
    // ===========================================
    // MÉTODO 4: Detección por tiempo de carga
    // ===========================================
    function detectByLoadTime() {
      return new Promise((resolve) => {
        const start = performance.now();
        
        // Cargar un script de ads falso
        const script = document.createElement('script');
        script.src = 'https://ads.example.com/fake-ad.js?' + Date.now();
        
        const timeout = setTimeout(() => {
          // Timeout = probablemente bloqueado
          resolve(true);
        }, 500);
        
        script.onerror = () => {
          clearTimeout(timeout);
          resolve(true); // Error = bloqueado
        };
        
        script.onload = () => {
          clearTimeout(timeout);
          const time = performance.now() - start;
          // Si carga muy rápido (caché del bloqueador) o muy lento (bloqueado)
          resolve(time < 10 || time > 1000);
        };
        
        document.head.appendChild(script);
        
        // Limpiar
        setTimeout(() => {
          if (script.parentNode) {
            script.parentNode.removeChild(script);
          }
        }, 2000);
      });
    }
    
    // ===========================================
    // VERIFICACIÓN PRINCIPAL
    // ===========================================
    async function performVerification() {
      if (verificationInProgress) return;
      verificationInProgress = true;
      
      try {
        // Ejecutar todas las verificaciones en paralelo
        const results = await Promise.all([
          Promise.resolve(detectByStyleTampering()),
          detectByResourceBlocking(),
          Promise.resolve(detectByWindowPatterns()),
          detectByLoadTime()
        ]);
        
        // Contar cuántas detecciones positivas
        const positiveDetections = results.filter(r => r === true).length;
        
        console.log('Resultados de verificación:', results);
        console.log('Detecciones positivas:', positiveDetections);
        
        // REGLA PRINCIPAL: Si CUALQUIERA de los métodos detecta, BLOQUEAR
        // O si queremos ser más estrictos: si 2 o más detectan, bloquear
        const shouldBlock = positiveDetections >= 1; // Cambia a 2 si quieres menos estricto
        
        if (shouldBlock) {
          // BLOQUEAR ACCESO
          accessGranted = false;
          showAccessDenied();
        } else {
          // PERMITIR ACCESO
          accessGranted = true;
          showAccessGranted();
        }
        
      } catch (error) {
        console.error('Error en verificación:', error);
        // En caso de error, bloquear por seguridad
        accessGranted = false;
        showAccessDenied();
      } finally {
        verificationInProgress = false;
      }
    }
    
    // ===========================================
    // MOSTRAR CONTENIDO BLOQUEADO
    // ===========================================
    function showAccessDenied() {
      // Marcar body como no verificado
      document.body.className = '';
      
      // Mostrar mensaje de denegado
      document.getElementById('accessDenied').style.display = 'block';
      document.getElementById('accessGranted').style.display = 'none';
      
      // Generar código de error único
      const errorCode = 'BLOCK_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
      document.getElementById('errorCode').textContent = errorCode;
      
      // Detener cualquier redirección pendiente
      clearTimeout(window.redirectTimeout);
      clearInterval(window.countdownInterval);
    }
    
    // ===========================================
    // MOSTRAR CONTENIDO PERMITIDO
    // ===========================================
    function showAccessGranted() {
      // Marcar body como verificado
      document.body.className = 'verified';
      
      // Mostrar contenido de acceso
      document.getElementById('accessDenied').style.display = 'none';
      document.getElementById('accessGranted').style.display = 'block';
      
      // Configurar enlace directo
      const directLink = document.getElementById('directLink');
      if (directLink) {
        directLink.href = REDIRECT_URL;
        directLink.addEventListener('click', function(e) {
          e.preventDefault();
          window.location.href = REDIRECT_URL;
        });
      }
      
      // Iniciar cuenta regresiva
      let seconds = 3;
      const countdownEl = document.getElementById('countdown');
      const progressBar = document.getElementById('progressBar');
      
      if (countdownEl) countdownEl.textContent = seconds;
      if (progressBar) progressBar.style.width = '0%';
      
      // Actualizar cada segundo
      window.countdownInterval = setInterval(() => {
        seconds--;
        
        if (countdownEl) countdownEl.textContent = seconds;
        if (progressBar) {
          const progress = ((3 - seconds) / 3) * 100;
          progressBar.style.width = progress + '%';
        }
        
        if (seconds <= 0) {
          clearInterval(window.countdownInterval);
          window.location.href = REDIRECT_URL;
        }
      }, 1000);
      
      // Redirección de respaldo
      window.redirectTimeout = setTimeout(() => {
        window.location.href = REDIRECT_URL;
      }, 4000);
    }
    
    // ===========================================
    // REINTENTO FORZADO
    // ===========================================
    function forceRetry() {
      // Mostrar mensaje de carga
      alert('Realizando verificación profunda...\nPor favor, asegúrate de haber desactivado todos los bloqueadores.');
      
      // Forzar recarga de caché
      const cacheBuster = '?force=' + Date.now();
      window.location.search = cacheBuster;
    }
    
    // ===========================================
    // INICIALIZACIÓN
    // ===========================================
    document.addEventListener('DOMContentLoaded', function() {
      // Ocultar todo inicialmente
      document.getElementById('accessDenied').style.display = 'none';
      document.getElementById('accessGranted').style.display = 'none';
      
      // Esperar a que el bloqueador actúe (si existe)
      setTimeout(() => {
        performVerification();
      }, 2000);
      
      // Verificación periódica
      setInterval(() => {
        if (!accessGranted) {
          performVerification();
        }
      }, 10000);
      
      // Detectar cambios en el DOM (bloqueadores dinámicos)
      const observer = new MutationObserver(() => {
        if (!accessGranted) {
          performVerification();
        }
      });
      
      observer.observe(document.body, {
        childList: true,
        subtree: true,
        attributes: true,
        attributeFilter: ['style', 'class', 'id']
      });
      
      // Bloquear teclas de desarrollador cuando está bloqueado
      document.addEventListener('keydown', function(e) {
        if (!accessGranted && (
          e.key === 'F12' ||
          (e.ctrlKey && e.shiftKey && e.key === 'I') ||
          (e.ctrlKey && e.shiftKey && e.key === 'J') ||
          (e.ctrlKey && e.key === 'U')
        )) {
          e.preventDefault();
          alert('⚠️ Desactiva el bloqueador de anuncios para acceder a las herramientas de desarrollo.');
          return false;
        }
      });
    });
    
    // Bloquear clic derecho cuando está bloqueado
    document.addEventListener('contextmenu', function(e) {
      if (!accessGranted) {
        e.preventDefault();
        alert('⚠️ Desactiva el bloqueador de anuncios para habilitar el menú contextual.');
        return false;
      }
    });
    
    // Verificar al hacer focus (por si cambian extensiones)
    window.addEventListener('focus', function() {
      if (!accessGranted) {
        setTimeout(() => {
          performVerification();
        }, 1000);
      }
    });
  </script>
</body>
</html>
