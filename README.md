# PLAN DE PRUEBAS DE SOFTWARE
## Sistema de Gestión de Asistencia por Código QR - UPeU

**Versión:** 1.0  
**Fecha:** 2025-01-15  
**Proyecto:** Sistema de Asistencia UPeU  
**Elaborado por:** Equipo de QA

---

## INDICE GENERAL

1. [REQUISITOS](#1-requisitos)
2. [CASOS DE PRUEBA POR SUITE](#2-casos-de-prueba-por-suite)
3. [TABLA DE CASOS DE PRUEBA](#3-tabla-de-casos-de-prueba)

---

## 1. REQUISITOS

### 1.1 Requisitos Funcionales (RF)

| ID | Descripción |
|----|-------------|
| RF-01 | El sistema debe permitir login con usuario y contraseña mediante endpoint POST `/users/login` |
| RF-02 | El sistema debe validar credenciales antes de permitir acceso al sistema |
| RF-03 | El sistema debe generar token JWT al autenticarse exitosamente |
| RF-04 | El sistema debe permitir registro de nuevos usuarios mediante endpoint POST `/users/register` |
| RF-05 | El sistema debe validar que el username sea único al registrar usuario |
| RF-06 | El sistema debe validar que el documento sea único al registrar persona |
| RF-07 | El sistema debe validar formato de email al registrar usuario |
| RF-08 | El sistema debe gestionar roles de usuario (SUPERADMIN, ADMIN, LIDER, INTEGRANTE) |
| RF-09 | El sistema debe construir menú dinámico según rol del usuario mediante endpoint POST `/accesos/menu` |
| RF-10 | El sistema debe permitir CRUD de sedes mediante endpoints `/sedes` |
| RF-11 | El sistema debe permitir CRUD de facultades mediante endpoints `/facultades` |
| RF-12 | El sistema debe permitir CRUD de programas de estudio mediante endpoints `/programas` |
| RF-13 | El sistema debe permitir CRUD de períodos académicos mediante endpoints `/periodos` |
| RF-14 | El sistema debe permitir obtener período activo mediante GET `/periodos/activo` |
| RF-15 | El sistema debe permitir CRUD de matrículas mediante endpoints `/matriculas` |
| RF-16 | El sistema debe permitir filtrar matrículas por sede, facultad, programa, período y tipo de persona mediante GET `/matriculas/filtrar` |
| RF-17 | El sistema debe permitir importar matrículas desde archivo Excel mediante POST `/matriculas/importar` |
| RF-18 | El sistema debe validar formato de archivo Excel (.xlsx, .xls) en importación |
| RF-19 | El sistema debe requerir período obligatorio para importación de matrículas |
| RF-20 | El sistema debe permitir exportar matrículas a Excel mediante GET `/matriculas/exportar` |
| RF-21 | El sistema debe permitir descargar plantilla de importación mediante GET `/matriculas/descargar-plantilla` |
| RF-22 | El sistema debe permitir CRUD de eventos generales mediante endpoints `/eventos-generales` |
| RF-23 | El sistema debe permitir filtrar eventos por período y programa mediante GET `/eventos-generales/periodo/{periodoId}/programa/{programaId}` |
| RF-24 | El sistema debe permitir filtrar eventos solo por período mediante GET `/eventos-generales/periodo/{periodoId}` |
| RF-25 | El sistema debe permitir obtener eventos activos en una fecha mediante GET `/eventos-generales/activos?fecha={fecha}` |
| RF-26 | El sistema debe permitir CRUD de sesiones específicas (eventos específicos) mediante endpoints `/eventos-especificos` |
| RF-27 | El sistema debe permitir crear sesiones recurrentes mediante POST `/eventos-especificos/recurrencia` |
| RF-28 | El sistema debe permitir filtrar sesiones por evento general mediante GET `/eventos-especificos/evento-general/{eventoGeneralId}` |
| RF-29 | El sistema debe permitir filtrar sesiones por fecha mediante GET `/eventos-especificos/fecha?fecha={fecha}` |
| RF-30 | El sistema debe permitir filtrar sesiones por rango de fechas mediante GET `/eventos-especificos/rango?eventoId={id}&inicio={fecha}&fin={fecha}` |
| RF-31 | El sistema debe permitir CRUD de grupos generales mediante endpoints `/grupos-generales` |
| RF-32 | El sistema debe permitir filtrar grupos generales por evento mediante GET `/grupos-generales/evento/{eventoGeneralId}` |
| RF-33 | El sistema debe permitir CRUD de grupos pequeños mediante endpoints `/grupos-pequenos` |
| RF-34 | El sistema debe permitir asignar líder a grupo pequeño |
| RF-35 | El sistema debe validar capacidad máxima de participantes en grupo pequeño |
| RF-36 | El sistema debe permitir obtener grupos pequeños por líder mediante GET `/grupos-pequenos/lider/{liderId}` |
| RF-37 | El sistema debe permitir obtener participantes disponibles para un evento mediante GET `/grupos-pequenos/disponibles/{eventoGeneralId}` |
| RF-38 | El sistema debe permitir CRUD de participantes en grupos mediante endpoints `/grupo-participantes` |
| RF-39 | El sistema debe permitir agregar participante a grupo pequeño mediante POST `/grupo-participantes` |
| RF-40 | El sistema debe validar que participante no esté duplicado en el mismo grupo |
| RF-41 | El sistema debe validar que participante no esté ya inscrito en otro grupo del mismo evento |
| RF-42 | El sistema debe permitir remover participante de grupo mediante PUT `/grupo-participantes/remover/{id}` |
| RF-43 | El sistema debe permitir obtener participantes por grupo mediante GET `/grupo-participantes/grupo/{grupoPequenoId}` |
| RF-44 | El sistema debe permitir obtener participantes por persona mediante GET `/grupo-participantes/persona/{personaId}` |
| RF-45 | El sistema debe permitir generar código QR para sesión mediante GET `/asistencias/generar-qr/{eventoEspecificoId}/lider/{liderId}` |
| RF-46 | El sistema debe validar que el líder tenga acceso a la sesión antes de generar QR |
| RF-47 | El sistema debe incluir datos de sesión (eventoId, fecha, hora, lugar, timestamp) en el código QR |
| RF-48 | El sistema debe retornar imagen QR en formato base64 |
| RF-49 | El sistema debe permitir registrar asistencia mediante escaneo QR mediante POST `/asistencias/registrar-qr` |
| RF-50 | El sistema debe validar que el registro de asistencia sea el día de la sesión |
| RF-51 | El sistema debe validar horario permitido para registro (30 minutos antes hasta 2 horas después de la sesión) |
| RF-52 | El sistema debe prevenir registros duplicados de asistencia para la misma sesión y persona |
| RF-53 | El sistema debe validar que la persona pertenezca al evento antes de registrar asistencia |
| RF-54 | El sistema debe determinar estado de asistencia (PRESENTE o TARDE) según tolerancia configurada |
| RF-55 | El sistema debe permitir obtener lista de participantes para llamado mediante GET `/asistencias/lista-llamado/{eventoEspecificoId}/lider/{liderId}` |
| RF-56 | El sistema debe mostrar estado de asistencia de cada participante en la lista de llamado |
| RF-57 | El sistema debe permitir marcar asistencia manualmente mediante POST `/asistencias/marcar-manual` |
| RF-58 | El sistema debe validar que el líder pertenezca al grupo antes de marcar asistencia |
| RF-59 | El sistema debe permitir marcar asistencia con estados: PRESENTE, TARDE, AUSENTE, JUSTIFICADO |
| RF-60 | El sistema debe permitir agregar observación al marcar asistencia manual |
| RF-61 | El sistema debe permitir consultar asistencias por sesión mediante GET `/asistencias/sesion/{eventoEspecificoId}` |
| RF-62 | El sistema debe permitir consultar asistencias por persona mediante GET `/asistencias/persona/{personaId}` |
| RF-63 | El sistema debe permitir generar reporte de asistencia por evento mediante GET `/asistencias/reporte/{eventoGeneralId}` |
| RF-64 | El sistema debe calcular porcentaje de asistencia por participante en el reporte |
| RF-65 | El sistema debe mostrar estadísticas de asistencia (presentes, tardes, ausentes, justificados) en el reporte |
| RF-66 | El sistema debe permitir obtener usuarios por rol mediante GET `/users/rol/{rolNombre}` |
| RF-67 | El sistema debe permitir obtener líderes disponibles mediante GET `/users/lideres-disponibles` |
| RF-68 | El sistema debe permitir CRUD de personas mediante endpoints `/personas` |
| RF-69 | El sistema debe permitir buscar persona por código de estudiante mediante GET `/personas/codigo/{codigo}` |
| RF-70 | El sistema debe permitir buscar matrículas por código de estudiante mediante GET `/matriculas/estudiante/{codigo}` |

### 1.2 Requisitos No Funcionales (RNF)

| ID | Descripción |
|----|-------------|
| RNF-01 | El sistema debe responder a peticiones HTTP en menos de 500ms para operaciones CRUD básicas |
| RNF-02 | El sistema debe soportar al menos 100 usuarios concurrentes |
| RNF-03 | El sistema debe mantener disponibilidad del 99% durante horario académico |
| RNF-04 | El sistema debe utilizar autenticación JWT con tokens que expiran en 5 horas |
| RNF-05 | El sistema debe encriptar contraseñas usando BCrypt antes de almacenarlas |
| RNF-06 | El sistema debe validar tokens JWT en cada petición a endpoints protegidos |
| RNF-07 | El sistema debe manejar errores y retornar respuestas estandarizadas mediante `CustomResponse` |
| RNF-08 | El sistema debe registrar logs de operaciones críticas |
| RNF-09 | El sistema debe ser compatible con navegadores modernos (Chrome, Firefox, Edge, Safari - últimas 2 versiones) |
| RNF-10 | El sistema debe ser responsive y funcionar en dispositivos móviles para escaneo QR |
| RNF-11 | El sistema debe mantener integridad referencial en base de datos mediante foreign keys |
| RNF-12 | El sistema debe prevenir duplicados mediante constraints UNIQUE en base de datos |
| RNF-13 | El sistema debe gestionar transacciones atómicas para operaciones complejas |
| RNF-14 | El sistema debe validar formato de datos de entrada mediante anotaciones Bean Validation |
| RNF-15 | El sistema debe transformar datos entre capas mediante DTOs y MapStruct |
| RNF-16 | El sistema debe permitir CORS desde cualquier origen mediante `@CrossOrigin(origins = "*")` |
| RNF-17 | El sistema debe almacenar coordenadas GPS (latitud, longitud) al registrar asistencia por QR |
| RNF-18 | El sistema debe generar códigos QR con timestamp para validar vigencia |

---

## 2. CASOS DE PRUEBA POR SUITE

### 2.1 AUTENTICACIÓN

TC-AUT-001 – Login exitoso con credenciales válidas  
TC-AUT-002 – Login con credenciales inválidas  
TC-AUT-003 – Login con usuario inexistente  
TC-AUT-004 – Login con contraseña incorrecta  
TC-AUT-005 – Validación de campos vacíos en login  
TC-AUT-006 – Persistencia de token JWT en localStorage  
TC-AUT-007 – Validación de formato de token JWT  
TC-AUT-008 – Expiración de token JWT después de 5 horas  
TC-AUT-009 – Logout elimina token y datos de sesión  
TC-AUT-010 – Redirección a dashboard según rol después de login  
TC-AUT-011 – Registro exitoso de nuevo usuario  
TC-AUT-012 – Registro con username duplicado  
TC-AUT-013 – Registro con documento duplicado  
TC-AUT-014 – Registro con email inválido  
TC-AUT-015 – Registro con campos obligatorios faltantes  
TC-AUT-016 – Validación de formato de email en registro  
TC-AUT-017 – Asignación de rol por defecto (INTEGRANTE) en registro  
TC-AUT-018 – Verificación de autenticación mediante `isAuthenticated()`  
TC-AUT-019 – Limpieza de token expirado automáticamente  
TC-AUT-020 – Acceso a ruta protegida sin token

### 2.2 GESTIÓN DE USUARIOS, ROLES Y PERMISOS

TC-USU-001 – Obtener usuarios por rol mediante GET `/users/rol/{rolNombre}`  
TC-USU-002 – Obtener líderes disponibles mediante GET `/users/lideres-disponibles`  
TC-USU-003 – Obtener menú dinámico por usuario mediante POST `/accesos/menu`  
TC-USU-004 – Obtener accesos por usuario mediante POST `/accesos/user`  
TC-USU-005 – Menú diferente según rol (SUPERADMIN, ADMIN, LIDER, INTEGRANTE)  
TC-USU-006 – Acceso restringido a funcionalidades según rol  
TC-USU-007 – Validación de permisos en endpoints protegidos  
TC-USU-008 – Redirección automática según rol al acceder a `/dashboard`  
TC-USU-009 – Visualización de menú lateral según permisos asignados  
TC-USU-010 – Ocultamiento de opciones no permitidas en menú

### 2.3 GESTIÓN DE ESTRUCTURA ACADÉMICA

TC-EST-001 – CRUD completo de sedes mediante endpoints `/sedes`  
TC-EST-002 – Validación de nombre único en sedes  
TC-EST-003 – CRUD completo de facultades mediante endpoints `/facultades`  
TC-EST-004 – Validación de nombre único en facultades  
TC-EST-005 – CRUD completo de programas de estudio mediante endpoints `/programas`  
TC-EST-006 – Validación de nombre único en programas  
TC-EST-007 – Relación facultad-programa en creación de programa  
TC-EST-008 – CRUD completo de períodos académicos mediante endpoints `/periodos`  
TC-EST-009 – Validación de nombre único en períodos  
TC-EST-010 – Obtener período activo mediante GET `/periodos/activo`  
TC-EST-011 – Filtrar períodos por estado mediante GET `/periodos/estado/{estado}`  
TC-EST-012 – Validación de fecha inicio menor que fecha fin en período  
TC-EST-013 – Solo un período ACTIVO a la vez (regla de negocio)

### 2.4 GESTIÓN DE MATRÍCULAS

TC-MAT-001 – Listar todas las matrículas mediante GET `/matriculas`  
TC-MAT-002 – Obtener matrícula por ID mediante GET `/matriculas/{id}`  
TC-MAT-003 – Crear matrícula mediante POST `/matriculas`  
TC-MAT-004 – Actualizar matrícula mediante PUT `/matriculas/{id}`  
TC-MAT-005 – Eliminar matrícula mediante DELETE `/matriculas/{id}`  
TC-MAT-006 – Filtrar matrículas por sede mediante GET `/matriculas/filtrar?sedeId={id}`  
TC-MAT-007 – Filtrar matrículas por facultad mediante GET `/matriculas/filtrar?facultadId={id}`  
TC-MAT-008 – Filtrar matrículas por programa mediante GET `/matriculas/filtrar?programaId={id}`  
TC-MAT-009 – Filtrar matrículas por período mediante GET `/matriculas/filtrar?periodoId={id}`  
TC-MAT-010 – Filtrar matrículas por tipo de persona mediante GET `/matriculas/filtrar?tipoPersona={tipo}`  
TC-MAT-011 – Filtrar matrículas con múltiples criterios simultáneos  
TC-MAT-012 – Buscar matrículas por código de estudiante mediante GET `/matriculas/estudiante/{codigo}`  
TC-MAT-013 – Importar matrículas desde Excel mediante POST `/matriculas/importar`  
TC-MAT-014 – Validación de formato de archivo Excel (.xlsx, .xls)  
TC-MAT-015 – Validación de período obligatorio en importación  
TC-MAT-016 – Procesamiento de archivo Excel con datos válidos  
TC-MAT-017 – Manejo de errores en filas inválidas durante importación  
TC-MAT-018 – Reporte de resultados de importación (total, exitosos, fallidos)  
TC-MAT-019 – Exportar matrículas a Excel mediante GET `/matriculas/exportar`  
TC-MAT-020 – Aplicación de filtros en exportación de matrículas  
TC-MAT-021 – Descargar plantilla de importación mediante GET `/matriculas/descargar-plantilla`  
TC-MAT-022 – Validación de estructura de plantilla Excel descargada  
TC-MAT-023 – Integridad referencial al eliminar sede con matrículas asociadas  
TC-MAT-024 – Integridad referencial al eliminar facultad con matrículas asociadas  
TC-MAT-025 – Integridad referencial al eliminar programa con matrículas asociadas

### 2.5 GESTIÓN DE EVENTOS GENERALES

TC-EVG-001 – Listar todos los eventos generales mediante GET `/eventos-generales`  
TC-EVG-002 – Obtener evento general por ID mediante GET `/eventos-generales/{id}`  
TC-EVG-003 – Crear evento general mediante POST `/eventos-generales`  
TC-EVG-004 – Actualizar evento general mediante PUT `/eventos-generales/{id}`  
TC-EVG-005 – Eliminar evento general mediante DELETE `/eventos-generales/{id}`  
TC-EVG-006 – Filtrar eventos por programa mediante GET `/eventos-generales/programa/{programaId}`  
TC-EVG-007 – Filtrar eventos por período y programa mediante GET `/eventos-generales/periodo/{periodoId}/programa/{programaId}`  
TC-EVG-008 – Filtrar eventos solo por período mediante GET `/eventos-generales/periodo/{periodoId}`  
TC-EVG-009 – Obtener eventos activos en fecha mediante GET `/eventos-generales/activos?fecha={fecha}`  
TC-EVG-010 – Validación de fecha inicio menor que fecha fin en evento  
TC-EVG-011 – Asignación de estado ACTIVO por defecto en creación  
TC-EVG-012 – Relación evento-período en creación  
TC-EVG-013 – Relación evento-programa en creación

### 2.6 GESTIÓN DE SESIONES (EVENTOS ESPECÍFICOS)

TC-SES-001 – Listar todas las sesiones mediante GET `/eventos-especificos`  
TC-SES-002 – Obtener sesión por ID mediante GET `/eventos-especificos/{id}`  
TC-SES-003 – Crear sesión individual mediante POST `/eventos-especificos`  
TC-SES-004 – Actualizar sesión mediante PUT `/eventos-especificos/{id}`  
TC-SES-005 – Eliminar sesión mediante DELETE `/eventos-especificos/{id}`  
TC-SES-006 – Filtrar sesiones por evento general mediante GET `/eventos-especificos/evento-general/{eventoGeneralId}`  
TC-SES-007 – Filtrar sesiones por fecha mediante GET `/eventos-especificos/fecha?fecha={fecha}`  
TC-SES-008 – Filtrar sesiones por rango de fechas mediante GET `/eventos-especificos/rango?eventoId={id}&inicio={fecha}&fin={fecha}`  
TC-SES-009 – Crear sesiones recurrentes mediante POST `/eventos-especificos/recurrencia`  
TC-SES-010 – Validación de días de semana en recurrencia (1=Lunes, 7=Domingo)  
TC-SES-011 – Generación de múltiples sesiones según días seleccionados  
TC-SES-012 – Validación de hora inicio menor que hora fin en sesión  
TC-SES-013 – Asignación de tolerancia por defecto (10 minutos) en sesión  
TC-SES-014 – Asignación de estado PROGRAMADO por defecto en sesión  
TC-SES-015 – Herencia de lugar y descripción del evento general si no se especifican

### 2.7 GESTIÓN DE GRUPOS GENERALES

TC-GRG-001 – Listar todos los grupos generales mediante GET `/grupos-generales`  
TC-GRG-002 – Obtener grupo general por ID mediante GET `/grupos-generales/{id}`  
TC-GRG-003 – Crear grupo general mediante POST `/grupos-generales`  
TC-GRG-004 – Actualizar grupo general mediante PUT `/grupos-generales/{id}`  
TC-GRG-005 – Eliminar grupo general mediante DELETE `/grupos-generales/{id}`  
TC-GRG-006 – Filtrar grupos generales por evento mediante GET `/grupos-generales/evento/{eventoGeneralId}`  
TC-GRG-007 – Relación grupo general-evento general en creación  
TC-GRG-008 – Validación de nombre obligatorio en grupo general

### 2.8 GESTIÓN DE GRUPOS PEQUEÑOS

TC-GRP-001 – Listar todos los grupos pequeños mediante GET `/grupos-pequenos`  
TC-GRP-002 – Obtener grupo pequeño por ID mediante GET `/grupos-pequenos/{id}`  
TC-GRP-003 – Crear grupo pequeño mediante POST `/grupos-pequenos`  
TC-GRP-004 – Actualizar grupo pequeño mediante PUT `/grupos-pequenos/{id}`  
TC-GRP-005 – Eliminar grupo pequeño mediante DELETE `/grupos-pequenos/{id}`  
TC-GRP-006 – Filtrar grupos pequeños por grupo general mediante GET `/grupos-pequenos/grupo-general/{grupoGeneralId}`  
TC-GRP-007 – Filtrar grupos pequeños por líder mediante GET `/grupos-pequenos/lider/{liderId}`  
TC-GRP-008 – Obtener participantes disponibles para evento mediante GET `/grupos-pequenos/disponibles/{eventoGeneralId}`  
TC-GRP-009 – Asignación de líder a grupo pequeño  
TC-GRP-010 – Validación de capacidad máxima en grupo pequeño (por defecto 20)  
TC-GRP-011 – Cálculo de participantes actuales en grupo pequeño  
TC-GRP-012 – Relación grupo pequeño-grupo general en creación  
TC-GRP-013 – Validación de líder disponible (no asignado a otro grupo)

### 2.9 GESTIÓN DE PARTICIPANTES EN GRUPOS

TC-PAR-001 – Listar todos los participantes mediante GET `/grupo-participantes`  
TC-PAR-002 – Obtener participante por ID mediante GET `/grupo-participantes/{id}`  
TC-PAR-003 – Agregar participante a grupo mediante POST `/grupo-participantes`  
TC-PAR-004 – Filtrar participantes por grupo pequeño mediante GET `/grupo-participantes/grupo/{grupoPequenoId}`  
TC-PAR-005 – Filtrar participantes por persona mediante GET `/grupo-participantes/persona/{personaId}`  
TC-PAR-006 – Remover participante de grupo mediante PUT `/grupo-participantes/remover/{id}`  
TC-PAR-007 – Eliminar participante mediante DELETE `/grupo-participantes/{id}`  
TC-PAR-008 – Validación de capacidad máxima antes de agregar participante  
TC-PAR-009 – Validación de participante no duplicado en mismo grupo  
TC-PAR-010 – Validación de participante no inscrito en otro grupo del mismo evento  
TC-PAR-011 – Cambio de estado a INACTIVO al remover participante  
TC-PAR-012 – Asignación de fecha de inscripción automática  
TC-PAR-013 – Asignación de estado ACTIVO por defecto al agregar participante

### 2.10 GESTIÓN DE CÓDIGOS QR

TC-QR-001 – Generar código QR para sesión mediante GET `/asistencias/generar-qr/{eventoEspecificoId}/lider/{liderId}`  
TC-QR-002 – Validación de acceso del líder a la sesión antes de generar QR  
TC-QR-003 – Inclusión de datos de sesión en código QR (eventoId, fecha, hora, lugar, timestamp)  
TC-QR-004 – Retorno de imagen QR en formato base64  
TC-QR-005 – Retorno de datos del QR en formato JSON  
TC-QR-006 – Validación de sesión del día actual para generar QR  
TC-QR-007 – Generación de QR con timestamp para validar vigencia  
TC-QR-008 – Visualización de QR en modal del frontend  
TC-QR-009 – Error al generar QR si líder no tiene acceso a la sesión  
TC-QR-010 – Error al generar QR si sesión no existe

### 2.11 REGISTRO DE ASISTENCIAS CON QR

TC-ASQ-001 – Registrar asistencia mediante escaneo QR mediante POST `/asistencias/registrar-qr`  
TC-ASQ-002 – Validación de fecha de sesión (solo el día de la sesión)  
TC-ASQ-003 – Validación de horario permitido (30 minutos antes hasta 2 horas después)  
TC-ASQ-004 – Prevención de registros duplicados para misma sesión y persona  
TC-ASQ-005 – Validación de pertenencia de persona al evento  
TC-ASQ-006 – Determinación de estado PRESENTE según tolerancia  
TC-ASQ-007 – Determinación de estado TARDE si excede tolerancia  
TC-ASQ-008 – Almacenamiento de coordenadas GPS (latitud, longitud) opcionales  
TC-ASQ-009 – Almacenamiento de observación opcional  
TC-ASQ-010 – Error al registrar fuera del horario permitido  
TC-ASQ-011 – Error al registrar en día diferente al de la sesión  
TC-ASQ-012 – Error al registrar asistencia ya existente  
TC-ASQ-013 – Error al registrar si persona no pertenece al evento  
TC-ASQ-014 – Escaneo exitoso de QR con cámara del dispositivo  
TC-ASQ-015 – Parseo correcto de datos JSON del QR  
TC-ASQ-016 – Mensaje de éxito después de registro exitoso  
TC-ASQ-017 – Actualización de estado en lista de llamado después de registro

### 2.12 REGISTRO DE ASISTENCIAS MANUAL (LÍDER)

TC-ASM-001 – Obtener lista de participantes para llamado mediante GET `/asistencias/lista-llamado/{eventoEspecificoId}/lider/{liderId}`  
TC-ASM-002 – Mostrar estado de asistencia de cada participante en lista  
TC-ASM-003 – Marcar asistencia manualmente mediante POST `/asistencias/marcar-manual`  
TC-ASM-004 – Validación de líder perteneciente al grupo antes de marcar  
TC-ASM-005 – Marcar asistencia con estado PRESENTE  
TC-ASM-006 – Marcar asistencia con estado TARDE  
TC-ASM-007 – Marcar asistencia con estado AUSENTE  
TC-ASM-008 – Marcar asistencia con estado JUSTIFICADO con motivo  
TC-ASM-009 – Agregar observación al marcar asistencia manual  
TC-ASM-010 – Error al marcar asistencia de participante de otro grupo  
TC-ASM-011 – Error al marcar asistencia si líder no tiene acceso  
TC-ASM-012 – Actualización de estado en lista después de marcado manual  
TC-ASM-013 – Timestamp automático al marcar asistencia manual

### 2.13 CONSULTA DE ASISTENCIAS

TC-ASC-001 – Listar todas las asistencias mediante GET `/asistencias`  
TC-ASC-002 – Obtener asistencia por ID mediante GET `/asistencias/{id}`  
TC-ASC-003 – Consultar asistencias por sesión mediante GET `/asistencias/sesion/{eventoEspecificoId}`  
TC-ASC-004 – Consultar asistencias por persona mediante GET `/asistencias/persona/{personaId}`  
TC-ASC-005 – Visualización de historial personal de asistencias (Integrante)  
TC-ASC-006 – Visualización de asistencias de grupos del líder  
TC-ASC-007 – Filtrado de asistencias por estado (PRESENTE, TARDE, AUSENTE, JUSTIFICADO)  
TC-ASC-008 – Visualización de fecha y hora de registro en consulta  
TC-ASC-009 – Visualización de observaciones en consulta

### 2.14 REPORTES Y CONSULTAS

TC-REP-001 – Generar reporte de asistencia por evento mediante GET `/asistencias/reporte/{eventoGeneralId}`  
TC-REP-002 – Cálculo de porcentaje de asistencia por participante  
TC-REP-003 – Estadísticas de asistencia (total sesiones, presentes, tardes, ausentes, justificados)  
TC-REP-004 – Visualización de reporte en tabla con métricas por participante  
TC-REP-005 – Filtrado de eventos generales para seleccionar reporte  
TC-REP-006 – Manejo de evento sin asistencias registradas  
TC-REP-007 – Cálculo correcto de porcentajes de asistencia  
TC-REP-008 – Visualización de datos consolidados en reporte

### 2.15 GESTIÓN DE PERSONAS

TC-PER-001 – Listar todas las personas mediante GET `/personas`  
TC-PER-002 – Obtener persona por ID mediante GET `/personas/{id}`  
TC-PER-003 – Crear persona mediante POST `/personas`  
TC-PER-004 – Actualizar persona mediante PUT `/personas/{id}`  
TC-PER-005 – Eliminar persona mediante DELETE `/personas/{id}`  
TC-PER-006 – Buscar persona por código de estudiante mediante GET `/personas/codigo/{codigo}`  
TC-PER-007 – Validación de código de estudiante único  
TC-PER-008 – Validación de documento único  
TC-PER-009 – Relación persona-usuario (OneToOne)

### 2.16 DASHBOARDS POR ROL

TC-DAS-001 – Visualización de dashboard de Admin con estadísticas  
TC-DAS-002 – Cálculo de total de personas en dashboard Admin  
TC-DAS-003 – Cálculo de total de matrículas en dashboard Admin  
TC-DAS-004 – Cálculo de eventos activos hoy en dashboard Admin  
TC-DAS-005 – Cálculo de asistencias hoy en dashboard Admin  
TC-DAS-006 – Visualización de dashboard de Líder con estadísticas  
TC-DAS-007 – Cálculo de total de grupos del líder  
TC-DAS-008 – Cálculo de total de participantes del líder  
TC-DAS-009 – Cálculo de asistencias registradas del líder  
TC-DAS-010 – Cálculo de porcentaje de asistencia promedio del líder  
TC-DAS-011 – Visualización de dashboard de Integrante  
TC-DAS-012 – Visualización de dashboard de SuperAdmin

### 2.17 SEGURIDAD

TC-SEG-001 – Validación de token JWT en peticiones protegidas  
TC-SEG-002 – Rechazo de petición sin token JWT  
TC-SEG-003 – Rechazo de petición con token JWT inválido  
TC-SEG-004 – Rechazo de petición con token JWT expirado  
TC-SEG-005 – Encriptación de contraseñas con BCrypt  
TC-SEG-006 – Validación de roles en endpoints protegidos  
TC-SEG-007 – Acceso restringido según permisos de rol  
TC-SEG-008 – Prevención de inyección SQL mediante JPA  
TC-SEG-009 – Validación de entrada mediante Bean Validation  
TC-SEG-010 – Manejo seguro de errores sin exponer información sensible  
TC-SEG-011 – CORS configurado para permitir origen desde frontend  
TC-SEG-012 – Validación de formato de datos en peticiones

### 2.18 BASE DE DATOS

TC-BD-001 – Integridad referencial: eliminar sede con matrículas asociadas  
TC-BD-002 – Integridad referencial: eliminar facultad con programas asociados  
TC-BD-003 – Integridad referencial: eliminar programa con eventos asociados  
TC-BD-004 – Integridad referencial: eliminar evento general con sesiones asociadas  
TC-BD-005 – Integridad referencial: eliminar grupo general con grupos pequeños asociados  
TC-BD-006 – Integridad referencial: eliminar grupo pequeño con participantes asociados  
TC-BD-007 – Constraint UNIQUE: username duplicado en tabla `upeu_usuario`  
TC-BD-008 – Constraint UNIQUE: documento duplicado en tabla `upeu_persona`  
TC-BD-009 – Constraint UNIQUE: código estudiante duplicado en tabla `upeu_persona`  
TC-BD-010 – Constraint UNIQUE: nombre duplicado en tabla `upeu_sede`  
TC-BD-011 – Constraint UNIQUE: nombre duplicado en tabla `upeu_facultad`  
TC-BD-012 – Constraint UNIQUE: nombre duplicado en tabla `upeu_programa_estudio`  
TC-BD-013 – Constraint UNIQUE: nombre duplicado en tabla `upeu_periodo`  
TC-BD-014 – Constraint UNIQUE: asistencia duplicada (evento_especifico_id, persona_id)  
TC-BD-015 – Constraint UNIQUE: participante duplicado (grupo_pequeno_id, persona_id)  
TC-BD-016 – Transacción atómica: crear evento general con múltiples sesiones  
TC-BD-017 – Rollback de transacción en caso de error  
TC-BD-018 – Foreign key: matrícula requiere persona, sede, facultad, programa, período válidos  
TC-BD-019 – Foreign key: evento general requiere período y programa válidos  
TC-BD-020 – Foreign key: sesión requiere evento general válido  
TC-BD-021 – Foreign key: grupo pequeño requiere grupo general y líder válidos  
TC-BD-022 – Foreign key: participante requiere grupo pequeño y persona válidos  
TC-BD-023 – Foreign key: asistencia requiere sesión y persona válidos

### 2.19 ERRORES Y EXCEPCIONES

TC-ERR-001 – Manejo de excepción `ModelNotFoundException`  
TC-ERR-002 – Manejo de excepción `RuntimeException` con mensaje descriptivo  
TC-ERR-003 – Manejo de excepción `MethodArgumentNotValidException` (validación Bean)  
TC-ERR-004 – Manejo de excepción genérica `Exception`  
TC-ERR-005 – Retorno de `CustomResponse` estandarizado en errores  
TC-ERR-006 – Códigos HTTP apropiados (400, 401, 404, 500)  
TC-ERR-007 – Mensajes de error descriptivos y útiles  
TC-ERR-008 – Manejo de error en importación Excel con lista de errores  
TC-ERR-009 – Manejo de error en registro de asistencia con mensaje claro  
TC-ERR-010 – Manejo de error de conexión a base de datos  
TC-ERR-011 – Manejo de error de validación de negocio  
TC-ERR-012 – Logging de errores para diagnóstico

### 2.20 RENDIMIENTO Y STRESS

TC-REN-001 – Tiempo de respuesta de login menor a 500ms  
TC-REN-002 – Tiempo de respuesta de listado de matrículas menor a 1s  
TC-REN-003 – Tiempo de respuesta de generación de QR menor a 200ms  
TC-REN-004 – Tiempo de respuesta de registro de asistencia menor a 300ms  
TC-REN-005 – Soporte de 50 usuarios concurrentes en login  
TC-REN-006 – Soporte de 100 usuarios concurrentes en consultas  
TC-REN-007 – Procesamiento de archivo Excel con 1000 filas en menos de 30s  
TC-REN-008 – Generación de reporte con 500 participantes en menos de 5s  
TC-REN-009 – Carga inicial de dashboard en menos de 2s  
TC-REN-010 – Consulta de asistencias con paginación eficiente

### 2.21 COMPATIBILIDAD

TC-COM-001 – Funcionamiento en Chrome (últimas 2 versiones)  
TC-COM-002 – Funcionamiento en Firefox (últimas 2 versiones)  
TC-COM-003 – Funcionamiento en Edge (últimas 2 versiones)  
TC-COM-004 – Funcionamiento en Safari (últimas 2 versiones)  
TC-COM-005 – Funcionamiento en dispositivos móviles Android  
TC-COM-006 – Funcionamiento en dispositivos móviles iOS  
TC-COM-007 – Acceso a cámara para escaneo QR en móviles  
TC-COM-008 – Visualización responsive en diferentes tamaños de pantalla  
TC-COM-009 – Funcionamiento con conexión lenta (3G)  
TC-COM-010 – Funcionamiento offline parcial (caché de datos)

---

## 3. TABLA DE CASOS DE PRUEBA

| Suite | ID | Título | Precondiciones | Pasos | Resultado Esperado | Prioridad | Tipo | Requisitos | Responsable |
|-------|----|--------|----------------|-------|-------------------|-----------|------|------------|-------------|
| Autenticación | TC-AUT-001 | Login exitoso con credenciales válidas | Usuario registrado y activo en BD. API accesible por HTTPS. | 1. Abrir aplicación en navegador<br>2. Acceder a ruta `/login`<br>3. Ingresar username válido<br>4. Ingresar password válido<br>5. Click en botón "Iniciar Sesión" | Se autentica exitosamente. Token JWT almacenado en localStorage. Redirección a dashboard según rol. Menú lateral visible con opciones del rol. | P1 | Funcional/UI | RF-01, RF-02, RF-03 | Tester |
| Autenticación | TC-AUT-002 | Login con credenciales inválidas | Usuario existe en BD. | 1. Acceder a `/login`<br>2. Ingresar username válido<br>3. Ingresar password incorrecto<br>4. Click en "Iniciar Sesión" | Mensaje de error: "Credenciales inválidas". No se genera token. Usuario permanece en página de login. | P1 | Funcional/UI | RF-02 | Tester |
| Autenticación | TC-AUT-003 | Login con usuario inexistente | Usuario NO existe en BD. | 1. Acceder a `/login`<br>2. Ingresar username inexistente<br>3. Ingresar cualquier password<br>4. Click en "Iniciar Sesión" | Mensaje de error descriptivo. No se genera token. Status HTTP 401 o 404. | P1 | Funcional/API | RF-02 | Tester |
| Autenticación | TC-AUT-004 | Login con contraseña incorrecta | Usuario existe en BD con contraseña conocida. | 1. Acceder a `/login`<br>2. Ingresar username correcto<br>3. Ingresar password incorrecto<br>4. Click en "Iniciar Sesión" | Error de autenticación. No se genera token. Mensaje de error claro. | P1 | Funcional/API | RF-02 | Tester |
| Autenticación | TC-AUT-005 | Validación de campos vacíos en login | Ninguna. | 1. Acceder a `/login`<br>2. Dejar campos username y password vacíos<br>3. Click en "Iniciar Sesión" | Validación de campos requeridos. Mensaje indicando campos obligatorios. Botón deshabilitado o error de validación. | P2 | Funcional/UI | RF-02 | Tester |
| Autenticación | TC-AUT-006 | Persistencia de token JWT en localStorage | Login exitoso realizado. | 1. Realizar login exitoso<br>2. Abrir DevTools del navegador<br>3. Verificar localStorage | Token JWT almacenado en clave "token". Datos de usuario almacenados en clave "user". Token tiene formato válido (3 partes separadas por punto). | P1 | Funcional/UI | RF-03, RNF-04 | Tester |
| Autenticación | TC-AUT-007 | Validación de formato de token JWT | Token almacenado en localStorage. | 1. Verificar token en localStorage<br>2. Decodificar payload del token<br>3. Verificar estructura | Token tiene formato JWT válido. Payload contiene: sub (username), role, app, exp, iat. | P2 | Funcional/Seguridad | RF-03, RNF-04 | Tester |
| Autenticación | TC-AUT-008 | Expiración de token JWT después de 5 horas | Token generado y almacenado. | 1. Realizar login<br>2. Esperar 5 horas o modificar exp del token<br>3. Intentar acceder a endpoint protegido | Token expirado. Redirección a `/login`. Token eliminado de localStorage. Mensaje de sesión expirada. | P1 | Funcional/Seguridad | RNF-04 | Tester |
| Autenticación | TC-AUT-009 | Logout elimina token y datos de sesión | Usuario autenticado. | 1. Usuario autenticado en sistema<br>2. Click en botón "Cerrar Sesión" o llamar a `authService.logout()` | Token eliminado de localStorage. Datos de usuario eliminados. Redirección a `/login`. | P1 | Funcional/UI | RF-03 | Tester |
| Autenticación | TC-AUT-010 | Redirección a dashboard según rol después de login | Usuarios de diferentes roles creados. | 1. Login como ADMIN<br>2. Login como LIDER<br>3. Login como INTEGRANTE<br>4. Login como SUPERADMIN | ADMIN redirige a `/dashboard/admin`. LIDER redirige a `/dashboard/lider`. INTEGRANTE redirige a `/dashboard/integrante`. SUPERADMIN redirige a `/superadmin`. | P1 | Funcional/UI | RF-08 | Tester |
| Autenticación | TC-AUT-011 | Registro exitoso de nuevo usuario | No existe usuario con mismo username/documento/correo. | 1. Acceder a `/register`<br>2. Completar formulario: username, nombreCompleto, correo, documento, password<br>3. Click en "Registrar" | Usuario creado en BD. Persona creada asociada. Mensaje de éxito. Redirección a `/login`. | P1 | Funcional/UI | RF-04 | Tester |
| Autenticación | TC-AUT-012 | Registro con username duplicado | Usuario con mismo username ya existe. | 1. Acceder a `/register`<br>2. Ingresar username existente<br>3. Completar resto del formulario<br>4. Click en "Registrar" | Mensaje de error: "El nombre de usuario ya está en uso". Usuario no creado. Status HTTP 400. | P1 | Funcional/API | RF-05 | Tester |
| Autenticación | TC-AUT-013 | Registro con documento duplicado | Persona con mismo documento ya existe. | 1. Acceder a `/register`<br>2. Ingresar documento existente<br>3. Completar resto del formulario<br>4. Click en "Registrar" | Mensaje de error: "El número de documento ya está registrado". Persona no creada. Status HTTP 400. | P1 | Funcional/API | RF-06 | Tester |
| Autenticación | TC-AUT-014 | Registro con email inválido | Ninguna. | 1. Acceder a `/register`<br>2. Ingresar email con formato inválido (ej: "email_sin_arroba")<br>3. Completar resto del formulario<br>4. Click en "Registrar" | Mensaje de error: "Debe ser un correo válido". Validación de formato de email. Status HTTP 400. | P1 | Funcional/Validación | RF-07 | Tester |
| Autenticación | TC-AUT-015 | Registro con campos obligatorios faltantes | Ninguna. | 1. Acceder a `/register`<br>2. Dejar campos obligatorios vacíos<br>3. Click en "Registrar" | Validación de campos requeridos. Mensajes de error por cada campo faltante. Formulario no se envía. | P1 | Funcional/UI | RF-04 | Tester |
| Autenticación | TC-AUT-016 | Validación de formato de email en registro | Ninguna. | 1. Acceder a `/register`<br>2. Probar diferentes formatos: "email@", "@dominio.com", "sin_arroba", "email@valido.com" | Solo formato válido aceptado. Validación mediante anotación `@Email` en backend. Mensaje claro de error. | P1 | Funcional/Validación | RF-07, RNF-14 | Tester |
| Autenticación | TC-AUT-017 | Asignación de rol por defecto (INTEGRANTE) en registro | Ninguna. | 1. Realizar registro sin especificar rol<br>2. Verificar usuario creado en BD | Usuario creado con rol INTEGRANTE por defecto. Estado ACTIVO por defecto. | P2 | Funcional/BD | RF-08 | Tester |
| Autenticación | TC-AUT-018 | Verificación de autenticación mediante `isAuthenticated()` | Token almacenado o no. | 1. Con token válido: llamar `authService.isAuthenticated()`<br>2. Sin token: llamar `authService.isAuthenticated()`<br>3. Con token expirado: llamar `authService.isAuthenticated()` | Retorna `true` con token válido. Retorna `false` sin token. Retorna `false` y limpia token si está expirado. | P2 | Funcional/UI | RF-03 | Tester |
| Autenticación | TC-AUT-019 | Limpieza de token expirado automáticamente | Token expirado en localStorage. | 1. Almacenar token expirado manualmente<br>2. Llamar `authService.isAuthenticated()` | Token eliminado de localStorage. Retorna `false`. | P2 | Funcional/UI | RF-03 | Tester |
| Autenticación | TC-AUT-020 | Acceso a ruta protegida sin token | Ninguna. | 1. Sin estar autenticado, intentar acceder a `/dashboard/admin` o cualquier ruta protegida | Redirección a `/login`. Status HTTP 401 Unauthorized si se accede por API. | P1 | Funcional/Seguridad | RNF-06 | Tester |
| Gestión de Usuarios | TC-USU-001 | Obtener usuarios por rol mediante GET `/users/rol/{rolNombre}` | Usuarios con diferentes roles existen en BD. Usuario autenticado con permisos. | 1. Autenticarse como ADMIN<br>2. Realizar GET a `/users/rol/LIDER`<br>3. Realizar GET a `/users/rol/ADMIN` | Lista de usuarios con rol LIDER. Lista de usuarios con rol ADMIN. Respuesta en formato JSON con array de UsuarioDTO. | P2 | Funcional/API | RF-66 | Tester |
| Gestión de Usuarios | TC-USU-002 | Obtener líderes disponibles mediante GET `/users/lideres-disponibles` | Líderes con rol LIDER existen. Algunos asignados a grupos, otros no. | 1. Autenticarse como ADMIN<br>2. Realizar GET a `/users/lideres-disponibles`<br>3. Opcional: excluir grupo con `?excludeGrupoId={id}` | Lista de líderes disponibles (no asignados a grupos). Formato PersonaDTO. Excluye líderes ya asignados si se especifica excludeGrupoId. | P2 | Funcional/API | RF-67 | Tester |
| Gestión de Usuarios | TC-USU-003 | Obtener menú dinámico por usuario mediante POST `/accesos/menu` | Usuario autenticado con rol asignado. Accesos configurados para el rol. | 1. Autenticarse como ADMIN<br>2. Realizar POST a `/accesos/menu` con body: username<br>3. Verificar respuesta | Lista de MenuGroup con estructura jerárquica. Menú contiene solo accesos permitidos para el rol. Formato JSON con grupos e items. | P1 | Funcional/API | RF-09 | Tester |
| Gestión de Usuarios | TC-USU-004 | Obtener accesos por usuario mediante POST `/accesos/user` | Usuario autenticado. | 1. Autenticarse<br>2. Realizar POST a `/accesos/user` con body: username | Lista de AccesoDTO con todos los accesos del usuario. Incluye: idAcceso, nombre, url, icono. | P2 | Funcional/API | RF-09 | Tester |
| Gestión de Usuarios | TC-USU-005 | Menú diferente según rol (SUPERADMIN, ADMIN, LIDER, INTEGRANTE) | Usuarios de cada rol autenticados. | 1. Login como SUPERADMIN y verificar menú<br>2. Login como ADMIN y verificar menú<br>3. Login como LIDER y verificar menú<br>4. Login como INTEGRANTE y verificar menú | SUPERADMIN ve todos los accesos. ADMIN ve accesos administrativos. LIDER ve accesos de líder. INTEGRANTE ve accesos básicos. | P1 | Funcional/UI | RF-08, RF-09 | Tester |
| Gestión de Usuarios | TC-USU-006 | Acceso restringido a funcionalidades según rol | Usuarios de diferentes roles autenticados. | 1. Como INTEGRANTE, intentar acceder a `/matriculas`<br>2. Como INTEGRANTE, intentar acceder a `/asistencias/registrar`<br>3. Como LIDER, intentar acceder a `/matriculas` | Redirección o mensaje de acceso denegado. Funcionalidad no visible en menú. Status HTTP 403 si se accede por API. | P1 | Funcional/Seguridad | RF-08, RNF-06 | Tester |
| Gestión de Usuarios | TC-USU-007 | Validación de permisos en endpoints protegidos | Token JWT válido pero sin permisos. | 1. Autenticarse como INTEGRANTE<br>2. Intentar POST a `/matriculas/importar` | Status HTTP 403 Forbidden o redirección. Mensaje de acceso denegado. | P1 | Funcional/Seguridad | RNF-06 | Tester |
| Gestión de Usuarios | TC-USU-008 | Redirección automática según rol al acceder a `/dashboard` | Usuarios de diferentes roles. | 1. Login como ADMIN y acceder a `/dashboard`<br>2. Login como LIDER y acceder a `/dashboard` | Redirección automática a `/dashboard/admin` o `/dashboard/lider` según rol. | P2 | Funcional/UI | RF-08 | Tester |
| Gestión de Usuarios | TC-USU-009 | Visualización de menú lateral según permisos asignados | Usuario autenticado. | 1. Autenticarse<br>2. Verificar Sidebar con opciones de menú | Menú lateral muestra solo opciones permitidas. Iconos y nombres correctos. Estructura jerárquica si aplica. | P1 | Funcional/UI | RF-09 | Tester |
| Gestión de Usuarios | TC-USU-010 | Ocultamiento de opciones no permitidas en menú | Usuario con rol limitado autenticado. | 1. Login como INTEGRANTE<br>2. Verificar menú lateral | Opciones de ADMIN y LIDER no visibles. Solo opciones de INTEGRANTE visibles. | P1 | Funcional/UI | RF-09 | Tester |
| Gestión de Estructura Académica | TC-EST-001 | CRUD completo de sedes mediante endpoints `/sedes` | Usuario ADMIN autenticado. | 1. GET `/sedes` - Listar<br>2. POST `/sedes` - Crear<br>3. GET `/sedes/{id}` - Obtener<br>4. PUT `/sedes/{id}` - Actualizar<br>5. DELETE `/sedes/{id}` - Eliminar | Operaciones CRUD funcionan correctamente. Respuestas en formato SedeDTO. Status HTTP apropiados (200, 201, 404). | P1 | Funcional/API | RF-10 | Tester |
| Gestión de Estructura Académica | TC-EST-002 | Validación de nombre único en sedes | Sede con nombre existe. | 1. Intentar crear sede con nombre existente | Error de constraint violation. Mensaje descriptivo. Sede no creada. Status HTTP 400. | P1 | Funcional/BD | RF-10, TC-BD-010 | Tester |
| Gestión de Estructura Académica | TC-EST-003 | CRUD completo de facultades mediante endpoints `/facultades` | Usuario ADMIN autenticado. | 1. GET `/facultades` - Listar<br>2. POST `/facultades` - Crear<br>3. GET `/facultades/{id}` - Obtener<br>4. PUT `/facultades/{id}` - Actualizar<br>5. DELETE `/facultades/{id}` - Eliminar | Operaciones CRUD funcionan correctamente. Respuestas en formato FacultadDTO. | P1 | Funcional/API | RF-11 | Tester |
| Gestión de Estructura Académica | TC-EST-004 | Validación de nombre único en facultades | Facultad con nombre existe. | 1. Intentar crear facultad con nombre existente | Error de constraint violation. Facultad no creada. | P1 | Funcional/BD | RF-11, TC-BD-011 | Tester |
| Gestión de Estructura Académica | TC-EST-005 | CRUD completo de programas de estudio mediante endpoints `/programas` | Usuario ADMIN autenticado. Facultad existe. | 1. GET `/programas` - Listar<br>2. POST `/programas` con facultadId<br>3. GET `/programas/{id}` - Obtener<br>4. PUT `/programas/{id}` - Actualizar<br>5. DELETE `/programas/{id}` - Eliminar | Operaciones CRUD funcionan correctamente. Relación con facultad mantenida. Respuestas en formato ProgramaEstudioDTO. | P1 | Funcional/API | RF-12 | Tester |
| Gestión de Estructura Académica | TC-EST-006 | Validación de nombre único en programas | Programa con nombre existe. | 1. Intentar crear programa con nombre existente | Error de constraint violation. Programa no creado. | P1 | Funcional/BD | RF-12, TC-BD-012 | Tester |
| Gestión de Estructura Académica | TC-EST-007 | Relación facultad-programa en creación de programa | Facultad existe en BD. | 1. Crear programa especificando facultadId válido<br>2. Verificar programa creado | Programa creado con relación a facultad correcta. Foreign key válida. | P1 | Funcional/BD | RF-12, TC-BD-018 | Tester |
| Gestión de Estructura Académica | TC-EST-008 | CRUD completo de períodos académicos mediante endpoints `/periodos` | Usuario ADMIN autenticado. | 1. GET `/periodos` - Listar<br>2. POST `/periodos` - Crear<br>3. GET `/periodos/{id}` - Obtener<br>4. PUT `/periodos/{id}` - Actualizar<br>5. DELETE `/periodos/{id}` - Eliminar | Operaciones CRUD funcionan correctamente. Respuestas en formato PeriodoDTO. | P1 | Funcional/API | RF-13 | Tester |
| Gestión de Estructura Académica | TC-EST-009 | Validación de nombre único en períodos | Período con nombre existe. | 1. Intentar crear período con nombre existente | Error de constraint violation. Período no creado. | P1 | Funcional/BD | RF-13, TC-BD-013 | Tester |
| Gestión de Estructura Académica | TC-EST-010 | Obtener período activo mediante GET `/periodos/activo` | Período con estado ACTIVO existe. | 1. Realizar GET a `/periodos/activo` | Retorna período con estado ACTIVO. Si hay múltiples, retorna el más reciente por fechaInicio. | P1 | Funcional/API | RF-14 | Tester |
| Gestión de Estructura Académica | TC-EST-011 | Filtrar períodos por estado mediante GET `/periodos/estado/{estado}` | Períodos con diferentes estados existen. | 1. GET `/periodos/estado/ACTIVO`<br>2. GET `/periodos/estado/INACTIVO`<br>3. GET `/periodos/estado/FINALIZADO` | Retorna solo períodos con el estado especificado. Lista filtrada correctamente. | P2 | Funcional/API | RF-13 | Tester |
| Gestión de Estructura Académica | TC-EST-012 | Validación de fecha inicio menor que fecha fin en período | Ninguna. | 1. Intentar crear período con fechaInicio > fechaFin | Error de validación. Mensaje descriptivo. Período no creado. | P1 | Funcional/Validación | RF-13, RNF-14 | Tester |
| Gestión de Estructura Académica | TC-EST-013 | Solo un período ACTIVO a la vez (regla de negocio) | Período ACTIVO existe. | 1. Intentar crear o actualizar otro período a ACTIVO | Validación en servicio. Solo un período puede estar ACTIVO. Otro período se desactiva o error. | P1 | Funcional/Validación | RF-13 | Tester |
| Gestión de Matrículas | TC-MAT-001 | Listar todas las matrículas mediante GET `/matriculas` | Matrículas existen en BD. Usuario ADMIN autenticado. | 1. Realizar GET a `/matriculas` | Lista completa de matrículas. Respuesta en formato array de MatriculaDTO. Status HTTP 200. | P1 | Funcional/API | RF-15 | Tester |
| Gestión de Matrículas | TC-MAT-002 | Obtener matrícula por ID mediante GET `/matriculas/{id}` | Matrícula con ID existe. | 1. Realizar GET a `/matriculas/1` | Matrícula específica retornada. Formato MatriculaDTO con todos los datos relacionados. | P1 | Funcional/API | RF-15 | Tester |
| Gestión de Matrículas | TC-MAT-003 | Crear matrícula mediante POST `/matriculas` | Sede, facultad, programa, período, persona existen. | 1. POST `/matriculas` con datos válidos<br>2. Verificar creación | Matrícula creada en BD. Relaciones establecidas correctamente. Status HTTP 201 Created. | P1 | Funcional/API | RF-15 | Tester |
| Gestión de Matrículas | TC-MAT-004 | Actualizar matrícula mediante PUT `/matriculas/{id}` | Matrícula existe. | 1. PUT `/matriculas/{id}` con datos actualizados<br>2. Verificar cambios | Matrícula actualizada. Cambios persistidos en BD. Status HTTP 200. | P1 | Funcional/API | RF-15 | Tester |
| Gestión de Matrículas | TC-MAT-005 | Eliminar matrícula mediante DELETE `/matriculas/{id}` | Matrícula existe. | 1. DELETE `/matriculas/{id}` | Matrícula eliminada. Status HTTP 200 con CustomResponse. | P1 | Funcional/API | RF-15 | Tester |
| Gestión de Matrículas | TC-MAT-006 | Filtrar matrículas por sede mediante GET `/matriculas/filtrar?sedeId={id}` | Matrículas de diferentes sedes existen. | 1. GET `/matriculas/filtrar?sedeId=1` | Solo matrículas de la sede especificada. Filtrado correcto. | P1 | Funcional/API | RF-16 | Tester |
| Gestión de Matrículas | TC-MAT-007 | Filtrar matrículas por facultad mediante GET `/matriculas/filtrar?facultadId={id}` | Matrículas de diferentes facultades existen. | 1. GET `/matriculas/filtrar?facultadId=1` | Solo matrículas de la facultad especificada. | P1 | Funcional/API | RF-16 | Tester |
| Gestión de Matrículas | TC-MAT-008 | Filtrar matrículas por programa mediante GET `/matriculas/filtrar?programaId={id}` | Matrículas de diferentes programas existen. | 1. GET `/matriculas/filtrar?programaId=1` | Solo matrículas del programa especificado. | P1 | Funcional/API | RF-16 | Tester |
| Gestión de Matrículas | TC-MAT-009 | Filtrar matrículas por período mediante GET `/matriculas/filtrar?periodoId={id}` | Matrículas de diferentes períodos existen. | 1. GET `/matriculas/filtrar?periodoId=1` | Solo matrículas del período especificado. | P1 | Funcional/API | RF-16 | Tester |
| Gestión de Matrículas | TC-MAT-010 | Filtrar matrículas por tipo de persona mediante GET `/matriculas/filtrar?tipoPersona={tipo}` | Matrículas de tipo ESTUDIANTE e INVITADO existen. | 1. GET `/matriculas/filtrar?tipoPersona=ESTUDIANTE` | Solo matrículas del tipo especificado. | P2 | Funcional/API | RF-16 | Tester |
| Gestión de Matrículas | TC-MAT-011 | Filtrar matrículas con múltiples criterios simultáneos | Matrículas con diferentes combinaciones existen. | 1. GET `/matriculas/filtrar?sedeId=1&facultadId=1&programaId=1&periodoId=1` | Matrículas que cumplen TODOS los criterios. Filtrado combinado correcto. | P1 | Funcional/API | RF-16 | Tester |
| Gestión de Matrículas | TC-MAT-012 | Buscar matrículas por código de estudiante mediante GET `/matriculas/estudiante/{codigo}` | Matrícula con código existe. | 1. GET `/matriculas/estudiante/20250001` | Lista de matrículas del estudiante. Puede haber múltiples si tiene varias matrículas. | P2 | Funcional/API | RF-70 | Tester |
| Gestión de Matrículas | TC-MAT-013 | Importar matrículas desde Excel mediante POST `/matriculas/importar` | Archivo Excel válido con formato correcto. Período existe. | 1. Preparar FormData con archivo Excel y parámetros (periodoId obligatorio)<br>2. POST `/matriculas/importar` con multipart/form-data<br>3. Verificar respuesta | Procesamiento exitoso. Matrículas creadas en BD. Respuesta con ImportResultDTO: total, exitosos, fallidos, errores, warnings. Status HTTP 200. | P1 | Funcional/API | RF-17 | Tester |
| Gestión de Matrículas | TC-MAT-014 | Validación de formato de archivo Excel (.xlsx, .xls) | Archivo con formato incorrecto. | 1. Intentar importar archivo .txt o .pdf<br>2. Intentar importar archivo corrupto | Mensaje de error: "El archivo debe ser un Excel (.xlsx o .xls)". Importación rechazada. Status HTTP 400. | P1 | Funcional/Validación | RF-18 | Tester |
| Gestión de Matrículas | TC-MAT-015 | Validación de período obligatorio en importación | Archivo Excel válido. | 1. Intentar importar sin especificar periodoId | Mensaje de error: "Debe seleccionar un periodo para la importación". Importación rechazada. | P1 | Funcional/Validación | RF-19 | Tester |
| Gestión de Matrículas | TC-MAT-016 | Procesamiento de archivo Excel con datos válidos | Archivo Excel con estructura correcta. | 1. Importar archivo con 100 filas válidas<br>2. Verificar resultados | 100 matrículas creadas. Reporte muestra: total=100, exitosos=100, fallidos=0. | P1 | Funcional/API | RF-17 | Tester |
| Gestión de Matrículas | TC-MAT-017 | Manejo de errores en filas inválidas durante importación | Archivo Excel con algunas filas inválidas. | 1. Importar archivo con 100 filas: 80 válidas, 20 inválidas<br>2. Verificar resultados | 80 matrículas creadas. 20 errores registrados. Lista de errores descriptivos por fila. Reporte detallado. | P1 | Funcional/API | RF-17 | Tester |
| Gestión de Matrículas | TC-MAT-018 | Reporte de resultados de importación (total, exitosos, fallidos) | Importación realizada. | 1. Realizar importación<br>2. Verificar ImportResultDTO retornado | Objeto con: totalRegistros, exitosos, fallidos, lista de errores, lista de warnings. Información completa y clara. | P1 | Funcional/API | RF-17 | Tester |
| Gestión de Matrículas | TC-MAT-019 | Exportar matrículas a Excel mediante GET `/matriculas/exportar` | Matrículas existen. | 1. GET `/matriculas/exportar` con filtros opcionales<br>2. Verificar descarga | Archivo Excel descargado. Nombre con timestamp. Formato .xlsx válido. Datos correctos en archivo. | P1 | Funcional/API | RF-20 | Tester |
| Gestión de Matrículas | TC-MAT-020 | Aplicación de filtros en exportación de matrículas | Matrículas con diferentes criterios existen. | 1. GET `/matriculas/exportar?sedeId=1&periodoId=1`<br>2. Verificar archivo descargado | Archivo contiene solo matrículas que cumplen filtros. Datos correctos. | P1 | Funcional/API | RF-20 | Tester |
| Gestión de Matrículas | TC-MAT-021 | Descargar plantilla de importación mediante GET `/matriculas/descargar-plantilla` | Ninguna. | 1. GET `/matriculas/descargar-plantilla` | Archivo Excel descargado. Nombre: "Plantilla_Importacion_Matriculas.xlsx". Columnas correctas según estructura esperada. | P1 | Funcional/API | RF-21 | Tester |
| Gestión de Matrículas | TC-MAT-022 | Validación de estructura de plantilla Excel descargada | Plantilla descargada. | 1. Descargar plantilla<br>2. Abrir en Excel<br>3. Verificar columnas | Plantilla tiene columnas correctas. Formato válido. Estructura coincide con MatriculaExcelDTO. | P2 | Funcional/Validación | RF-21 | Tester |
| Gestión de Matrículas | TC-MAT-023 | Integridad referencial al eliminar sede con matrículas asociadas | Sede con matrículas existe. | 1. Intentar DELETE `/sedes/{id}` de sede con matrículas | Error de constraint violation. Sede no eliminada. Mensaje descriptivo. | P1 | Funcional/BD | TC-BD-001 | Tester |
| Gestión de Matrículas | TC-MAT-024 | Integridad referencial al eliminar facultad con matrículas asociadas | Facultad con matrículas existe. | 1. Intentar DELETE `/facultades/{id}` de facultad con matrículas | Error de constraint violation. Facultad no eliminada. | P1 | Funcional/BD | TC-BD-002 | Tester |
| Gestión de Matrículas | TC-MAT-025 | Integridad referencial al eliminar programa con matrículas asociadas | Programa con matrículas existe. | 1. Intentar DELETE `/programas/{id}` de programa con matrículas | Error de constraint violation. Programa no eliminado. | P1 | Funcional/BD | TC-BD-003 | Tester |
| Gestión de Eventos Generales | TC-EVG-001 | Listar todos los eventos generales mediante GET `/eventos-generales` | Eventos generales existen. | 1. GET `/eventos-generales` | Lista completa de eventos. Formato array de EventoGeneralDTO. | P1 | Funcional/API | RF-22 | Tester |
| Gestión de Eventos Generales | TC-EVG-002 | Obtener evento general por ID mediante GET `/eventos-generales/{id}` | Evento general existe. | 1. GET `/eventos-generales/1` | Evento específico retornado. Datos completos incluyendo relaciones (periodo, programa). | P1 | Funcional/API | RF-22 | Tester |
| Gestión de Eventos Generales | TC-EVG-003 | Crear evento general mediante POST `/eventos-generales` | Período y programa existen. | 1. POST `/eventos-generales` con datos válidos (nombre, periodoId, programaId, fechaInicio, fechaFin)<br>2. Verificar creación | Evento creado en BD. Estado ACTIVO por defecto. Relaciones establecidas. Status HTTP 201. | P1 | Funcional/API | RF-22 | Tester |
| Gestión de Eventos Generales | TC-EVG-004 | Actualizar evento general mediante PUT `/eventos-generales/{id}` | Evento general existe. | 1. PUT `/eventos-generales/{id}` con datos actualizados | Evento actualizado. Cambios persistidos. | P1 | Funcional/API | RF-22 | Tester |
| Gestión de Eventos Generales | TC-EVG-005 | Eliminar evento general mediante DELETE `/eventos-generales/{id}` | Evento general existe. | 1. DELETE `/eventos-generales/{id}` | Evento eliminado. Status HTTP 200. | P1 | Funcional/API | RF-22 | Tester |
| Gestión de Eventos Generales | TC-EVG-006 | Filtrar eventos por programa mediante GET `/eventos-generales/programa/{programaId}` | Eventos de diferentes programas existen. | 1. GET `/eventos-generales/programa/1` | Solo eventos del programa especificado. | P2 | Funcional/API | RF-22 | Tester |
| Gestión de Eventos Generales | TC-EVG-007 | Filtrar eventos por período y programa mediante GET `/eventos-generales/periodo/{periodoId}/programa/{programaId}` | Eventos con diferentes combinaciones existen. | 1. GET `/eventos-generales/periodo/1/programa/1` | Solo eventos que cumplen ambos criterios. | P1 | Funcional/API | RF-23 | Tester |
| Gestión de Eventos Generales | TC-EVG-008 | Filtrar eventos solo por período mediante GET `/eventos-generales/periodo/{periodoId}` | Eventos de diferentes períodos existen. | 1. GET `/eventos-generales/periodo/1` | Solo eventos del período especificado. | P1 | Funcional/API | RF-24 | Tester |
| Gestión de Eventos Generales | TC-EVG-009 | Obtener eventos activos en fecha mediante GET `/eventos-generales/activos?fecha={fecha}` | Eventos con diferentes rangos de fechas existen. | 1. GET `/eventos-generales/activos?fecha=2025-01-15` | Solo eventos donde fecha está entre fechaInicio y fechaFin. Estado ACTIVO. | P1 | Funcional/API | RF-25 | Tester |
| Gestión de Eventos Generales | TC-EVG-010 | Validación de fecha inicio menor que fecha fin en evento | Ninguna. | 1. Intentar crear evento con fechaInicio > fechaFin | Error de validación. Evento no creado. Mensaje descriptivo. | P1 | Funcional/Validación | RF-22, RNF-14 | Tester |
| Gestión de Eventos Generales | TC-EVG-011 | Asignación de estado ACTIVO por defecto en creación | Ninguna. | 1. Crear evento sin especificar estado<br>2. Verificar evento creado | Estado ACTIVO asignado automáticamente. | P2 | Funcional/BD | RF-22 | Tester |
| Gestión de Eventos Generales | TC-EVG-01
