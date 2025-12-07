<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Acceso</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      padding: 50px;
      background: #f5f5f5;
    }
    #blocked {
      background: white;
      padding: 40px;
      border-radius: 10px;
      max-width: 500px;
      margin: 0 auto;
      border-left: 5px solid #ff4444;
      box-shadow: 0 5px 15px rgba(255, 68, 68, 0.2);
    }
    #allowed {
      background: white;
      padding: 40px;
      border-radius: 10px;
      max-width: 500px;
      margin: 0 auto;
      border-left: 5px solid #00C851;
      box-shadow: 0 5px 15px rgba(0, 200, 81, 0.2);
    }
    h2 {
      margin-top: 0;
    }
    .red {
      color: #ff4444;
    }
    .green {
      color: #00C851;
    }
    .btn {
      display: inline-block;
      padding: 12px 30px;
      background: #33b5e5;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin: 10px;
      font-size: 16px;
      text-decoration: none;
    }
    .btn-red {
      background: #ff4444;
    }
    .btn-green {
      background: #00C851;
    }
    
    /* Elemento trampa - los bloqueadores lo ocultan */
    #adBanner {
      position: absolute;
      top: -9999px;
      width: 300px;
      height: 250px;
      background: transparent;
      border: 1px dashed #ccc;
    }
    
    #adBanner:before {
      content: "Publicidad";
      color: #666;
      font-size: 12px;
    }
  </style>
</head>
<body>

<!-- CONTENIDO BLOQUEADO (se muestra SI hay bloqueador) -->
<div id="blocked" style="display: none;">
  <h2 class="red">🚫 BLOQUEADOR DETECTADO</h2>
  <p><strong>Desactiva AdBlock, uBlock o cualquier bloqueador de anuncios.</strong></p>
  <p>Después, recarga esta página.</p>
  <button onclick="location.reload()" class="btn btn-red">Ya lo desactivé, recargar</button>
</div>

<!-- CONTENIDO PERMITIDO (se muestra SOLO si NO hay bloqueador) -->
<div id="allowed" style="display: none;">
  <h2 class="green">✓ ACCESO PERMITIDO</h2>
  <p>Redirigiendo en <span id="timer">3</span> segundos...</p>
  <a href="https://devuploads.com/nvgoz9e9zjag" class="btn btn-green">Acceder ahora</a>
</div>

<!-- ELEMENTO TRAMPA (los bloqueadores lo ocultan) -->
<div id="adBanner"></div>

<script>
// Función ULTRA SIMPLE de detección
function checkAdBlock() {
  const adElement = document.getElementById('adBanner');
  
  // Si el elemento NO existe o está oculto = HAY BLOQUEADOR
  if (!adElement) {
    return true; // Bloqueador detectado
  }
  
  // Verificar estilo
  const style = window.getComputedStyle(adElement);
  if (style.display === 'none' || 
      style.visibility === 'hidden' || 
      adElement.offsetHeight === 0 || 
      adElement.offsetWidth === 0) {
    return true; // Bloqueador detectado
  }
  
  return false; // No hay bloqueador
}

// Función para mostrar resultado
function showResult() {
  const hasAdBlock = checkAdBlock();
  
  if (hasAdBlock) {
    // HAY BLOQUEADOR: Mostrar mensaje de bloqueo
    document.getElementById('blocked').style.display = 'block';
    document.getElementById('allowed').style.display = 'none';
    console.log('🚫 Bloqueador detectado - NO se redirige');
  } else {
    // NO HAY BLOQUEADOR: Redirigir
    document.getElementById('blocked').style.display = 'none';
    document.getElementById('allowed').style.display = 'block';
    
    // Redirección automática después de 3 segundos
    let seconds = 3;
    const timerElement = document.getElementById('timer');
    
    const countdown = setInterval(function() {
      seconds--;
      if (timerElement) {
        timerElement.textContent = seconds;
      }
      
      if (seconds <= 0) {
        clearInterval(countdown);
        // SOLO REDIRIGE si NO hay bloqueador
        window.location.href = "https://devuploads.com/nvgoz9e9zjag";
      }
    }, 1000);
  }
}

// Iniciar cuando la página cargue
window.addEventListener('load', function() {
  // Esperar 1 segundo para que el bloqueador actúe
  setTimeout(showResult, 1000);
});

// También verificar si el usuario hace clic derecho (bloqueadores a veces interceptan)
document.addEventListener('contextmenu', function(e) {
  // Verificar si estamos en modo bloqueado
  if (document.getElementById('blocked').style.display === 'block') {
    alert('⚠️ Desactiva el bloqueador para continuar');
    e.preventDefault();
  }
});
</script>

</body>
</html>
