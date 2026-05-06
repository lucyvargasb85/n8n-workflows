# 🤖 n8n-workflows

Colección de workflows de n8n que voy construyendo mientras aprendo la plataforma. Cada carpeta es un workflow independiente con su propio README, JSON exportable y screenshot.

> 📚 Estoy aprendiendo n8n desde cero y este repositorio es mi diario público de ese proceso. Los workflows van desde automatizaciones simples hasta flujos más complejos conforme avanzo. Si estás en el mismo camino, espero que te sirva de referencia o punto de partida.

---

## Workflows

| Workflow | Descripción | Nodos | Estado |
|---|---|---|---|
| [Tracker de Pisos](./tracker-de-pisos/) | Extrae pisos de emails de Fotocasa, Idealista y Yaencontre y los guarda en Google Sheets | Gmail · Code · SplitOut · Google Sheets | ✅ Activo |

---

## Estructura del repositorio

```
n8n-workflows/
├── README.md                          ← Este archivo
│
└── tracker-de-pisos/                  ← Workflow 01
    ├── README.md                      ← Documentación detallada
    ├── workflow.json                  ← JSON exportado (sin credenciales)
    └── screenshot.png                 ← Captura del canvas en n8n
```

---

## Cómo usar un workflow

1. Descarga el archivo `workflow.json` del workflow que te interese
2. En n8n: **Workflows → Import from file** y selecciona el JSON
3. Sigue los pasos del `README.md` de ese workflow para configurar credenciales y parámetros
4. Activa el workflow con el toggle superior derecho

---

## Stack

- **[n8n](https://n8n.io)** — plataforma de automatización self-hosted / cloud
- **Gmail API** — trigger de correo electrónico
- **Google Sheets API** — almacenamiento de datos
- JavaScript (nodos Code) — lógica de parsing y transformación

---

## Contacto

**Lucy Vargas** · lucy.vargasb85@gmail.com

Si tienes preguntas, sugerencias o quieres colaborar, no dudes en escribirme o abrir un issue. ¡Siempre bienvenido el feedback! 🙌
