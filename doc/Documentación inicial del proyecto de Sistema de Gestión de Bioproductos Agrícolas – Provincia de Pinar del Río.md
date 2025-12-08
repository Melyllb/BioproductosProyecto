
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

El diagrama de clases implementa un patrón MVC simplificado que mapea 1:1 con las historias de usuario. Cada clase de dominio representa una tabla lógica requerida por las HU, contiene los atributos necesarios para mostrar y validar la información (p. ej. `añoInicioIntroduccion` para filtrado en HU#1), y expone métodos CRUD para persistencia. El controlador actúa como mediador entre las vistas y los modelos, proporcionando datos preparados para UI (listas, selects, filtros) y centralizando reglas de orquestación (p. ej. validación compuesta).
## 1) **DiagnosticoCienciaTecnologia**

**Historias de usuario relacionadas:**

- HU #1: Consultar Diagnóstico Científico-Técnico de Bioproductos
    
- HU #2: Registrar Nuevo Diagnóstico Científico-Técnico
    

**Responsabilidad:**  
Representa un diagnóstico científico-técnico registrado en el sistema (resultado introducido, año, procedencia, impactos y barreras). Es la entidad principal para listar, filtrar por año y crear diagnósticos.

**Atributos (por qué y uso):**

- `id` — identificador único de la fila.
    
- `añoInicioIntroduccion` — necesario para filtrado por año (HU#1 exige filtro).
    
- `resultadoIntroducido` — texto principal que describe el resultado (se muestra en la tabla).
    
- `lugarGeneralizacion` — mostrado en la tabla.
    
- `procedenciaEntidad` (EntidadConsumidora) — relación que indica origen/procedencia.
    
- `impactoEconomico`, `impactoSocial`, `impactoAmbiental` — booleans para marcar X en la columna “Impacto”.
    
- `barreras` — texto opcional para mostrar barreras, puede estar vacío.
    

**Métodos (por qué y uso):**

- `mostrarTodos()` — devuelve la lista completa para cargar la vista de consulta (HU#1).
    
- `filtrarPorAño(Integer año)` — requisito explícito de HU#1.
    
- `insertar(DiagnosticoCienciaTecnologia d)` — operación usada por la interfaz de registro (HU#2).
    
- `modificar(...)` / `eliminar(String id)` — métodos CRUD generales para administración (pueden ser necesarios en roles administrativos).
    

**Relaciones relevantes:**

- `DiagnosticoCienciaTecnologia --> EntidadConsumidora` porque la procedencia es una entidad (HU1 solicita mostrar procedencia).
    

**Interacción con controlador y vista:**

- La vista (IConsultarDiagnosticos) llama al `ControladorPrincipal.listarDiagnosticos()` o `filtrarDiagnosticosPorAño(año)`.
    
- El controlador invoca `DiagnosticoCienciaTecnologia.mostrarTodos()` o `filtrarPorAño(año)` y formatea/entrega los datos a la tabla.



**Validaciones prácticas:**

- `añoInicioIntroduccion` rango permitido (ej. 2015–2025).
    
- `resultadoIntroducido` obligatorio.
    
- Al insertar, validar existencia/consistencia de `procedenciaEntidad`.
    

---

## 2) **EntidadConsumidora**

**Historias de usuario relacionadas:**

- HU #3: Consultar Catálogo Consolidado (usa entidades para buscar/filtrar)
    
- HU #4 / HU #5: Aplicaciones en Campo (selector de entidad consumidora)
    
- También usada en HU#1 y HU#2 como procedencia.
    

**Responsabilidad:**  
Catálogo maestro de organizaciones/entidades que consumen los bioproductos (UEB, productores, CREE, etc.). Se usa como lista desplegable y para filtros en varias vistas.

**Atributos (por qué y uso):**

- `id`, `nombre`, `tipo`, `municipio` — información para mostrar en el catálogo consolidado.
    

**Métodos (por qué y uso):**

- `mostrarTodas()` — usado por el controlador para llenar combos y filtros.
    
- `insertar/modificar/eliminar()` — útiles en administración (no expuestos a usuarios finales).
    

**Relaciones relevantes:**

- Relacionada con `Pedido`, `AplicacionCampo`, `CatalogoAplicacion`, `DiagnosticoCienciaTecnologia`.
    

**Interacción con controlador y vista:**

- El catálogo consolidado (HU#3) usa entidades como filtro: vista usa `ctrl.filtrarCatalogoPorEntidad(nombre)` que internamente usa `CatalogoAplicacion.filtrarPorEntidad()` y puede usar `EntidadConsumidora` para validar nombres/IDs.
    

**Validaciones prácticas:**

- `nombre` obligatorio.
    
- Evitar duplicados por nombre/tipo.
    

---

## 3) **Bioproducto**

**Historias de usuario relacionadas:**

- HU #3 (filtrado por bioproducto en catálogo)
    
- HU #4 / HU #5 (selector en registro de aplicación)
    
- Catalogado como entidad referencial.
    

**Responsabilidad:**  
Define los bioproductos disponibles (EcoMic, QuitoMax, etc.) para usos en aplicaciones y catálogos.

**Atributos:**

- `id`, `nombre`, `tipo`, `descripcion` — necesarios para mostrar en selects y detallar en tablas.
    

**Métodos:**

- CRUD: `mostrarTodos()`, `insertar()`, `modificar()`, `eliminar()`.
    

**Relaciones:**

- `CatalogoAplicacion --> Bioproducto` y `AplicacionCampo --> Bioproducto`.
    

**Interacción:**

- Vista de registro (HU#5) solicita `ctrl.listarBioproductos()` → `Bioproducto.mostrarTodos()` para poblar el dropdown.
    
- Catalogo y reportes usan `filtrarPorBioproducto`.
    

**Validaciones:**

- `nombre` obligatorio; comprobar que `tipo` sea válido (según catálogo).
    

---

## 4) **Cultivo**

**Historias de usuario relacionadas:**

- HU #3 (catalogo por cultivo)
    
- HU #4 / HU #5 (selección de cultivo en registro de aplicación)
    

**Responsabilidad:**  
Catálogo de cultivos (arroz, maíz, frijol, etc.) usado para clasificar aplicaciones y resultados.

**Atributos:**

- `id`, `nombre`, `variedad` — info para selects y filtros.
    

**Métodos:**

- `mostrarTodos()` y CRUD.
    

**Relaciones:**

- `AplicacionCampo --> Cultivo`
    
- `CatalogoAplicacion --> Cultivo`
    

**Interacción:**

- Para registrar una aplicación, la vista pide lista de cultivos al controlador que llama a `Cultivo.mostrarTodos()`.
    

**Validaciones:**

- `nombre` obligatorio; `variedad` opcional o con longitud máxima.
    

---

## 5) **Pedido**

**Historias de usuario relacionadas:**

- HU #4 / HU #5 (el formulario de aplicación asocia una aplicación a un pedido)
    

**Responsabilidad:**  
Representa la solicitud/orden que motiva la aplicación en campo.

**Atributos:**

- `id`, `numeroPedido`, `fechaSolicitud`, `entidad` (EntidadConsumidora), `estado`.
    

**Métodos:**

- `mostrarTodos()` → útil si el productor selecciona a qué pedido pertenece la aplicación.
    
- `mostrarPorId(String id)` → obtener detalles para mostrar en formularios o validaciones.
    
- CRUD.
    

**Relaciones:**

- `Pedido --> EntidadConsumidora` (pedido está ligado a una entidad).
    
- `AplicacionCampo --> Pedido` (aplicación pertenece a un pedido).
    

**Interacción:**

- Al abrir el formulario de registrar aplicación (HU#5), la vista obtiene la lista de pedidos disponibles para ese productor vía `ctrl.listarPedidos()` que llama a `Pedido.mostrarTodos()` (o filtra por usuario).
    
- Al guardar una aplicación, `AplicacionCampo.insertar()` puede validar que `pedido.id` exista y que el `estado` del pedido permita nuevas aplicaciones.
    

**Validaciones:**

- Fecha en formato correcto; `numeroPedido` único o bien validado; `estado` en valores permitidos.
    

---

## 6) **AplicacionCampo**

**Historias de usuario relacionadas:**

- HU #4: Consultar Historial de Aplicaciones de Bioproductos en Campo
    
- HU #5: Registrar Nueva Aplicación de Bioproducto en Campo
    

**Responsabilidad:**  
Registra una aplicación real en el campo: qué bioproducto, en qué cultivo, área, dosis, método y condiciones climáticas; sirve como entidad central para historial y para relacionar evaluaciones post-cosecha.

**Atributos (clave):**

- `id`, `pedido`, `bioproducto`, `entidad`, `cultivo`, `variedad`, `areaAplicada`, `dosisAplicada`, `metodoAplicacion`, `condicionesClimaticas`.
    

**Métodos:**

- `mostrarTodas()` — para cargar la tabla de historial (HU#4). Debe soportar paginación y formato numérico (2 decimales para área/dosis).
    
- `insertar(AplicacionCampo a)` — validar campos obligatorios y rangos; persistir.
    
- `modificar` / `eliminar` — disponibles para administración.
    

**Relaciones:**

- Con `Pedido`, `Bioproducto`, `EntidadConsumidora`, `Cultivo`, `EvaluacionResultado`.
    

**Interacción con controlador y vista:**

- Vista pide datos maestros (pedidos, bioproductos, cultivos, entidades) al controlador para poblar selects.
    
- Al guardar, la vista invoca `ControladorPrincipal.registrarAplicacion(a)`; el controlador valida reglas de negocio (ej. `areaAplicada` dentro de 0.01–1000 ha) y luego llama `AplicacionCampo.insertar(a)`.
    
- La tabla de historial se llena con `ctrl.listarAplicaciones()` → `AplicacionCampo.mostrarTodas()`. La vista no realiza filtrados complejos; el controlador puede ofrecer filtros si se requiere (por fecha, por bioproducto, etc.).
    

**Validaciones prácticas:**

- `areaAplicada` rango (0.01–1000), formato 2 decimales.
    
- `dosisAplicada` formato (ej. regex para "N L/ha" o "N kg/ha" si se requiere).
    
- Campos select obligatorios: Pedido, Bioproducto, Entidad, Cultivo, Método de aplicación.
    

---

## 7) **EvaluacionResultado**

**Historias de usuario relacionadas:**

- HU #6: Consultar Resultados Post-Cosecha
    
- HU #7: Registrar Resultados Post-Cosecha
    

**Responsabilidad:**  
Almacenar los resultados de la evaluación post-cosecha asociados a una aplicación concreta: rendimiento, incremento, calidad, incidencia de plagas, vigor de planta, análisis de suelo, validación por investigador.

**Atributos:**

- `id`, `aplicacion` (link a AplicacionCampo), `fechaEvaluacion`, `rendimiento`, `incrementoPorcentual`, `calidadProducto`, `incidenciaPlagas`, `efectividadControl`, `vigorPlanta`, `desarrolloVegetativo`, `costoProduccion`, `analisisSueloPost`, `validado`, `investigadorValidador`.
    

**Métodos:**

- `mostrarTodos()` — para mostrar la lista en HU#6 con formatos y etiquetas coloreadas (vigor, validado).
    
- `insertar(EvaluacionResultado e)` — registrar evaluación, validar rangos numéricos (efectividad 0–100%, rendimiento >0, etc.).
    
- `modificar` / `eliminar` — soporte administrativo.
    

**Relaciones:**

- `EvaluacionResultado --> AplicacionCampo` (evaluación pertenece a una aplicación registrada).
    

**Interacción con controlador y vista:**

- En el formulario de registro (HU#7), la vista pide al controlador la lista de `AplicacionCampo` disponibles para seleccionar la aplicada a evaluar.
    
- Al guardar, `ControladorPrincipal.registrarResultado(r)` valida: si `validado==true` entonces `investigadorValidador` debe ser seleccionado. Luego llama a `EvaluacionResultado.insertar(r)`.
    
- La vista de resultados (HU#6) usa `ctrl.listarResultados()` para llenar la tabla y mostrar etiquetas coloreadas según reglas (por ejemplo, `vigorPlanta=="Muy Alto"` → etiqueta verde).
    

**Validaciones prácticas:**

- `fechaEvaluacion` formato dd-mm-aaaa.
    
- `rendimiento` > 0; `efectividadControl` entre 0 y 100; `costoProduccion` >= 0.01; si `validado==true` entonces `investigadorValidador` obligatorio.
    

---

## 8) **CatalogoAplicacion**

**Historias de usuario relacionadas:**

- HU #3: Consultar Catálogo Consolidado de Bioproductos por Entidad y Cultivo
    

**Responsabilidad:**  
Entidad que consolida registros por entidad, bioproducto y cultivo y almacena un resultado agregado (Éxito, Moderado, Fallido). Sirve para la vista de catálogo consolidado que permite búsqueda por entidad y filtrado por bioproducto.

**Atributos:**

- `id`, `entidad`, `bioproducto`, `cultivo`, `resultado` (string o enum para estado).
    

**Métodos:**

- `mostrarTodos()` — devuelve listado para tabla del catálogo.
    
- `filtrarPorEntidad(String nombre)` — implementa búsqueda dinámica por entidad (HU#3 exige campo "Buscar por entidad").
    
- `filtrarPorBioproducto(String idBio)` — filtro desplegable por bioproducto.
    

**Relaciones:**

- `CatalogoAplicacion --> Bioproducto`
    
- `CatalogoAplicacion --> Cultivo`
    
- `CatalogoAplicacion --> EntidadConsumidora`
    

**Interacción con controlador y vista:**

- Vista de catálogo (IConsultarCatalogo) llama a `ControladorPrincipal.listarCatalogo()` o a `filtrarCatalogoPorEntidad(nombre)`; el controlador invoca `CatalogoAplicacion.*` y devuelve los datos con el recuento “Mostrando X de Y registros”.
    
- La vista presenta botones/etiquetas coloreadas según `resultado` (verde/naranja/rojo).
    

**Validaciones prácticas:**

- `resultado` ser uno de los valores permitidos (Éxito/Moderado/Fallido).
    
- Filtrado eficiente (preferible delegar a BD con índices).











