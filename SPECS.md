# SPECS.md - AgentHub Admin Panel

## 1. Descripcion del producto

### Que es AgentHub
AgentHub es una plataforma SaaS para alquiler de agentes de IA preconfigurados que empresas usan para operaciones repetitivas, soporte y productividad.

### Quien usa el panel
El panel es utilizado por el administrador interno de AgentHub para supervisar clientes, usuarios, agentes, skills, contrataciones y errores operativos.

### Que problema resuelve
Centraliza la gestion operativa en una unica interfaz para monitorear estado del servicio, calidad de ejecucion, adopcion de agentes y eventos criticos sin depender de backend en esta etapa.

### Que informacion administra
- Usuarios y cuentas de clientes.
- Agentes disponibles y su estado.
- Skills habilitadas por agente.
- Contrataciones activas y su detalle.
- Errores con severidad y trazas.
- Metricas clave para operacion.

## 2. Stack tecnologico y restricciones

### Stack
- HTML semantico.
- Tailwind CSS via CDN.
- JavaScript vanilla.
- Datos hardcodeados en JSON.
- Uso obligatorio de utilidades dark: de Tailwind para tema.

### Restricciones
- Sin frameworks.
- Sin backend.
- Sin archivos CSS externos.
- Sin estilos inline.

## 3. Secciones del panel

### Dashboard
1. Especificacion 1
Componente: Tarjeta de metrica.
Contenido visual: Cuatro tarjetas con icono, etiqueta y valor para ingresos del mes, perdida por descuentos/cupones, agentes activos y agentes fallando.
Comportamiento: Render inmediato al cargar la seccion y actualizacion al cambiar dataset hardcodeado.
Datos usados: dashboardMetrics y agregaciones de contracts y errors.

2. Especificacion 2
Componente: Grid de metric cards.
Contenido visual: Distribucion uniforme en desktop y reorganizacion en tablet sin perder jerarquia visual.
Comportamiento: Mantener contraste y legibilidad en modo claro y oscuro.
Datos usados: dashboardMetrics.

3. Especificacion 3
Componente: Placeholder de grafico de actividad semanal.
Contenido visual: Bloque destacado con ejes y leyenda simulada para actividad por dia.
Comportamiento: Solo representacion visual estatica en esta fase, sin librerias de chart.
Datos usados: Serie hardcodeada derivada de errors y contracts.

### Gestion de usuarios
1. Especificacion 1
Componente: Tabla de usuarios.
Contenido visual: Minimo 5 filas con nombre, email, plan y estado.
Comportamiento: Scroll horizontal controlado en tablet cuando sea necesario.
Datos usados: users.

2. Especificacion 2
Componente: Dropdown de acciones por fila.
Contenido visual: Acciones Ver detalle y Eliminar.
Comportamiento: Abre al hacer clic y cierra al hacer clic fuera.
Datos usados: id de usuario y estado de fila seleccionada.

3. Especificacion 3
Componente: Modal de detalle de usuario.
Contenido visual: Registro completo del usuario con campos principales y estado.
Comportamiento: Se abre desde Ver detalle y se cierra con boton o backdrop.
Datos usados: users por userId.

### Gestion de agentes
1. Especificacion 1
Componente: Listado de agentes.
Contenido visual: Minimo 4 agentes con nombre, propietario, estado y resumen de skills.
Comportamiento: Tarjetas o filas consistentes con badge de estado.
Datos usados: agents.

2. Especificacion 2
Componente: Lista colapsable de skills por agente.
Contenido visual: Skills ocultas por defecto.
Comportamiento: Expandir y colapsar con transicion visible al interactuar.
Datos usados: agents.skillIds y skills.

3. Especificacion 3
Componente: Dropdown y modal de configuracion.
Contenido visual: Acciones Configurar y Eliminar; modal con prompt de sistema en textarea editable.
Comportamiento: Dropdown abre/cierra por clic externo; modal cierra por boton y backdrop.
Datos usados: agents, skills y prompt hardcodeado por agente.

### Skills
1. Especificacion 1
Componente: Catalogo de skills.
Contenido visual: Minimo 4 skills con nombre y descripcion.
Comportamiento: Render ordenado con cards o tabla segun breakpoint.
Datos usados: skills.

2. Especificacion 2
Componente: Contador de adopcion por skill.
Contenido visual: Cantidad de agentes que tienen habilitada cada skill.
Comportamiento: Conteo calculado desde relaciones hardcodeadas.
Datos usados: skills y agents.skillIds.

3. Especificacion 3
Componente: Bloque explicativo y dropdown de acciones.
Contenido visual: Texto breve sobre que significa una skill en AgentHub y acciones Ver detalle y Eliminar.
Comportamiento: Dropdown abre/cierra por interaccion de clic y cierre externo.
Datos usados: skills y referencias desde agents.

### Contrataciones de agentes
1. Especificacion 1
Componente: Tabla de contratos.
Contenido visual: Minimo 4 filas con cliente, agente, skills contratadas, fechas e importe total.
Comportamiento: Priorizacion de columnas clave y legibilidad en tablet.
Datos usados: contracts, users, agents y skills.

2. Especificacion 2
Componente: Dropdown de acciones por contrato.
Contenido visual: Acciones Ver detalle y Eliminar o equivalente administrativo.
Comportamiento: Apertura por clic y cierre al clic fuera.
Datos usados: contractId y estado del contrato.

3. Especificacion 3
Componente: Modal de desglose de contrato.
Contenido visual: Resumen completo con skills y precios individuales.
Comportamiento: Apertura desde Ver detalle y cierre por boton o backdrop.
Datos usados: contracts y detalle hardcodeado de pricing por skill.

