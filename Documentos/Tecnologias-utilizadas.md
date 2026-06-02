# Tecnologías Utilizadas

## Stack general
React 18, HTML5, CSS3 y JavaScript en frontend. Node.js 18 y Express en backend. MySQL 8 o PostgreSQL como base de datos. Git/GitHub para control de versiones.

## Frontend
- React con Hooks y Context API.
- React Router para navegación.
- Axios para consumo de API.
- CSS3 responsive con Flexbox y Grid.
- HTML5 semántico.

```javascript
import { useEffect, useState } from 'react';
import axios from 'axios';

function Mascotas() {
  const [mascotas, setMascotas] = useState([]);
  useEffect(() => {
    axios.get('/api/mascotas').then(res => setMascotas(res.data));
  }, []);
  return <div>{mascotas.map(m => <div key={m.id}>{m.nombre}</div>)}</div>;
}
```

## Backend
- Node.js como runtime.
- Express para API REST.
- Middleware para JSON, CORS y seguridad.
- Nodemailer para correos.
- Multer para cargas de archivos.

```javascript
const express = require('express');
const app = express();
app.use(express.json());
app.get('/health', (req, res) => res.json({ status: 'ok' }));
```

## Base de datos
- Tablas principales: usuarios, mascotas, solicitudes_adopcion, historiales_clinicos.
- Índices para estado, fecha y relaciones.
- ORM sugerido: Sequelize.

```sql
CREATE TABLE mascotas (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100),
  estado ENUM('disponible','en_proceso','adoptado')
);
```

## Autenticación
- JWT para sesiones.
- bcryptjs para contraseñas.
- RBAC por roles: admin, veterinario, voluntario, adoptante.

## Almacenamiento
- Archivos locales con Multer.
- Alternativa en nube: AWS S3.

## Testing
- Jest para pruebas unitarias.
- React Testing Library para componentes.
- Cypress para pruebas end-to-end.

## Seguridad y monitoreo
- Helmet para headers seguros.
- Rate limiting para evitar abuso.
- Validación de entrada con Joi o express-validator.
- Logging con Winston.

## Despliegue
- Docker para contenerización.
- Heroku, AWS o DigitalOcean como hosting.

## Variables de entorno
```env
NODE_ENV=production
PORT=5000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=secreto
JWT_SECRET=clave-secreta
```

## Scripts comunes
```json
{
  "start": "node app.js",
  "dev": "nodemon app.js",
  "test": "jest",
  "lint": "eslint src/"
}
```

## Versiones recomendadas
- Node.js: 18.x o 20.x
- React: 18.x
- Express: 4.18.x
- MySQL: 8.x
- PostgreSQL: 15.x+

## Futuro
- TypeScript.
- Docker/Kubernetes.
- WebSockets.
- GraphQL.

---

Versión 1.0 | Junio 2026