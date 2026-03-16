# TEST_CASES_AI.md - Matriz de Casos de Prueba Generados para Frontend

A Continuacion se presentan casos de prueba generados para el frontend de FoodTech Frontend, enfocados en autenticacion, registro y flujo basico de sesiones. Incluye la tabla de ajustes realizados por el probador con su justificacion tecnica.

## Tabla de Contenido
- HU-FRONT-010: Iniciar Sesion
- HU-FRONT-011: Cerrar Sesion
- HU-FRONT-012: Registro de Usuario

### TC-01: Inicio de Sesion Exitoso
```
Caso de prueba: Inicio de sesion exitoso con credenciales validas
  Dado que un usuario tiene una cuenta registrada
  Cuando el usuario ingresa email y password correctos
  Entonces el sistema inicia sesion y devuelve un token valido
  Y el token se almacena en el almacenamiento de sesion
  Y se redirige al dashboard principal
```

### TC-02: Inicio de Sesion con Credenciales Invalidas
```
Caso de prueba: Inicio de sesion con credenciales invalidas
  Dado que un usuario tiene una cuenta registrada
  Cuando el usuario ingresa email correcto pero password incorrecto
  Entonces el sistema no inicia sesion
  Y devuelve una respuesta de error JSON con mensaje de credenciales invalidas
```

### TC-03: Registro de Usuario Exitoso
```
Caso de prueba: Registro de nuevo usuario exitoso
  Dado que no existe una cuenta con el email introducido
  Cuando el usuario completa email, username y password
  Y envía el registro
  Entonces el sistema crea la cuenta y inicia sesion automaticamente
```

### TC-04: Registro con Email Duplicado
```
Caso de prueba: Registro con email duplicado
  Dado que ya existe una cuenta con ese email
  Cuando el usuario intenta registrarse con ese email
  Entonces el sistema devuelve 409 CONFLICT y un mensaje de duplicidad
```

### TC-05: Inicio de Sesion con Sesion Persistente (Remember Me)
```
Caso de prueba: Login con remember me
  Dado que el usuario elige recordar sesion
  Cuando inicia sesion
  Entonces se guarda el token con una vida util extendida y la sesion persiste
```

### TC-06: Cerrar Sesion Exitosa
```
Caso de prueba: Logout exitoso
  Dado que el usuario esta autenticado
  Cuando el usuario hace click en Cerrar Sesion
  Entonces se elimina el token y se redirige al login
```

### Ajustes realizados por el Probador
| TC | Caso de Prueba generado | Ajuste realizado | Por que se ajusto |
|---|---|---|---|
| TC-01 | Inicio de Sesion Exitoso | Verificar que el token se guarda en localStorage en lugar de sessionStorage | El flujo de seguridad del front puede variar segun la configuracion; se especifica una practica comun. |
| TC-02 | Inicio de Sesion con Credenciales Invalidas | Ajuste para validar que la respuesta de error es un objeto JSON con campo message | Para estandarizar las respuestas de la API y la UI |
| TC-04 | Registro con Email Duplicado | Recalcular estado a 409 CONFLICT | El backend retorna 409, el frontend debe mostrar esa condicion como conflicto. |
