# API - Alumnos RDS v2 (Ejercicio 1)

En este ejercicio implementaremos una API RESTful que lista alumnos almacenados en una base de datos MySQL (RDS), utilizando **AWS Secrets Manager** para manejar de forma segura las credenciales de conexión. Desarrollado con Python, Serverless Framework y AWS Lambda.

---

## ✅ Objetivo del Ejercicio 1

> Implementar el `api-alumnos-rds-v2` reemplazando el uso de **Systems Manager Parameter Store** por **AWS Secrets Manager**

---

## ⚙️ Tecnología utilizada

- AWS Lambda  
- API Gateway  
- AWS Secrets Manager ✅  
- Amazon RDS (MySQL)  
- Serverless Framework  
- Python 3.13  
- PyMySQL  

---

## 📁 Estructura del Proyecto

api-alumnos-rds-v2/
│
├── ListarAlumnos.py # Lógica Lambda
├── serverless.yml # Configuración Serverless Framework
├── requirements.txt # pymysql
└── pymysql/ # Librería instalada

pgsql
Copiar
Editar

---

## 🗃️ Base de datos en Amazon RDS (MySQL)

```sql
CREATE DATABASE dev;
USE dev;

CREATE TABLE alumnos (
  alumno_id VARCHAR(20) NOT NULL PRIMARY KEY,
  apellidos VARCHAR(100) NOT NULL,
  nombres VARCHAR(100) NOT NULL
);

INSERT INTO alumnos (alumno_id, apellidos, nombres) VALUES
('2025100001', 'Delgado Ríos', 'Juan'),
('2025100002', 'Ruiz Hinojosa', 'Fernanda'),
('2025100003', 'Colchado Li', 'Carolina');

-- Usuarios por stage
CREATE USER 'user_dev'@'%' IDENTIFIED BY 'xyz-324@54';
GRANT ALL PRIVILEGES ON dev.* TO 'user_dev';

CREATE DATABASE test;
GRANT ALL PRIVILEGES ON test.* TO 'user_test'@'%';

CREATE DATABASE prod;
GRANT ALL PRIVILEGES ON prod.* TO 'user_prod'@'%';
```

🚀 Despliegue
bash
Copiar
Editar
pip install pymysql -t .
sls deploy --stage dev
sls deploy --stage test
sls deploy --stage prod

🌐 Endpoints
Stage	URL
dev	https://p1ds8bh0i1.execute-api.us-east-1.amazonaws.com/dev/alumnos/listar
test	https://p1ds8bh0i1.execute-api.us-east-1.amazonaws.com/test/alumnos/listar
prod	https://p1ds8bh0i1.execute-api.us-east-1.amazonaws.com/prod/alumnos/listar

✅ Resultado esperado
json
Copiar
Editar
[
  ["2025100001", "Delgado Ríos", "Juan"],
  ["2025100002", "Ruiz Hinojosa", "Fernanda"],
  ["2025100003", "Colchado Li", "Carolina"]
]


🧑‍💻 Autor
Dylan Cabezas
CS2032
