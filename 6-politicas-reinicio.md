# Políticas de reinicio

## Para esta parte de la práctica
1. Usa el archivo Dockerfile que se encuentra en cada carpeta con el nombre de la política de reinicio para crear una imagen. Analiza las instrucciones de cada Dockerfile 
2. Usa la imagen para ejecutar un contenedor agregando la política respectiva y observar lo que sucede verificando el cumplimiento de la política de reinicio

### no
No reinicia el contenedor bajo ninguna razón. Esta es la política por default
```
docker run -d --name <nombre contenedor> <nombre imagen>
```
## Construir imagen
```
docker build -t imagen-no:1.0 -f no/Dockerfile .
```
## Ejecutar contenedor
```
docker run -d --name contenedor-no imagen-no:1.0
```
<img width="1716" height="730" alt="image" src="https://github.com/user-attachments/assets/87838fda-a57c-44df-846c-9e8481bab6c8" />
### Observación
Al verificar con `docker ps -a` el contenedor aparece con STATUS 
`Exited (0)` confirmando que se detuvo y no volvió a iniciarse, 
cumpliendo la política no.
<img width="1537" height="270" alt="image" src="https://github.com/user-attachments/assets/1579b3ba-6a51-4b0e-bc8e-73835c70bfa7" />


### always
Reinicia siempre el contenedor si se detiene. Si se detiene manualmente, sólo se reiniciará cuando se reinicie el demonio Docker o cuando se reinicie manualmente el propio contenedor
```
docker run -d --name <nombre contenedor> --restart always <nombre imagen>
```
## Construir imagen
```
docker build -t imagen-always:1.0 -f always/Dockerfile always
```
## Ejecutar contenedor
```
>docker run -d --name contenedor-always --restart always imagen-always:1.0
```
<img width="1728" height="741" alt="image" src="https://github.com/user-attachments/assets/724a4418-5f21-4733-afcc-5b8bf5553f0e" />
### Observación
El contenedor muestra STATUS `Restarting (255)` porque el script 
termina con `exit 1` y Docker lo reinicia indefinidamente debido 
a la política always.
<img width="1537" height="270" alt="image" src="https://github.com/user-attachments/assets/1579b3ba-6a51-4b0e-bc8e-73835c70bfa7" />


### unless-stopped

Similar a always, excepto que cuando el contenedor se detiene (manualmente o de otra manera), no se reinicia incluso después de reiniciar el demonio Docker.
```
docker run -d --name <nombre contenedor> --restart unless-stopped <nombre imagen>
```
## Construir imagen
```
docker build -t imagen-unless:1.0 -f unless-stopped/Dockerfile unless-stopped
```
## Ejecutar contenedor
```
docker run -d --name contenedor-unless --restart unless-stopped imagen-unless:1.0
```
<img width="1709" height="627" alt="image" src="https://github.com/user-attachments/assets/eeda7200-26af-48dd-81f1-3307eea34ea8" />

### Observación
Similar a always, el contenedor muestra `Restarting (255)`. 
La diferencia es que si se detuviera manualmente con `docker stop`, 
no se reiniciaría ni al reiniciar Docker Desktop.
<img width="1537" height="270" alt="image" src="https://github.com/user-attachments/assets/1579b3ba-6a51-4b0e-bc8e-73835c70bfa7" />

### on-failure
Se reinicia únicamente cuando hay una falla en la ejecución del código que se manifiesta con un código diferente de 0. No se reinicia si el contenedor se detiene manualmente.

```
docker run -d --name <nombre contenedor> --restart on-failure <nombre imagen>
```
## Construir imagen
```
docker build -t imagen-onfailure:1.0 -f on-failure/Dockerfile on-failure
```
## Ejecutar contenedor
```
docker run -d --name contenedor-onfailure --restart on-failure imagen-onfailure:1.0
```
<img width="1699" height="646" alt="image" src="https://github.com/user-attachments/assets/2fac66df-37cf-4b62-8145-cb9b35a579b9" />
### Observación
El contenedor muestra `Restarting (255)` porque el script termina 
con `exit 1`. Solo se reinicia ante fallos, si terminara con 
`exit 0` no se reiniciaría.
<img width="1537" height="270" alt="image" src="https://github.com/user-attachments/assets/1579b3ba-6a51-4b0e-bc8e-73835c70bfa7" />
