## 1. Introducción 

Este documento presenta la Especificación de Requerimientos de Software (ESRE) del sistema de gestión para "El buen descanso". Su objetivo es describir las funcionalidades, reglas de negocio y requerimientos del sistema, sirviendo como base para el desarrollo de la aplicación y facilitando la comunicación entre los usuarios y el equipo de desarrollo. 

## 2. Alcance del producto / Software 

El propósito del sistema es gestionar socios y espacios fúnebres (parcelas, panteones, nichos) para el cementerio privado "El buen descanso", automatizando el proceso desde la solicitud web de afiliación hasta la administración de los núcleos familiares, la asignación de espacios y el registro de los pagos mensuales. 

## 1.2 Clases y Características de Usuarios 

Usuario Descripción Privilegios Interesado / Postulante Persona que desea afiliarse al servicio funerario. Completar solicitudes de afiliacion y consultar el estado de su solicitud. Socio Titular Persona responsable del nucleo familiar afiliado. Consultar información personal, gestionar integrantes del nucleo familiar y visualizar pagos realizados. 

Administrador Empleado encargado de la administracion del sistema. Aprobar o rechazar solicitudes, registrar socios, administrar pagos, gestionar espacios funebres, administrar empleados y generar reportes. 

## 1.3 Requerimientos Funcionales 

SEBA: RF1 – Solicitud de Afiliación Web Código: RF1 Nombre: Solicitud de afiliación web Descripción El sistema permitirá que cualquier persona interesada complete un formulario de afiliación desde la página web ingresando sus datos personales. 

La solicitud quedará registrada con estado Pendiente hasta que sea evaluada por un administrador. Prioridad Alta. Acción iniciadora El postulante presiona el botón Enviar Solicitud. Comportamiento esperado El sistema deberá: -validar los datos ingresados; -registrar la solicitud; -asignar el estado “Pendiente”; -informar al usuario que la solicitud fue registrada correctamente. 

RF2 – Gestión de Socios Código RF2 Descripción El administrador podrá registrar nuevos socios aprobados, modificar sus datos personales y consultar su información. Prioridad Alta. Acción iniciadora El administrador selecciona la opción Gestión de Socios. Comportamiento esperado El sistema deberá: verificar que exista una solicitud aprobada; registrar el socio; asignar número de socio; registrar la fecha de ingreso; asociar un espacio fúnebre. 

RF3 – Registro de Pagos mensuales Código RF3 Descripción El administrador podrá registrar el pago correspondiente al núcleo familiar. Prioridad Alta. Acción iniciadora El administrador selecciona “Registrar Pago”. Comportamiento esperado El sistema deberá: verificar que el monto sea mayor a cero; validar la fecha del pago; registrar el comprobante; actualizar el historial de pagos. 

RF4 – Administración de Núcleos Familiares Código RF4 Descripción El sistema permitirá crear, modificar y consultar los núcleos familiares asociados a un socio titular. 

Prioridad Media. Acción iniciadora El administrador accede a la opción “Núcleos Familiares”. Comportamiento esperado El sistema deberá: crear nuevos núcleos; asociar integrantes; registrar vínculos familiares; permitir modificaciones. 

## MATEO: 

RF1 – Solicitud de Afiliación Web 

Descripción: Permite al interesado completar un formulario web con sus datos para solicitar la afiliación. 

Prioridad: Alta. 

Estímulo: El interesado accede al sitio web y selecciona la opción "Solicitar afiliación". Comportamiento esperado del sistema: El sistema valida que los datos obligatorios estén completos, registra la solicitud con estado "Pendiente", genera un número identificador y confirma que la solicitud fue enviada correctamente. 

## RF2 – Gestión del Núcleo Familiar 

Descripción: Permite al Socio Titular declarar y mantener actualizados los integrantes de su grupo familiar. 

Prioridad: Media. 

Estímulo: El Socio Titular, luego de iniciar sesión, selecciona la opción "Gestionar mi grupo familiar". 

Comportamiento esperado del sistema: El sistema permite agregar, modificar o eliminar integrantes del núcleo familiar, registrando el vínculo de cada integrante y manteniendo actualizada la información del grupo familiar. 

## RF3 – Registro de Pagos Mensuales 

Descripción: Permite al Administrador registrar el pago mensual correspondiente a un núcleo familiar. 

Prioridad: Alta. 

Estímulo: El Administrador recibe el pago y registra la operación en el sistema. Comportamiento esperado del sistema: El sistema valida que el monto sea mayor a 0, que la 

