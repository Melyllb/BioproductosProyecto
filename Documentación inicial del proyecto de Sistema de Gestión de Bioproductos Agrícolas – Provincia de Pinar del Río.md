
Este documento constituye la especificación técnica inicial del sistema de gestión de bioproductos agrícolas, desarrollado en respuesta al **Programa de Bioproductos de uso agrícola (2021–2030)** del Ministerio de la Agricultura (MINAG) en la provincia de Pinar del Río.

El sistema tiene como **objetivo general** apoyar la toma de decisiones estratégicas y operativas mediante el registro, seguimiento y evaluación de la aplicación de bioproductos en el territorio, con el fin de:
- Incrementar sosteniblemente la producción agrícola (>30%),
- Reducir la dependencia de insumos importados,
- Generalizar los resultados de la ciencia y la técnica en el 100% de los centros productivos.

Este informe detalla **de dónde provienen cada una de las clases del diagrama de clases**, **cómo se derivan de las historias de usuario y las interfaces descritas**, y **cómo se alinean con el documento oficial del programa**. 

---

## Actores del Sistema

| **Rol** | **Responsabilidades** | **Historias de Usuario Asociadas** |
|--------|------------------------|-----------------------------------|
| **Gerente** | Evaluar avances científicos, registrar diagnósticos tecnológicos y definir estrategias. | HU #1, HU #2 |
| **Director Provincial MINAG** | Tomar decisiones estratégicas basadas en resultados consolidados (aprobación de objetivos, inversiones, reportes). | HU #3 |
| **Productor de Base** | Registrar aplicaciones en campo, monitorear actividades y evaluar resultados post-cosecha. | HU #4, HU #5, HU #6, HU #7 |

---

## Interfaces y Derivación a Clases

Cada interfaz descrita en las historias de usuario se traduce directamente en clases del modelo de dominio. A continuación, se muestra la traza **Interfaz → Historia de Usuario → Clase**.

### **Interfaz 1 y 2: Gestión de Diagnóstico Científico-Técnico**
- **Historias**: HU #1 (Consultar), HU #2 (Registrar)
- **Clase derivada**: `DiagnosticoCienciaTecnologia`
- **Justificación**: La interfaz muestra campos como “Resultado introducido”, “Año inicio introducción”, “Procedencia”, “Impacto” y “Barreras”. Estos se convierten en atributos de la clase. La relación con `EntidadConsumidora` se justifica porque cada diagnóstico se asocia a una entidad donde se generalizó el resultado (ver Tabla 6a del programa).

### **Interfaz 3: Catálogo Consolidado**
- **Historia**: HU #3
- **Clase derivada**: `CatalogoAplicacion`
- **Justificación**: Aunque esta clase representa una **vista lógica** (no una entidad persistente), se modela como clase en el diagrama para reflejar la estructura de datos que ve el Director Provincial. Sus atributos (`entidad`, `bioproducto`, `cultivo`, `resultado`) son una proyección de `AplicacionCampo` + `EvaluacionResultado`.

### **Interfaz 4 y 5: Registro de Aplicaciones en Campo**
- **Historias**: HU #4 (Consultar), HU #5 (Registrar)
- **Clase derivada**: `AplicacionCampo`
- **Justificación**: La interfaz lista campos como “Pedido”, “Bioproducto”, “Entidad Consumidora”, “Cultivo”, “Variedad”, “Área”, “Dosis”, etc. Todos se incluyen como atributos. Las relaciones con `Pedido`, `Bioproducto`, `EntidadConsumidora` y `Cultivo` reflejan que una aplicación depende de estas entidades maestras.

### **Interfaz 6 y 7: Evaluación Post-Cosecha**
- **Historias**: HU #6 (Consultar), HU #7 (Registrar)
- **Clase derivada**: `EvaluacionResultado`
- **Justificación**: La interfaz muestra métricas como “Rendimiento”, “Incidencia de plagas”, “Efectividad”, “Costo de producción”, etc. Estos campos se convierten en atributos. La relación con `AplicacionCampo` es obligatoria: cada evaluación pertenece a una aplicación específica.

