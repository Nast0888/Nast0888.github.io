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
    
    /* Elementos trampa - Ocultos para humanos, visibles para bloqueadores */
    .banner-container, .sponsored-content, .promo-box {
      position: absolute;
      opacity: 0.001;
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
        <li><strong>O haz clic en el botón verde "Recargar Página"</strong> abajo</li>
      </ol>
      <p><em>Si usas Brave: Desactiva "Brave Shields" en la barra de direcciones</em></p>
      <p><em>Si usas Opera: Desactiva "Bloqueador de anuncios" en Configuración del sitio</em></p>
      <p style="color: #27ae60; font-weight: bold; margin-top: 10px;">
        ⚠️ Importante: Después de desactivar el bloqueador, debes RECARGAR la página
      </p>
    </div>
    
    <p style="color: #666; font-size: 14px;">
      Esta verificación es necesaria para prevenir acceso automatizado y asegurar la disponibilidad del servicio.
    </p>
    
    <div style="margin-top: 30px;">
      <button onclick="hardReload()" class="btn btn-success">Recargar Página</button>
      <button onclick="testWithoutCache()" class="btn">Probar sin caché</button>
    </div>
    
    <!-- Información de diagnóstico (solo visible en consola) -->
    <div id="debugInfo" style="display: none; font-size: 12px; color: #999; margin-top: 20px; text-align: left;">
      Información de diagnóstico disponible en consola (F12)
    </div>
  </div>

  <!-- ================= TRAMPAS MEJORADAS ================= -->
  <!-- NOTA: Estos elementos NO deben estar ocultos con CSS, para que los bloqueadores los vean -->
  <div id="adTest1" class="ad-banner" style="width: 1px; height: 1px; position: absolute; top: -1px; left: -1px;"></div>
  <div id="adTest2" class="adsbygoogle" style="display: inline-block !important; width: 1px; height: 1px;"></div>
  <div id="adTest3" data-ad="true" style="width: 1px; height: 1px; position: absolute;"></div>

  <!-- ================= LÓGICA PRINCIPAL MEJORADA ================= -->
  <script>
    // URL de destino
    const TARGET_URL = "https://devuploads.com/nvgoz9e9zjag";
    
    // Función para recargar sin caché
    function hardReload() {
      console.log('Recargando página sin caché...');
      window.location.reload(true);
    }
    
    // Función para probar sin caché
    function testWithoutCache() {
      console.log('Forzando recarga sin caché...');
      // Borrar localStorage y sessionStorage
      localStorage.clear();
      sessionStorage.clear();
      
      // Forzar recarga sin caché
      window.location.href = window.location.href + '?nocache=' + Date.now();
    }
    
    // Función principal que se ejecuta al cargar
    function initVerification() {
      // Mostrar body inmediatamente
      document.body.style.display = 'block';
      document.getElementById('loading').style.display = 'none';
      
      // Esperar un momento para que los bloqueadores actúen
      setTimeout(performAdBlockCheck, 500);
    }
    
    // Función de verificación - SÍNCRONA y RESETEABLE
    function performAdBlockCheck() {
      console.log('=== INICIANDO VERIFICACIÓN DE BLOQUEADOR ===');
      
      let isBlocked = false;
      let reasons = [];
      
      // PRUEBA 1: Verificar elementos ad por su estilo COMPUTADO
      const adElements = ['adTest1', 'adTest2', 'adTest3'];
      
      adElements.forEach(id => {
        const element = document.getElementById(id);
        if (element) {
          const computedStyle = window.getComputedStyle(element);
          const originalHTML = element.outerHTML;
          
          console.log(`Elemento ${id}:`);
          console.log(`- display: ${computedStyle.display}`);
          console.log(`- visibility: ${computedStyle.visibility}`);
          console.log(`- height: ${element.offsetHeight}px`);
          console.log(`- width: ${element.offsetWidth}px`);
          console.log(`- opacity: ${computedStyle.opacity}`);
          
          // Si el bloqueador modificó el elemento
          if (computedStyle.display === 'none' || 
              computedStyle.visibility === 'hidden' ||
              element.offsetHeight === 0 ||
              element.offsetWidth === 0 ||
              computedStyle.opacity === '0') {
            
            isBlocked = true;
            reasons.push(`Elemento ${id} modificado por bloqueador`);
            console.log(`⚠️ ${id} DETECTADO COMO BLOQUEADO`);
          } else {
            console.log(`✓ ${id} sin modificaciones`);
          }
        }
      });
      
      // PRUEBA 2: Intentar crear y detectar un script de ads
      try {
        const testScript = document.createElement('script');
        testScript.src = 'https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js';
        testScript.async = true;
        
        // Establecer un timeout para la carga
        let scriptLoaded = false;
        testScript.onload = function() {
          scriptLoaded = true;
          console.log('✓ Script de Google Ads cargado correctamente');
        };
        
        testScript.onerror = function() {
          isBlocked = true;
          reasons.push('Script de Google Ads bloqueado');
          console.log('⚠️ Script de Google Ads bloqueado');
        };
        
        // Agregar el script al documento
        document.head.appendChild(testScript);
        
        // Esperar un momento para ver si se bloquea
        setTimeout(() => {
          if (!scriptLoaded) {
            // Verificar si el script aún está en el DOM
            if (!document.contains(testScript)) {
              isBlocked = true;
              reasons.push('Script de Google Ads removido');
              console.log('⚠️ Script de Google Ads removido del DOM');
            }
          }
          showFinalResult(isBlocked, reasons);
        }, 1000);
        
      } catch (error) {
        console.error('Error en prueba de script:', error);
        showFinalResult(isBlocked, reasons);
      }
      
      // Timeout de seguridad
      setTimeout(() => {
        showFinalResult(isBlocked, reasons);
      }, 1500);
    }
    
    // Mostrar resultado final
    function showFinalResult(isBlocked, reasons) {
      console.log('=== RESULTADO DE VERIFICACIÓN ===');
      console.log(`Bloqueador detectado: ${isBlocked ? 'SÍ' : 'NO'}`);
      if (reasons.length > 0) {
        console.log('Razones:', reasons);
      }
      
      if (isBlocked) {
        // MOSTRAR ERROR
        document.getElementById('errorMessage').style.display = 'block';
        document.getElementById('successMessage').style.display = 'none';
        document.getElementById('debugInfo').style.display = 'block';
        
        console.log('INSTRUCCIONES PARA EL USUARIO:');
        console.log('1. Desactiva tu bloqueador de anuncios');
        console.log('2. Haz clic en "Recargar Página"');
        console.log('3. La verificación se reiniciará desde cero');
        
      } else {
        // MOSTRAR ÉXITO
        document.getElementById('successMessage').style.display = 'block';
        document.getElementById('errorMessage').style.display = 'none';
        
        console.log('✓ Todo correcto, redirigiendo...');
        setupRedirect();
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
    
    // Iniciar la verificación cuando se carga la página
    window.addEventListener('load', initVerification);
    
    // También iniciar si DOM ya está listo
    if (document.readyState === 'interactive' || document.readyState === 'complete') {
      setTimeout(initVerification, 100);
    }
  </script>
</body>
</html>
