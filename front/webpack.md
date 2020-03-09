# Webpack

Transpilación y agrupación javascript.

- **Codificación interactiva** - en lugar de escribir código, compilar, esperar, recargar, Hot Module Reload (HMR)
- **Compilación perfecta de cualquier cosa** - code, styles, layout, images, fonts, etc. Hassel. Grafos.
- **Herramientas consistentes** - no atado a un particular IDE and/o OS.
- **Modularity**
- **Bundling** - paquete por página, división de paquete / código, minificar, paquetes de alojamiento diferido, eliminar código no utilizado.
- **lodash** - Lodash es una biblioteca de JavaScript que proporciona funciones de utilidad para tareas de programación comunes utilizando el paradigma de programación funcional. 

~~~
npm install lodash
import _ from 'lodash';
~~~
- **Interoperabilidad de formato de módulo** - CJS (node), ESM (harmony), **AMD (requireJS)**, UMD, globals
- **Módulo cargador / resolución** - Su responsabilidad es especificar las relaciones entre los módulos, no las rutas y el orden de los scripts.
- **Chaching** - que se pueden adaptar al desarrollo y la producción por separado.
- **Dev isn´t prod** -  puedes personalizar fácilmente las compilaciones por entorno.
- **Source Map** support - a través de todas tus transformaciones.
- **Platform for transformation** - cargadores - mediante babel, pero también webpack - codegen, codemod, funciones de inyección como soporte fuera de línea, etc.
- **AOT (Ahead-of-Time compiler) everything** - cuál es el mejor para su aplicación.
- **Incremental builds**