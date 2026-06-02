# Tecnologías Utilizadas - Sistema del Refugio de Animales

## 1. Descripción General

El Sistema de Información del Refugio de Animales es una aplicación web full-stack construida con tecnologías modernas y escalables. A continuación se describe en detalle cada componente tecnológico del proyecto.

---

## 2. Frontend (Interfaz de Usuario)

### 2.1 React

**Versión Recomendada:** 18.x o superior

**Descripción:**
React es una biblioteca de JavaScript mantenida por Meta (Facebook) para la construcción de interfaces de usuario interactivas y responsive. En este proyecto se utiliza para crear una experiencia dinámica y reactiva.

**Funcionalidades utilizadas:**
- Componentes funcionales con Hooks (useState, useEffect, useContext)
- Gestión de estado con Context API
- Routing con React Router
- Aplicación de una sola página (SPA)

**Por qué se eligió:**
- Comunidad grande y activa
- Curva de aprendizaje razonable
- Ecosystem rico con librerías complementarias
- Rendimiento optimizado con Virtual DOM

---

### 2.2 HTML5

**Descripción:**
Lenguaje de marcado estándar para crear la estructura de las páginas web.

**Características utilizadas:**
- Semántica HTML5 (header, nav, main, footer, etc.)
- Formularios con validación nativa (type="email", required, etc.)
- Elementos multimedia (img, video, audio)
- Data attributes para vinculación con JavaScript

---

### 2.3 CSS3

**Descripción:**
Lenguaje de estilos para la presentación visual de la aplicación.

**Características utilizadas:**
- Flexbox para diseño responsive
- CSS Grid para layouts complejos
- Media queries para adaptación móvil
- Animaciones CSS para transiciones suaves
- Variables CSS (custom properties) para temas

**Librerías complementarias:**
- Bootstrap (versión 5.x) - Para componentes predefinidos
- Tailwind CSS (opcional) - Para utilidad first approach

---

### 2.4 JavaScript (ECMA 2020+)

**Versión:** ES6 (ES2020 o superior)

**Descripción:**
Lenguaje de programación interpretado que permite la interactividad en el cliente.

**Características utilizadas:**
- Arrow functions
- Destructuring
- Template literals
- Async/Await para manejo de promesas
- Módulos ES6 (import/export)

---

### 2.5 Dependencias Frontend Clave

| Paquete | Versión | Propósito |
|---------|---------|----------|
| React Router | 6.x | Enrutamiento dentro de la SPA |
| Axios | 1.x | Cliente HTTP para llamadas a API |
| Moment.js | 2.x | Formato y manipulación de fechas |
| React Icons | 4.x | Iconografía |
| SweetAlert2 | 11.x | Modales y notificaciones |
| Formik | 2.x | Gestión de formularios |
| Yup | 1.x | Validación de esquemas |

---

## 3. Backend (Servidor)

### 3.1 Node.js

**Versión Recomendada:** 18.x LTS o superior

**Descripción:**
Entorno de ejecución JavaScript del lado del servidor construido sobre el motor V8 de Chrome.

**Ventajas:**
- Event-driven, non-blocking I/O
- Ideal para aplicaciones escalables
- Ecosistema de paquetes NPM muy extenso
- Rendimiento optimizado

---

### 3.2 Express.js

**Versión Recomendada:** 4.18.x

**Descripción:**
Framework web minimalista y flexible para Node.js que simplifica la creación de APIs RESTful.

**Funcionalidades utilizadas:**
- Enrutamiento HTTP (GET, POST, PUT, DELETE)
- Middleware para procesamiento de solicitudes
- Gestión de sesiones
- Manejo de CORS
- Logging de solicitudes

**Estructura típica:**

```
app.js → routes → controllers → models → database
```

---

### 3.3 Dependencias Backend Clave

| Paquete | Versión | Propósito |
|---------|---------|----------|
| dotenv | 16.x | Gestión de variables de entorno |
| bcryptjs | 2.x | Hashing y verificación de contraseñas |
| jsonwebtoken | 9.x | Generación y validación de JWT |
| cors | 2.x | Control de acceso entre orígenes |
| validator | 13.x | Validación de datos de entrada |
| uuid | 9.x | Generación de identificadores únicos |
| multer | 1.x | Gestión de carga de archivos |
| nodemailer | 6.x | Envío de correos electrónicos |

---

## 4. Base de Datos

### 4.1 MySQL / PostgreSQL

**Versión:**
- MySQL 8.x o PostgreSQL 13.x+

**Descripción:**
Sistema de gestión de bases de datos relacional (RDBMS) para almacenar y recuperar datos de forma eficiente.

**Tablas principales:**

