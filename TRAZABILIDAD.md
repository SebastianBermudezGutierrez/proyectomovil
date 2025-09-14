# Matriz de Trazabilidad – Lion Fit Pro

| **Requisito** | **Historias de Usuario** | **Casos de Uso** | **Pruebas** |
|---------------|--------------------------|------------------|-------------|
| **RF-01: Crear catálogo local de ejercicios** | HU-01 (Crear rutina → necesita catálogo de ejercicios base) | CU-2 (Nueva rutina, A1 crear ejercicio personalizado) | - Dado nombre válido, cuando guarda → aparece en catálogo.<br>- Dado nombre duplicado → se rechaza y muestra mensaje.<br>- Guardar tarda ≤200ms. |
| **RF-02: Registrar entrenamiento del día** | HU-01 (Ejecutar rutina)<br>HU-02 (Acceso offline) | CU-1 (Entrenamiento del día) | - Dada fecha y set válido (reps > 0, peso ≥ 0) → se persiste.<br>- Registro accesible en historial.<br>- Operación ≤200ms p95. |
| **RF-03: Añadir/editar/eliminar sets** | HU-01 (Gestión de series y peso) | CU-1 (A1 editar serie) | - Editar set actualiza totales inmediatamente.<br>- Eliminar set quita datos y recalcula volumen.<br>- Persistencia en almacenamiento local. |
| **RF-04: Historial semanal con resumen** | HU-02 (Acceso offline al historial) | CU-1 (flujo normal y A2 sin conexión) | - Historial muestra sesiones y volumen agregados de L-D.<br>- Renderizado ≤800ms.<br>- Funciona sin red. |
| **RF-05: Progreso por ejercicio (línea de tiempo de PRs)** | HU-03 (Ver avance y estadísticas) | CU-1 (después de registrar, cálculo de PRs) | - Mostrar mejor marca semanal por ejercicio.<br>- Permitir filtros (semana, mes).<br>- Respuesta ≤900ms. |
| **RF-06: Recordatorios configurables** | HU-04 (Notificaciones de entrenamiento) | No requiere CU formal, flujo de sistema | - Configurar L-Mi-Vi 19:00 dispara notificación local.<br>- Funciona aun sin abrir la app ese día.<br>- Notificación abre rutina. |
| **RF-07: Modo offline-first** | HU-02 (Acceso sin conexión) | CU-1 (A2 sin conectividad) | - En modo avión se registran sets sin error.<br>- Historial consultable offline.<br>- Datos marcan “pendientes” y sincronizan luego. |
| **RF-08: Fotos de progreso locales (opcional)** | HU-05 (Subir fotos de evolución) | Subfunción en perfil, no descrita como CU formal | - Al tomar foto, se guarda en almacenamiento privado.<br>- Foto aparece en galería interna con fecha.<br>- No se comparte a terceros. |

