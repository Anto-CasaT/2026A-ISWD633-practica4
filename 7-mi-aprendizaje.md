# COMPLETAR  
Comparando sus conocimientos antes de hacer la práctica con sus conocimientos después de hacer la tarea, explicar los principales aprendizajes logrados para beneficio de su formación profesional.  
Si solucionó un problema presentado al realizar la práctica también se debe documentar.

## Mi Aprendizaje

* Aprendí que un Dockerfile define instrucciones para construir imágenes 
  y que cada instrucción genera una capa.

* `docker build` requiere un contexto al final; si los archivos están en 
  subcarpeta se usa esa carpeta como contexto en lugar del punto.

* Docker reutiliza capas en caché si no cambiaron, acelerando builds posteriores.

* CentOS 7/8 tiene repositorios caídos; se soluciona redirigiendo a 
  vault.centos.org con `sed` en el Dockerfile.

* Las políticas de reinicio controlan qué pasa cuando un contenedor se 
  detiene: `no` nunca reinicia, `always` siempre, `unless-stopped` excepto 
  si fue detenido manualmente, `on-failure` solo ante errores (exit != 0).

* Los Healthchecks permiten que Docker monitoree automáticamente si un 
  servicio dentro del contenedor está funcionando correctamente.

* Con `--memory` y `--cpus` se limitan los recursos que un contenedor 
  puede consumir, evitando que afecte al sistema host.
