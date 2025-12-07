<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Acceso al contenido</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      padding: 50px;
      background: #f5f5f5;
    }
    
    .container {
      max-width: 800px;
      margin: 0 auto;
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 0 20px rgba(0,0,0,0.1);
    }
    
    #normalAccess {
      display: none;
      color: green;
    }
    
    #blockedAccess {
      display: none;
      color: #d32f2f;
      border-left: 5px solid #d32f2f;
      padding: 20px;
      background: #ffebee;
      text-align: left;
    }
    
    #blockedAccess h2 {
      margin-top: 0;
    }
    
    .instructions {
      background: #fff8e1;
      padding: 15px;
      border-radius: 5px;
      margin: 20px 0;
    }
    
    button {
      background: #1976d2;
      color: white;
      border: none;
      padding: 12px 24px;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
      margin: 10px;
    }
    
    button:hover {
      background: #1565c0;
    }
    
    button#forceAccess {
      background: #388e3c;
    }
    
    /* ESTILOS INVISIBLES PARA TRAMPAS - NO MODIFICAR */
    .adsbygoogle-noablate,
    .pub_300x250,
    .ad-placement,
    ._ap_apex_ad,
    .advertising-notice,
    .ad-unit,
    .ads-system,
    .ad-container,
    #div-gpt-ad,
    #ad-wrapper,
    [data-ad-status="unfilled"],
    [data-adblockdetector="true"] {
      display: block !important;
      position: absolute !important;
      top: -9999px !important;
      left: -9999px !important;
      width: 1px !important;
      height: 1px !important;
      overflow: hidden !important;
      opacity: 0.001 !important;
      pointer-events: none !important;
      z-index: -9999 !important;
    }
    
    /* Una trampa que parece real */
    #carbon-ads {
      width: 300px !important;
      height: 250px !important;
      background: transparent !important;
      border: none !important;
    }
  </style>
