# Programación de Horarios de Clase mediante Algoritmos Genéticos

## Descripción del problema

El problema de la programación de horarios de clase es un desafío complejo que consiste en generar un cronograma para un conjunto de cursos, considerando disponibilidad de profesores, aulas, horarios, grupos de alumnos, etc., cumpliendo una serie de restricciones y optimizando ciertos criterios.

Para este proyecto, se trabaja una **versión simplificada**:

- Hay un conjunto de **cursos universitarios**, cada uno con una **cantidad de alumnos**.
- El objetivo es **asignar a cada curso** un **horario, un aula y un profesor**, generando un cronograma válido.

La asignación debe respetar las siguientes **restricciones**:

### Restricciones obligatorias

1. Un aula no puede ser ocupada por más de una clase al mismo tiempo.
2. Un profesor no puede dictar clase en diferentes aulas al mismo tiempo.
3. La cantidad de alumnos de un curso no debe exceder la capacidad del aula asignada.

### Restricciones opcionales

1. Ser eficiente en la asignación de aula (capacidad cercana a la cantidad de alumnos).
2. Tener en cuenta el horario preferido del profesor.
3. No asignar clases los jueves de 10:00 a 14:00 por eventos culturales.

---

## Implementación solicitada

Se pide implementar un **algoritmo genético** para encontrar soluciones (cronogramas) óptimas para la Facultad de Ciencias e Ingeniería de la PUCP.

Los pasos específicos son:

1. **Codificación**: Definir la representación de cromosomas y genes para un cronograma de clases.
2. **Función de fitness**: Evaluar la calidad de cada cronograma considerando el cumplimiento de las restricciones.
3. **Operadores genéticos**: Implementar o mejorar operadores de cruzamiento y mutación para generar soluciones más eficientes.
4. **Condición de parada**: Definir un criterio como número máximo de generaciones, fitness objetivo alcanzado o estancamiento.
5. **Experimentos**: Evaluar el algoritmo usando diferentes operadores y tasas de mutación. 
6. **Evolución**: Mostrar la mejora progresiva del cronograma y el número de conflictos a lo largo de las generaciones.
7. **Cronograma óptimo**: Presentar el mejor cronograma encontrado que cumpla las restricciones obligatorias (y ojalá también las opcionales).
8. **Análisis de resultados**: Concluir sobre el desempeño de los operadores y tasas de mutación utilizadas.
9. **Entrega**: Entregar un **notebook** con las implementaciones y un **informe** de acuerdo al formato.

---

## Caso de estudio: datasets disponibles

### 1. Horario

| horario_id | horario              |
|------------|----------------------|
| H001       | L-Mi-V 09:00 – 10:00  |
| H002       | L-Mi-V 10:00 – 11:00  |
| H003       | Ma-J 09:00 – 10:30    |
| H004       | Ma-J 10:30 – 12:00    |

---

### 2. Profesor

| profesor_id | nombre                  | horario_preferido |
|-------------|--------------------------|-------------------|
| P001        | Dr. Edwin Villanueva      |                   |
| P002        | Mg. Layla Hirsh           | H001              |
| P003        | Dr. Manuel Tupia          |                   |
| P004        | Mg. Cesar Aguilera        | H002              |

---

### 3. Aula

| aula_id | capacidad |
|---------|-----------|
| A001    | 45        |
| A002    | 35        |
| A003    | 25        |

---

### 4. Curso

| curso_id | curso                        | cantidad_alumnos | lista_profesores      |
|----------|------------------------------|------------------|------------------------|
| C001     | Fundamentos de programación  | 45               | P001, P002, P003, P004 |
| C002     | Bases de Datos               | 45               | P004                   |
| C003     | Algoritmia                   | 35               | P002, P003             |
| C004     | Sistemas de información      | 30               | P003, P004             |
| C005     | Sistemas de Información 2    | 30               | P003, P004             |
| C006     | Machine Learning             | 25               | P001, P002             |
| C007     | Deep Learning                | 20               | P001                   |

---

##  Enfoque de la solucción

- Cada individuo de la población representa un cronograma completo de la clase, dicha representación se modeló como una lista de clases asignadas, la cual incluye: curso asignado, profesor elegido, aula asignada y horario asignado.
- El algoritmo genético recibe como entrada los datos de cursos, profesores, aulas y horarios, junto con parámetros como tamaño de población y tasas de mutación. Como salida, genera un cronograma de clases que maximiza el cumplimiento de restricciones y optimiza el uso de recursos. Durante el proceso, crea poblaciones iniciales, evalúa fitness, y aplica operadores de selección, cruzamiento y mutación para mejorar las soluciones generación tras generación.
- Se diseñó un operador de cruzamiento uniforme que mezcla clases de dos padres al azar, manteniendo consistencia entre cursos y horarios. Para la mutación, se adaptó un operador que cambia aleatoriamente el profesor, aula o horario de una clase asignada, respetando las restricciones académicas. La evaluación del fitness penaliza sobrecupos, conflictos de horarios y premia la cercanía entre la capacidad del aula y el número de alumnos, además de considerar las preferencias horarias de los profesores.

