<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Verificar AdBlock — continuar</title>
  <style>
    body { font-family: sans-serif; text-align: center; padding: 50px; }
    #content { display: none; }
    #blocked { display: none; color: red; }
    .adbox { width: 1px; height: 1px; position: absolute; top: -100px; }
  </style>
</head>
<body>

  <div id="content">
    <p>Redirigiendo… Si no pasa nada, <a id="go" href="https://devuploads.com/nvgoz9e9zjag">haz clic aquí</a>.</p>
  </div>

  <div id="blocked">
    <p>⚠️ Parece que usas AdBlock o un bloqueador de anuncios. Por favor, desactívalo para continuar.</p>
  </div>

  <!-- Elemento “trampa” que los AdBlockers suelen ocultar -->
  <div class="adbox" id="adbox"></div>

  <script>
    // Espera un pequeño instante para que el bloqueador tenga tiempo de ocultar la caja
    window.addEventListener('load', function() {
      // Obtener el elemento “trampa”
      var ad = document.getElementById('adbox');

      // Si su altura o visibilidad es cero, es probable que AdBlock lo haya bloqueado
      var adBlocked = false;
      if (!ad || ad.offsetParent === null || ad.offsetHeight === 0 || getComputedStyle(ad).display === 'none') {
        adBlocked = true;
      }

      if (adBlocked) {
        // Mostrar mensaje de bloqueo
        document.getElementById('blocked').style.display = 'block';
      } else {
        // Mostrar contenido y redirigir
        document.getElementById('content').style.display = 'block';
        // Redirección automática tras 0.5 segundos
        setTimeout(function() {
          window.location.href = "https://devuploads.com/nvgoz9e9zjag";
        }, 500);
      }
    });
  </script>

</body>
</html>
