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