### Log de errores
1. Especificacion 1
Componente: Tabla o listado de errores.
Contenido visual: Minimo 5 errores con timestamp, agente, tipo y descripcion.
Comportamiento: Orden descendente por fecha para priorizar incidentes recientes.
Datos usados: errors y agents.

2. Especificacion 2
Componente: Badges de severidad o tipo.
Contenido visual: Distintivos visuales por gravedad (low, medium, high, critical).
Comportamiento: Cambio de color segun severidad con contraste accesible en ambos temas.
Datos usados: errors.severity.

3. Especificacion 3
Componente: Dropdown y modal de detalle de error.
Contenido visual: Acciones Ver detalle y Marcar como resuelto; modal con traza completa.
Comportamiento: Dropdown cierra al clic fuera; modal cierra por boton y backdrop; accion de resuelto actualiza estado visual local.
Datos usados: errors, agentId y contractId.

## 4. Inventario de componentes reutilizables

1. Sidebar lateral persistente
Proposito: Navegacion principal entre seis secciones.
Donde se usa: Estructura global del panel.
Comportamiento esperado: Mantiene seccion activa visible y oculta las demas.

2. Barra superior
Proposito: Contexto de seccion y acciones globales.
Donde se usa: Encabezado fijo del area principal.
Comportamiento esperado: Contiene toggle de tema y mantiene estado entre navegacion.

3. Toggle de modo claro/oscuro
Proposito: Cambiar tema global.
Donde se usa: Barra superior.
Comportamiento esperado: Aplica dark: en todo el panel y persiste estado visual.

4. Tarjeta de metrica
Proposito: Mostrar KPI clave.
Donde se usa: Dashboard.
Comportamiento esperado: Presenta icono, etiqueta y valor con jerarquia clara.

5. Tabla responsive
Proposito: Listar registros estructurados.
Donde se usa: Usuarios, contratos y errores.
Comportamiento esperado: Mantiene legibilidad en desktop y tablet.

6. Badge de estado
Proposito: Destacar estado o severidad.
Donde se usa: Agentes, usuarios y errores.
Comportamiento esperado: Color semantico consistente por estado.

7. Dropdown de acciones
Proposito: Agrupar acciones por fila o item.
Donde se usa: Usuarios, agentes, skills, contratos y errores.
Comportamiento esperado: Abre por clic, cierra por clic fuera.

8. Modal overlay
Proposito: Mostrar detalle ampliado o configuracion.
Donde se usa: Minimo en usuarios, agentes, contratos y errores.
Comportamiento esperado: Cierre por boton y por clic en backdrop.

9. Lista colapsable de skills
Proposito: Compactar detalle de capacidades por agente.
Donde se usa: Gestion de agentes y detalle de contratos.
Comportamiento esperado: Inicia colapsada y expande con transicion.

10. Boton primario
Proposito: Accion principal del contexto actual.
Donde se usa: Formularios y modales.
Comportamiento esperado: Estado hover y foco visible con contraste suficiente.

11. Boton secundario
Proposito: Accion alternativa o cancelacion.
Donde se usa: Modales y controles de seccion.
Comportamiento esperado: Diferenciacion visual clara respecto al primario.

12. Placeholder de grafico
Proposito: Reservar espacio visual para tendencia semanal.
Donde se usa: Dashboard.
Comportamiento esperado: Bloque estatico consistente con tema claro/oscuro.

## 5. Datos hardcodeados requeridos

Resumen basado en data/agenthub-data.json:
- Usuarios: Coleccion users con al menos 5 registros y campos de identidad operativa y estado.
- Agentes: Coleccion agents con al menos 4 agentes, estado, version y skillIds.
- Skills: Coleccion skills con al menos 4 habilidades, categoria y descripcion.
- Contratos: Coleccion contracts con al menos 4 contrataciones, referencias cruzadas a userId, agentId y skillIds.
- Errores: Coleccion errors con al menos 5 logs, severidad, agente asociado y mensaje.
- Metricas: Objeto dashboardMetrics con cuatro metricas principales del panel.

Condicion de consistencia:
- Las referencias entre users, agents, skills, contracts y errors deben mantenerse consistentes en todas las secciones visuales.

## 6. Comportamientos interactivos obligatorios

1. Dropdowns abren por clic y cierran al hacer clic fuera.
2. Modales abren desde acciones especificas en tablas o listados.
3. Modales cierran con boton de cierre y clic en backdrop.
4. Skills de agentes inician colapsadas y se expanden con transicion visible.
5. Toggle claro/oscuro afecta todo el panel usando utilidades dark:.
6. Navegacion lateral marca la seccion activa y oculta secciones inactivas.

## 7. Criterios de aceptacion

1. SPECS.md existe en la raiz del proyecto.
2. SPECS.md fue creado antes del primer archivo HTML funcional.
3. La especificacion contiene al menos tres requisitos concretos para cada una de las seis secciones.
4. El panel final contiene las seis secciones requeridas.
5. Las seis secciones son accesibles desde la navegacion lateral.
6. Todas las filas o listados tienen dropdown funcional.
7. Ver detalle abre modal en al menos cuatro secciones diferentes.
8. Los modales se cierran con boton y backdrop.
9. Las skills de agentes estan colapsadas por defecto.
10. Las skills se expanden y colapsan con transicion visible.
11. El modo claro y oscuro cambia todo el panel usando utilidades dark: de Tailwind.
12. Los datos hardcodeados son consistentes entre secciones.
13. El HTML final usa etiquetas semanticas como header, nav, main, section y table.
14. El layout es usable en desktop y tablet.
15. No se usan frameworks ni backend.
16. No hay CSS externo ni estilos inline.
