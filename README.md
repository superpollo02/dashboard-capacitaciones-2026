# Dashboard de Capacitaciones 2026 — Ministerio de Salud y Deportes

Dashboard analítico interactivo para la gestión, seguimiento, auditoría y visualización estratégica de las instancias de capacitación planificadas y ejecutadas por el Ministerio de Salud y Deportes (Gobierno de Mendoza).

El proyecto transforma la planilla de registro de capacitaciones en una aplicación web moderna, accesible online para todo el equipo sin requerir instalación local ni bases de datos complejas.

---

## 🌐 Enlace del Repositorio
- **GitHub:** [https://github.com/superpollo02/dashboard-capacitaciones-2026](https://github.com/superpollo02/dashboard-capacitaciones-2026)

---

## 📈 ¿Cómo Funciona el Dashboard?

### 1. Indicadores Principales (KPIs)
- **Total de Instancias:** Conteo dinámico de cursos, talleres, jornadas y ateneos según los filtros activos.
- **Horas Totales Estimadas:** Suma de carga horaria de las instancias y promedio de duración.
- **Distribución de Situación:**
  - **Ejecutadas:** Instancias cuya fecha ya ha transcurrido.
  - **Planificadas:** Instancias con fecha futura programada (con desglose de aprobadas vs. en gestión).
  - **Sin fecha precisa:** Instancias que requieren definición de cronograma.
- **Calidad de Carga:** Porcentaje de actividades que cuentan con carga horaria completa.

### 2. Gráficos Analíticos e Interactividad (Cross-Filtering)
El dashboard cuenta con **11 visualizaciones interactivas** construidas sobre Chart.js:
1. **Organismos x Modalidad:** Barras apiladas que contrastan la modalidad de dictado (Presencial, Virtual, Híbrido, Asincrónico) en cada organismo.
2. **Distribución por Modalidad:** Proporción global de instancias por modalidad.
3. **Distribución por Estado:** Estado administrativo (Aprobado, Pendiente, En gestión, etc.).
4. **Distribución por Tipo de Formación:** Cursos, Talleres, Jornadas y Ateneos.
5. **Carga Horaria:** Segmentación por tramos de duración (`0-4 hs`, `4-8 hs`, `8-20 hs`, `+20 hs`).
6. **Destinatarios:** Clasificación automática del público objetivo (Enfermería, Medicina / Equipo de salud, Odontología, Nutrición, Salud Mental, Docentes, Residentes, etc.).
7. **Top Organismos más Activos:** Ranking de dependencias con mayor cantidad de actividades con fecha.
8. **Estado por Organismo:** Desglose del nivel de aprobación en las dependencias principales.
9. **Instancias Planificadas por Organismo:** Identificación de actividades planificadas que aún esperan aprobación.
10. **Instancias Sin Fecha por Organismo:** Detección de áreas con actividades pendientes de programar en calendario.
11. **Cronograma Mensual y Curva Acumulada:** Histograma de actividades por mes con curva de crecimiento acumulado anual.

> **Interactividad Bidireccional:** Al hacer clic en cualquier barra o segmento de los gráficos, todo el dashboard (tarjetas de KPI, los otros 10 gráficos y la tabla de detalle) se filtra automáticamente para ese valor. Los filtros aplicados se visualizan en un banner superior y pueden removerse con un clic.

### 3. Tabla de Detalle y Búsqueda
- Tabla paginada con ordenamiento multidireccional por cualquiera de sus columnas (Organismo, Instancia, Tipo, Modalidad, Estado, Situación, Fecha, Horas).
- Buscador libre por texto que filtra instancias en tiempo real.
- Modo de **Alto Contraste** para accesibilidad visual.

### 4. Exportación Ejecutiva a PDF
- El botón **"📄 Exportar consulta a PDF"** genera un informe apaisado A4 de alta resolución que incluye el encabezado institucional, la lista de filtros aplicados, capturas de los gráficos y la tabla de detalle completa.

---

## 🔄 ¿Cómo se Actualizan los Datos?

El sistema cuenta con un procesador en el navegador (`SheetJS`) con normalización automática de organismos, duraciones y fechas. Dispone de dos métodos de actualización:

### Método A (Recomendado): Conexión Directa en Vivo a Google Sheets
Podés vincular el dashboard directamente a tu planilla original en Google Drive para que cualquier cambio o carga nueva se refleje en el tablero automáticamente:

1. **Publicar la planilla:**
   - En Google Sheets, andá a **Archivo** > **Compartir** > **Publicar en la web**.
   - En la sección *Vínculo*, seleccioná la hoja de capacitaciones (o *Todo el documento*) y en formato elegí: **Valores separados por comas (.csv)**.
   - Hacé clic en **Publicar** y copiá el enlace generado.
2. **Vincular en el proyecto:**
   - Pegá ese enlace en la variable `GOOGLE_SHEETS_CSV_URL` en [index.html](file:///c:/Users/mfischer/Documents/antigravitiy%20proyectos/dashboard%20capacitaciones/index.html).
3. **Listo:** Cada vez que alguien abra el dashboard en Vercel o pulse el botón **"🔄 Sincronizar Google Sheets"**, los datos se consultarán en vivo desde Google Drive. Si falla la red o Google no responde, el dashboard recurre automáticamente a los datos de respaldo.

---

### Método B (Respaldo): Carga Manual desde Archivo Local
1. **Carga reactiva en vivo:**
   - Hacé clic en **"📂 Adjuntar Excel local"** y seleccioná la planilla oficial (`.xlsx` o `.csv`).
   - El dashboard normaliza y procesa los datos en el navegador al instante.
2. **Persistencia oficial en el repositorio:**
   - Al cargar el archivo, aparecerá el botón **"💾 Descargar capacitaciones.json"**.
   - Descargá ese archivo y reemplazalo en la carpeta `data/capacitaciones.json` de este repositorio.
   - Al hacer `git push` a GitHub, Vercel actualizará la copia de respaldo en segundos.

---

## 🚀 Despliegue en Vercel (Paso a Paso)

1. En tu panel de [Vercel](https://vercel.com/), hacé clic en **"Add New Project"**.
2. Seleccioná el repositorio `superpollo02/dashboard-capacitaciones-2026`.
3. Mantené la configuración por defecto:
   - **Framework Preset:** `Other`
   - **Root Directory:** `./`
4. Hacé clic en **"Deploy"**.
5. Vercel generará automáticamente tu URL pública segura HTTPS (ej. `https://dashboard-capacitaciones-2026.vercel.app`).

---

## 💻 Consulta y Uso Local

Podés utilizar el dashboard en tu computadora localmente:
- Abriendo directamente `index.html` con doble clic en tu navegador.
- O iniciando un servidor local:
```bash
npx serve -s . -l 3000
```
Y navegando a `http://localhost:3000`.

---

## 📁 Estructura del Repositorio

```text
├── index.html                                  # Aplicación web completa del dashboard
├── data/
│   └── capacitaciones.json                    # Dataset estructurado sincronizado (156 instancias)
├── assets/
│   └── logo.png                               # Isotipo institucional
├── Planilla_registro capacitaciones 2026.xlsx  # Planilla original de carga
├── vercel.json                                 # Configuración de despliegue y caché de Vercel
├── package.json                                # Scripts de servidor local y metadatos
├── .gitignore                                  # Reglas de exclusión para Git
└── README.md                                   # Documentación completa del proyecto
```
