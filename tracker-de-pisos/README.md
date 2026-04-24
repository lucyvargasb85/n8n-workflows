🏠 Tracker de Pisos — Gmail a Google Sheets
Workflow de n8n que monitoriza automáticamente emails de portales inmobiliarios (Fotocasa, Idealista, Yaencontré) y extrae los pisos en venta para guardarlos en una hoja de cálculo de Google Sheets.

📋 Descripción general
CampoValorNombreTracker de Pisos - Gmail a Google SheetsID[WORKFLOW_ID]EstadoInactivo (ejecución manual)Creado20 de abril de 2026Última actualización23 de abril de 2026

🔄 Flujo del workflow
[Gmail Trigger] → [Extraer Pisos del Email] → [Separar Pisos en Items] → [Guardar en Google Sheets]
Diagrama de nodos
Nuevos Emails de Pisos
        │
        ▼
Extraer Pisos del Email (Code)
        │
        ▼
Separar Pisos en Items (Split Out)
        │
        ▼
Guardar Piso en Google Sheets

🧩 Nodos
1. Nuevos Emails de Pisos

Tipo: n8n-nodes-base.gmailTrigger (v1.3)
Descripción: Trigger que revisa la bandeja de Gmail cada hora buscando emails de los portales inmobiliarios.
Frecuencia de polling: Cada hora (everyHour)
Filtro de emails:

  from:enviosfotocasa@fotocasa.es 
  OR from:news@diario.idealista.com 
  OR from:no-reply@envios.yaencontre.com

Estado de lectura: Lee emails leídos y no leídos


2. Extraer Pisos del Email

Tipo: n8n-nodes-base.code (v2)
Modo: runOnceForEachItem
Descripción: Nodo de código JavaScript que parsea el contenido de cada email y extrae los datos de cada piso (título, precio, fuente y fecha).

Lógica de extracción por portal:
PortalLógicaFotocasaDetecta líneas con formato XXXXX € y busca el título en las siguientes 6 líneas con patrón piso · [título]IdealistaBusca líneas con precio en formato XXXXX € y toma la línea anterior como títuloYaencontréBusca patrones Piso en venta en [zona] y extrae precios con regex
Campos de salida:
json{
  "pisos": [
    {
      "titulo": "nombre/descripción del piso",
      "precio": "XXXXX €",
      "fuente": "Fotocasa | Idealista | Ya encontré",
      "fecha": "DD de Mes AAAA"
    }
  ]
}

3. Separar Pisos en Items

Tipo: n8n-nodes-base.splitOut (v1)
Descripción: Divide el array pisos del paso anterior en items individuales para procesarlos de forma independiente.
Campo a separar: pisos


4. Guardar Piso en Google Sheets

Tipo: n8n-nodes-base.googleSheets (v4.7)
Operación: appendOrUpdate (añade si no existe, actualiza si ya existe)
Hoja de cálculo: Ver Google Sheets
Pestaña: Pisos

Mapeo de columnas:
Columna SheetsValor n8nMatchTITULO{{ $json.titulo }}✅ Columna de matchPRECIO{{ $json.precio }}FUENTE{{ $json.fuente }}FECHA{{ $json.fecha }}

Nota: La columna TITULO se usa como clave para evitar duplicados.


⚙️ Requisitos y configuración
Credenciales necesarias

Gmail OAuth2 — para leer emails del trigger
Google Sheets OAuth2 — para escribir en la hoja de cálculo

Google Sheets esperada
La hoja debe tener las siguientes columnas en la primera fila:
TITULOPRECIOFUENTEFECHA

🚀 Cómo ejecutar

Abrir el workflow en n8n
Asegurarse de que las credenciales de Gmail y Google Sheets están configuradas
Activar el workflow para ejecución automática cada hora, o bien ejecutarlo manualmente desde el editor


📌 Notas adicionales

El workflow fue creado con asistencia de AI Builder de n8n
Actualmente está en modo inactivo (solo ejecución manual)
Para activarlo en producción, cambiar el estado a activo desde el editor de n8n
Si el campo from del email tiene un formato inesperado, el nodo "Extraer Pisos" incluye JSON.stringify para detectar el portal de forma robusta
