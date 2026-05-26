# AgentHub - Diseno UI/UX

## Estilo visual general
El panel debe tener una estetica SaaS moderna, profesional, limpia y altamente usable.

Objetivos de estilo:
- Priorizar legibilidad y claridad de jerarquia visual.
- Mantener una apariencia sobria y consistente en todas las vistas.
- Facilitar la operacion administrativa con componentes previsibles y ordenados.

## Layout
Estructura base del prototipo:
- Sidebar lateral persistente para navegacion principal.
- Barra superior (header/topbar) para contexto global y acciones transversales.
- Area principal de contenido para renderizar cada seccion del panel.

Comportamiento de secciones:
- Las secciones se muestran u ocultan mediante navegacion lateral.
- Solo una seccion principal debe estar activa y visible a la vez.

## Modo claro/oscuro
Requisitos de tema:
- Incluir toggle de claro/oscuro en la barra superior.
- Implementar estilos usando utilidades `dark:` de Tailwind CSS.
- El estado visual seleccionado (claro u oscuro) debe mantenerse al cambiar entre secciones.

## Componentes reutilizables
Componentes base definidos para el sistema UI:
- Sidebar.
- Header/topbar.
- Metric cards.
- Tables.
- Badges.
- Dropdown de acciones.
- Modal overlay.
- Collapsible skills list.
- Placeholder de grafico.

Criterio de reutilizacion:
- Cada componente debe mantener estructura visual y comportamiento consistente sin duplicar variantes innecesarias.

## Reglas visuales
Lineamientos obligatorios de diseno:
- Buen contraste en textos, superficies y estados interactivos.
- Espaciado consistente entre bloques, titulos, controles y tablas.
- Bordes redondeados en contenedores y elementos interactivos.
- Sombras suaves para separar niveles de interfaz sin ruido visual.
- Diseno usable en desktop y tablet.
- Sin estilos inline.

## Interacciones requeridas
Comportamientos esperados para la siguiente etapa de implementacion:
- Dropdowns que abren al hacer clic y cierran al hacer clic fuera.
- Modales que abren desde acciones.
- Modales que cierran con boton y backdrop.
- Skills colapsadas por defecto y expandibles con transicion.
- Navegacion lateral con estado activo.