```sql
-- Tabla de usuarios
CREATE TABLE usuarios (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100),
  email VARCHAR(100) UNIQUE,
  contraseña_hash VARCHAR(255),
  rol ENUM('admin', 'veterinario', 'voluntario', 'adoptante'),
  fecha_registro TIMESTAMP
);

-- Tabla de mascotas
CREATE TABLE mascotas (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(50),
  especie VARCHAR(30),
  estado ENUM('disponible', 'en_proceso', 'adoptado'),
  fecha_ingreso DATE,
  foto_url VARCHAR(255)
);

-- Tabla de solicitudes de adopción
CREATE TABLE solicitudes_adopcion (
  id INT PRIMARY KEY AUTO_INCREMENT,
  usuario_id INT FOREIGN KEY,
  mascota_id INT FOREIGN KEY,
  estado ENUM('pendiente', 'aprobada', 'rechazada'),
  fecha_solicitud TIMESTAMP
);

-- Tabla de historiales clínicos
CREATE TABLE historiales_clinicos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  mascota_id INT FOREIGN KEY,
  veterinario_id INT FOREIGN KEY,
  tipo_registro VARCHAR(50),
  descripcion TEXT,
  fecha_registro TIMESTAMP
);
```

---

### 4.2 Opciones de Gestión

**Node.js Drivers:**
- `mysql2` / `mysql` para MySQL
- `pg` para PostgreSQL

**ORMs (Object-Relational Mapping):**
- Sequelize
- TypeORM
- Prisma

**Ejemplo con Sequelize:**

```javascript
const { DataTypes } = require('sequelize');

const Mascota = sequelize.define('Mascota', {
  nombre: DataTypes.STRING,
  especie: DataTypes.STRING,
  estado: DataTypes.ENUM('disponible', 'en_proceso', 'adoptado'),
  foto_url: DataTypes.STRING
});
```

---

## 5. Autenticación y Autorización

### 5.1 JWT (JSON Web Tokens)

**Descripción:**
Sistema estateless de tokens para autenticación en APIs REST.

**Flujo:**
1. Usuario inicia sesión con email/contraseña
2. Servidor genera JWT con información del usuario
3. Cliente almacena el token (localStorage o sessionStorage)
4. Token se envía en header `Authorization: Bearer <token>` en cada solicitud
5. Servidor valida el token antes de procesar

**Estructura de Token:**

```
Header.Payload.Signature

{
  "alg": "HS256",
  "typ": "JWT"
}

{
  "sub": "123456",
  "name": "Juan Pérez",
  "rol": "adoptante",
  "iat": 1516239022
}
```

---

### 5.2 bcryptjs

**Descripción:**
Librería para hashear contraseñas de forma segura.

**Ventajas:**
- Algoritmo adaptable con factor de costo
- Protección contra ataques de fuerza bruta
- Implementación de salt automático

**Ejemplo:**

```javascript
const bcrypt = require('bcryptjs');

// Al registrar
const hash = await bcrypt.hash(contraseña, 10);

// Al autenticar
const esValida = await bcrypt.compare(contraseña, hash);
```

---

## 6. Almacenamiento de Archivos

### 6.1 Multer (Local)

Para carga de fotografías de mascotas:

```javascript
const multer = require('multer');

const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, 'uploads/mascotas/');
  },
  filename: (req, file, cb) => {
    cb(null, Date.now() + '-' + file.originalname);
  }
});

const upload = multer({ storage });
```

### 6.2 Alternativa: Almacenamiento en la Nube

- **AWS S3** - Escalable, confiable
- **Firebase Storage** - Integración fácil con servicios Google
- **Azure Blob Storage** - Ecosistema Microsoft

---

## 7. Servidor Web y Hosting

### 7.1 Opciones de Despliegue

| Plataforma | Tipo | Costo | Ideal para |
|-----------|------|-------|-----------|
| Heroku | PaaS | Freemium/Pago | Prototipo rápido |
| AWS EC2 | IaaS | Pago | Escalabilidad |
| Vercel | PaaS | Freemium/Pago | Frontend (Next.js) |
| DigitalOcean | IaaS | Accesible | Small/Medium apps |
| Google Cloud | IaaS | Pago | Integración Google |
| Railway | PaaS | Pago | Deploy rápido |

---

## 8. Control de Versiones

### 8.1 Git y GitHub

**Descripción:**
Sistema de control de versiones distribuido.

**Flujo de trabajo:**

```bash
# Crear rama de feature
git checkout -b feature/nueva-funcionalidad

# Realizar cambios
git add .
git commit -m "feat: Agregar nueva funcionalidad"

# Pushear a repositorio remoto
git push origin feature/nueva-funcionalidad

# Pull Request y revisión de código
# Merge a rama main
```

**Estructura de ramas:**
- `main` - Código en producción
- `develop` - Rama de desarrollo principal
- `feature/*` - Nuevas características
- `hotfix/*` - Correcciones críticas
- `release/*` - Preparación de versiones

