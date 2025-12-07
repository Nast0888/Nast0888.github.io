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
    
    /* Elementos trampa */
    .publi, .ad-frame, .adsbygoogle {
      position: absolute;
      top: -9999px;
      left: -9999px;
      width: 300px;
      height: 250px;
    }
    
    /* Texto que atrae a los bloqueadores */
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
  <div id="loading">
    Verificando seguridad...
    <div style="margin-top: 20px; font-size: 14px; color: #999;">
      Por favor, espera unos segundos
    </div>
  </div>
  
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
    </div>
    
    <div style="margin-top: 30px;">
      <button onclick="location.reload()" class="btn">Ya desactivé el bloqueador, recargar</button>
    </div>
  </div>

  <div class="publi" id="ad1"></div>
  <div class="ad-frame" id="ad2"></div>
  <div class="adsbygoogle" id="ad3"></div>
  <ins class="adsbygoogle" style="display:block" data-ad-client="ca-pub-123456789" data-ad-slot="123456789"></ins>
  
  <script>
    var fakeAdScript = document.createElement('script');
    fakeAdScript.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';
    fakeAdScript.onerror = function() {
      window.adScriptBlocked = true;
    };
    document.head.appendChild(fakeAdScript);
  </script>

  <script>
    // URL de destino
    const TARGET_URL = "https://devuploads.com/nvgoz9e9zjag";
    
    // Mostrar body después de que todo cargue
    window.addEventListener('load', function() {
      // Primero mostramos todo
      document.body.style.display = 'block';
      document.getElementById('loading').style.display = 'none';
      
      // Luego verificamos
      setTimeout(checkAdBlock, 1000);
    });
    
    // Función principal de verificación
    function checkAdBlock() {
      let adBlockDetected = false;
      
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
          }
        }
      });
      
      // MÉTODO 2: Verificar si el script de ads fue bloqueado
      if (window.adScriptBlocked) {
        adBlockDetected = true;
      }
      
      // MÉTODO 3: Intentar cargar un recurso de ads
      const img = new Image();
      img.src = 'https://www.google-analytics.com/collect?v=1&t=pageview&tid=UA-TEST-1';
      img.onerror = function() {
        adBlockDetected = true;
        showResult();
      };
      
      // Timeout para la verificación
      setTimeout(function() {
        showResult();
      }, 1500);
      
      function showResult() {
        if (adBlockDetected) {
          // MOSTRAR ERROR - BLOQUEADOR DETECTADO
          document.getElementById('errorMessage').style.display = 'block';
          document.getElementById('successMessage').style.display = 'none';
          
          // NO redirigir en absoluto
          console.log('Bloqueador detectado - Acceso denegado');
        } else {
          // MOSTRAR ÉXITO - SIN BLOQUEADOR
          document.getElementById('successMessage').style.display = 'block';
          document.getElementById('errorMessage').style.display = 'none';
          
          // Configurar redirección
          setupRedirect();
        }
      }
    }
    
    // Configurar redirección automática
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
      
      // Contador regresivo (3 segundos)
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
    
    // Verificar periódicamente (por si activan/desactivan bloqueador)
    setInterval(checkAdBlock, 10000);
  </script>
</body>
</html>
