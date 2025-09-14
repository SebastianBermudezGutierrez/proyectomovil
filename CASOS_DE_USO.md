# Casos de Uso – Lion Fit Pro

---

## Caso de uso 1 – Registrar entrenamiento del día
- **Flujo principal:**  
  1. El usuario abre **"Entrenamiento del día"** donde la app muestra ejercicios y series previstas.  
  2. El usuario inicia ejercicio y registra repeticiones/peso/nota.  
  3. La app guarda el registro localmente.  
  4. La app actualiza los totales de la sesión.  
  5. Si hay conexión, se sincroniza con el backend y actualiza los PRs.  

- **Flujos alternos:**  
  - **A1:** El usuario edita una serie ya registrada → La app vuelve a calcular los totales.  
  - **A2:** Sin conectividad → La app marca el registro como **"pendiente"** y lo actualiza al reconectar.  

- **Excepciones:**  
  - **E1:** Error de almacenamiento local → La app muestra mensaje y ofrece reintentar.  

- **Extensión (Subir progreso):**  
  - Cuando selecciona la opción **"Subir progreso"**  
  - Entonces la aplicación guarda la foto con la fecha actual.  

---

## Caso de uso 2 – Crear nueva rutina
- **Flujo principal:**  
  1. El usuario selecciona **"Nueva rutina"**.  
  2. Añade sesiones y ejercicios con series/repeticiones/peso objetivo.  
  3. Guarda la rutina indicando un **nombre** y un **objetivo**.  
  4. La app muestra la rutina en la lista semanal.  

- **Flujos alternos:**  
  - **A1:** Crear ejercicio personalizado si no existe en catálogo.  

- **Excepciones:**  
  - **E1:** Campos obligatorios vacíos → La app no permite guardar y resalta los campos.  

