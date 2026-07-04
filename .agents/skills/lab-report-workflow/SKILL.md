---
name: lab-report-workflow
description: "Guia paso a paso para automatizar informes completos de laboratorio de fisica. Orquesta el flujo: organizacion de datos (xlsx), redaccion tecnica (physics-lab-report-es), maquetacion (docx) y exportacion pdf. Usala cuando el usuario quiera generar un informe completo de principio a fin."
---

# Lab Report Workflow

## Proposito

Orquestar la elaboracion completa de un informe universitario de laboratorio de fisica en espanol, guiando al usuario paso a paso a traves del pipeline:

```
Datos crudos -> XLSX -> physics-lab-report-es -> DOCX -> PDF
```

Esta skill **no reemplaza** a las otras skills: las invoca en secuencia y le indica al usuario que hacer en cada paso.

---

## Cuando NO usar esta skill

- El usuario solo quiere procesar datos o hacer graficas -> usa `xlsx`.
- El usuario solo quiere redactar contenido -> usa `physics-lab-report-es`.
- El usuario solo quiere maquetar un documento -> usa `docx`.
- El usuario solo quiere exportar a PDF -> usa `pdf`.

---

## Flujo de trabajo

### Paso 0: Recoleccion de datos

Preguntar al usuario que informacion tiene disponible. No arrancar hasta tener claro:

1. **Titulo de la practica**
2. **Objetivo(s)** del experimento
3. **Marco teorico**: ecuaciones, principios fisicos, leyes
4. **Instrumentos y sus resoluciones**
5. **Procedimiento experimental**
6. **Datos crudos** (tabla de mediciones directas)
7. **Valor teorico o esperado** (si aplica)
8. **Formato de cita** (por defecto: IEEE)
9. **Incluye fotos/figuras?** (microscopia, montaje, etc.)

Si faltan datos criticos, no inventar. Pedir solo lo minimo necesario y proceder.

---

### Paso 1: Organizar datos en XLSX

**Skill a usar:** `xlsx`

**Instruccion para el usuario:**
"Pega tus datos experimentales crudos y te los organizo en una hoja de calculo con:

- Tablas de mediciones con unidades
- Promedios, desviacion estandar, incertidumbre absoluta y relativa
- Graficas con ejes etiquetados en SI
- Ajuste de curvas (lineal, polinomial, etc.) segun corresponda"

**Output esperado:** Archivo `.xlsx` con datos procesados y graficas.

**Verificacion:** El usuario confirma que los datos, calculos y graficas son correctos.

---

### Paso 2: Redactar informe tecnico

**Skill a usar:** `physics-lab-report-es`

**Instruccion para el usuario:**
"Con estos resultados procesados, redacto el contenido completo del informe en espanol con:

- Estructura academica: titulo, objetivos, fundamento teorico, metodologia, resultados, discusion, conclusiones
- Ecuaciones numeradas con su respectivo numero entre parentesis: (1), (2), etc.
- Figuras citadas como Fig. 1, Fig. 2...
- Tablas con titulo superior (TABLA I, TABLA II...)
- Citas IEEE [1], [2] con referencias al final
- Propagacion de incertidumbres
- Cifras significativas correctas
- Discusion cuantitativa comparando con valor teorico"

**Output esperado:** Contenido textual completo del informe listo para maquetar.

**Verificacion:** El usuario revisa el contenido cientifico y solicita correcciones si es necesario.

---

### Paso 3: Maquetar en DOCX (doble columna)

**Skill a usar:** `docx`

**Instruccion para el usuario:**
"Con el contenido listo, armo el documento .docx en formato IEEE:

- Portada en columna unica (titulo, autores, afiliacion)
- Cuerpo en **doble columna**
- Ecuaciones numeradas con `MathRun`
- Figuras insertadas con pie (Fig. 1: ...)
- Tablas con formato y titulo superior
- Citas IEEE [1], [2] como texto
- Referencias bibliograficas al final en columna unica
- Margenes 1", papel carta
- Encabezado con titulo corto y numero de pagina"

**Output esperado:** Archivo `.docx` con formato listo para entrega.

**Verificacion:** El usuario abre el archivo y confirma que el formato es correcto.

---

### Paso 4: Exportar a PDF final

**Skill a usar:** `pdf`

**Instruccion para el usuario:**
"Exporto el informe a PDF manteniendo:

- Formato doble columna intacto
- Ecuaciones y simbolos matematicos correctos
- Tablas y figuras en su posicion
- Fuentes incrustadas
- Hipervinculos (si aplica)"

**Output esperado:** Archivo `.pdf` listo para entrega.

**Verificacion:** El usuario revisa el PDF final.

---

## Resumen para el usuario

Al final del flujo, entregar:

| Paso | Archivo generado    | Formato   |
| ---- | ------------------- | --------- |
| 1    | Datos procesados    | `.xlsx`   |
| 2    | Contenido redactado | (en chat) |
| 3    | Informe maquetado   | `.docx`   |
| 4    | Informe final       | `.pdf`    |

---

## Notas importantes

- **No saltarse pasos.** Cada paso produce la entrada del siguiente.
- **El usuario valida cada paso** antes de continuar. No asumir que todo esta bien.
- Si el usuario ya tiene algun paso resuelto (ej: ya tiene el .xlsx), empezar desde donde corresponda.
- Preguntar al final si el usuario quiere mejorar algo o si esta satisfecho para entrega.
