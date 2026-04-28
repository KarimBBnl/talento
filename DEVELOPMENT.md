# Guía de Desarrollo y Deployment - Elijo Quedarme

## 📋 Requisitos del Sistema

### Mínimos
- Node.js 18.0.0+
- npm 9.0.0+ o yarn 3.0.0+
- Git

### Recomendado para desarrollo
- Visual Studio Code
- Extensiones recomendadas:
  - ES7+ React/Redux/React-Native snippets
  - Tailwind CSS IntelliSense
  - TypeScript Vue Plugin (Volar)
  - Prettier - Code formatter

## 🚀 Instalación Local

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/elijoquedarme.git
cd Talento
```

### 2. Instalar dependencias
```bash
npm install
# o
yarn install
```

### 3. Configurar variables de entorno
```bash
cp .env.example .env.local
# Editar .env.local con tus valores
```

### 4. Ejecutar en desarrollo
```bash
npm run dev
# o
yarn dev
```

La aplicación estará disponible en `http://localhost:3000`

## 📚 Estructura de Carpetas

```
src/
├── app/                  # App directory de Next.js
│   ├── globals.css      # Estilos globales
│   ├── layout.tsx       # Layout principal
│   ├── page.tsx         # Home page
│   ├── talento/         # Sección para talento
│   └── empresas/        # Sección para empresas
├── components/          # Componentes React reutilizables
│   ├── Navbar.tsx
│   ├── Footer.tsx
│   ├── Button.tsx
│   ├── EmpresaCard.tsx
│   ├── SelloCard.tsx
│   └── sections/        # Secciones de la landing
├── types/               # Tipos TypeScript
│   └── index.ts
├── data/                # Data y mocks
│   └── mock.ts
├── utils/               # Funciones utilidad
│   └── helpers.ts
└── constants/           # Constantes de la app
    └── index.ts
```

## 🛠️ Comandos Disponibles

```bash
# Desarrollo
npm run dev              # Inicia servidor de desarrollo

# Build y producción
npm run build            # Compila la aplicación
npm run start            # Inicia servidor de producción
npm run lint             # Ejecuta linter

# Otros
npm run type-check       # Verifica tipos TypeScript
npm run format           # Formatea código con Prettier
```

## 🎨 Personalizando Colores

Los colores se configuran en `tailwind.config.ts`:

```ts
colors: {
  primary: '#D63031',      // Rojo pasión
  secondary: '#00B894',    // Verde esperanza
  accent: '#FDCB6E',       // Amarillo energía
  dark: '#2C3E50',         // Oscuro profesional
  light: '#ECF0F1',        // Claro minimalista
}
```

## 🌐 Deployment

### Opción 1: Vercel (Recomendado)

```bash
# Instalar Vercel CLI
npm i -g vercel

# Deploy
vercel
```

### Opción 2: Docker

```dockerfile
# Dockerfile ya incluido en el proyecto
docker build -t elijoquedarme .
docker run -p 3000:3000 elijoquedarme
```

### Opción 3: Manual en servidor

```bash
npm install
npm run build
npm start
```

## 📊 Monitoreo y Logs

Los logs de aplicación están en `logs/` (cuando se implemente backend)

## 🔒 Variables de Entorno - Producción

Para producción, configurar en el dashboard del hosting:
- DATABASE_URL
- NEXTAUTH_SECRET
- API_SECRET_KEY
- STRIPE_SECRET_KEY (si usas pagos)
- etc.

## 🧪 Testing (Por implementar)

```bash
npm test                 # Ejecuta tests
npm run test:watch      # Tests en modo watch
npm run test:coverage   # Cobertura
```

## 📝 Convenciones de Código

### Componentes
- Use `'use client'` para componentes interactivos
- Prefer funciones de flecha
- Use TypeScript para type safety
- Props interface siempre

```tsx
'use client';

interface MyComponentProps {
  title: string;
  onClick?: () => void;
}

export default function MyComponent({ title, onClick }: MyComponentProps) {
  return <div onClick={onClick}>{title}</div>;
}
```

### Estilos
- Usar Tailwind CSS clases
- Definir clases reutilizables en `globals.css`
- Evitar CSS inline

### Rutas
- Usar `next/link` para navegación interna
- Usar `next/router` en cliente si es necesario

## 🚨 Troubleshooting

### Error: "Cannot find module '@/...'"
- Revisar `tsconfig.json` paths configuration
- Reinicar servidor: `npm run dev`

### Error: "Tailwind styles not loading"
- Verificar `globals.css` está importado en layout
- Ejecutar `npm install` nuevamente

### Error de CORS
- Configurar headers en `next.config.js`
- Verificar URLs en `.env.local`

## 🐛 Reportar Problemas

Si encuentras bugs:
1. Describe el problema claramente
2. Pasos para reproducir
3. Screenshots si es necesario
4. Información del sistema

## 📚 Recursos

- [Next.js Docs](https://nextjs.org/docs)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [TypeScript](https://www.typescriptlang.org/docs/)
- [React](https://react.dev)

## 📞 Soporte

Para preguntas o soporte: info@elijoquedarme.es

---

Happy coding! 🚀