### **Clases Maestras 
- **`EntidadConsumidora`**: Derivada de la Tabla 1a del programa (UBPC, UEB, CPA, CCS) y usada en HU #3, #4, #5.
- **`Bioproducto`**: Listados en la Sección 4.3 y Tabla 13 del programa (EcoMic, Trichoderma, Nicosave). Usada en HU #3, #4, #5.
- **`Cultivo`**: Mencionado en múltiples casos de la Tabla 6a (“arroz”, “maíz”, “tabaco”). Usado en HU #3, #4, #5.
- **`Pedido`**: Implícito en HU #4 y #5 como paso previo a la aplicación.

---

## Diagrama de Clases

## **Estructura General del Diagrama**

El modelo consta de **8 clases principales**, que representan los **conceptos del dominio agrícola-biotecnológico**:
- Clases maestras o catálogos: `EntidadConsumidora`, `Bioproducto`, `Cultivo`, `Pedido`.
- Clases operativas del ciclo productivo: `AplicacionCampo`, `EvaluacionResultado`.
- Clase estratégica de ciencia y tecnología: `DiagnosticoCienciaTecnologia`.
- Clase de vista consolidada: `CatalogoAplicacion`.

Cada clase incluye **métodos derivados directamente de las acciones descritas en las historias de usuario**: consultar, registrar, filtrar.

---

## **Descripción Detallada de Clases y Métodos**

### **`EntidadConsumidora`**
- **Propósito**: Representa a las unidades productivas que consumen bioproductos: UBPC (45), UEB (12), CCS (236), CPA (68), etc. (Tabla 1a del programa).
- **Atributos**:
  - `id`: Identificador único.
  - `nombre`: Ej: “UEB Genética Arrocera”.
  - `tipo`: “UBPC”, “UEB”, “CCS”, etc.
  - `municipio`: Localización geográfica.
- **Relaciones**: Usada por `Pedido`, `AplicacionCampo`, `DiagnosticoCienciaTecnologia` y `CatalogoAplicacion`.

---

### **`Bioproducto`**
- **Propósito**: Define los insumos biológicos disponibles: EcoMic, Trichoderma, Nicosave, etc. (Sección 4.3 y Tabla 13 del programa).
- **Atributos**:
  - `id`: Identificador único.
  - `nombre`: “Trichoderma harzianum”.
  - `tipo`: “Biofertilizante”, “Bioplaguicida”, “Bioestimulante”.
  - `descripcion`: Detalles técnicos del producto.
- **Relaciones**: Usada en `AplicacionCampo` y `CatalogoAplicacion`.

---

### **`Cultivo`**
- **Propósito**: Representa los cultivos agrícolas objetivo: arroz, maíz, frijol, tabaco, etc. (Tabla 6a del programa).
- **Atributos**:
  - `id`: Identificador único.
  - `nombre`: “Arroz”, “Maíz”.
  - `variedad`: “INCA LP-5”, “Corojo” (aunque también aparece en `AplicacionCampo`, se mantiene aquí por el diseño original).
- **Relaciones**: Contexto de `AplicacionCampo` y `CatalogoAplicacion`.

---

### **`Pedido`**
- **Propósito**: Registra la solicitud formal de bioproductos por parte de una entidad.
- **Atributos**:
  - `id`: Identificador único.
  - `numeroPedido`: Número de control.
  - `fechaSolicitud`: Fecha de la solicitud.
  - `entidad`: Referencia a `EntidadConsumidora`.
  - `estado`: “Aprobado”, “Pendiente”, etc.
- **Relaciones**: Pertenece a una `EntidadConsumidora` y origina una o más `AplicacionCampo`.

---

