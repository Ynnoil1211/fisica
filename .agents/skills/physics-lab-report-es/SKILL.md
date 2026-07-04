---
name: physics-lab-report-es
description: Redacta informes universitarios de laboratorio de física en español con estructura académica, análisis cuantitativo, incertidumbres, citas IEEE, formato doble columna y checklist de calidad para entrega final. Úsala siempre que el usuario necesite redactar, corregir o completar un informe de laboratorio de física en español.
---

# Physics Lab Report ES (Universidad)

## Propósito

Esta skill guía la elaboración de informes de laboratorio de física a nivel universitario en español, priorizando:

- rigor científico,
- trazabilidad de cálculos,
- tratamiento de incertidumbres,
- conclusiones sustentadas en datos.

También está diseñada para **complementar skills de documentos y análisis** del ecosistema de este repositorio cuando estén disponibles. Si el usuario activó la skill `lab-report-workflow`, seguir su secuencia en vez de trabajar independientemente.

---

## Cuándo usar

Usa esta skill si el usuario necesita:

1. Crear un informe desde cero a partir de apuntes o datos crudos.
2. Reescribir un borrador informal en formato académico universitario.
3. Validar unidades, cifras significativas, propagación de error y consistencia lógica.
4. Preparar versión final para entrega (con checklist y mejoras priorizadas).

**Formato por defecto:** IEEE (citas numéricas entre corchetes), doble columna, márgenes 1", papel carta.

---

## Modo de trabajo (universidad)

### Fase 1: Recolección mínima obligatoria

Si faltan datos, pide solo lo esencial:

- título de práctica,
- objetivo(s),
- marco teórico o ecuaciones base,
- instrumentos (con resolución),
- procedimiento,
- tabla de datos crudos,
- formato de cita exigido por cátedra (por defecto: IEEE).

No inventar datos experimentales.

### Fase 2: Construcción del informe

Generar el informe con:

- **Secciones formales** y notación física correcta.
- **Formato doble columna** (salvo portada y bibliografía).
- **Ecuaciones numeradas** entre paréntesis: (1), (2), etc., citadas en el texto.
- **Figuras y fotos** numeradas (Fig. 1, Fig. 2...) con pie descriptivo inferior.
- **Tablas** numeradas (TABLA I, TABLA II...) con título superior.
- **Citas IEEE** numéricas entre corchetes [1], [2].

### Fase 3: Verificación técnica

Aplicar controles:

- consistencia dimensional,
- unidades SI,
- cifras significativas,
- incertidumbre absoluta y relativa,
- coherencia entre resultados, discusión y conclusiones.

### Fase 4: Entrega

Devolver:

- versión final limpia,
- lista breve de supuestos (si hubo),
- mejoras opcionales para subir calificación.

---

## Integración con skills del repositorio (si están disponibles)

Esta skill puede trabajar en conjunto con skills de:

- **documentos** (formato/estructura de salida),
- **análisis y transformación de contenido** (pasar notas a texto académico),
- **revisión/edición** (mejora de claridad y calidad final).

Regla de integración:

1. Mantener esta skill como orquestadora del contenido científico.
2. Usar skills de documento para formato final (si el usuario lo pide: PDF/DOCX/XLSX/PPTX).
3. Conservar siempre prioridad en exactitud física sobre estilo.

---

## Estructura estándar del informe universitario

1. **Título**
2. **Resumen** (si la cátedra lo requiere)
3. **Objetivos**
4. **Fundamento teórico**
5. **Materiales e instrumentos**
6. **Procedimiento experimental**
7. **Datos experimentales**
8. **Procesamiento de datos y cálculos**
9. **Análisis de incertidumbre y errores**
10. **Discusión de resultados**
11. **Conclusiones**
12. **Referencias**
13. **Anexos** (opcional)

---

## Reglas de redacción científica (español)

