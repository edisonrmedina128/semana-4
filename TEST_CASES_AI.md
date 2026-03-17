# Matriz de Casos de Prueba - FoodTech Frontend

Este documento contiene los escenarios de prueba generados por la IA (SKAI) en lenguaje Gherkin, junto con la validación y ajustes técnicos realizados por el equipo de QA.

---

## HU-FRONT-010: Iniciar Sesión (Login)

### TC-01: Login exitoso con credenciales válidas
**Caso de prueba:** Login exitoso con credenciales válidas  

**Dado** que el usuario tiene una cuenta registrada con email "usuario@foodtech.com" y password "Password123"  
**Cuando** el usuario ingresa email y password correctos  
**Y** hace clic en "Iniciar Sesión"  
**Entonces** el sistema valida las credenciales  
**Y** guarda el token de autenticación  
**Y** redirige a la vista principal  

---

### TC-02: Login con credenciales inválidas
**Caso de prueba:** Login con password incorrecto  

**Dado** que el usuario tiene una cuenta registrada  
**Cuando** el usuario ingresa email correcto pero password incorrecto  
**Entonces** el sistema muestra error "Credenciales inválidas"  
**Y** no inicia sesión  

---

### TC-03: Login con "recordarme"
**Caso de prueba:** Usuario marca "recordarme" para sesión persistente  

**Dado** que el usuario tiene una cuenta registrada  
**Cuando** el usuario marca la opción "recordarme"  
**Y** inicia sesión  
**Entonces** el sistema guarda token con fecha de expiración  
**Y** la sesión persiste después de cerrar el navegador  

---

### TC-04: Modo demo sin cuenta
**Caso de prueba:** Usuario accede con modo demo  

**Dado** que el usuario no tiene cuenta  
**Cuando** el usuario activa el modo demo  
**Entonces** el sistema permite acceso sin autenticación  
**Y** crea una sesión de demo  

---

## HU-FRONT-011: Cerrar Sesión (Logout)

### TC-05: Logout exitoso
**Caso de prueba:** Usuario hace click en cerrar sesión  

**Dado** que el usuario está autenticado  
**Cuando** el usuario hace click en "Cerrar Sesión"  
**Entonces** el sistema elimina el token de autenticación  
**Y** redirige a la página de login  

---

### TC-06: Token expirado obliga logout
**Caso de prueba:** Sesión expira por tiempo  

**Dado** que el usuario tiene una sesión activa  
**Cuando** el token de autenticación expira  
**Entonces** el sistema cierra sesión automáticamente  
**Y** redirige a la página de login  

---

## HU-FRONT-012: Registro de Usuario

### TC-07: Registro exitoso
**Caso de prueba:** Nuevo usuario se registra exitosamente  

**Dado** que el usuario no tiene cuenta  
**Cuando** el usuario ingresa email, username y password  
**Y** completa el registro  
**Entonces** el sistema crea la cuenta  
**Y** inicia sesión automáticamente  

---

### TC-08: Registro con email duplicado
**Caso de prueba:** Usuario intenta registrar con email existente  

**Dado** que ya existe una cuenta con ese email  
**Cuando** el usuario intenta registrarse con ese email  
**Entonces** el sistema muestra error  
**Y** no crea la cuenta  

---

### TC-09: Toggle entre login y registro
**Caso de prueba:** Usuario cambia entre modo login y registro  

**Dado** que está en la página de login  
**Cuando** el usuario hace click en "Regístrate"  
**Entonces** el formulario cambia a modo registro  
**Y** puede completar el registro  

---

## Análisis de Casos de Prueba vs Implementación

| ID    | Caso de Prueba generado por la instrucción       | Ajuste del probador                                      | Razón del ajuste                                      |
|-------|------------------------------------------------|----------------------------------------------------------|------------------------------------------------------|
| TC-01 | Login exitoso con credenciales válidas         | Añadir verificación de guardado de token en localStorage | La IA no especifica dónde se guarda el token         |
| TC-02 | Login con credenciales inválidas               | Mismo caso                                              | No aplica                                            |
| TC-03 | Login con "recordarme"                         | Verificar tiempo exacto de expiración extendida         | La IA no especifica el TTL                          |
| TC-04 | Modo demo                                     | Verificar alcance de funcionalidades limitadas          | La IA no específica qué funcionalidades están limitadas |
| TC-05 | Logout exitoso                                | Añadir verificación de limpieza de datos de sesión      | Verificar que se eliminen todos los datos           |
| TC-06 | Token expirado                                | Verificar tiempo de expiración del JWT                  | La IA no especifica el TTL del token               |
| TC-07 | Registro exitoso                              | Añadir verificación de password hasheada                | La password debe guardarse hasheada                |
| TC-08 | Registro con email duplicado                  | Mismo caso                                              | No aplica                                            |
| TC-09 | Toggle login/registro                         | Añadir verificación de cambio visual del formulario     | Validar que los campos cambien correctamente       |

---

## Notas Técnicas de QA

- Técnicas ISTQB aplicadas:  
  - Partición de Equivalencia  
  - Valores Límite  
  - Transición de Estados  

- Arquitectura:  
  - React SPA con API REST  
  - JWT para autenticación  

- Stack de Automatización:  
  - Selenium WebDriver  
  - Serenity BDD  
  - Gradle  
  - Java  

- Patrones:  
  - Page Object Model (POM)  
  - Screenplay  
