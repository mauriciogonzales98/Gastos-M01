# PRD-001: Gestion de Gastos — Aplicacion para el registro y gestion de gastos personales

## Contexto y Problema
Llevar el control de los gastos personales suele requerir anotar todo en una hoja de cálculo o app genérica, categorizando manualmente cada movimiento. Eso genera fricción: la gente deja de registrar gastos porque cargarlos "bien" (con categoría, fecha, etc.) toma tiempo. El resultado es que no se tiene una visión clara de en qué se gasta la plata. 

## Objetivos
Registrar gastos e ingresos de dinero de una manera simple y luego poder visualizarlos y consultarlos de manera sencilla en un dashboard.

## Requerimientos Funcionales
- RF-01: El sistema debe permitir registrar un gasto indicando monto, categoría y fecha (por defecto, la fecha actual).
- RF-02: El sistema debe permitir registrar un ingreso indicando monto, categoría y fecha (por - defecto, la fecha actual).
- RF-03: El sistema debe mostrar un dashboard con el total de gastos agrupado por categoría (gráfico de torta o barras).
- RF-04: El sistema debe permitir filtrar el listado y los totales por rango de fechas (este mes, mes anterior, rango personalizado).
- RF-05: El sistema debe listar los movimientos individuales (gastos e ingresos), filtrables por categoría y por fecha.
- RF-06: El sistema debe mostrar en la pantalla principal un resumen rápido con el total ingresado y el total gastado en el mes actual.
- RF-07: El sistema debe requerir autenticacion(email + contraseña, con sesion)

## Requerimientos No Funcionales
- RNF-01: El dashboard debe cargar en < 2 s p95 con hasta 1000 movimientos registrados.
- RNF-02: El registro de un gasto o ingreso debe confirmarse (guardado) en < 1 s p95.
- RNF-03: La API key del modelo no debe estar en el código; se lee de la variable
  de entorno ANTHROPIC_API_KEY.
- RNF-04: Las contraseñas deben almacenarse con hash seguro (bcrypt/argon2), nunca
  en texto plano; la sesión expira tras 24 h de inactividad.

## Criterios de Aceptación
- AC-01 (RF-01): Dado que el usuario completa monto y categoría de un gasto sin especificar fecha, cuando lo guarda, entonces el gasto queda registrado con la fecha del día actual.
- AC-02 (RF-02): Dado que el usuario completa monto y categoría de un ingreso, cuando lo guarda, entonces el ingreso queda registrado y disponible para los cálculos del mes.
- AC-03 (RF-03): Dado que existen gastos cargados en distintas categorías, cuando el usuario abre el dashboard, entonces ve el total correcto por cada categoría representado en un gráfico.
- AC-04 (RF-04): Dado que el usuario selecciona "mes anterior" como filtro, cuando aplica el filtro, entonces el listado y los totales muestran únicamente movimientos de ese rango.
- AC-05 (RF-06): Dado que hay gastos e ingresos cargados en el mes actual, cuando el usuario entra a la pantalla principal, entonces ve el total ingresado y el total gastado del mes, coincidentes con los que muestra el dashboard filtrado por "este mes".
- AC-06 (RF-07): Dado un usuario no autenticado este no debe poder realizar ninguna accion en la aplicacion que no sean crear una cuenta o iniciar sesion.(log in/sign in)

## Fuera de Alcance
- Conexión con bancos o tarjetas (APIs bancarias, Plaid, etc.)
- Multi-usuario / gastos compartidos
- Notificaciones push o recordatorios
- Exportación a otros formatos (PDF, Excel)
- Presupuestos y alertas de tope 

## Riesgos y Dependencias
- Riesgo: la categorización manual repetitiva puede generar la misma fricción que se buscaba evitar → mitigación: lista de categorías predefinida y acotada (no campo libre) para que cargar sea rápido.
- Dependencia: base de datos (MySQL) disponible para persistir gastos e ingresos
