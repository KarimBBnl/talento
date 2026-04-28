# Esquema de Base de Datos - Elijo Quedarme

Cuando sea momento de conectar con backend, usar este esquema.

---

## 📊 Tablas Principales

### 1. `users` (Usuarios)
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR UNIQUE NOT NULL,
  password_hash VARCHAR NOT NULL,
  nombre VARCHAR NOT NULL,
  tipo ENUM('talento', 'empresa', 'admin'),
  fecha_creacion TIMESTAMP DEFAULT NOW(),
  fecha_actualizacion TIMESTAMP DEFAULT NOW(),
  activo BOOLEAN DEFAULT true
);
```

### 2. `empresas` (Empresas)
```sql
CREATE TABLE empresas (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  nombre VARCHAR NOT NULL UNIQUE,
  sector VARCHAR NOT NULL,
  ubicacion VARCHAR NOT NULL,
  descripcion TEXT,
  website VARCHAR,
  telefono VARCHAR,
  logo_url VARCHAR,
  num_empleados INT,
  fecha_fundacion DATE,
  certificado BOOLEAN DEFAULT false,
  fecha_certificacion DATE,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### 3. `sellos` (Sellos de Certificación)
```sql
CREATE TABLE sellos (
  id UUID PRIMARY KEY,
  nombre VARCHAR NOT NULL UNIQUE,
  icono VARCHAR,
  descripcion TEXT,
  requisitos JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### 4. `empresas_sellos` (Relación Many-to-Many)
```sql
CREATE TABLE empresas_sellos (
  id UUID PRIMARY KEY,
  empresa_id UUID REFERENCES empresas(id) ON DELETE CASCADE,
  sello_id UUID REFERENCES sellos(id) ON DELETE CASCADE,
  estado ENUM('solicitado', 'auditado', 'certificado', 'vencido', 'rechazado'),
  fecha_solicitud TIMESTAMP DEFAULT NOW(),
  fecha_auditoria DATE,
  auditor_id UUID,
  notas TEXT,
  fecha_proximo_review DATE,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW(),
  UNIQUE(empresa_id, sello_id)
);
```

### 5. `talento` (Profesionales)
```sql
CREATE TABLE talento (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  nombre VARCHAR NOT NULL,
  email VARCHAR UNIQUE NOT NULL,
  profesion VARCHAR,
  ubicacion VARCHAR,
  anos_experiencia INT,
  skills JSONB,
  sectores_interes JSONB,
  sellos_buscados JSONB,
  cv_url VARCHAR,
  linkedin_profile VARCHAR,
  activo BOOLEAN DEFAULT true,
  fecha_creacion TIMESTAMP DEFAULT NOW(),
  fecha_actualizacion TIMESTAMP DEFAULT NOW()
);
```

### 6. `aplicaciones` (Job Applications)
```sql
CREATE TABLE aplicaciones (
  id UUID PRIMARY KEY,
  talento_id UUID REFERENCES talento(id),
  empresa_id UUID REFERENCES empresas(id),
  puesto VARCHAR NOT NULL,
  estado ENUM('enviada', 'revisada', 'entrevista', 'oferta', 'rechazada'),
  carta_presentacion TEXT,
  fecha_aplicacion TIMESTAMP DEFAULT NOW(),
  fecha_respuesta TIMESTAMP,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### 7. `mediaciones` (Mediación Laboral)
```sql
CREATE TABLE mediaciones (
  id UUID PRIMARY KEY,
  talento_id UUID REFERENCES talento(id),
  empresa_id UUID REFERENCES empresas(id),
  asunto VARCHAR NOT NULL,
  descripcion TEXT NOT NULL,
  estado ENUM('abierta', 'en_proceso', 'resuelta', 'cerrada'),
  mediador_id UUID REFERENCES users(id),
  fecha_creacion TIMESTAMP DEFAULT NOW(),
  fecha_resolucion TIMESTAMP,
  resolucion TEXT,
  resolucion_tipo ENUM('permanencia', 'cambio_empresa', 'cese'),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### 8. `auditorias` (Auditoría Presencial)
```sql
CREATE TABLE auditorias (
  id UUID PRIMARY KEY,
  empresa_sello_id UUID REFERENCES empresas_sellos(id),
  auditor_id UUID REFERENCES users(id),
  fecha_programada DATE,
  fecha_realizacion DATE,
  resultado ENUM('aprobado', 'rechazado', 'revisión_pendiente'),
  puntuacion INT (0-100),
  observaciones TEXT,
  fotos JSONB,
  entrevistas_realizadas INT,
  documentos_verificados JSONB,
  created_at TIMESTAMP DEFAULT NOW(),
  updated_at TIMESTAMP DEFAULT NOW()
);
```

### 9. `encuestas` (Encuestas a Empleados)
```sql
CREATE TABLE encuestas (
  id UUID PRIMARY KEY,
  empresa_id UUID REFERENCES empresas(id),
  tipo ENUM('ambiente', 'formacion', 'flexibilidad', 'nutricion'),
  pregunta TEXT NOT NULL,
  es_anonima BOOLEAN DEFAULT true,
  respuestas JSONB,
  fecha_creacion TIMESTAMP DEFAULT NOW(),
  fecha_cierre TIMESTAMP,
  resultados_promedio DECIMAL(3, 2)
);
```

### 10. `reportes_ods` (Reportes de ODS)
```sql
CREATE TABLE reportes_ods (
  id UUID PRIMARY KEY,
  empresa_id UUID REFERENCES empresas(id),
  periodo VARCHAR (YYYY-MM),
  ods_numero INT,
  metricas_cumplidas JSONB,
  impacto TEXT,
  puntuacion INT,
  created_at TIMESTAMP DEFAULT NOW()
);
```

### 11. `newsletter` (Suscripciones)
```sql
CREATE TABLE newsletter (
  id UUID PRIMARY KEY,
  email VARCHAR UNIQUE NOT NULL,
  tipo ENUM('talento', 'empresa', 'general'),
  activa BOOLEAN DEFAULT true,
  fecha_suscripcion TIMESTAMP DEFAULT NOW(),
  fecha_baja TIMESTAMP
);
```

### 12. `auditors` (Auditores)
```sql
CREATE TABLE auditors (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  certificacion VARCHAR,
  especialidades JSONB,
  numero_auditorias INT DEFAULT 0,
  rating DECIMAL(3, 2),
  activo BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT NOW()
);
```

---

## 🔑 Índices Importantes

```sql
-- Para búsquedas frecuentes
CREATE INDEX idx_empresas_sector ON empresas(sector);
CREATE INDEX idx_empresas_ubicacion ON empresas(ubicacion);
CREATE INDEX idx_empresas_certificado ON empresas(certificado);
CREATE INDEX idx_talento_email ON talento(email);
CREATE INDEX idx_aplicaciones_talento_id ON aplicaciones(talento_id);
CREATE INDEX idx_aplicaciones_empresa_id ON aplicaciones(empresa_id);
CREATE INDEX idx_mediaciones_estado ON mediaciones(estado);
```

---

## 🔐 Seguridad

### Roles y Permisos
```sql
CREATE TABLE roles (
  id UUID PRIMARY KEY,
  nombre VARCHAR UNIQUE NOT NULL
);

CREATE TABLE permisos (
  id UUID PRIMARY KEY,
  nombre VARCHAR UNIQUE NOT NULL
);

CREATE TABLE roles_permisos (
  role_id UUID REFERENCES roles(id),
  permiso_id UUID REFERENCES permisos(id),
  PRIMARY KEY (role_id, permiso_id)
);
```

---

## 📈 Estadísticas Iniciales

### Datos de prueba
```sql
-- Crear 6 empresas de ejemplo
INSERT INTO empresas VALUES (...)

-- Crear 4 sellos
INSERT INTO sellos VALUES (...)

-- Crear relaciones
INSERT INTO empresas_sellos VALUES (...)
```

---

## 🔄 Relaciones Principales

```
users (1) ──→ (N) empresas
users (1) ──→ (N) talento
empresas (N) ──→ (M) sellos (through empresas_sellos)
talento (N) ──→ (M) aplicaciones ←→ (M) empresas
talento (1) ──→ (M) mediaciones ←→ (M) empresas
usuarios (1) ──→ (M) auditorias (como auditor)
empresas (1) ──→ (M) reportes_ods
```

---

## 🚀 Próximas Fases de Base de Datos

### Fase 2: Analytics
- `eventos` (page views, clicks)
- `conversiones` (aplicaciones, mediaciones)

### Fase 3: Machine Learning
- `recomendaciones` (talento → empresa)
- `predicciones` (churn risk)

### Fase 4: Integración
- `integraciones_terceros` (Stripe, SendGrid)
- `logs_api` (auditoría de accesos)

---

## 🔍 Queries Comunes

```sql
-- Empresas certificadas por sector
SELECT * FROM empresas 
WHERE certificado = true AND sector = 'Tecnología'
ORDER BY fecha_certificacion DESC;

-- Talento disponible por habilidades
SELECT * FROM talento 
WHERE skills && ARRAY['IA', 'Python']
AND activo = true;

-- Empresas con mejor rating ODS
SELECT empresa_id, AVG(puntuacion) as rating_ods
FROM reportes_ods
GROUP BY empresa_id
ORDER BY rating_ods DESC
LIMIT 10;

-- Mediaciones pendientes
SELECT * FROM mediaciones
WHERE estado IN ('abierta', 'en_proceso')
ORDER BY fecha_creacion;
```

---

## 📦 Herramientas Recomendadas

- **ORM**: Prisma o TypeORM
- **Base de datos**: PostgreSQL
- **Migraciones**: Prisma Migrate o Flyway
- **Versionado**: Git

---

Este esquema es flexible y puede adaptarse según las necesidades reales del proyecto.
