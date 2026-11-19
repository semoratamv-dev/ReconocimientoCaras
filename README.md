# Reconocimiento de caras

Aplicación web que utiliza la cámara del dispositivo y un modelo de imagen de
TensorFlow.js exportado desde Teachable Machine para clasificar en tiempo real
las imágenes en las clases **hombres** y **mujeres**.

> El proyecto clasifica imágenes según las categorías con las que se entrenó el
> modelo; no identifica a personas concretas ni verifica identidades. Las
> predicciones son estimaciones del modelo y pueden ser incorrectas.

## Requisitos

- Un navegador moderno con acceso a una cámara.
- Conexión a Internet para cargar TensorFlow.js, Teachable Machine y las fuentes
  desde sus CDN.
- Un servidor web local o un alojamiento con HTTPS. Los navegadores normalmente
  solo permiten el acceso a la cámara en contextos seguros como `localhost` o
  HTTPS; abrir `index.html` directamente puede impedirlo.

## Cómo ejecutar

Desde la carpeta del proyecto, inicia un servidor web local. Por ejemplo, con
Python instalado:

```powershell
py -m http.server 8000
```

Abre [http://localhost:8000](http://localhost:8000) en el navegador. También
puedes usar cualquier otro servidor estático, siempre que sirva esta carpeta
como raíz para que la ruta `modelo/` sea accesible.

1. Pulsa **Iniciar reconocimiento**.
2. Concede permiso para usar la cámara cuando el navegador lo solicite.
3. Consulta las probabilidades de cada clase en el panel de análisis.
4. Pulsa **Detener reconocimiento** para apagar la cámara y reiniciar los
   porcentajes.

Si no se puede abrir la cámara, revisa los permisos del sitio y confirma que la
aplicación se está ejecutando desde `localhost` o HTTPS.

## Estructura

```text
.
├── index.html          # Interfaz, estilos y lógica de la aplicación
└── modelo/
    ├── model.json      # Arquitectura del modelo de Teachable Machine
    ├── metadata.json   # Metadatos y nombres de las clases
    └── weights.bin     # Pesos entrenados del modelo
```

## Tecnologías

- HTML, CSS y JavaScript sin proceso de compilación.
- TensorFlow.js y `@teachablemachine/image`, cargados desde jsDelivr.
- Modelo de Teachable Machine con entrada de imagen de 224 × 224 píxeles y las
  clases indicadas en `modelo/metadata.json`.
- Cámara web, cuyo acceso y permiso gestiona el navegador.

## Privacidad y uso responsable

La aplicación obtiene imágenes de la cámara para generar predicciones en el
navegador. El código de este proyecto no incluye una función para guardar o
enviar imágenes. Aun así, usa la cámara solo con el consentimiento de las
personas involucradas y evita presentar las predicciones como una identificación
o una determinación fiable de la identidad o del género de una persona.

## Personalización del modelo

Para usar otro modelo compatible de Teachable Machine, sustituye los archivos
correspondientes dentro de `modelo/` y conserva los nombres `model.json` y
`metadata.json`, junto con el archivo de pesos referenciado por el modelo. Las
etiquetas que aparecen en la interfaz se leen de los metadatos.
