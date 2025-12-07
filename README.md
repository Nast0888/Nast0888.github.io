<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Verificación Requerida</title>
  <style>
    /* Todo oculto inicialmente */
    body {
      display: none;
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 50px;
      background: #f0f0f0;
    }
    
    /* Solo se muestran después de JS */
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
    
    h1 {
      margin-top: 0;
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
    
    .steps {
      text-align: left;
      background: #f8f9fa;
      padding: 20px;
      border-radius: 5px;
      margin: 20px 0;
    }
    
    /* Elementos trampa - más sutiles */
    .banner-container, .sponsored-content, .promo-box {
      position: absolute;
      opacity: 0;
      pointer-events: none;
      width: 1px;
      height: 1px;
      overflow: hidden;
    }
    
    /* Clases que los bloqueadores buscan */
    .adsbygoogle, .ad-slot, .ad-container, .ad-wrapper,
    .ad-banner, .google-ad, .ad-placement {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      white-space: nowrap;
      border: 0;
    }
    
    /* Texto trampa que atrae bloqueadores */
    [data-ad="true"]::after,
    [data-adunit]::after,
    [data-ad-client]::after {
      content: none;
    }
  </style>
</head>
<body>
  <!-- Pantalla de carga inicial -->
  <div id="loading">
    Verificando seguridad...
    <div style="margin-top: 20px; font-size: 14px; color: #999;">
      Por favor, espera unos segundos
    </div>
  </div>
  
  <!-- Mensaje de ÉXITO (sin bloqueador) -->
  <div id="successMessage" class="message success" style="display: none;">
    <h1 style="color: #27ae60;">✓ Verificación Exitosa</h1>
    <p>Redirigiendo al contenido en <span id="countdown">3</span> segundos...</p>
    <div style="margin: 30px 0;">
      <div style="height: 10px; background: #eee; border-radius: 5px; overflow: hidden;">
        <div id="progressBar" style="height: 100%; background: #2ecc71; width: 0%; transition: width 0.5s;"></div>
      </div>
    </div>
    <p>Si no redirige automáticamente:</p>
    <a href="#" id="directLink" class="btn btn-success">Acceder al contenido ahora</a>
  </div>
  
  <!-- Mensaje de ERROR (con bloqueador) -->
  <div id="errorMessage" class="message error" style="display: none;">
    <h1 style="color: #e74c3c;">⛔ Bloqueador Detectado</h1>
    <p><strong>Se ha detectado un bloqueador de anuncios o contenido.</strong></p>
    
    <div class="steps">
      <h3>Para continuar necesitas:</h3>
      <ol>
        <li><strong>Haz clic en el icono de tu bloqueador</strong> (AdBlock, uBlock, etc.) en la barra de extensiones</li>
        <li><strong>Selecciona "Desactivar en este sitio"</strong> o "Pausar"</li>
        <li><strong>Recarga esta página</strong> presionando F5 o Ctrl+R</li>
      </ol>
      <p><em>Si usas Brave: Desactiva "Brave Shields" en la barra de direcciones</em></p>
      <p><em>Si usas Opera: Desactiva "Bloqueador de anuncios" en Configuración del sitio</em></p>
    </div>
    
    <p style="color: #666; font-size: 14px;">
      Esta verificación es necesaria para prevenir acceso automatizado y asegurar la disponibilidad del servicio.
    </p>
    
    <div style="margin-top: 30px;">
      <button onclick="location.reload()" class="btn">Ya desactivé el bloqueador, recargar</button>
    </div>
  </div>

  <!-- ================= TRAMPAS MEJORADAS ================= -->
  <!-- Elementos que los bloqueadores buscan activamente -->
  <div class="adsbygoogle" data-ad-client="ca-pub-123456789" data-ad-slot="123456789"></div>
  <div class="ad-slot" id="div-gpt-ad-123456789-0"></div>
  <div class="ad-container" style="display: none !important;"></div>
  <div class="ad-wrapper" aria-hidden="true"></div>
  <div class="google-ad" role="region" aria-label="advertisement"></div>
  
  <!-- Elementos con atributos que los bloqueadores detectan -->
  <div data-ad="true" data-refresh="30"></div>
  <div data-adunit="/123456789/banner_ad"></div>
  <div data-ad-client="ca-pub-fake" data-ad-slot="fake-slot"></div>
  
  <!-- Scripts trampa -->
  <script>
    // Primer script trampa
    (function() {
      var s = document.createElement('script');
      s.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';
      s.setAttribute('data-ad-client', 'ca-pub-123456789');
      s.onerror = function() {
        window.adsbygoogleBlocked = true;
      };
      document.head.appendChild(s);
    })();
    
    // Segundo script trampa - Analytics
    (function() {
      var s = document.createElement('script');
      s.src = 'https://www.google-analytics.com/analytics.js';
      s.onerror = function() {
        window.analyticsBlocked = true;
      };
      document.head.appendChild(s);
    })();
    
    // Tercer script trampa - Facebook Pixel
    (function() {
      var s = document.createElement('script');
      s.src = 'https://connect.facebook.net/en_US/fbevents.js';
      s.onerror = function() {
        window.fbBlocked = true;
      };
      document.head.appendChild(s);
    })();
  </script>

  <!-- ================= LÓGICA PRINCIPAL MEJORADA ================= -->
  <script>
    // URL de destino
    const TARGET_URL = "https://devuploads.com/nvgoz9e9zjag";
    
    // Mostrar body después de que todo cargue
    window.addEventListener('load', function() {
      // Primero mostramos todo
      document.body.style.display = 'block';
      document.getElementById('loading').style.display = 'none';
      
      // Luego verificamos con un pequeño delay
      setTimeout(enhancedAdBlockCheck, 800);
    });
    
    // Función mejorada de verificación
    function enhancedAdBlockCheck() {
      let detectionScore = 0;
      const maxScore = 8; // Número total de pruebas
      
      // PRUEBA 1: Verificar scripts bloqueados
      if (window.adsbygoogleBlocked) detectionScore++;
      if (window.analyticsBlocked) detectionScore++;
      if (window.fbBlocked) detectionScore++;
      
      // PRUEBA 2: Verificar elementos ad ocultos o alterados
      const adSelectors = [
        '.adsbygoogle',
        '.ad-slot',
        '.ad-container',
        '.ad-wrapper',
        '.google-ad',
        '[data-ad="true"]',
        '[data-adunit]',
        '[data-ad-client]'
      ];
      
      adSelectors.forEach(selector => {
        const elements = document.querySelectorAll(selector);
        elements.forEach(el => {
          const style = window.getComputedStyle(el);
          
          // Verificar si el elemento fue alterado por bloqueador
          if (style.display === 'none' || 
              style.visibility === 'hidden' ||
              el.offsetHeight === 0 ||
              el.offsetWidth === 0 ||
              style.opacity === '0' ||
              style.position === 'absolute' && style.top === '-9999px') {
            detectionScore += 0.5;
          }
        });
      });
      
      // PRUEBA 3: Intentar cargar una imagen de tracker
      const trackerTest = new Image();
      trackerTest.onerror = function() {
        detectionScore += 2;
        evaluateDetection();
      };
      trackerTest.onload = function() {
        evaluateDetection();
      };
      trackerTest.src = 'https://www.google-analytics.com/collect?v=1&tid=UA-XXXXX-Y&cid=123&t=pageview';
      
      // PRUEBA 4: Verificar fetch de recursos comunes de ads
      fetch('https://googleads.g.doubleclick.net/pagead/id', {
        method: 'HEAD',
        mode: 'no-cors'
      }).catch(() => {
        detectionScore++;
        evaluateDetection();
      });
      
      // Timeout de seguridad
      setTimeout(evaluateDetection, 2000);
      
      function evaluateDetection() {
        const threshold = 3; // Puntuación mínima para considerar bloqueador
        
        if (detectionScore >= threshold) {
          // BLOQUEADOR DETECTADO
          document.getElementById('errorMessage').style.display = 'block';
          document.getElementById('successMessage').style.display = 'none';
          
          // Registrar para debugging
          console.log(`Bloqueador detectado. Puntuación: ${detectionScore}/${maxScore}`);
        } else {
          // SIN BLOQUEADOR
          document.getElementById('successMessage').style.display = 'block';
          document.getElementById('errorMessage').style.display = 'none';
          
          // Configurar redirección más rápida (3 segundos)
          setupRedirect();
          
          // Registrar para debugging
          console.log(`Sin bloqueador. Puntuación: ${detectionScore}/${maxScore}`);
        }
      }
    }
    
    // Configurar redirección automática (3 segundos)
    function setupRedirect() {
      const countdownEl = document.getElementById('countdown');
      const progressBar = document.getElementById('progressBar');
      const directLink = document.getElementById('directLink');
      
      // Configurar enlace directo
      if (directLink) {
        directLink.href = TARGET_URL;
        directLink.onclick = function(e) {
          e.preventDefault();
          window.location.href = TARGET_URL;
        };
      }
      
      // Contador regresivo de 3 segundos
      let seconds = 3;
      const interval = setInterval(function() {
        seconds--;
        
        if (countdownEl) countdownEl.textContent = seconds;
        if (progressBar) {
          const progress = ((3 - seconds) / 3) * 100;
          progressBar.style.width = progress + '%';
        }
        
        if (seconds <= 0) {
          clearInterval(interval);
          window.location.href = TARGET_URL;
        }
      }, 1000);
    }
    
    // Verificar periódicamente
    setInterval(enhancedAdBlockCheck, 15000);
  </script>
</body>
</html>
