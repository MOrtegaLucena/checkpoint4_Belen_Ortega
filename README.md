# TP 4: Integraciones Avanzadas e Interconexión de Sistemas (n8n)

## 📋 Descripción del Proyecto

Este repositorio contiene el flujo de trabajo exportado desde **n8n** (`checkpoint4_Belen_Ortega.json`) correspondiente al **Checkpoint 4**. El sistema evoluciona la arquitectura multi-agente con memoria persistente incorporando integraciones bidireccionales reales con herramientas externas del ecosistema de negocio mediante autenticación **OAuth2**, estableciendo controles preventivos no-code de gobernanza y seguridad operativa.

---

## 🔗 Herramientas Integradas (OAuth2)

1. **Gmail (`Gmail account`):** 
   * **Entrada:** Escucha activa de correos entrantes en la casilla de soporte mediante el nodo `Gmail Trigger (Soporte)`.
   * **Salida (Gobernanza):** Creación segura de borradores de respuesta mediante la herramienta `Gmail - Create Draft (HITL) ③` conectada al Agente AI.
2. **Airtable (`Airtable account` - CRM / Fuente Única de Verdad):** 
   * Búsqueda previa de registros por correo electrónico (`Session_ID`) para recuperar historial o crear nuevos perfiles sin duplicar contactos, además de actualizar el resumen consolidado de cada caso.
3. **Slack (`Slack account`):** 
   * Envío de notificaciones operativas estructuradas al canal `#operaciones` para alertar al equipo sobre los leads y consultas procesadas.

---

## 🛡️ Controles Preventivos y Gobernanza Implementados

El diseño del flujo incorpora las cuatro barreras de seguridad exigidas por la arquitectura:

* **① Control Anti Auto-Reply (`IF - Anti Auto-Reply`):** Ubicado inmediatamente después del trigger de Gmail. Evalúa mediante expresiones regulares que el asunto o cuerpo del correo no contenga etiquetas automáticas (`auto-reply`, `out of office`, `undeliverable`, `no-reply`), neutralizando bucles infinitos con otros bots.
* **② Prevención de Duplicados (`Search records (Look up)`):** Compuerta de búsqueda previa en Airtable antes de crear un nuevo registro de contacto/sesión, evitando errores de duplicidad (Error 409) y manteniendo una fuente única de verdad.
* **③ Human-in-the-Loop (`Gmail - Create Draft (HITL)`):** El agente tiene configurado exclusivamente el recurso `draft` para redactar la propuesta o respuesta al cliente. Ningún correo se emite automáticamente sin la revisión y aprobación previa de un operador humano.
* **④ Normalización y Limpieza de Payload (`Set - Clean Payload`):** Nodo intermedio que filtra y estandariza únicamente los campos esenciales (`From`, `Subject`, `BodyText`) antes de enrutar a los sub-workflows (`Worker_CRM_Extraccion` / `Worker_Email_Redaccion`) y notificar a Slack, evitando la saturación de datos pesados.

---

## 🔐 Evidencia de Credenciales Conectadas (OAuth2)

A continuación se adjunta la captura de la sección **Credentials** de n8n verificando las conexiones activas para Gmail, Slack y Airtable:

<img width="621" height="360" alt="image" src="https://github.com/user-attachments/assets/bf3f03dc-c06a-4be5-a1e3-8b6f7cace2f9" />

---

## 🔐 Evidencia de funcionamiento del flujo:


<img width="628" height="362" alt="image" src="https://github.com/user-attachments/assets/90b9c8be-6147-4a28-819b-0f8ef2c51aad" />
