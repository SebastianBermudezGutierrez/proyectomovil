# 📱 Lion Fit Pro – SRS

## 1.1 Introducción

### 1.1.1 Propósito
Este **SRS** define el alcance funcional y no funcional de **Lion Fit Pro**, una app móvil Android para registrar rutinas, entrenamientos y progreso, con recordatorios básicos.  

Está dirigido a:
- Equipo de desarrollo  
- QA  
- Docentes evaluadores  

Servirá como base para diseño, pruebas y validación.

---

### 1.1.2 Alcance
**Lo que hace el sistema:**
- Registrar entrenamientos diarios (ejercicios, series, repeticiones, peso).
- Visualizar historial semanal organizado.
- Seguimiento del progreso por ejercicio (ej. sentadilla).
- Recordatorios de entrenamiento.
- (Opcional) Carga local de fotos de progreso.

**Lo que NO incluye en el MVP:**
- Pagos, planes premium, comunidad de usuarios.
- Sincronización en la nube.
- Rutinas inteligentes con IA.
- Integración con wearables o conteo automático de repeticiones.

---

### 1.1.3 Definiciones, acrónimos y abreviaturas
- **RF:** Requisito Funcional  
- **RNF:** Requisito No Funcional  
- **MVP:** Producto Mínimo Viable  
- **Set:** Serie de repeticiones × peso en un ejercicio  
- **p95:** Percentil 95 de un tiempo medido (rendimiento)  
- **Room:** Librería de persistencia local (Jetpack)  

---

### 1.1.4 Referencias
- Plantilla SRS y lineamientos del taller de la Unidad 1 (IEEE 830, historias de usuario, casos de uso, trazabilidad).  
- Guías de **Material Design 3** (Android).  
- Requisitos de publicación **Google Play Store** (privacidad y permisos).  

---

### 1.1.5 Visión general del documento
Aplicación móvil nativa Android dirigida a estudiantes universitarios de **18–30 años** que entrenan con frecuencia.  

Características principales:
- Registro de rutinas (ejercicios, series, peso).
- Historial semanal.  
- Evolución del rendimiento.  
- Recordatorios de entrenamiento.  

Diseñada para un público con nivel tecnológico medio–alto, habituado al uso diario de apps.

---

## 1.2 Descripción general

### 1.2.1 Perspectiva del producto
- App **nativa Android (Kotlin)**.  
- Offline-first con **Room** (base de datos local).  
- Notificaciones locales para recordatorios.  
- Sin backend en MVP (futuro: API REST).  

---

### 1.2.2 Funciones del producto
- **F1.** Registro de entrenamiento diario.  
- **F2.** Historial semanal de entrenamientos.  
- **F3.** Seguimiento de progreso por ejercicio.  
- **F4.** Recordatorios configurables.  
- **F5.** (Opc.) Fotos de progreso locales.  

---

### 1.2.3 Características de los usuarios
- Perfil: Personas **18–40 años**, alfabetización digital media-alta.  
- Frecuencia: Diario o **3–5 veces/semana**.  
- Necesidades clave: rapidez, registro fluido, métricas claras.  

---

### 1.2.4 Restricciones
- Android **únicamente**.  
- Lenguaje **Kotlin**, entorno Android Studio.  
- Solo almacenamiento local y notificaciones.  
- Interfaz simple siguiendo guías Android.  
- Alcance limitado al **MVP**.  

---

### 1.2.5 Supuestos y dependencias
- Android **8.0+**, con almacenamiento disponible.  
- Permiso de notificaciones otorgado.  
- Sin necesidad de conexión a internet en MVP.  

---

## 1.3 Requerimientos específicos

### 1.3.1 Interfaces externas
**UI:**
- Pantallas: Inicio/Hoy, Registrar ejercicio, Historial, Progreso, Recordatorios, (Opc.) Fotos.  
- Navegación inferior (3–4 pestañas).  
- Modo oscuro por defecto.  

**Hardware / SO:**
- Notificaciones locales.  
- Vibración opcional.  
- Scoped Storage para fotos (si aplica F5).  

**Persistencia (Room):**
- Tablas: `ExerciseCatalog`, `WorkoutSession`, `WorkoutSet`, `Reminder`, `ProgressPhoto (opcional)`  
- Futuro: exportación **CSV local**.  

---

### 1.3.2 Funciones del sistema (RF)

| ID      | Descripción | Prioridad | Criterios de aceptación |
|---------|-------------|-----------|-------------------------|
| RF-01 | Crear catálogo local de ejercicios | Alta | Guardado correcto y disponible en registros |
| RF-02 | Registrar entrenamiento diario | Alta | Persistencia ≤200 ms p95, visible en historial |
| RF-03 | Añadir/editar/eliminar sets | Alta | Cambios reflejados inmediatamente |
| RF-04 | Historial semanal | Alta | Muestra últimos 7 días en ≤800 ms p95 |
| RF-05 | Progreso por ejercicio | Alta | Línea de tiempo de marcas en ≤900 ms p95 |
| RF-06 | Recordatorios configurables | Alta | Notificaciones a la hora definida |
| RF-07 | Modo offline-first | Alta | Funcional en modo avión |
| RF-08 | (Opc.) Fotos de progreso | Baja | Guardado privado y visible en galería interna |

---

### 1.3.3 Rendimiento (RNF-Performance)
- **Arranque frío:** ≤ 2.5 s (Android 10+, gama media).  
- **Guardar set:** ≤ 200 ms p95.  
- **Abrir historial:** ≤ 800 ms p95 (6–10 sesiones).  
- **Uso memoria:** ≤ 250 MB p95 con 3 meses de historial.  

---

### 1.3.4 Lógica de datos / base de datos
- **ExerciseCatalog:** id (PK), name (unique), muscle_group, notes, created_at.  
- **WorkoutSession:** id (PK), session_date (index), notes.  
- **WorkoutSet:** id (PK), session_id (FK), exercise_id (FK), reps, weight_kg, order_idx, created_at.  
- **Reminder:** id (PK), days_mask, hour, minute, enabled.  
- **ProgressPhoto (opcional):** id (PK), taken_at, file_uri, note.  

---

### 1.3.5 Restricciones de diseño
- Lenguaje **Kotlin**, arquitectura **MVVM**.  
- **Room**, **ViewModel**, **LiveData/Flow**, **WorkManager/AlarmManager**.  
- UI con **Material Design 3**.  
- Accesibilidad táctil ≥ 48dp, contraste **WCAG AA**.  
- Localización **es-CO**, unidades en **kg**.  

---

### 1.3.6 Atributos del sistema (RNF)
- **Seguridad:** datos privados, permisos mínimos.  
- **Disponibilidad:** offline total.  
- **Mantenibilidad:** separación de capas, inyección de dependencias (**Hilt/Koin**).  
- **Portabilidad:** Android 8.0+, pantallas adaptables.  
- **Accesibilidad:** soporte TalkBack, labels, foco visible.  
- **Observabilidad:** logs locales sin PII (opcional exportación).  

---

### 1.3.7 Internacionalización / localización
- Idioma base: **es-CO**.  
- Preparado para **en-US** en fases posteriores.  

---

### 1.3.8 Requisitos legales y privacidad
- Aviso de privacidad dentro de la app.  
- Permisos justificados (notificaciones, cámara/almacenamiento opcional).  
- Cumplimiento con políticas de **Google Play**.  

---