fecha del pago no sea anterior a la fecha de ingreso del socio ni al último pago registrado, y actualiza el historial de pagos del núcleo familiar. 

## 4. Reglas de Negocio(RNE) 

proveniente de la solucion del ejercicio de empresa funebre parte 1. 

-RNE1 (Integridad Cronológica): En la tabla PAGOS, la fecha de pago (fec_ap) no puede ser anterior a la fecha de ingreso del socio (fec_ing). 

- RNE2 (Validación de Edad): El SOCIO debe tener una fec_nac que indique mayoría de edad (18 años o más). 

-RNE3 (Consistencia de Pagos): Fec_ap debe ser mayor o igual a la fecha de ingreso, pero también debe ser menor o igual a la actual (podría validarse que fuera mayor a la del último pago). 

-RNE4 (Consistencia de Pagos): En la tabla PAGOS monto debe ser mayor que 0. 

-RNE5 (Acceso Seguro): En SYS_LOG, si el campo 2FA es verdadero, el sistema no debe permitir el inicio de sesión sin la validación del segundo factor de autenticación. 

-RNE6 (Estado de solicitud): estado {"Aprobado",”Pendiente”,”Rechazado”}. 

- RNE7 (Flujo de Aprobación): No se puede crear un registro en SOCIOS si el estado de su respectiva SOLICITUD no es "Aprobado" por un ADMINISTRADOR. 

-RNE8 (Fecha de ingreso): cuando se genera la fec:ing debe ser menor o igual a la del sistema. -RNE9 (Tipos de espacios fúnebres): tipo {Parcela, Panteón, Nicho}. 

Código Regla RNE1 La fecha del pago no podrá ser anterior a la fecha de ingreso del socio. RNE2 Todo socio deberá ser mayor de edad (18 años o más). RNE3 

La fecha del pago deberá ser menor o igual a la fecha actual del sistema. RNE4 El monto del pago deberá ser mayor a cero. RNE5 

Cuando el segundo factor esté habilitado será obligatorio validarlo antes del acceso. 

## RNE6 

Toda solicitud tendrá estado Pendiente, Aprobado o Rechazado. RNE7 

No podrá registrarse un socio sin una solicitud previamente aprobada. RNE8 

La fecha de ingreso nunca podrá ser posterior a la fecha del sistema. RNE9 

Los espacios fúnebres únicamente podrán ser Parcela, Nicho o Panteón. 

## 5 Requerimientos No Funcionales 

## SEBA: 

RNF1 – Eficiencia 

El sistema deberá responder cualquier consulta en un tiempo máximo de 3 segundos para una carga de hasta 100 usuarios concurrentes. 

## RNF2 – Seguridad 

Todas las contraseñas deberán almacenarse cifradas. 

El sistema realizará respaldos automáticos diariamente. 

El acceso de administradores requerirá autenticación mediante usuario, contraseña y segundo factor cuando esté habilitado. 

## RNF3 – Usabilidad 

Un usuario con conocimientos básicos de informática deberá poder aprender el funcionamiento del sistema en menos de 30 minutos. 

Los mensajes de error deberán indicar claramente el problema y sugerir cómo solucionarlo. 

--- 

## MATEO: 

Requerimientos No Funcionales 

- Eficiencia: La consulta de espacios disponibles no debe superar los 2 segundos, con hasta 50 usuarios conectados a la vez. 

- Seguridad lógica y de datos: El acceso al sistema requiere usuario y contraseña. Cuando un usuario tenga habilitada la autenticación en dos factores (2FA), deberá validar el segundo factor antes de ingresar al sistema. Además, se realizará un respaldo diario de la base de datos. 

- Usabilidad: Un Interesado sin capacitación previa debe poder completar el formulario de afiliación en menos de 5 minutos, con mensajes de error claros y fáciles de comprender. 

## LEONARDO
2.1 Funcionalidades del producto
Las funcionalidades que el producto debe brindar son:
Gestión de Solicitudes de afiliación
Evaluación de solicitudes
Gestión socios
Gestión Personas
Gestión Administradores
Gestión Integrantes
Gestión Núcleos
Gestión Espacios fúnebres
Gestión Pagos
Consultas
Pagina web usuarios y administradores

2.2 Clases y características de usuarios
El producto a elaborar estará dirigido principalmente a tres tipos de usuarios:


