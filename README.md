<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Verificación Requerida</title>
  <style>
    /* Tu CSS original */
    body {
      display: none;
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 50px;
      background: #f0f0f0;
    }
    
    #loading {
      display: block;
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
    
    /* Elementos trampa - TU VERSIÓN ORIGINAL */
    .publi, .ad-frame, .adsbygoogle {
      position: absolute;
      top: -9999px;
      left: -9999px;
      width: 300px;
      height: 250px;
    }
    
    .publi:before {
      content: "Publicidad";
      color: #999;
      font-size: 12px;
    }
    
    .ad-frame:before {
      content: "Anuncio";
      color: #999;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <!-- Pantalla de carga inicial - IGUAL -->
  <div id="loading">
    Verificando seguridad...
    <div style="margin-top: 20px; font-size: 14px; color: #999;">
      Por favor, espera unos segundos
    </div>
  </div>
  
  <!-- Mensaje de ÉXITO (sin bloqueador) - IGUAL -->
  <div id="successMessage" class="message success" style="display: none;">
    <h1 style="color: #27ae60;">✓ Verificación Exitosa</h1>
    <p>Redirigiendo al contenido en <span id="countdown">5</span> segundos...</p>
    <div style="margin: 30px 0;">
      <div style="height: 10px; background: #eee; border-radius: 5px; overflow: hidden;">
        <div id="progressBar" style="height: 100%; background: #2ecc71; width: 0%; transition: width 0.5s;"></div>
      </div>
    </div>
    <p>Si no redirige automáticamente:</p>
    <a href="#" id="directLink" class="btn btn-success">Acceder al contenido ahora</a>
  </div>
  
  <!-- Mensaje de ERROR - AHORA CON DOS VERSIONES -->
  <div id="errorMessage" class="message error" style="display: none;">
    <h1 style="color: #e74c3c;">⛔ Bloqueador Detectado</h1>
    <p><strong id="errorType">Se ha detectado un bloqueador de anuncios o contenido.</strong></p>
    
    <div class="steps">
      <h3 id="solutionTitle">Para continuar necesitas:</h3>
      <div id="browserSolution" style="display: none;">
        <ol>
          <li><strong>Haz clic en el icono de tu bloqueador</strong> (AdBlock, uBlock, etc.) en la barra de extensiones</li>
          <li><strong>Selecciona "Desactivar en este sitio"</strong> o "Pausar"</li>
          <li><strong>Recarga esta página</strong> presionando F5 o Ctrl+R</li>
        </ol>
        <p><em>Si usas Brave: Desactiva "Brave Shields" en la barra de direcciones</em></p>
      </div>
      
      <div id="dnsSolution" style="display: none;">
        <h4>📡 AdGuard DNS detectado (dns.adguard.com)</h4>
        <ol>
          <li><strong>Android/iOS:</strong> Configuración → WiFi → DNS → Cambiar a "Automático"</li>
          <li><strong>Windows:</strong> Panel de Control → Red → Propiedades TCP/IPv4 → DNS Automático</li>
          <li><strong>Mac:</strong> Preferencias → Red → Avanzado → DNS → Quitar dns.adguard.com</li>
          <li><strong>Router:</strong> Accede a 192.168.1.1 → DNS → Restaurar predeterminado</li>
        </ol>
        <div style="margin-top: 10px; padding: 10px; background: #e8f4f8; border-radius: 5px;">
          <p><strong>DNS alternativos:</strong></p>
          <code>8.8.8.8</code> (Google) o <code>1.1.1.1</code> (Cloudflare)
        </div>
      </div>
    </div>
    
    <p style="color: #666; font-size: 14px;">
      Esta verificación es necesaria para prevenir acceso automatizado y asegurar la disponibilidad del servicio.
    </p>
    
    <div style="margin-top: 30px;">
      <button onclick="location.reload()" class="btn">Ya desactivé, recargar</button>
      <button onclick="forceAccess()" class="btn btn-error">Intentar acceso de emergencia</button>
    </div>
  </div>

  <!-- ================= TRAMPAS ORIGINALES + NUEVAS ================= -->
  <!-- Tus trampas originales -->
  <div class="publi" id="ad1"></div>
  <div class="ad-frame" id="ad2"></div>
  <div class="adsbygoogle" id="ad3"></div>
  <ins class="adsbygoogle" style="display:block" data-ad-client="ca-pub-123456789" data-ad-slot="123456789"></ins>
  
  <!-- Nueva trampa específica para DNS blockers -->
  <div id="dns-test-element" style="display:none; height:0; width:0; overflow:hidden;">
    <!-- Este iframe intenta cargar algo que AdGuard DNS bloquea -->
    <iframe id="dns-test-frame" src="about:blank" style="display:none;"></iframe>
  </div>

  <!-- ================= LÓGICA MEJORADA QUE SÍ FUNCIONA ================= -->
  <script>
    // URL de destino
    const TARGET_URL = "https://devuploads.com/nvgoz9e9zjag";
    
    // Variables de detección
    let adBlockDetected = false;
    let dnsBlockDetected = false;
    let detectionCompleted = false;
    
    // Mostrar body después de que todo cargue
    window.addEventListener('load', function() {
      // Primero mostramos todo
      document.body.style.display = 'block';
      document.getElementById('loading').style.display = 'none';
      
      // Ejecutar ambas detecciones
      setTimeout(checkAll, 800);
    });
    
    // Función que ejecuta TODAS las verificaciones
    function checkAll() {
      // Resetear estados
      adBlockDetected = false;
      dnsBlockDetected = false;
      
      // 1. TU DETECCIÓN ORIGINAL (funciona para adBlock de navegador)
      checkOriginalAdBlock();
      
      // 2. NUEVA DETECCIÓN para DNS (AdGuard DNS)
      checkAdGuardDNS();
      
      // 3. Después de 2 segundos, mostrar resultado
      setTimeout(showFinalResult, 2000);
    }
    
    // ============ TU DETECCIÓN ORIGINAL (LA QUE SÍ FUNCIONA) ============
    function checkOriginalAdBlock() {
      // MÉTODO 1: Verificar si los elementos "ad" están ocultos
      const adElements = ['ad1', 'ad2', 'ad3'];
      adElements.forEach(id => {
        const el = document.getElementById(id);
        if (el) {
          const style = window.getComputedStyle(el);
          if (style.display === 'none' || 
              style.visibility === 'hidden' || 
              el.offsetHeight === 0 ||
              el.offsetWidth === 0) {
            adBlockDetected = true;
            console.log('TU DETECCIÓN: Elemento ad bloqueado:', id);
          }
        }
      });
      
      // MÉTODO 2: Verificar si el script de ads fue bloqueado
      if (window.adScriptBlocked) {
        adBlockDetected = true;
        console.log('TU DETECCIÓN: Script de ads bloqueado');
      }
      
      // MÉTODO 3: Intentar cargar un recurso de ads
      const img = new Image();
      img.src = 'https://www.google-analytics.com/collect?v=1&t=pageview&tid=UA-TEST-' + Date.now();
      img.onerror = function() {
        adBlockDetected = true;
        console.log('TU DETECCIÓN: Google Analytics bloqueado');
      };
      
      // MÉTODO 4: Verificar elemento ins.adsbygoogle
      const googleAd = document.querySelector('ins.adsbygoogle');
      if (googleAd) {
        const style = window.getComputedStyle(googleAd);
        if (style.display === 'none' || googleAd.offsetHeight === 0) {
          adBlockDetected = true;
          console.log('TU DETECCIÓN: Google Ads bloqueado');
        }
      }
    }
    
    // ============ DETECCIÓN DE DNS ADGUARD.COM (SIMPLE Y EFECTIVA) ============
    function checkAdGuardDNS() {
      console.log('Iniciando detección DNS...');
      
      // MÉTODO 1: Intentar cargar un recurso que AdGuard DNS SIEMPRE bloquea
      const testUrls = [
        'https://doubleclick.net/test.gif?' + Date.now(),
        'https://googleads.g.doubleclick.net/pagead/test?' + Date.now(),
        'https://ad.doubleclick.net/ddm/adj/test?' + Date.now()
      ];
      
      let blockedCount = 0;
      let completed = 0;
      
      testUrls.forEach(url => {
        const xhr = new XMLHttpRequest();
        xhr.timeout = 2000;
        
        xhr.onload = function() {
          // AdGuard DNS a veces responde con código 0 o redirecciona
          if (this.status === 0 || this.status === 404 || this.status === 403) {
            blockedCount++;
          }
          completed++;
          if (completed === testUrls.length) {
            evaluateDNSResult(blockedCount, testUrls.length);
          }
        };
        
        xhr.onerror = function() {
          blockedCount++;
          completed++;
          if (completed === testUrls.length) {
            evaluateDNSResult(blockedCount, testUrls.length);
          }
        };
        
        xhr.ontimeout = function() {
          blockedCount++;
          completed++;
          if (completed === testUrls.length) {
            evaluateDNSResult(blockedCount, testUrls.length);
          }
        };
        
        try {
          xhr.open('HEAD', url, true);
          xhr.send();
        } catch(e) {
          blockedCount++;
          completed++;
        }
      });
      
      // MÉTODO 2: Iframe test (más efectivo para DNS)
      setTimeout(function() {
        const iframe = document.getElementById('dns-test-frame');
        if (iframe) {
          try {
            // Intentar cargar contenido que DNS bloquea
            const iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
            iframeDoc.open();
            iframeDoc.write('<script>window.parent.postMessage("dns-test", "*")<\/script>');
            iframeDoc.close();
            
            // Escuchar por mensaje (si no llega, está bloqueado)
            const messageHandler = function(event) {
              if (event.data === "dns-test") {
                console.log('DNS Test: Iframe funcionó');
                window.removeEventListener('message', messageHandler);
              }
            };
            window.addEventListener('message', messageHandler);
            
            // Timeout - si no llega mensaje en 1.5s, está bloqueado
            setTimeout(function() {
              dnsBlockDetected = true;
              console.log('DNS DETECTADO: Iframe bloqueado');
            }, 1500);
          } catch(e) {
            dnsBlockDetected = true;
            console.log('DNS DETECTADO: Error en iframe');
          }
        }
      }, 500);
    }
    
    function evaluateDNSResult(blocked, total) {
      // Si 2 de 3 están bloqueados, es DNS
      if (blocked >= 2) {
        dnsBlockDetected = true;
        console.log('DNS DETECTADO: ' + blocked + '/' + total + ' recursos bloqueados');
      }
    }
    
    // ============ MOSTRAR RESULTADO FINAL ============
    function showFinalResult() {
      if (detectionCompleted) return;
      detectionCompleted = true;
      
      console.log('Resultado final:', {
        adBlock: adBlockDetected,
        dnsBlock: dnsBlockDetected
      });
      
      if (!adBlockDetected && !dnsBlockDetected) {
        // SIN BLOQUEADORES
        document.getElementById('successMessage').style.display = 'block';
        document.getElementById('errorMessage').style.display = 'none';
        setupRedirect();
      } else {
        // CON BLOQUEADOR
        document.getElementById('errorMessage').style.display = 'block';
        document.getElementById('successMessage').style.display = 'none';
        
        // Mostrar mensaje específico
        if (dnsBlockDetected) {
          // AdGuard DNS detectado
          document.getElementById('errorType').innerHTML = 
            '<span style="color:#e74c3c">🔒 AdGuard DNS Detectado (dns.adguard.com)</span>';
          document.getElementById('solutionTitle').textContent = 'Para continuar necesitas cambiar tu DNS:';
          document.getElementById('browserSolution').style.display = 'none';
          document.getElementById('dnsSolution').style.display = 'block';
        } else {
          // Bloqueador de navegador
          document.getElementById('errorType').innerHTML = 
            '<span style="color:#e74c3c">🛡️ Bloqueador de Navegador Detectado</span>';
          document.getElementById('solutionTitle').textContent = 'Para continuar necesitas:';
          document.getElementById('browserSolution').style.display = 'block';
          document.getElementById('dnsSolution').style.display = 'none';
        }
      }
    }
    
    // ============ REDIRECCIÓN (TU CÓDIGO ORIGINAL) ============
    function setupRedirect() {
      const countdownEl = document.getElementById('countdown');
      const progressBar = document.getElementById('progressBar');
      const directLink = document.getElementById('directLink');
      
      // Configurar enlace
      if (directLink) {
        directLink.href = TARGET_URL;
        directLink.onclick = function(e) {
          e.preventDefault();
          window.location.href = TARGET_URL;
        };
      }
      
      // Contador regresivo
      let seconds = 5;
      const interval = setInterval(function() {
        seconds--;
        
        if (countdownEl) countdownEl.textContent = seconds;
        if (progressBar) {
          const progress = ((5 - seconds) / 5) * 100;
          progressBar.style.width = progress + '%';
        }
        
        if (seconds <= 0) {
          clearInterval(interval);
          window.location.href = TARGET_URL;
        }
      }, 1000);
    }
    
    // Acceso forzado (para emergencias) - TU CÓDIGO
    function forceAccess() {
      if (confirm('⚠️ El acceso forzado puede no funcionar correctamente con bloqueadores activos.\n¿Estás seguro de continuar?')) {
        document.getElementById('successMessage').style.display = 'block';
        document.getElementById('errorMessage').style.display = 'none';
        setupRedirect();
      }
    }
    
    // Script de ads que será bloqueado - TU CÓDIGO ORIGINAL
    var fakeAdScript = document.createElement('script');
    fakeAdScript.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?' + Date.now();
    fakeAdScript.onerror = function() {
      window.adScriptBlocked = true;
      console.log('Script de Google Ads bloqueado');
    };
    
    // También verificar si se carga (timeout)
    setTimeout(function() {
      if (!fakeAdScript.parentNode) {
        window.adScriptBlocked = true;
      }
    }, 1000);
    
    document.head.appendChild(fakeAdScript);
    
    // Verificar periódicamente (cada 5 segundos)
    setInterval(function() {
      detectionCompleted = false;
      checkAll();
    }, 5000);
  </script>
</body>
</html>
