# PostgreSQL_RELATIONS

## 1. Propósito

Documento de referencia del entorno de prácticas **RELATIONS** para Zadex Learn SQL KIDS. Describe exclusivamente el esquema y los datos facilitados por el responsable del curso. No contiene las reglas pedagógicas generales del curso.

- Motor: PostgreSQL.
- Base de datos lógica: RELATIONS (nombre utilizado por el responsable; no se ha verificado el nombre físico de la base de datos).
- Uso: consultas de solo lectura (`SELECT`).
- Tablas: `Employees`, `Customers`, `Project`, `Employee_Project`.

## 2. Tablas y columnas

### Employees

| Columna | Tipo declarado | Restricción |
|---|---|---|
| IDEmployee | VARCHAR(10) | PRIMARY KEY |
| Employee | VARCHAR(100) | NOT NULL |
| Salary | FLOAT | — |
| RateHour | FLOAT | — |

### Customers

| Columna | Tipo declarado | Restricción |
|---|---|---|
| IDCustomer | VARCHAR(10) | PRIMARY KEY |
| Description | VARCHAR(100) | NOT NULL |
| Manager | VARCHAR(10) | FK → Employees.IDEmployee; admite NULL |

### Project

| Columna | Tipo declarado | Restricción |
|---|---|---|
| IDProject | VARCHAR(10) | PRIMARY KEY |
| Description | VARCHAR(100) | NOT NULL |
| Sale | FLOAT | NOT NULL |
| Hours | FLOAT | NOT NULL |
| IDCustomer | VARCHAR(10) | NOT NULL; FK → Customers.IDCustomer |

### Employee_Project

| Columna | Tipo declarado | Restricción |
|---|---|---|
| IDEmployee | VARCHAR(10) | PK compuesta; FK → Employees.IDEmployee |
| IDProject | VARCHAR(10) | PK compuesta; FK → Project.IDProject |

## 3. Relaciones verificadas en el DDL aportado

- `Customers.Manager` → `Employees.IDEmployee` (un empleado puede gestionar varios clientes; un cliente tiene cero o un gestor).
- `Project.IDCustomer` → `Customers.IDCustomer` (un cliente puede tener varios proyectos; cada proyecto pertenece a un cliente).
- `Employee_Project.IDEmployee` → `Employees.IDEmployee`.
- `Employee_Project.IDProject` → `Project.IDProject`.
- `Employees` ↔ `Project`: relación muchos a muchos a través de `Employee_Project`.

## 4. Datos de referencia facilitados

### Employees (6 filas)

| IDEmployee | Employee | Salary | RateHour |
|---|---|---:|---:|
| E01 | Name01 | 100000 | 120 |
| E02 | Name02 | 80000 | 100 |
| E03 | Name03 | 60000 | 60 |
| E04 | Name04 | 50000 | 50 |
| E98 | Name98 | 10000 | 50 |
| E99 | Name99 | 10000 | 50 |

### Customers (7 filas)

| IDCustomer | Description | Manager |
|---|---|---|
| C01 | Customer01 | E03 |
| C02 | Customer02 | E03 |
| C03 | Customer03 | E04 |
| C04 | Customer04 | E01 |
| C05 | Customer05 | E02 |
| C98 | Customer98 | NULL |
| C99 | Customer99 | E99 |

### Project (10 filas)

| IDProject | Description | IDCustomer | Sale | Hours |
|---|---|---|---:|---:|
| P01 | Project01 | C01 | 100000 | 1500 |
| P02 | Project02 | C03 | 200000 | 2500 |
| P03 | Project03 | C04 | 300000 | 7000 |
| P04 | Project04 | C01 | 400000 | 800 |
| P05 | Project05 | C01 | 500000 | 1200 |
| P06 | Project06 | C02 | 600000 | 1900 |
| P07 | Project07 | C05 | 700000 | 2000 |
| P08 | Project08 | C01 | 800000 | 1000 |
| P09 | Project09 | C05 | 900000 | 8000 |
| P10 | Project10 | C03 | 1000000 | 10000 |

### Employee_Project (16 filas)

| IDEmployee | IDProject |
|---|---|
| E01 | P01 |
| E02 | P02 |
| E03 | P03 |
| E04 | P03 |
| E04 | P06 |
| E04 | P07 |
| E01 | P10 |
| E02 | P01 |
| E03 | P02 |
| E02 | P04 |
| E01 | P05 |
| E02 | P07 |
| E01 | P09 |
| E04 | P10 |
| E01 | P04 |
| E03 | P08 |

## 5. Casos especiales útiles para consultas

- `E98` y `E99` no tienen asignaciones en `Employee_Project`.
- `C98` no tiene gestor (`Manager IS NULL`).
- `C98` y `C99` no tienen proyectos en los datos aportados.
- `P03`, `P10`, `P01`, `P02`, `P04` y `P07` tienen más de un empleado asignado.
- La existencia de clientes sin proyectos y empleados sin asignaciones permite comparar `INNER JOIN` y `LEFT JOIN`.

## 6. Reglas de utilización por Zrek

1. Utilizar exclusivamente nombres de tablas y columnas documentados aquí al trabajar con RELATIONS.
2. No inventar datos ni resultados. Si la base real ha cambiado, solicitar al alumno que ejecute la consulta y comparta el resultado, o verificarlo mediante una conexión disponible.
3. Los datos de este archivo son una instantánea del SQL proporcionado, no una comprobación en directo de la instalación.
4. Formular ejercicios exclusivamente de consulta. No pedir `INSERT`, `UPDATE`, `DELETE`, `DROP`, `ALTER` ni otras operaciones de modificación.
5. Separar el planteamiento del ejercicio de su solución; las reglas de pistas y corrección corresponden a `CORE`, `CORE_KIDS` y `SQL_KIDS`.
6. Al cambiar a otro dataset, usar el MD de ese dataset y no trasladar nombres de columnas por analogía.

## 7. Estado de verificación

- DDL y filas: **proporcionados por el responsable del curso**.
- Ejecución efectiva en PostgreSQL: **confirmada verbalmente por el responsable**.
- Conteos de filas: **calculados a partir de los INSERT proporcionados**.
- Estado actual de la base instalada: **no consultado directamente**.