---

## 9. Testing y Calidad de Código

### 9.1 Frameworks de Testing

**Frontend:**
- **Jest** - Testing framework para JavaScript
- **React Testing Library** - Pruebas de componentes React
- **Cypress / Playwright** - Testing end-to-end (E2E)

**Backend:**
- **Jest** - Testing de funciones, modelos
- **Supertest** - Testing de APIs HTTP
- **Mocha + Chai** - Alternativa popular

### 9.2 Herramientas de Calidad

| Herramienta | Propósito |
|-------------|----------|
| ESLint | Análisis estático de código JavaScript |
| Prettier | Formateador de código |
| Husky | Hooks de Git para validaciones |
| SonarQube | Análisis de calidad de código |

---

## 10. PM2 (Production Process Manager)

**Descripción:**
Gestor de procesos para Node.js en producción.

**Características:**
- Reinicio automático de aplicación si falla
- Balanceo de carga (clustering)
- Monitoreo de recursos
- Logs persistentes

**Configuración:**

```javascript
// ecosystem.config.js
module.exports = {
  apps: [{
    name: 'refugio-api',
    script: './server.js',
    instances: 'max',
    exec_mode: 'cluster',
    env: {
      NODE_ENV: 'production'
    }
  }]
};
```

---

## 11. Monitoreo e Instrumentación

### 11.1 Logging

- **Winston** - Logger flexible para Node.js
- **Morgan** - Middleware de logging HTTP para Express

### 11.2 Monitoreo APM

- **New Relic** - Monitoreo de performance
- **Datadog** - Observabilidad inteligente
- **Scout APM** - Alternativa económica

---

## 12. Seguridad

### 12.1 Dependencias de Seguridad

| Paquete | Propósito |
|---------|----------|
| helmet | Configuración de headers de seguridad HTTP |
| express-rate-limit | Limitación de rate para prevenir abuse |
| express-validator | Validación sanitizado de entrada |
| express-mongo-sanitize | Prevención de NoSQL injection |

---

## 13. Variables de Entorno (.env)

```
# Base de Datos
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=tu_contraseña
DB_NAME=refugio_animales

# JWT
JWT_SECRET=tu_clave_secreta_super_larga
JWT_EXPIRES_IN=7d

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=tu_email@gmail.com
SMTP_PASS=tu_contraseña_app

# Servidor
PORT=5000
NODE_ENV=development
CORS_ORIGIN=http://localhost:3000

# Almacenamiento
UPLOAD_DIR=./uploads
MAX_FILE_SIZE=10485760
```

---

## 14. Estructura del Proyecto Recomendada

```
refugio-animales/
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── utils/
│   │   └── App.js
│   ├── package.json
│   └── README.md
│
├── backend/
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── middleware/
│   │   ├── config/
│   │   ├── utils/
│   │   └── app.js
│   ├── tests/
│   ├── .env
│   ├── ecosystem.config.js
│   ├── package.json
│   └── README.md
│
├── database/
│   ├── migrations/
│   ├── seeds/
│   └── schema.sql
│
├── docker/
│   ├── Dockerfile.backend
│   ├── Dockerfile.frontend
│   └── docker-compose.yml
│
└── docs/
    ├── manual-usuario.md
    ├── plan-pruebas.md
    ├── soporte-postproyecto.md
    └── tecnologias-utilizadas.md
```

---

## 15. Scripts NPM Comunes

**Backend:**
```json
{
  "start": "node src/app.js",
  "dev": "nodemon src/app.js",
  "test": "jest --coverage",
  "lint": "eslint src/",
  "lint:fix": "eslint src/ --fix"
}
```

**Frontend:**
```json
{
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject",
  "lint": "eslint src/"
}
```

---

## 16. Versiones Recomendadas (Stack Moderno - 2026)

| Tecnología | Versión |
|-----------|---------|
| Node.js | 18.x LTS o 20.x |
| npm | 9.x o 10.x |
| React | 18.x |
| Express | 4.18.x |
| MySQL | 8.x |
| PostgreSQL | 15.x+ |
| Linux (Producción) | Ubuntu 22.04 LTS |

---

## 17. Próximas Tecnologías a Considerar

- **TypeScript** - Para mayor seguridad de tipos en JavaScript
- **Docker** - Containerización para ambiente consistente
- **GraphQL** - Alternativa a REST API
- **WebSockets (Socket.io)** - Para notificaciones en tiempo real
- **Kubernetes** - Orquestación de contenedores
- **CI/CD (GitHub Actions)** - Integración y despliegue continuo

---

**Documento Versión:** 1.0  
**Última Actualización:** Junio 2026  
**Mantenido por:** Equipo de Desarrollo del Refugio de Animales
