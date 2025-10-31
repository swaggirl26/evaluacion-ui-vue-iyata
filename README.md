# Dashboard UI/UX - Iyata

Dashboard moderno y funcional construido con **Vue.js 3** y **Chart.js**, diseñado como parte de la evaluación técnica para el rol de Diseñador UI/UX con Frontend.

![Dashboard Preview](./public/screenshot.png)

## 🎯 Características

- **KPI Cards interactivas** con íconos, tendencias y porcentajes de crecimiento
- **Gráfico de barras** con datos mensuales y gradiente de colores
- **Gráfico circular (pizza)** para distribución de ventas por categoría
- **Sidebar moderno** con navegación, calendario integrado e información de usuario
- **Header funcional** con barra de búsqueda, notificaciones y acciones rápidas
- **Diseño responsivo** adaptable a diferentes tamaños de pantalla
- **Paleta de colores coherente** en tonos lilas y morados

## 🛠️ Tecnologías Utilizadas

- **Vue.js 3** - Framework progresivo de JavaScript
- **Vue Router** - Enrutamiento oficial de Vue
- **Chart.js + vue-chartjs** - Librería de gráficos interactivos
- **Lucide Vue** - Librería de íconos moderna
- **CSS3** - Estilos personalizados con Flexbox y Grid
- **Vite** - Build tool y dev server ultrarrápido

## 📦 Instalación

### Prerrequisitos
- Node.js (v16 o superior)
- npm o yarn

### Pasos

1. Clona el repositorio:
```bash
git clone https://github.com/swaggirl26/evaluacion-ui-vue-iyata.git
cd evaluacion-ui-vue-iyata
```

2. Instala las dependencias:
```bash
npm install
```

3. Inicia el servidor de desarrollo:
```bash
npm run dev
```

4. Abre tu navegador en `http://localhost:5173`

## 📁 Estructura del Proyecto
```
src/
├── components/
│   ├── Card.vue              # KPI Cards con íconos y tendencias
│   ├── ChartCard.vue         # Gráfico de barras
│   ├── PieChart.vue          # Gráfico circular
│   ├── Sidebar.vue           # Navegación lateral
│   └── Header.vue            # Barra superior
├── views/
│   └── DashboardView.vue     # Vista principal
├── App.vue                   # Componente raíz
└── main.js                   # Punto de entrada
```

## 🎨 Componentes Principales

### 1. KPI Cards
Tarjetas métricas con:
- Íconos personalizados
- Valores principales
- Porcentajes de crecimiento
- Indicadores de tendencia

### 2. Gráfico de Barras
Visualización de clientes nuevos por mes con:
- Gradiente de colores lila
- Tooltips interactivos
- Resumen interpretativo

### 3. Gráfico de Pizza
Distribución de ventas por categoría:
- Hover interactivo
- Leyenda con valores
- Centro dinámico

### 4. Sidebar
Navegación lateral que incluye:
- Logo y branding
- Menú con íconos
- Calendario mini integrado
- Información de usuario

## 📸 Screenshots

### Vista Desktop
![Dashboard Desktop](./public/screenshot-desktop.png)

### Vista Mobile
![Dashboard Mobile](./public/screenshot-mobile.png)

## 🚀 Scripts Disponibles
```bash
# Desarrollo
npm run dev

# Build para producción
npm run build

# Preview del build
npm run preview

# Lint
npm run lint
```

## 👩‍💻 Desarrollado por

**Diana Gomez**
- GitHub: [@swaggirl26](https://github.com/swaggirl26)
- Email: dianacarolinagomez8@gmail.com

## 📄 Licencia

Este proyecto fue desarrollado como parte de una evaluación técnica para Iyata.

---

⭐ Si te gusta este proyecto, ¡dale una estrella en GitHub!