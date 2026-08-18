# Analytics Engineering: Data Warehouse para Costos y Gestión. 📊✈️

Este repositorio contiene el desarrollo de extremo a extremo de un ecosistema moderno de datos aplicado al control de gestión industrial.
---

## 🎯 Caso de Negocio: Fábrica Estacional de Alfajores (Córdoba)
Se modeló el comportamiento operativo y comercial de una planta industrial con un **Nivel de Actividad Previsto (NAP) de 10.000 unidades constantes mensuales** y una estructura de costos rígida:
*   **Precio Unitario:** $1.000 | **Costo Variable Unitario:** $500
*   **CIF Fijos Totales:** $1.200.000 | **Tasa Fija de CIF:** $120/unidad (\frac{\$1.200.000}{10.000 \text{ NAP}})

---

## 🚀 Arquitectura Tecnológica
*   **Ingeniería de Datos:** Python (Pandas, NumPy, SQLAlchemy) para simulación estacional automatizada e idempotente.
*   **Almacenamiento Cloud:** PostgreSQL Serverless en **Neon.tech** implementando un modelo relacional en estrella puro.
*   **Capa Analítica & BI:** Power BI Desktop + Modelado semántico dinámico mediante lenguaje **DAX**.

---

## 🔄 Flujo de Datos: Entradas y Salidas

Para garantizar la transparencia y el gobierno de datos del proyecto, el ecosistema procesa y genera los siguientes componentes de forma estricta:

### 📥 Archivos y Datos de Entrada (Inputs)
El sistema se alimenta de dos orígenes de datos clave:
1.  **Parámetros Doctrinarios Fijos (Hardcoded en Script):** Constantes rígidas exigidas por el planteo práctico de la cátedra (Precio, Costo Variable Unitario, CIF Fijos y el NAP de 10.000 unidades).
2.  **Señales de Simulación Estacional (Algorítmicas):** Vectores matemáticos generados con NumPy basados en una función senoidal que modela el consumo cordobés (picos de demanda en invierno y ociosidad en temporada estival).

### 📤 Archivos de Salida del Ecosistema (Outputs)
Al ejecutar el proceso completo, el proyecto consolida e impacta **4 archivos finales** con propósitos específicos:

1.  **`Tablero_Analisis_Costos1.pbix` (Archivo de Inteligencia de Negocios):** Tablero interactivo final de Power BI Desktop de dos páginas, completamente modelado en esquema de estrella y optimizado para la toma de decisiones gerenciales.
2.  **`Auditoria_Costos1.xlsx` (Libro de Auditoría Multipestaña):** Archivo Excel exportado nativamente por Python desde la nube de Neon. Contiene dos pestañas independientes (`Costeo Variable` y `Costeo por Absorcion`) para facilitar el control manual a los contadores de la empresa.
3.  **`Reporte_Costeo_Variable.csv` (Dataset Plano - Costeo Directo):** Archivo de texto plano con los 12 meses consolidados bajo el modelo de la Unidad 4 (aislado de variaciones de stock, ideal para data science o machine learning).
4.  **`Reporte_Costeo_Absorcion.csv` (Dataset Plano - Costeo Integral):** Archivo de texto plano con el impacto mensual de la Variación Capacidad contable sobre la utilidad neta.

---

## 🧠 Lógica Contable Implementada (Motores DAX)

El tablero se divide estratégicamente en dos páginas de alta dirección:

### 1. Gestión de Modelos y Conciliación
*   **Regla de Oro:** Demuestra en vivo cómo la variación de los stocks de inventario impacta de manera diferente en la Utilidad Variable frente a la Utilidad por Absorción.
*   **Variación Capacidad Nativa:** Cálculo algorítmico automatizado para aislar las pérdidas del período provocadas por la subactividad de la planta: 
    $$\text{Variación Capacidad} = (\text{Producción Real} - \text{NAP}) \times \text{Tasa Fija}$$

### 2. Análisis Decisiones Operativas (Costo-Volumen-Utilidad)
*   **Punto de Equilibrio Dinámico ($Q_e$):** Fijado de forma exacta en **2.000 unidades físicas** o **$2,4 millones monetarios** para la cobertura total de la estructura de costos fijos.
*   **Evaluación del Riesgo de Explotación:** Visualización de la curva de Ingresos Reales vs. Costos Totales ($C_V + C_F$), acompañada por segmentadores trimestrales interactivos para analizar la volatilidad del **Margen de Seguridad %**.

*   ## 🔐 Seguridad y Despliegue Local (Nota para Evaluadores)

Para proteger las credenciales de administración del clúster cloud en **Neon.tech**, la cadena de conexión se gestiona de forma segura mediante variables de entorno cifradas utilizando el gestor nativo de Google Colab (`google.colab.userdata`).

Si desea replicar el pipeline de datos localmente o en su propio entorno, debe seguir estos pasos:

1. **Crear las credenciales:** Registre una base de datos gratuita en [Neon.tech](https://neon.tech) (PostgreSQL).
2. **Configurar el Secreto:** En la barra lateral izquierda de Google Colab, acceda al ícono de la llave (**Secrets**) y añada un registro con:
   * **Nombre:** `NEON_DB_URL`
   * **Valor:** Su cadena de conexión larga agrupada (*Pooled Connection String*), la cual incluye el usuario y contraseña de su servidor.
3. **Otorgar Permisos:** Asegúrese de activar el interruptor de **"Acceso desde el notebook"** (botón en color azul) antes de ejecutar la celda. El script leerá el entorno dinámicamente mediante `userdata.get('NEON_DB_URL')` sin exponer datos críticos en el código.