USUARIO: Interesado
ROL: Persona que desea afiliarse a la empresa fúnebre mediante un formulario web
PRIVILEGIOS: Completar solicitud, consultar estado de la misma
USUARIO: Socio titular
ROL: Responsable del grupo familiar
PRIVILEGIOS: Gestionar datos personales, consultar pagos, visualizar integrantes del grupo familiar y espacio funerario asignado
USUARIO: Representante grupo familiar
ROL: Integrante autorizado que representa al grupo familiar cuando el titular no pueda hacerlo
PRIVILEGIOS: Consultar información del grupo familiar y datos personales autorizados, consultar pagos
USUARIO: Administrador
ROL: Empleado de la empresa encargado en la gestión de espacios fúnebres, socios y grupos familiares
PRIVILEGIOS: Aprobar solicitudes, registrar socios, asignar espacios fúnebres, control de pagos, gestionar socios y espacios fúnebres

## RF y RNF de LEONARDO
2.3 Requerimientos funcionales
A continuación se detallan los requisitos funcionales que el sistema deberá
implementar


RF-1 Solicitud Web de Afiliación
Descripción: El sistema deberá permitir que cualquier persona interesada complete un formulario de afiliación desde la web proporcionando toda la información requerida 
Prioridad: Alta
Acción iniciadora:
Interesado completa el formulario 
presiona en el botón de “Enviar”
Comportamiento esperado:
Validar los datos obligatorios del formulario
Registrar la solicitud con estado pendiente
Generar un número único de solicitud
Notificar al administrador para su evaluación
Mostrar al interesado el número de solicitud generado para su seguimiento

RF-2 Evaluación de Solicitudes
Descripción: El administrador podrá consultar todas las solicitudes pendientes y aprobarlas o rechazarlas
Prioridad: Alta
Acción iniciadora:
El administrador inicia sesión
Se dirige a la pantalla de solicitudes pendientes
Comportamiento esperado:
Mostrar todas las solicitudes pendientes
Permitir visualizar los datos completos del formulario
Registrar la fecha de evaluación
Registrar el administrador responsable
Cambiar el estado a aprobado o rechazado
Permitir generar posteriormente el alta del socio únicamente cuando la solicitud se encuentre aprobada

RF-3 Alta de Socio
Descripción: El sistema permitirá registrar un nuevo socio únicamente cuando se le haya aprobado su solicitud
Prioridad: Alta
Acción iniciadora:
El administrador aprueba la solicitud
Comportamiento esperado:
Crear el registro del socio
Registrar la fecha de ingreso
Asignar un número de socio
Registrar el núcleo familiar
Habilitar el acceso web del nuevo socio
Habilitar  el pago de cuota por afiliación

RF-4 Asignación de Espacio Funerario
Descripción: El sistema permitirá al administrador asignar un espacio fúnebre a un socio/grupo familiar
Prioridad: Alta
Acción iniciadora:
El administrador controla el correcto pago por afiliación realizado
Ingresa a la pantalla de gestión de socio
Selecciona el botón “Asignar espacio fúnebre”
Comportamiento esperado:
Asigna un espacio fúnebre dependiendo disponibilidad

RF-5 Portal del Socio
Descripción: El socio podrá consultar toda su información personal desde la web
Prioridad: Alta
Acción iniciadora:
El socio inicia sesión
Comportamiento esperado:
El sistema deberá mostrar:
Datos personales
Integrantes del grupo familiar y datos
Espacio fúnebre asignado
Historial de pagos

2.4 Requerimientos no funcionales
Eficiencia:
RNF-1 Toda funcionalidad del sistema debe responder al usuario en menos de 3 segundos.
RNF-2 El sistema debe ser capaz de operar adecuadamente con hasta 10.000 usuarios con sesiones concurrentes.
RNF-3 Los datos modificados en la base de datos deben ser actualizados para todos los usuarios del sistema en menos de 3 segundos.


Seguridad lógica y de datos
RNF-4 Autentificar los usuarios mediante usuario y contraseña, y autentificación en 2 pasos (codigo al celular)
RNF-5 Realizar copias de seguridad automáticas diariamente
RNF-6 Restringir el acceso según el rol del usuario
RNF-7 Realizar un monitoreo continuo ante posibles ataques de seguridad


Usabilidad
RNF-8 El sistema deberá ser intuitivo, de forma que un usuario administrativo pueda aprender su utilización básica en un tiempo máximo de 2 horas de capacitación
RNF-9 El sistema debe proporcionar mensajes de error que indiquen causa del problema y acción requerida para solucionarlo
RNF-10 El sistema debe poseer interfaces gráficas intuitivas para socios
