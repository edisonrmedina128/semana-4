# FoodTech Frontend - Contexto de Negocio

## 1. Descripcion del Proyecto

Nombre del Proyecto: FoodTech Frontend

Objetivo: Proporcionar una interfaz de usuario para gestionar pedidos, ver y filtrar tareas por estaciones, revisar historial y gestionar usuarios. El frontend consume una API REST segura y maneja la autenticacion mediante JWT, mostrando dashboards, formularios y flujos operativos para usuarios autenticados y demostra la experiencia de usuario de un flujo ofrecido por el backend FoodTech Kitchen Service.

La arquitectura del frontend se alinea con practicas modernas (SPA, componentes reutilizables, gestion de estado) para facilitar la navegacion entre modulos como: inicio de sesion, registro de usuario, gestion de pedidos, visualizacion de tareas por estacion y facturacion en el plano visual, manteniendo la integridad de los datos recibidos desde el backend.

---

## 2. Flujos Criticos del Negocio

- Inicio de sesion y gestion de sesion (JWT) para acceso a endpoints protegidos.
- Creacion y gestion de pedidos desde el frontend, con validaciones basicas en el cliente antes de llamar a la API.
- Visualizacion de tareas por estacion, con filtros y campos relevantes para el usuario: numero de mesa, productos, hora de creacion, estado y identificador de la tarea.
- Flujo de facturacion, requerimiento de estado COMPLETED para activar la facturacion y notificaciones de fallo.
- Notificaciones de errores claras y consistentes (formatos JSON, canales de presentacion en UI).

---

## 3. Reglas de Negocio y Restricciones

- El frontend debe validar entradas basicas: numero de mesa, al menos un producto, y que los campos obligatorios esten presentes antes de enviar a la API.
- El estado de las tareas y pedidos se deriva de la respuesta del backend; el frontend debe reflejar los estados y garantizar que las transiciones validas sean mostradas a los usuarios.
- La autenticacion se maneja a traves de JWT obtenido al login; las llamadas protegidas requieren el token valido.
- Errores de conectividad o respuesta del backend deben mostrarse al usuario con un formato estandar. 

---

## 4. Perfiles de Usuario y Roles

- Usuario Autenticado: usuarios que han iniciado sesion y consumen endpoints protegidos.
- Operadores de Fachada: visibilidad de tareas por estacion, consulta de estado, y acciones permitidas segun el flujo de negocio (p. ej., iniciar/monitorizar tareas) en el frontend;
- A nivel frontend no se implementan permisos a nivel fino sino rutas protegidas y habilitacion de acciones segun el estado de la entidad.

---

## 5. Condiciones del Entorno Tecnico

- Plataforma: Frontend SPA (React o similar) con TypeScript para tipado, gestion de estado y llamadas a API.
- Comunicaciones: REST API con JWT; la token se envia en el header Authorization para endpoints protegidos.
- Almacenamiento: token de sesion en almacenamiento seguro (preferentemente almacenamiento seguro del navegador o cookies http-only si el servidor habilita CORS y cookies). Se recomienda evitar exponer el token en el almacenamiento local cuando sea posible.
- Pruebas: cobertura con pruebas unitarias de componentes, pruebas de integracion para flujos de login/registro y pruebas de extremo a extremo para flujos criticos.
- Entorno: pruebas locales con docker-compose simulando el backend, o entornos de staging.

---

## 6. Casos Especiales o Excepciones

- Sesiones caducadas o token invalido: redirigir a login, mostrar alerta explicita.
- Fallos en llamadas a la API: mostrar mensaje de error, registrar en logs UI y permitir reintento manual.
- Campos obligatorios ausentes: mostrar errores claros junto a cada campo.
- Registro de usuario duplicado: mostrar conflicto (409) y explicitar que el email/usuario ya existe.

---

## Recomendaciones de Uso
- El front debe permanecer alineado con las respuestas del backend; cualquier cambio en el modelo de datos debe ser reflejado en el frontend.
- Mantener consistencia visual y una UX centrada en menus, filtros y acciones faciles para operadores y clientes.
