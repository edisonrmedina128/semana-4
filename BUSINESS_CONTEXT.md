# Contexto de Negocio - FoodTech Frontend

## 1. Descripción del Proyecto

**Nombre del Proyecto:** FoodTech Frontend - Vista de Mesero

**Objetivo del Proyecto:** Sistema de gestión de pedidos para meseros en restaurante. Permite visualizar disponibilidad de mesas, construir pedidos por categorías de productos, enviarlos a cocina y monitorear el estado de las órdenes en tiempo real.

El frontend está desarrollado en **React + TypeScript** siguiendo una arquitectura hexagonal, consumiendo una API REST del backend.

---

## 2. Flujos Críticos del Negocio

### Principales Flujos de Trabajo:

**1. Autenticación de Usuario**
- Registro de nuevos usuarios con email, username y password.
- Inicio de sesión con credenciales válidas.
- Opción "recordarme" para sesión persistente.
- Acceso sin cuenta mediante modo demo.
- Cierre de sesión manual o por expiración de token.

**2. Gestión de Mesas**
- Visualización de disponibilidad de mesas en tiempo real.
- Selección de mesa para crear pedido.

**3. Construcción de Pedido**
- Navegación por categorías de productos (bebidas, platos calientes, platos fríos).
- Selección de múltiples productos.
- Modificación del pedido antes de enviarlo.
- Envío del pedido completo a cocina.

**4. Monitoreo de Órdenes**
- Visualización del estado y progreso de órdenes.
- Actualización automática de estados mediante polling.

---

## 3. Reglas de Negocio y Restricciones

### Reglas de Negocio Relevantes:

- **Autenticación JWT:** El sistema utiliza tokens JWT para la autenticación de usuarios.
- **Sesión persistente (rememberMe):** Cuando se marca "recordarme", el token se guarda con una fecha de expiración extendida y persiste después de cerrar el navegador.
- **Expiración de token:** El token JWT expira después de un tiempo definido, forzando logout automático.
- **Unicidad de registro:** El email y username deben ser únicos en el sistema.
- **Token requerido:** Todas las requests a endpoints protegidos requieren el token en el header.

### Regulaciones o Normativas:

- No se identifican normativas legales explícitas.
- Se aplicarán prácticas de seguridad estándar para manejo de credenciales y tokens.

---

## 4. Perfiles de Usuario y Roles

### Perfiles o Roles de Usuario en el Sistema:

**Mesero (Waiter)**
- Usuario principal del sistema.
- Puede crear pedidos, seleccionar mesas, monitorear estados.

**Usuario Demo**
- Acceso sin registro completo.
- Funcionalidad limitada para pruebas.

### Permisos y Limitaciones de Cada Perfil:

- **Usuario registrado:** Acceso completo a funcionalidades de mesero.
- **Usuario demo:** Acceso de solo lectura o funcionalidad parcial.

---

## 5. Condiciones del Entorno Técnico

### Plataformas Soportadas:

- **Web:** Aplicación React SPA con soporte responsivo.

### Tecnologías o Integraciones Clave:

- **Frontend:** React 18, TypeScript, Vite
- **Estilo:** CSS Modules / Styled Components
- **Estado:** React Context + Hooks
- **Comunicación:** API REST con fetch/axios
- **Autenticación:** JWT (JSON Web Tokens)
- **Arquitectura:** Hexagonal (Ports & Adapters)
- **Contenerización:** Docker

---

## 6. Casos Especiales o Excepciones

### Escenarios Alternos o Excepciones que Deben Considerarse:

- **Credenciales inválidas:** Mostrar mensaje de error "Credenciales inválidas" sin iniciar sesión.
- **Token expirado:** Logout automático y redirección a login.
- **Email duplicado en registro:** Mostrar error y no crear la cuenta.
- **Fallo en guardado de token:** Manejo de errores en localStorage/sessionStorage.
- **Sesión demo:** Crear sesión temporal sin autenticación real.
