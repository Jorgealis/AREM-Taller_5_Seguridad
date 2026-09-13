# 🗒️ Registro de Trabajo en Clase - Taller 5: Evaluación de Seguridad con STRIDE

## 📆 Fecha de la sesión
_11 de septiembre de 2026_ — **(ajustar si la fecha real de la sesión fue otra)**

## 👥 Integrantes presentes
- Jorge Alarcón
- Julián Aguirre
- Brayan Presiga

## 🧠 Actividades realizadas en clase

- Repasamos la [guía paso a paso del Taller 5](guia_paso_a_paso_stride.md) y las 6 categorías de STRIDE, apoyándonos también en la versión visual interactiva [`modelado-de-amenazas.html`](modelado-de-amenazas.html) para tener el DFD clickeable y la matriz STRIDE-por-tipo-de-elemento antes de construir nuestra propia tabla.
- Elegimos, dentro del caso base de EdukIT, el flujo de **acceso de estudiantes a cursos y materiales** — el mismo que trae resuelto la guía — y lo reprodujimos en draw.io como `dfd-edukit-borrador.drawio`: el estudiante se autentica (P1), obtiene un token y luego solicita contenido al módulo de cursos (P2), marcando el límite de confianza entre el estudiante (fuera) y el backend de EdukIT (dentro).
- Sobre ese DFD aplicamos las 6 categorías STRIDE, una amenaza por categoría (T1 a T6), y completamos las columnas de impacto, probabilidad, nivel de riesgo, mitigación, responsable y estado siguiendo exactamente la tabla ya resuelta en la guía — quedó registrada en `tabla-stride-clase.xlsx`.
- Discutimos la diferencia entre una amenaza genérica ("puede haber un hackeo") y una amenaza bien formulada sobre un elemento específico del DFD (ej. "el token de sesión F3 puede ser interceptado si no se usa TLS") — uno de los errores comunes que señala la guía.
- Completamos el **reto práctico #1 de OWASP Juice Shop** (login bypass explotando la ausencia de consultas parametrizadas) en una instancia local levantada con Docker, y lo integramos como una fila adicional (T7) en la tabla de clase, tal como pide el punto 6 del README. No se repitió ninguna técnica activa contra ningún sistema real — ese límite se respetó estrictamente.
- Con el ejemplo de EdukIT ya resuelto, discutimos qué flujo crítico del cliente real ameritaba el mismo análisis. Se descartó "gestión de eventos" (bajo volumen de datos sensibles) y se eligió **el registro y gestión de datos personales de usuarios/afiliados en Koha y Llave del Saber**, por ser el flujo que más directamente conecta con los hallazgos ya diagnosticados en los Talleres 3 y 4 (duplicidad de sistemas, credencial única, datos de menores de edad).
- Herramientas usadas: draw.io para los DFD, Excel/`openpyxl` para las tablas STRIDE siguiendo la plantilla oficial, Docker para levantar OWASP Juice Shop.
- Alcanzamos a completar el caso base de EdukIT por completo (DFD + tabla STRIDE de 7 filas) y a bocetar el DFD inicial del cliente real. Quedó pendiente para fuera de clase el reconocimiento pasivo autorizado sobre el sistema real, la tabla STRIDE completa del cliente, y la redacción del informe y las referencias.

## 🧩 Boceto inicial del modelo

<img width="762" height="452" alt="DFD EdukIT - Taller 5" src="dfd-edukit-borrador.drawio.jpeg" />

> El archivo `dfd-edukit-borrador.drawio` de esta carpeta corresponde al diagrama de flujo de datos del caso base de EdukIT, resuelto en clase siguiendo el ejemplo guiado (Paso 1 de la metodología). El boceto inicial del cliente real (a mano/pizarra) solo tenía los 2 procesos y los 2 almacenes de datos identificados, sin marcar todavía el límite de confianza ni los flujos numerados. El DFD completo del cliente, con el límite de confianza entre la biblioteca y la infraestructura externa ya trazado, quedó como `dfd-cliente-final.drawio` en `entrega/` — un ajuste que se hizo *después* de clase, al hacer el reconocimiento pasivo sobre el manual oficial de Llave del Saber: nos dimos cuenta de que la credencial de acceso (F4) merecía quedar resaltada como el flujo más crítico del diagrama, algo que no era evidente en el boceto de pizarra.

## 📋 Resumen de la tabla STRIDE de clase (EdukIT)

| ID | Tipo STRIDE | Componente / Activo | Nivel de Riesgo |
|---|---|---|---|
| T4 | Information Disclosure | BD de Usuarios (D1) | Alto |
| T1 | Spoofing | Sistema de Autenticación (P1) / Credenciales (F1) | Alto |
| T7 | Spoofing | Formulario de login (reto práctico Juice Shop) | Alto |
| T6 | Elevation of Privilege | Solicitud de curso con rol (F4) | Medio |
| T2 | Tampering | Token de sesión (F3) | Medio |
| T3 | Repudiation | Sistema de Autenticación (P1) — registro de acciones | Medio |
| T5 | Denial of Service | Módulo de Cursos (P2) | Bajo |

_Tabla completa con las 12 columnas (impacto, probabilidad, controles, mitigación, responsable, estado) en `tabla-stride-clase.xlsx`._

## 🔁 Tareas definidas para complementar el taller

| Tarea asignada | Responsable | Fecha estimada |
|---|---|---|
| Reconocimiento pasivo autorizado sobre Koha y Llave del Saber | Brayan Presiga | 12/09 |
| Construir el DFD completo del cliente en draw.io | Julián Aguirre | 12/09 |
| Completar la tabla STRIDE del cliente (`tabla-stride-cliente.xlsx`) | Jorge Alarcón | 13/09 |
| Redactar `informe.md` y `referencias.md` | Jorge Alarcón / Brayan Presiga | 13/09 |

---

_Este documento resume el trabajo colaborativo realizado durante la sesión del Taller 5 en el curso AREM - Universidad de La Sabana._
