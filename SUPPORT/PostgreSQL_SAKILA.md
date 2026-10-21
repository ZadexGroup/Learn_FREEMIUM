# PostgreSQL_SAKILA

> Entorno de datos de Zadex Learn SQL KIDS. Fuente: backup `dvdrental.tar` proporcionado por el responsable.

## Identificación

- Motor: PostgreSQL.
- Nombre del backup: `dvdrental` (familia de datos Sakila).
- Esquema: `public`.
- Uso del alumno: consultas de solo lectura.
- Esta documentación describe el backup, no garantiza que la instalación actual del alumno sea idéntica.

## Catálogo real de tablas y columnas

### `public.customer`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `customer_id` | `integer DEFAULT nextval('public.customer_customer_id_seq'::regclass) NOT NULL` |
| `store_id` | `smallint NOT NULL` |
| `first_name` | `character varying(45) NOT NULL` |
| `last_name` | `character varying(45) NOT NULL` |
| `email` | `character varying(50)` |
| `address_id` | `smallint NOT NULL` |
| `activebool` | `boolean DEFAULT true NOT NULL` |
| `create_date` | `date DEFAULT ('now'::text)::date NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now()` |
| `active` | `integer` |

### `public.actor`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `actor_id` | `integer DEFAULT nextval('public.actor_actor_id_seq'::regclass) NOT NULL` |
| `first_name` | `character varying(45) NOT NULL` |
| `last_name` | `character varying(45) NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.category`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `category_id` | `integer DEFAULT nextval('public.category_category_id_seq'::regclass) NOT NULL` |
| `name` | `character varying(25) NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.film`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `film_id` | `integer DEFAULT nextval('public.film_film_id_seq'::regclass) NOT NULL` |
| `title` | `character varying(255) NOT NULL` |
| `description` | `text` |
| `release_year` | `public.year` |
| `language_id` | `smallint NOT NULL` |
| `rental_duration` | `smallint DEFAULT 3 NOT NULL` |
| `rental_rate` | `numeric(4,2) DEFAULT 4.99 NOT NULL` |
| `length` | `smallint` |
| `replacement_cost` | `numeric(5,2) DEFAULT 19.99 NOT NULL` |
| `rating` | `public.mpaa_rating DEFAULT 'G'::public.mpaa_rating` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |
| `special_features` | `text[]` |
| `fulltext` | `tsvector NOT NULL` |

### `public.film_actor`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `actor_id` | `smallint NOT NULL` |
| `film_id` | `smallint NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.film_category`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `film_id` | `smallint NOT NULL` |
| `category_id` | `smallint NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.address`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `address_id` | `integer DEFAULT nextval('public.address_address_id_seq'::regclass) NOT NULL` |
| `address` | `character varying(50) NOT NULL` |
| `address2` | `character varying(50)` |
| `district` | `character varying(20) NOT NULL` |
| `city_id` | `smallint NOT NULL` |
| `postal_code` | `character varying(10)` |
| `phone` | `character varying(20) NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.city`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `city_id` | `integer DEFAULT nextval('public.city_city_id_seq'::regclass) NOT NULL` |
| `city` | `character varying(50) NOT NULL` |
| `country_id` | `smallint NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.country`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `country_id` | `integer DEFAULT nextval('public.country_country_id_seq'::regclass) NOT NULL` |
| `country` | `character varying(50) NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.inventory`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `inventory_id` | `integer DEFAULT nextval('public.inventory_inventory_id_seq'::regclass) NOT NULL` |
| `film_id` | `smallint NOT NULL` |
| `store_id` | `smallint NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.language`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `language_id` | `integer DEFAULT nextval('public.language_language_id_seq'::regclass) NOT NULL` |
| `name` | `character(20) NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.payment`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `payment_id` | `integer DEFAULT nextval('public.payment_payment_id_seq'::regclass) NOT NULL` |
| `customer_id` | `smallint NOT NULL` |
| `staff_id` | `smallint NOT NULL` |
| `rental_id` | `integer NOT NULL` |
| `amount` | `numeric(5,2) NOT NULL` |
| `payment_date` | `timestamp without time zone NOT NULL` |

### `public.rental`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `rental_id` | `integer DEFAULT nextval('public.rental_rental_id_seq'::regclass) NOT NULL` |
| `rental_date` | `timestamp without time zone NOT NULL` |
| `inventory_id` | `integer NOT NULL` |
| `customer_id` | `smallint NOT NULL` |
| `return_date` | `timestamp without time zone` |
| `staff_id` | `smallint NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

### `public.staff`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `staff_id` | `integer DEFAULT nextval('public.staff_staff_id_seq'::regclass) NOT NULL` |
| `first_name` | `character varying(45) NOT NULL` |
| `last_name` | `character varying(45) NOT NULL` |
| `address_id` | `smallint NOT NULL` |
| `email` | `character varying(50)` |
| `store_id` | `smallint NOT NULL` |
| `active` | `boolean DEFAULT true NOT NULL` |
| `username` | `character varying(16) NOT NULL` |
| `password` | `character varying(40)` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |
| `picture` | `bytea` |

### `public.store`

| Columna | Tipo y restricciones según DDL |
|---|---|
| `store_id` | `integer DEFAULT nextval('public.store_store_id_seq'::regclass) NOT NULL` |
| `manager_staff_id` | `smallint NOT NULL` |
| `address_id` | `smallint NOT NULL` |
| `last_update` | `timestamp without time zone DEFAULT now() NOT NULL` |

## Relaciones declaradas mediante claves foráneas

| Origen | Columna | Destino | Columna |
|---|---|---|---|
| `customer` | `address_id` | `address` | `address_id` |
| `film_actor` | `actor_id` | `actor` | `actor_id` |
| `film_actor` | `film_id` | `film` | `film_id` |
| `film_category` | `category_id` | `category` | `category_id` |
| `film_category` | `film_id` | `film` | `film_id` |
| `film` | `language_id` | `language` | `language_id` |
| `address` | `city_id` | `city` | `city_id` |
| `city` | `country_id` | `country` | `country_id` |
| `inventory` | `film_id` | `film` | `film_id` |
| `payment` | `customer_id` | `customer` | `customer_id` |
| `payment` | `rental_id` | `rental` | `rental_id` |
| `payment` | `staff_id` | `staff` | `staff_id` |
| `rental` | `customer_id` | `customer` | `customer_id` |
| `rental` | `inventory_id` | `inventory` | `inventory_id` |
| `rental` | `staff_id` | `staff` | `staff_id` |
| `staff` | `address_id` | `address` | `address_id` |
| `store` | `address_id` | `address` | `address_id` |
| `store` | `manager_staff_id` | `staff` | `staff_id` |

## Reglas de uso pedagógico

- No inventar nombres de tablas, columnas, claves ni valores.
- Comprobar cada ejercicio contra el esquema real antes de proponerlo.
- Para un resultado exacto, ejecutar la consulta en una copia de la base o usar resultados efectivamente verificados; nunca deducir valores sin datos.
- Evitar ejercicios que impliquen escribir, borrar o modificar datos.
- No mostrar soluciones completas antes de que el alumno las intente, salvo lo que permitan las reglas vigentes de CORE/CORE_KIDS.
- Las consultas de ejemplo deben utilizar nombres reales y sintaxis PostgreSQL.

## Procedencia técnica

- Tablas `CREATE TABLE` verificadas: 15.
- Relaciones `FOREIGN KEY` verificadas: 18.
- Extracción realizada sobre `restore.sql` incluido en el TAR; no se ha restaurado ni conectado a una instancia PostgreSQL.
