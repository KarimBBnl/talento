# Elijo Quedarme - Plataforma de Certificación de Talento en Aragón

Una plataforma web innovadora diseñada para retener y atraer talento joven en Aragón mediante certificación verificada de empresas y visibilidad de oportunidades reales.

## 🎯 Visión

Transformar el ecosistema laboral aragonés en un referente de confianza y desarrollo, rompiendo la narrativa de "fuera es mejor" mediante transparencia real, certificación local potente y visibilidad para el talento.

## 🚀 Características Principales

### Para Talento Joven
- **Explorador de Empresas Certificadas**: Busca y filtra por sector, ubicación, sello y salario
- **Comparador Inteligente**: Compara Aragón vs Madrid/Barcelona en costes, oportunidades y calidad de vida
- **Mediación Laboral**: Equipo especializado si las cosas no van bien
- **Red de Conexión**: Conecta con talento joven de Aragón

### Para Empresas
- **Sistema de Sellos**: 4 categorías verificadas (Cantera, Energía, Anti-Rutina, Flex-Aragón)
- **Auditoría Presencial**: Verificación real de compromisos
- **Ranking Público**: Visibilidad en la plataforma
- **Acceso a Talento**: Pool de candidatos certificados
- **Medición ODS**: Reporte automático de impacto sostenible

## 📊 Los 4 Sellos

| Sello | Descripción | Requisitos Clave |
|-------|-------------|-----------------|
| 🎓 **Cantera y Éxito Dual** | Inversión en prácticas y talento joven | >70% prácticas→indefinido, mentoría, crecimiento |
| 🥗 **Energía Mañica** | Nutrición y bienestar | Desayunos saludables, Km0, espacios certificados |
| 🔄 **Anti-Rutina** | Rotación, formación y evolución | Rotación anual, >40h formación/año, innovación |
| ⏰ **Flex-Aragón** | Flexibilidad y solidez empresarial | Horarios flexibles, teletrabajo, >10 años estabilidad |

## 🌍 Alineación ODS

- **ODS 3**: Salud y Bienestar
- **ODS 4**: Educación de Calidad  
- **ODS 8**: Trabajo Decente
- **ODS 11**: Ciudades Sostenibles

## 🛠️ Instalación

### Requisitos Previos
- Node.js 18+
- npm o yarn

### Pasos de Instalación

1. **Clonar o descargar el repositorio**
```bash
cd Talento
```

2. **Instalar dependencias**
```bash
npm install
```

3. **Ejecutar en desarrollo**
```bash
npm run dev
```

La aplicación estará disponible en `http://localhost:3000`

4. **Compilar para producción**
```bash
npm run build
npm run start
```

## 📁 Estructura del Proyecto

```
Talento/
├── src/
│   ├── app/
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── talento/
│   │   │   └── page.tsx
│   │   └── empresas/
│   │       └── page.tsx
│   └── components/
│       ├── Navbar.tsx
│       ├── Footer.tsx
│       └── sections/
│           ├── HeroSection.tsx
│           ├── ProblemaSection.tsx
│           ├── SolucionSection.tsx
│           ├── SellosSection.tsx
│           ├── ComparisonSection.tsx
│           ├── OdsSection.tsx
│           └── CtaSection.tsx
├── package.json
├── tailwind.config.ts
├── tsconfig.json
├── next.config.js
└── postcss.config.js
```

## 🎨 Paleta de Colores

- **Primario**: #D63031 (Rojo pasión - Aragón)
- **Secundario**: #00B894 (Verde esperanza)
- **Accent**: #FDCB6E (Amarillo energía)
- **Dark**: #2C3E50 (Oscuro profesional)
- **Light**: #ECF0F1 (Claro minimalista)

## 🔧 Tecnologías

- **Framework**: Next.js 14
- **Styling**: Tailwind CSS
- **Language**: TypeScript
- **UI Components**: Componentes personalizados React

## 📱 Responsive

La plataforma está completamente optimizada para:
- Desktop (1920px+)
- Tablet (768px - 1024px)
- Mobile (320px - 767px)

## 🚦 Páginas Principales

- **/** - Landing page con visión completa
- **/talento** - Explorador de empresas certificadas
- **/empresas** - Información y proceso de certificación
- **/talento/mis-oportunidades** (próxima)
- **/empresas/dashboard** (próxima)

## 📈 Próximas Fases

- [ ] Backend API (Node.js/Express)
- [ ] Base de datos (PostgreSQL)
- [ ] Sistema de autenticación
- [ ] Dashboard de empresas
- [ ] Portal de aplicaciones
- [ ] Sistema de mediación
- [ ] Reportes y analytics
- [ ] Integración de pagos
- [ ] APP móvil

## 🤝 Contribuir

Este es un proyecto para retener talento en Aragón. Si quieres contribuir:

1. Fork el proyecto
2. Crea tu rama (`git checkout -b feature/mejora`)
3. Commit tus cambios (`git commit -m 'Añade mejora'`)
4. Push a la rama (`git push origin feature/mejora`)
5. Abre un Pull Request

## 📧 Contacto

Para preguntas, sugerencias o participar:
- Email: info@elijoquedarme.es
- Web: www.elijoquedarme.es

## 📄 Licencia

Este proyecto está bajo licencia MIT. Ver archivo `LICENSE` para más detalles.

---

**Elijo Quedarme**: La plataforma que hace que el talento joven quiera quedarse en Aragón.

*"Porque Aragón es tu futuro"*
