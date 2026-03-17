# Refinamiento de Historias de Usuario - FoodTech Frontend

Este documento presenta el refinamiento de las historias de usuario del módulo Frontend del sistema FoodTech, generado mediante el apoyo de la herramienta SKAI y validado manualmente bajo los principios INVEST.

---

## 🎯 Objetivo del Refinamiento

Mejorar la calidad de las historias de usuario originales mediante:

- Mayor claridad funcional  
- Inclusión de criterios de aceptación formales (Gherkin)  
- Incorporación de aspectos técnicos (JWT, seguridad, sesiones)  
- Identificación de escenarios alternativos y edge cases  

---

## 🔧 Cambios Principales

- Adición de validaciones de seguridad  
- Especificación del uso de JWT para autenticación  
- Definición de política de contraseñas  
- Inclusión de flujos alternativos (modo demo, remember me)  
- Mejora en la definición de actores y contexto  

---

# 🔐 HU-FRONT-010: Iniciar Sesión (Login)

## 📄 Descripción

Como usuario registrado del sistema de restaurante, quiero autenticarme mediante email y password para acceder de forma segura al panel de gestión de pedidos y obtener un token de sesión válido.

## ✅ Criterios de Aceptación

### 🟢 Escenario: Login exitoso

- **Given** que el usuario tiene una cuenta registrada  
- **When** ingresa email y password correctos  
- **Then** el sistema inicia sesión exitosamente  
- **And** guarda el token de autenticación  
- **And** redirige a la vista principal  

---

### 🔴 Escenario: Password incorrecto

- **Given** que el usuario tiene una cuenta registrada  
- **When** ingresa email correcto pero password incorrecto  
- **Then** el sistema muestra el error `"Credenciales inválidas"`  
- **And** no inicia sesión  

---

### 🟡 Escenario: Recordarme (sesión persistente)

- **Given** que el usuario tiene una cuenta registrada  
- **When** marca la opción `"recordarme"`  
- **And** inicia sesión  
- **Then** el sistema guarda el token con fecha de expiración  
- **And** la sesión persiste después de cerrar el navegador  

---

### 🔵 Escenario: Modo demo

- **Given** que el usuario no tiene cuenta  
- **When** activa el modo demo  
- **Then** el sistema permite acceso sin autenticación  
- **And** crea una sesión de demo  

---

# 🚪 HU-FRONT-011: Cerrar Sesión (Logout)

## 📄 Descripción

Como usuario autenticado con sesión activa, quiero cerrar sesión de forma manual o automática para invalidar el token de autenticación y proteger mi cuenta de accesos no autorizados.

## ✅ Criterios de Aceptación

### 🟢 Escenario: Logout manual

- **Given** que el usuario está autenticado  
- **When** hace click en `"Cerrar Sesión"`  
- **Then** el sistema elimina el token de autenticación  
- **And** redirige a la página de login  

---

### ⏱️ Escenario: Expiración de sesión

- **Given** que el usuario tiene una sesión activa  
- **When** el token de autenticación expira  
- **Then** el sistema cierra sesión automáticamente  
- **And** redirige a la página de login  

---

# 🧾 HU-FRONT-012: Registro de Usuario

## 📄 Descripción

Como nuevo usuario del sistema de restaurante, quiero crear una cuenta proporcionando email válido, username único y password segura para obtener acceso autenticado al sistema de gestión de pedidos.

## ✅ Criterios de Aceptación

### 🟢 Escenario: Registro exitoso

- **Given** que el usuario no tiene cuenta  
- **When** ingresa email, username y password  
- **And** completa el registro  
- **Then** el sistema crea la cuenta  
- **And** inicia sesión automáticamente  

---

### 🔴 Escenario: Email ya registrado

- **Given** que ya existe una cuenta con ese email  
- **When** intenta registrarse con ese email  
- **Then** el sistema muestra un error  
- **And** no crea la cuenta  

---

### 🔄 Escenario: Cambio entre login y registro

- **Given** que el usuario está en la página de login  
- **When** hace click en `"Regístrate"`  
- **Then** el formulario cambia a modo registro  
- **And** permite completar el registro  

---

# 📊 Cuadro Comparativo - Historias de Usuario (Frontend)

| HU original | HU refinada por la instrucción | Diferencias detectadas |
|------------|-------------------------------|------------------------|
| HU-FRONT-010: Login  <br> Como usuario  <br> Quiero iniciar sesión  <br> Para entrar al sistema | HU-FRONT-010: Iniciar Sesión (Login)  <br> Como usuario registrado del sistema de restaurante  <br> Quiero autenticarme mediante email y password  <br> Para acceder de forma segura al panel de gestión de pedidos y obtener un token de sesión válido | - Se especificó **"usuario registrado"** para mayor precisión del actor  <br> - Se añadió detalle técnico del mecanismo **JWT**  <br> - Se añadió criterio de **"recordarme"** con expiración extendida  <br> - Se añadió el escenario de **modo demo sin cuenta** |
| HU-FRONT-011: Logout  <br> Como usuario  <br> Quiero cerrar sesión  <br> Para salir del sistema | HU-FRONT-011: Cerrar Sesión (Logout)  <br> Como usuario autenticado con sesión activa  <br> Quiero cerrar sesión de forma manual o automática  <br> Para invalidar el token de autenticación y proteger mi cuenta de accesos no autorizados | - Se añadió condición **"con sesión activa"** como precondición  <br> - Se añadió el escenario de **logout automático por expiración de token**  <br> - Se añadió **limpieza de datos de sesión en el cliente** |
| HU-FRONT-012: Registro  <br> Como usuario nuevo  <br> Quiero registrarme  <br> Para usar el sistema | HU-FRONT-012: Registro de Usuario  <br> Como nuevo usuario del sistema de restaurante  <br> Quiero crear una cuenta proporcionando email válido, username único y password segura  <br> Para obtener acceso autenticado al sistema de gestión de pedidos | - Se añadió validación de formato de email (**sintaxis RFC**)  <br> - Se añadió validación de longitud de username (**3-20 caracteres**)  <br> - Se añadió política de password (**mínimo 8 caracteres, mayúscula, número**)  <br> - Se añadió verificación de **unicidad de email y username**  <br> - Se añadió generación de **token JWT post-registro** |

---