### ** `AplicacionCampo`**
- **Propósito**: Registra cada aplicación real de un bioproducto en el campo (HU #4, #5).
- **Atributos**:
  - `variedad`: Específica por aplicación (ej: “INCA LP-5”).
  - `areaAplicada`, `dosisAplicada`, `metodoAplicacion`, `condicionesClimaticas`, `fechaAplicacion`.
- **Métodos** (derivados de HU #4 y #5):
  - `+ consultarHistorialAplicaciones(): List<AplicacionCampo>`: Permite al Productor de Base ver todas sus aplicaciones registradas.
  - `+ registrarNuevaAplicacion(AplicacionCampo aplicacion): void`: Permite registrar una nueva aplicación.
- **Relaciones**: Depende de `Pedido`, `Bioproducto`, `EntidadConsumidora`, `Cultivo`.

---

### **`EvaluacionResultado`**
- **Propósito**: Documenta los resultados post-cosecha de una aplicación (HU #6, #7).
- **Atributos**:
  - `rendimiento`, `incrementoPorcentual`, `calidadProducto`.
  - `incidenciaPlagas`, `efectividadControl`.
  - `vigorPlanta`, `desarrolloVegetativo`.
  - `costoProduccion`, `analisisSueloPost`, `validado`, `investigadorValidador`.
- **Métodos** (derivados de HU #6 y #7):
  - `+ consultarResultadosPostCosecha(): List<EvaluacionResultado>`: Permite al Productor consultar sus resultados.
  - `+ registrarEvaluacionPostCosecha(EvaluacionResultado evaluacion): void`: Permite registrar una nueva evaluación.
- **Relaciones**: Asociada a una única `AplicacionCampo`.

---

### **`DiagnosticoCienciaTecnologia`**
- **Propósito**: Documenta los avances científicos y tecnológicos introducidos (HU #1, #2; Tabla 6a del programa).
- **Atributos**:
  - `resultadoIntroducido`: Descripción del resultado.
  - `añoInicioIntroduccion`: Año de generalización.
  - `procedencia`: “P. del Río”, “Nacional”, “Extranjero”.
  - `impactoEconomico/Social/Ambiental`: Booleanos.
  - `barreras`: Texto libre (ej: “No existe escalado de la producción”).
- **Métodos** (derivados de HU #1 y #2):
  - `+ consultarDiagnosticoPorAño(Integer año): List<DiagnosticoCienciaTecnologia>`: Permite filtrar diagnósticos por año.
  - `+ registrarNuevoDiagnostico(DiagnosticoCienciaTecnologia diagnostico): void`: Permite registrar un nuevo diagnóstico.
- **Relaciones**: Asociada a una `EntidadConsumidora`.

---

### **`CatalogoAplicacion`**
- **Propósito**: Provee una vista consolidada para el Director Provincial (HU #3).
- **Atributos**:
  - `resultado`: “Éxito”, “Moderado” o “Fallido” (derivado de la evaluación).
- **Métodos** (derivados de HU #3):
  - `+ consultarCatalogoConsolidado(): List<CatalogoAplicacion>`: Muestra todos los registros.
  - `+ filtrarPorEntidad(String nombreEntidad): List<CatalogoAplicacion>`: Filtra dinámicamente por entidad (ej: “UEB Genética Arrocera”).
  - `+ filtrarPorBioproducto(String bioproductoId): List<CatalogoAplicacion>`: Filtra por bioproducto específico.
- **Relaciones**: Asociada a `EntidadConsumidora`, `Bioproducto` y `Cultivo`.

> **Nota**: Aunque esta clase existe en el modelo, su implementación ideal es como **vista lógica derivada** de `AplicacionCampo` + `EvaluacionResultado`, no como tabla física.









---

## **Ciclo de Vida del Objeto y Flujo del Sistema**

El sistema sigue un flujo orientado a objetos coherente con el ciclo científico-productivo descrito en el programa:

1. **Diagnóstico**: Un `DiagnosticoCienciaTecnologia` se asocia a una `EntidadConsumidora`.
2. **Solicitud**: Una `EntidadConsumidora` crea un `Pedido`.
3. **Aplicación**: Un `Pedido` da origen a una `AplicacionCampo`.
4. **Evaluación**: Una `AplicacionCampo` tiene una `EvaluacionResultado`.
5. **Consolidación**: El sistema genera un `CatalogoAplicacion` derivado (vista) para el Director Provincial.








