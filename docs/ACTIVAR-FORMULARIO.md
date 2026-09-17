# Activar el formulario de propuestas

La web ya no depende de `mailto:` para enviar una propuesta. El navegador hace un `POST` AJAX y muestra una confirmación solo cuando Formspree responde correctamente. El endpoint definitivo ya está configurado.

## 1. Crear el destino

1. Entra en [Formspree](https://formspree.io/) con la cuenta vinculada a `contacto@apsagency.es`.
2. Abre el formulario definitivo de AP's Agency.
3. Confirma que el endpoint público es `https://formspree.io/f/mvkgonrz`.
4. En **Workflow/Email**, comprueba que la dirección de destino es la tuya y que está verificada.

Formspree guarda las solicitudes en su panel y puede enviar notificaciones al correo configurado. También admite integraciones adicionales, como una hoja de cálculo, desde su panel; comprueba qué opciones y límites tiene el plan que elijas.

## 2. Pegar el endpoint

`contact-config.js` debe quedar así:

```js
window.AP_CONTACT_CONFIG = Object.freeze({
  endpoint: 'https://formspree.io/f/mvkgonrz',
  timeoutMs: 10000
});
```

No pegues contraseñas, tokens privados ni claves de API. El endpoint de un formulario frontend es público por diseño; la seguridad se apoya en la configuración del formulario, el filtrado antispam y la revisión periódica del panel.

## 3. Publicar y probar

1. Sube de nuevo la carpeta `aps-agency` a Vercel.
2. Prueba desde móvil y ordenador con un lead de prueba real, usando un correo que controles.
3. Confirma que aparece en el panel y que llega la notificación a `contacto@apsagency.es` (revisa también spam).
4. Comprueba un envío correcto, un intento con datos incompletos, un doble clic en el botón y un fallo de red. El código desactiva el botón mientras espera y no muestra “recibido” sin una respuesta válida.

Si activas un reto reCAPTCHA visible en Formspree, informa de ello en la política de cookies y prueba su flujo móvil. El honeypot `_gotcha` ya se incluye en la web como filtro silencioso.

## Para mejorar la conversión

El formulario pide solo lo imprescindible, conserva los campos cuando falla el envío y ofrece WhatsApp y correo como vías alternativas. Responde rápido a cada aviso y etiqueta la solicitud en el panel para no perder seguimientos. No prometas plazos o resultados concretos que no puedas garantizar.
