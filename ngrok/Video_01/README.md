# Viendo la luz al final del Túnel 🚇con NGROK

Hoy vamos a hablar de una de esas herramientas que no pueden faltar en tu kit de trasteo con nuevas tecnologías, NGROK un proxy reverso con el que podrás probar tus aplicaciones o servicios fuera de tu LAN.

**Video:** https://youtu.be/I1HaB1CDJco

0:00 Inicio

0:08 Intro

0:19 Descripción

0:31 Instalación

1:16 Comandos basicos

1:39 Demo 01 (Vault)

4:08 Demo 02 (ArgoCD)

8:10 Demo 03 (Token/Edge)

11:19 Demo 04 (OAuth)

13:17 Dashboard

14:16 Conclusion

15:31 Despedida

15:42 Outro


GitHub:
https://github.com/TheAutomationRules/tools/blob/main/ngrok/Video_01/README.md

Twitter: @TheAutomaRules
Instagram: TheAutomationRules

#ngrok #reverse #proxy #tunnel

---

## INSTALACION
https://ngrok.com/download

Instalación en macOS con Brew.

````
 brew install ngrok
````

## COMANDOS BASICOS
Para ver la version instalada
````
ngrok -v
````
Para ver la ayuda
````
ngrok -h
````

## EJEMPLO DE USO CON HASHICORP VAULT DEV
Teniendo instalado el binario de HashiCorp Vault y ejecutamos lo siguiente:
````
vault server -dev
````
Ahora accedemos en local http://localhost:8200 y accedemos con el token de ROOT que se genera en la inicialización.

Ahora podemos levantar un Tunnel con NGROK para publicar nuestro Vault al exterior:
````
ngrok http http://localhost:8200
````
Y ahora accedemos desde la URL del tunel de NGROK.


## EJEMPLO DE USO CON ARGOCD EN KUBERNETES (Docker Desktop)
Sigue los pasos de mi segundo video de ArgoCD y instalalo desde Helm https://youtu.be/7wn_LOxQPMI y cuando termines levanta un Port Forward para acceder a el.

````
kubectl port-forward service/argo-cd-argocd-server -n argocd 8080:443
````
Ahora puedes acceder y iniciar sesion desde https://localhost:8080

Ahora podemos levantar un tunel con NGROK.
`````
ngrok http https://localhost:8080
`````
Accedemos a ArgoCD desde la URL generada por el tunnel de NGROK que hemos creado.

## Configurando NGROK con nuestro token
Creamos una cuenta de NGROK y una vez dentro copiamos el comando para configurar el binario de NGROK con nuestro token.
````
ngrok config add-authtoken 2HRqw7Zaa8klHSYEubjKyVCPzRU_2zq8obobWXUASRBvJ4Vrn
````
Esto nos permite crear un Edge y usarlo para desplegar un tunnel de nuestro servicio asignandole la Url de este edge, por ejemplo:
````
ngrok tunnel --label edge=edghts_2XM0s4SCpywIXx5g4aPqZKLHZBH https://localhost:8080
````
Con esto ya tenemos el tunnel levantado y podemos acceder a el desde el Edge creado en nuestra cuenta de NGROK.

Si queremos securizar el acceso una cosa que podemos hacer es por ejemplo definir el acceso con autenticacion con tu cuenta de Google:
````
ngrok http https://localhost:8080 --oauth=google
````

## API LOCAL
Podemos comprobar las requests que se van gestionando desde un dashboard web desde http://127.0.0.1:4040