</head>
<body>
  <div class="container">
    
    <!-- ESTE CONTENIDO SE MUESTRA SOLO SIN BLOQUEADOR -->
    <div id="normalAccess">
      <h1>✓ Acceso permitido</h1>
      <p>Redirigiendo a la descarga en <span id="countdown">5</span> segundos...</p>
      <div class="instructions">
        <p><strong>Enlace directo:</strong> <a href="#" id="directLink">Haz clic aquí si no redirige automáticamente</a></p>
      </div>
    </div>
    
    <!-- ESTE CONTENIDO SE MUESTRA CON BLOQUEADOR -->
    <div id="blockedAccess">
      <h2>⛔ ACCESO BLOQUEADO</h2>
      <p><strong>Se ha detectado software de bloqueo de anuncios o seguridad.</strong></p>
      
      <div class="instructions">
        <h3>Para continuar, necesitas:</h3>
        <ol>
          <li><strong>Desactivar completamente</strong> AdBlock, uBlock Origin, uMatrix, AdGuard o cualquier extensión similar</li>
          <li><strong>Recargar esta página</strong> después de desactivarlo</li>
          <li>O intentar acceder desde otro navegador sin extensiones de bloqueo</li>
        </ol>
        
        <p><strong>Nota:</strong> Algunos navegadores como Brave o Firefox con protecciones estrictas también activan esta detección.</p>
      </div>
      
      <div>
        <button onclick="location.reload()">Ya desactivé el bloqueador, recargar</button>
        <button id="forceAccess">Intentar acceso forzado</button>
      </div>
      
      <p style="font-size: 12px; margin-top: 20px; color: #666;">
        Este sitio requiere desactivar bloqueadores para garantizar la sostenibilidad del servicio.
      </p>
    </div>
    
  </div>

  <!-- ============================================= -->
  <!-- ZONA DE TRAMPAS PARA BLOQUEADORES - NO BORRAR -->
  <!-- ============================================= -->
  
  <!-- Trampas clásicas que todos los bloqueadores reconocen -->
  <div class="adsbygoogle" id="div-gpt-ad-123456789-0" style="width: 300px; height: 250px;"></div>
  <ins class="adsbygoogle" data-ad-client="ca-pub-1234567890123456" data-ad-slot="1234567890" style="display:block;"></ins>
  <div id="carbon-ads"></div>
  <div class="ad-unit pub_300x250"></div>
  <div class="ad-placement" data-revive-zoneid="1"></div>
  <div class="advertising-notice"></div>
  
  <!-- Trampa especial para AdBlock Plus -->
  <div id="ad-wrapper" class="_ap_apex_ad"></div>
  
  <!-- Scripts falsos que los bloqueadores interceptan -->
  <script data-adblockdetector="true">
    // Este script se bloquea normalmente
    var fakeAdScript = document.createElement('script');
    fakeAdScript.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';
    fakeAdScript.async = true;
    fakeAdScript.onerror = function() {
      window.adBlockDetected = true;
    };
    document.head.appendChild(fakeAdScript);
  </script>

  <!-- ============================================= -->
  <!-- SCRIPT PRINCIPAL DE DETECCIÓN -->
  <!-- ============================================= -->
  <script>
    // Variables de control
    let adblockDetected = false;
    let detectionAttempts = 0;
    const maxAttempts = 3;
    
    // ENLACE REAL (cámbialo si es necesario)
    const redirectUrl = "https://devuploads.com/nvgoz9e9zjag";
    
    // MÉTODO 1: Detección por fetch de recursos bloqueados
    function detectByResourceBlocking() {
      const adResources = [
        'https://www.googletagmanager.com/gtag/js',
        'https://www.google-analytics.com/analytics.js',
        'https://connect.facebook.net/en_US/fbevents.js',
        'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js',
        'https://static.ads-twitter.com/uwt.js'
      ];
      
      let blockedCount = 0;
      let checked = 0;
      
      adResources.forEach(url => {
        fetch(url, {
          method: 'HEAD',
          mode: 'no-cors',
          cache: 'no-store'
        })
        .then(response => {
          checked++;
        })
        .catch(error => {
          blockedCount++;
          checked++;
        });
      });
      
      // Esperar un momento para las respuestas
      return new Promise(resolve => {
        setTimeout(() => {
          // Si más de la mitad están bloqueados, probablemente hay adblock
          resolve(blockedCount > adResources.length / 2);
        }, 1000);
      });
    }
    
    // MÉTODO 2: Detección por comportamiento de elementos
    function detectByElementBehavior() {
      // Crear un elemento que parezca un anuncio
      const bait = document.createElement('div');
      bait.id = 'ads-bait-' + Date.now();
      bait.className = 'adsbygoogle ad-unit pub_300x250';
      bait.style.cssText = 'width: 300px; height: 250px; position: absolute; top: -9999px; left: -9999px;';
      bait.innerHTML = '<ins class="adsbygoogle" style="display:block;"></ins>';
      
      document.body.appendChild(bait);
      
      // Verificar si fue modificado/ocultado
      return new Promise(resolve => {
        setTimeout(() => {
          const style = window.getComputedStyle(bait);
          const isHidden = (
            bait.offsetHeight === 0 ||
            bait.offsetWidth === 0 ||
            style.display === 'none' ||
            style.visibility === 'hidden' ||
            style.opacity === '0' ||
            style.height === '0px'
          );
          
          // Limpiar
          document.body.removeChild(bait);
          resolve(isHidden);
        }, 500);
      });
    }
    
    // MÉTODO 3: Detección por errores en scripts
    function detectByScriptErrors() {
      return new Promise(resolve => {
        const script = document.createElement('script');
        script.src = 'https://cdn.adox.io/ads/load.js?' + Math.random();
        script.onerror = () => {
          resolve(true); // Error = probable bloqueo
        };
        script.onload = () => {
          resolve(false); // Cargó = probablemente sin bloqueo
        };
        
        // Timeout por si no hay respuesta
        setTimeout(() => {
          resolve(true); // Timeout = probable bloqueo
        }, 2000);
        
        document.head.appendChild(script);
        
        // Limpiar después
        setTimeout(() => {
          if (script.parentNode) {
            script.parentNode.removeChild(script);
          }
        }, 3000);
      });
    }
    
    // MÉTODO 4: Detección por patrones conocidos
    function detectByPatterns() {
      // Verificar si hay variables globales de adblockers
      const adblockVars = [
        'blockAdBlock',
        'sniffAdBlock',
        'adblock',
        'uBlock',
        'adguard'
      ];
      
      let detected = false;
      
      // Buscar en el objeto window
      adblockVars.forEach(varName => {
        if (window[varName] !== undefined) {
          detected = true;
        }
      });
      
      // Verificar si hay listeners de eventos de adblock
      if (typeof EventTarget !== 'undefined') {
        const originalAddEventListener = EventTarget.prototype.addEventListener;
        EventTarget.prototype.addEventListener = function(type) {
          if (type && type.toString().toLowerCase().includes('ad')) {
            detected = true;
          }
          return originalAddEventListener.apply(this, arguments);
        };
      }
      
      return detected;
    }
    
    // FUNCIÓN PRINCIPAL DE DETECCIÓN
    async function performAdblockDetection() {
      detectionAttempts++;
      
      // Ejecutar todos los métodos en paralelo
      const results = await Promise.all([
        detectByResourceBlocking(),
        detectByElementBehavior(),
        detectByScriptErrors(),
        Promise.resolve(detectByPatterns())
      ]);
      
      // Si la mayoría de métodos detectan adblock
      const trueCount = results.filter(r => r === true).length;
      adblockDetected = trueCount >= 2; // 2 o más métodos positivos
      
      console.log('Detección #' + detectionAttempts + ' - Resultados:', results, 'Adblock detectado:', adblockDetected);
      
      // Mostrar el contenido adecuado
      showAppropriateContent();
      
      // Si después de varios intentos no detecta pero queremos ser estrictos
      if (detectionAttempts >= maxAttempts && !adblockDetected) {
        // Última verificación: forzar detección con método más agresivo
        const forcedCheck = await detectByElementBehavior();
        if (forcedCheck) {
          adblockDetected = true;
          showAppropriateContent();
        }
      }
    }
    
    // MOSTRAR CONTENIDO SEGÚN DETECCIÓN
    function showAppropriateContent() {
      if (adblockDetected) {
        // MOSTRAR MENSAJE DE BLOQUEO
        document.getElementById('normalAccess').style.display = 'none';
        document.getElementById('blockedAccess').style.display = 'block';
        
        // Detener cualquier redirección pendiente
        clearTimeout(window.redirectTimeout);
      } else {
        // PERMITIR ACCESO
        document.getElementById('normalAccess').style.display = 'block';
        document.getElementById('blockedAccess').style.display = 'none';
        
        // Configurar redirección
        setupRedirect();
      }
    }
    
    // CONFIGURAR REDIRECCIÓN
    function setupRedirect() {
      const countdownEl = document.getElementById('countdown');
      const directLink = document.getElementById('directLink');
      
      // Configurar enlace
      if (directLink) {
        directLink.href = redirectUrl;
        directLink.onclick = function(e) {
          e.preventDefault();
          window.location.href = redirectUrl;
        };
      }
      
      // Contador regresivo
      let seconds = 5;
      const countdownInterval = setInterval(() => {
        seconds--;
        if (countdownEl) countdownEl.textContent = seconds;
        
        if (seconds <= 0) {
          clearInterval(countdownInterval);
          window.location.href = redirectUrl;
        }
      }, 1000);
      
      // Guardar referencia para poder cancelar
      window.redirectTimeout = setTimeout(() => {
        window.location.href = redirectUrl;
      }, 5000);
    }
    
    // ACCESO FORZADO (para usuarios que insisten)
    document.getElementById('forceAccess').addEventListener('click', function() {
      if (confirm("⚠️ Acceso forzado activado. El contenido puede no funcionar correctamente con bloqueadores activos. ¿Continuar?")) {
        adblockDetected = false;
        showAppropriateContent();
      }
    });
    
    // INICIALIZACIÓN
    document.addEventListener('DOMContentLoaded', function() {
      // Ocultar todo inicialmente
      document.getElementById('normalAccess').style.display = 'none';
      document.getElementById('blockedAccess').style.display = 'none';
      
      // Iniciar detección después de un breve retraso
      setTimeout(() => {
        performAdblockDetection();
      }, 1500);
      
      // Monitoreo continuo
      setInterval(() => {
        if (!adblockDetected) {
          performAdblockDetection();
        }
      }, 10000);
      
      // También detectar cambios dinámicos
      const observer = new MutationObserver(() => {
        if (!adblockDetected) {
          performAdblockDetection();
        }
      });
      
      observer.observe(document.body, {
        childList: true,
        subtree: true,
        attributes: true
      });
    });
    
    // Detectar si el usuario intenta inspeccionar elementos
    document.addEventListener('contextmenu', function(e) {
      if (adblockDetected) {
        e.preventDefault();
        return false;
      }
    });
    
    // Detectar teclas de desarrollador (F12, Ctrl+Shift+I)
    document.addEventListener('keydown', function(e) {
      if (adblockDetected && (
        e.key === 'F12' ||
        (e.ctrlKey && e.shiftKey && e.key === 'I') ||
        (e.ctrlKey && e.shiftKey && e.key === 'J') ||
        (e.ctrlKey && e.key === 'U')
      )) {
        e.preventDefault();
        alert('Por favor, desactiva el bloqueador de anuncios antes de usar herramientas de desarrollador.');
        return false;
      }
    });
  </script>
</body>
</html>
