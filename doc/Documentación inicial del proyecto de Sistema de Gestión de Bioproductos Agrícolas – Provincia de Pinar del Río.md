
Este documento constituye la especificación técnica inicial del sistema de gestión de bioproductos agrícolas, desarrollado en respuesta al **Programa de Bioproductos de uso agrícola (2021–2030)** del Ministerio de la Agricultura (MINAG) en la provincia de Pinar del Río.

El sistema tiene como **objetivo general** apoyar la toma de decisiones estratégicas y operativas mediante el registro, seguimiento y evaluación de la aplicación de bioproductos en el territorio, con el fin de:
- Incrementar sosteniblemente la producción agrícola (>30%),
- Reducir la dependencia de insumos importados,
- Generalizar los resultados de la ciencia y la técnica en el 100% de los centros productivos.


---

## **Actores del Sistema**

| **Rol** | **Responsabilidades** | **Historias de Usuario Asociadas** |
|--------|------------------------|-----------------------------------|
| **Gerente** | Evaluar avances científicos, registrar diagnósticos tecnológicos y definir estrategias. | HU #1, HU #2 |
| **Director Provincial MINAG** | Tomar decisiones estratégicas basadas en resultados consolidados (aprobación de objetivos, inversiones, reportes). | HU #3 |
| **Productor de Base** | Registrar aplicaciones en campo, monitorear actividades y evaluar resultados post-cosecha. | HU #4, HU #5, HU #6, HU #7 |

---

## **Correspondencia entre Requisitos Funcionales y el Programa de Bioproductos**
#### **Interfaz 1 y 2: Gestión de Diagnóstico Científico-Técnico**  
**Historias de Usuario**: HU #1 (consultar) y HU #2 (registrar)  
**Tabla del documento original**: **Tabla 6a – “Aplicación de la ciencia y la técnica”** (páginas 11–13)

Estas interfaces permite **consultar y registrar los resultados científico-técnicos introducidos** en el territorio. Los campos clave —*resultado introducido, año de inicio, lugar de generalización, procedencia (provincial/nacional/extranjera), impacto económico/social/ambiental y barreras*— corresponden **exactamente** a las columnas de la **Tabla 6a**, que enumera resultados como *“Incremento de los rendimientos con EcoMic”*, *“Obtención de Quitosano”* o *“Efectividad del Nicosave”*, junto con sus impactos y limitaciones (ej: *“No existe escalado de la producción”*).  
Esta funcionalidad responde al **objetivo específico 3 del Programa**: *“Generalizar los resultados de la ciencia y la técnica en el 100% de los centros de producción”*.

---

#### **Interfaz 3: Catálogo Consolidado de Bioproductos**  
**Historia de Usuario**: HU #3  
**Secciones del documento original**: **Tabla 6a** y **Sección 17 – “Indicadores para la evaluación del impacto”**

Esta interfaz muestra un **resumen consolidado de aplicaciones**, con campos como *entidad, bioproducto, cultivo y resultado (Éxito/Moderado/Fallido)*.  
- La **combinación “bioproducto + cultivo + entidad”** se deriva directamente de ejemplos en la **Tabla 6a** (ej: *“EcoMic en arroz, maíz, frijol…” aplicado en “Productores”*).  
- El **“resultado” cualitativo** (Éxito/Moderado/Fallido) se basa en los **indicadores de impacto descritos en la Sección 17**, que miden rendimiento, calidad biológica y reducción de costos.  
Esta funcionalidad apoya la **toma de decisiones estratégicas** del Director Provincial, en línea con el **objetivo general del Programa**.

---

#### **Interfaz 4 y 5: Registro de Aplicaciones en Campo**  
**Historias de Usuario**: HU #4 (consultar) y HU #5 (registrar)  
**Tablas del documento original**: **Tabla 13 – “Resultados de la ciencia”** (páginas 26–29) y **Tabla de Balance de Tierras** (página 35)

