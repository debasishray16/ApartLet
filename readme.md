#

1. Steps:

- Move the file to Xampp folder location.
- Then, run the XAMPP server and start Apache and Server and type:

```bash
localhost/phpmyadmin/8366
```

- Upload the whole project in:

```bash
C:\xampp\htdocs
```

- Upload the database in **localhost/phpmyadmin/8366** by creating database with name:

```bash
house_rental_db
```

## Starting website

```bash
http://localhost/house_rental/login.php
```

### Tables

1. categories table

```sql
CREATE TABLE categories (
    id INTEGER(30) PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name VARCHAR(200) NOT NULL
);

```

2. houses table

```sql
CREATE TABLE houses (
    id INTEGER(30) PRIMARY KEY NOT NULL,
    house_no VARCHAR(50) NOT NULL,
    category_id INTEGER(30) NOT NULL,
    description TEXT NOT NULL,
    price DOUBLE
);

```

3. payments table

```sql
CREATE TABLE payments (
    id INTEGER(30) NOT NULL,
    tenant_id INTEGER(30) NOT NULL,
    amount FLOAT NOT NULL,
    invoice VARCHAR(50) NOT NULL,
    date_created DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

4. system_settings table

```sql
CREATE TABLE system_settings (
    id INTEGER(30) NOT NULL,
    name TEXT NOT NULL,
    email VARCHAR(200) NOT NULL,
    contact VARCHAR(20) NOT NULL,
    cover_img TEXT NOT NULL,
    about_content TEXT NOT NULL
);
```

5. tenants table

```sql
CREATE TABLE tenants (
    id INTEGER(30) NOT NULL PRIMARY KEY,
    firstname VARCHAR(100) NOT NULL,
    lastname VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    contact VARCHAR(50) NOT NULL,
    house_id INTEGER(30) NOT NULL,
    status TINYINT(1) NOT NULL,
    date_in DATE
);
```

6. users table

```sql
CREATE TABLE users (
    id INTEGER(30) NOT NULL PRIMARY KEY,
    name TEXT NOT NULL,
    username VARCHAR(200) NOT NULL,
    password TEXT NOT NULL,
    type TINYINT(1) NOT NULL
);
```

#### Functional Dependancies

```text
1. houses Table:
id uniquely determines all other attributes (house_no, category_id, description, price).
house_no and category_id together determine id.

Functional dependencies:
id -> house_no, category_id, description, price
house_no, category_id -> id

2. categories Table:
id uniquely determines name.

Functional dependencies:
id -> name

3. payments Table:
id uniquely determines all other attributes (tenant_id, amount, invoice, date_created).

Functional dependencies:
id -> tenant_id, amount, invoice, date_created

4. system_settings Table:
id uniquely determines all other attributes (name, email, contact, cover_img, about_content).

Functional dependencies:
id -> name, email, contact, cover_img, about_content

5. tenants Table:
id uniquely determines all other attributes (firstname, lastname, email, contact, house_id, status, date_in).
house_id and date_in together determine id.

Functional dependencies:
id -> firstname, lastname, email, contact, house_id, status, date_in
house_id, date_in -> id

6. users Table:
id uniquely determines all other attributes (name, username, password, type).

Functional dependencies:
id -> name, username, password, type
```

#### Foreign-Key Dependancies

```text
1. houses Table:
The category_id column references the id column in the categories table.
Foreign key relationship:
category_id REFERENCES categories(id)

2. payments Table:
The tenant_id column references the id column in the tenants table.
Foreign key relationship:
tenant_id REFERENCES tenants(id)

3. tenants Table:
The house_id column references the id column in the houses table.
Foreign key relationship:
house_id REFERENCES houses(id)
```


#### DBML Code

https://dbdiagram.io/d

```dbml
Table categories {
  "id" int(30) [pk, not null]
  "name" varchar(200) [not null]
}

Table houses {
  "id" int(30) [pk, not null]
  "house_no" varchar(50) [not null]
  "category_id" int(30) [not null]
  "description" text [not null]
  "price" double [not null]
}

Table payments {
  "id" int(30) [pk, not null]
  "tenant_id" int(30) [not null]
  "amount" float [not null]
  "invoice" varchar(50) [not null]
  "date_created" datetime [not null, default: `current_timestamp()`]
}

Table system_settings {
  "id" int(30) [pk, not null]
  "name" text [not null]
  "email" varchar(200) [not null]
  "contact" varchar(20) [not null]
  "cover_img" text [not null]
  "about_content" text [not null]
}

Table tenants {
  "id" int(30) [pk, not null]
  "firstname" varchar(100) [not null]
  "middlename" varchar(100) [not null]
  "lastname" varchar(100) [not null]
  "email" varchar(100) [not null]
  "contact" varchar(50) [not null]
  "house_id" int(30) [not null]
  "status" tinyint(1) [not null, default: 1, note: '1 = active, 0= inactive']
  "date_in" date [not null]
  
}

Table users {
  "id" int(30) [pk, not null]
  "name" text [not null]
  "username" varchar(200) [not null]
  "password" text [not null]
  "type" tinyint(1) [not null, default: 2, note: '1=Admin,2=Staff']
}




Ref: "categories"."id" < "users"."id"
Ref: "users"."id" < "houses"."category_id"
Ref: "tenants"."id" - "houses"."id"
Ref: "tenants"."id" < "payments"."id"
Ref: "system_settings"."id" - "users"."id"
```