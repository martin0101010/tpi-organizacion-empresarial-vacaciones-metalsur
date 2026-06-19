# TPI - Organización Empresarial: Chatbot de Gestión de Vacaciones

Trabajo Práctico Integrador de la cátedra **Organización Empresarial** (Tecnicatura Universitaria en Programación a Distancia - UTN).

Automatización del proceso de **gestión de solicitudes de vacaciones** de Metal Sur S.A. (empresa ficticia del sector manufacturero) mediante un chatbot simulador.

## Integrante
- Martín Milich — Comisión n° 17

**Docente Titular:** Esp. Lic. Gabriela Martínez
**Docente Tutor:** Cdor. Guillermo Carvajal

## Descripción del proyecto
El proceso de solicitud de vacaciones de Metal Sur S.A. se realizaba de forma completamente manual (pedido verbal, consulta de planilla por el encargado, comunicación informal de la decisión), sin trazabilidad ni registro automatizado.

Este proyecto modela el proceso actual (AS-IS) y propone una solución optimizada (TO-BE) mediante notación BPMN 2.0, implementada a través de un chatbot simulador que ejecuta el flujo de extremo a extremo: verifica saldo de días contra una base de datos simulada, aplica reglas de decisión (gateways) y registra el resultado de la solicitud.

## Documentación
-  Informe completo (PDF): `docs/TPI_OE.pdf`
-  Anexo de capturas de pantalla: `docs/Anexo.pdf`
-  Diagramas BPMN 2.0:
  - AS-IS (proceso actual): `docs/bpmn/BPMN_as_is.bpmn`
  - TO-BE (proceso propuesto): `docs/bpmn/BPMN_to-be.bpmn`
  - (Abrir con [bpmn.io](https://bpmn.io) o cualquier visor BPMN 2.0)
-  Base de datos simulada (saldos, solicitudes): `data/Base_de_Datos.xlsx`

## Stack tecnológico
- **Lenguaje:** HTML5 + CSS3 + JavaScript (vanilla, sin dependencias externas)
- **Plataforma:** simulador web ejecutable en cualquier navegador
- **Persistencia:** planilla Excel simulando base de datos (saldos de días por empleado, historial de solicitudes)
- **Gestión de estados:** máquina de estados implementada en JavaScript dentro de `chatbot_vacaciones.html`, que mantiene el paso del flujo en el que se encuentra cada usuario (selección de fecha → verificación de saldo → decisión del encargado → notificación)

## Estructura del repositorio
```
/
├── README.md
├── docs/
│   ├── TPI_OE.pdf
│   ├── Anexo_Capturas_de_pantalla.pdf
│   └── bpmn/
│       ├── BPMN_as_is.bpmn
│       └── BPMN_to-be.bpmn
├── src/
│   └── chatbot_vacaciones.html
└── data/
    └── Base_de_Datos.xlsx
```

## Cómo desplegar / ejecutar el bot

No requiere instalación ni dependencias.

### Opción 1: Abrir directo en el navegador
1. Clonar el repositorio:
   ```bash
   git clone https://github.com/martin0101010/tpi-organizacion-empresarial-vacaciones-metalsur
   cd tpi-organizacion-empresarial-vacaciones-metalsur
   ```
2. Abrir `src/chatbot_vacaciones.html` con doble clic, o arrastrarlo a una pestaña del navegador.

### Opción 2: Servidor local (opcional)
```bash
cd src
python -m http.server 8000
```
Y abrir `http://localhost:8000/chatbot_vacaciones.html`

### Flujo de prueba sugerido (camino feliz)
1. Iniciar la simulación con el botón de inicio del chat.
2. Seleccionar fechas de vacaciones solicitadas.
3. El bot consulta el saldo disponible (simulación de consulta a `Base_de_Datos.xlsx`).
4. Si hay saldo suficiente → el encargado aprueba → notificación de confirmación.

### Flujo de prueba sugerido (camino infeliz)
1. Solicitar más días de los disponibles en el saldo → el bot rechaza automáticamente y explica el motivo.
2. Ingresar una fecha en formato inválido → el bot solicita corrección sin perder el estado de la conversación.

## Máquina de estados (resumen)
El bot mantiene en memoria el estado de cada conversación a lo largo de las etapas: **inicio → solicitud de fecha → verificación de saldo → decisión (gateway) → aprobación/rechazo → notificación final**. El detalle completo de transiciones y manejo de errores de entrada está documentado en la sección 6.7 y 6.8 del informe (`docs/TPI_OE.pdf`).

## Herramientas de IA utilizadas
Ver capturas de pantalla de las consultas y respuestas en `docs/Anexo.pdf` y sección 6.11 del informe.

## Licencia / Uso académico
Proyecto desarrollado con fines académicos para la Tecnicatura Universitaria en Programación a Distancia (UTN).