- Tono formal, claro, impersonal y verificable.
- Cada afirmación importante debe apoyarse en dato, ecuación o referencia.
- Definir variables/símbolos al primer uso.
- Evitar conclusiones genéricas sin respaldo numérico.
- Conectar explícitamente: objetivo → método → resultado → conclusión.

---

## Cálculos, unidades y cifras significativas

- Usar SI de forma consistente.
- Homogeneizar unidades antes de operar.
- Reportar magnitudes con unidad siempre.
- Mantener cifras significativas coherentes con la resolución instrumental.
- Redondear el valor final en consonancia con su incertidumbre.

Formato recomendado:

- \(x = (\bar{x} \pm \Delta x)\,\text{unidad}\)
- Error relativo: \(\Delta x / x\)
- Error porcentual: \((\Delta x/x)\cdot 100\%\)

---

## Incertidumbre (nivel universitario)

Cuando aplique:

1. Identificar fuentes de error (instrumental, método, operador, ambiente).
2. Estimar incertidumbre en mediciones directas.
3. Propagar en magnitudes derivadas (linealización o aproximación estándar).
4. Reportar incertidumbre absoluta y relativa/porcentual.
5. Comparar con valor teórico y evaluar compatibilidad.

Si faltan parámetros, explicitar supuesto mínimo y su impacto.

---

## Plantilla de salida (modo completo)

### 1) Título

[Completar]

### 2) Resumen

[Problema, método, resultado principal y conclusión breve]

### 3) Objetivos

- [Objetivo 1]
- [Objetivo 2]

### 4) Fundamento teórico

[Ecuaciones, principios físicos y variables]

### 5) Materiales e instrumentos

- [Instrumento] — resolución: [valor]
- [Instrumento] — rango: [valor]

### 6) Procedimiento experimental

[Secuencia replicable de pasos]

### 7) Datos experimentales

[Tabla: magnitud | símbolo | valor | unidad | incertidumbre]

### 8) Procesamiento y cálculos

[Desarrollo paso a paso]

### 9) Incertidumbre y errores

[Estimación + propagación + análisis]

### 10) Discusión

[Interpretación física, comparación con teoría, causas de discrepancia]

### 11) Conclusiones

- [Conclusión cuantitativa 1]
- [Limitación]
- [Mejora propuesta]

### 12) Referencias

[Formato IEEE — numeración correlativa entre corchetes]

Ejemplo:
[1] L. S. García y M. E. Torres, "Propiedades ópticas de películas delgadas," _Rev. Mex. Fís._, vol. 68, n.º 3, pp. 123–130, 2022.
[2] J. D. Jackson, _Classical Electrodynamics_, 3rd ed. New York: Wiley, 1999, cap. 5.

### 13) Anexos

[Datos crudos, gráficas, ajustes, etc.]

---

## Checklist final (previo a entrega)

- [ ] Todas las magnitudes tienen unidad.
- [ ] No hay inconsistencias dimensionales.
- [ ] Cifras significativas correctas.
- [ ] Tablas/figuras tituladas y con ejes/unidades.
- [ ] Incertidumbre reportada cuando corresponde.
- [ ] Comparación teórica cuantificada.
- [ ] Conclusiones responden objetivos.
- [ ] Citas en formato IEEE [1], [2] numeradas correlativamente.
- [ ] Referencias completas al final.

---

## Comportamiento con información incompleta

Si faltan datos críticos:

1. No asumir valores experimentales.
2. Entregar versión parcial claramente marcada.
3. Pedir únicamente los datos mínimos faltantes.
4. Ofrecer plantilla editable para completar.

---

## Prompt de activación sugerido

“Redacta un informe universitario de laboratorio de física en español (modo completo) con estos datos: [pegar datos]. Exige formato IEEE, doble columna, ecuaciones numeradas, figuras con pie, SI, cifras significativas, propagación de incertidumbre y conclusiones sustentadas cuantitativamente.”