Esta interfaz permite al Productor **registrar y consultar aplicaciones detalladas**. Los campos tienen correspondencia directa con el documento:
- **Cultivo y variedad**: listados en la **Tabla 13** (ej: *“frijol, maíz, arroz, tabaco, viandas”* y variedades como *“INCA LP-5”*).
- **Área aplicada**: se fundamenta en el **Balance de Tierras** (pág. 35), que detalla la superficie agrícola cultivable (351 527,89 ha).
- **Condiciones climáticas**: se alinea con el **ODS 13 (Acción por el clima)** y la **Sección 2**, que mencionan la necesidad de adaptación al *“cambio climático”* y a *“fenómenos meteorológicos extremos”*.
Esta funcionalidad materializa la **implementación operativa** de los resultados de la ciencia descritos en la **Tabla 13**.

---

#### **Interfaz 6 y 7: Evaluación Post-Cosecha**  
**Historias de Usuario**: HU #6 (consultar) y HU #7 (registrar)  
**Secciones del documento original**: **Tabla 6a** y **párrafo final de la Sección 5**

Esta interfaz permite **registrar y consultar los resultados técnicos y económicos** tras la cosecha. Los campos se alinean con el documento:
- **Rendimiento, calidad, incidencia de plagas, efectividad del control y costo de producción** se corresponden con afirmaciones de la **Tabla 6a** y la **Sección 5**, como: *“Se eleva la calidad y sanidad biológica de los productos agrícolas y disminuyen los costos de la producción”*.
- **Análisis de suelo post-aplicación** se vincula con el **ODS 15.3** (pág. 4), que promueve la *“rehabilitación de suelos degradados”* y la *“degradación neutra de suelo”*.
Esta funcionalidad cierra el **ciclo científico-productivo**, permitiendo validar y cuantificar el impacto de las aplicaciones, tal como exige el **Plan Nacional de Desarrollo Económico y Social**.

---





## **Interfaces y Derivación a Clases**
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

## **Diagrama de Clases**
#### **Descripción Detallada de Clases y Métodos**

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

### **`AplicacionCampo`**
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
Atributos
- `id`: Identificador único.
- `resultadoIntroducido`: Descripción del resultado científico.
- `descripcion`: Detalle adicional del diagnóstico.
- `añoInicioIntroduccion`: Año de generalización (clave para el filtro de HU #1).
- `procedencia`: “P. del Río”, “Nacional”, “Extranjero” (columnas 4–6 de la Tabla 6a).
- `impactoEconomico/Social/Ambiental`: Booleanos que indican el tipo de impacto.
- `barreras`: Obstáculos identificados (ej: “No existe escalado de la producción”).
- `entidad`: Entidad donde se generalizó el resultado (columna 3 de la Tabla 6a).
- **Métodos** (derivados de HU #1 y #2):
   - `+ mostrarTodos()`: Listado completo de diagnósticos (HU #1).
   - `+ filtrarPorAño(...)`: Filtro por año de introducción (HU #1).
   - `+ insertar(...)`: Registro de nuevo diagnóstico (HU #2).
   - `- modificar(...)`, `- eliminar(...)`: Privados.
- **Relaciones**: Asociada a una `EntidadConsumidora`.

---

### **`CatalogoAplicacion`**
**Propósito**: Provee una **vista consolidada para el Director Provincial MINAG**, tal como se describe en HU #3: _“Catálogo consolidado… con resultado (Éxito/Moderado/Fallido)”_.

 **Atributos**
- `id`: Identificador único.
- `entidad`: Entidad consumidora.
- `bioproducto`: Bioproducto aplicado.
- `cultivo`: Cultivo objetivo.
- `resultado`: Estado resumido (“Éxito”, “Moderado”, “Fallido”), derivado de los datos de `EvaluacionResultado`.

**Métodos**
- `+ mostrarTodos()`: Muestra todos los registros (HU #3).
- `+ filtrarPorEntidad(...)`: Búsqueda dinámica por nombre de entidad (HU #3).
- `+ filtrarPorBioproducto(...)`: Filtro por bioproducto (HU #3).
- `- insertar(...)`, `- modificar(...)`, `- eliminar(...)`: **Todos privados**, ya que el catálogo es **de solo lectura** y **no se edita directamente**.











