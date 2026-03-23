# 📊 Asesor IA Financiero

Una aplicación web completa y moderna para gestionar finanzas personales y empresariales con asesoramiento automático generado por IA.

## 🎯 Descripción General

**Asesor IA Financiero** es un dashboard interactivo que permite:

- **Gestión Financiera Personal**: Registra ingresos, gastos fijos y variables. Obtén análisis automático de tu salud financiera.
- **Gestión Empresarial**: Controla ingresos, costos directos, gastos operativos. Visualiza márgenes y rentabilidad.
- **Asesoramiento Automático**: Genera planes personalizados con recomendaciones de estructura financiera.
- **Simulador de Ingresos**: Modela diferentes productos/servicios y proyecta ganancias a 12 meses.
- **Análisis Comparativo**: Escenarios pesimista, base y optimista para cada operación.

---

## ✨ Características Principales

### 1. **Dashboard de Finanzas Personales**
- 📈 Métricas en tiempo real: ingresos, gastos fijos, variables y saldo neto.
- 📊 Gráficos interactivos: composición del ingreso, distribución de gastos, proyección acumulada.
- 🎯 Puntuación financiera (0-100) con estado y recomendaciones.
- 📋 KPIs: tasa de gasto total, carga de deudas, tasa de ahorro, margen disponible.
- 🏦 Alertas contextuales en verde/ámbar/rojo según estado financiero.

### 2. **Plan Asesor Personalizado** (Personas)
Cuando tienes datos completos, genera automáticamente:
- **4 Pilares de Gestión Financiera**:
  1. **Obligaciones**: Deudas, vivienda, familiar (no negociable).
  2. **Ahorro**: Fondo de emergencia, metas corto plazo.
  3. **Inversión**: CDT, fiduciaria, ETF, pensión voluntaria.
  4. **Vida**: Alimentación, entretenimiento, viajes (gastar sin culpa).
- **Asignación de dinero**: Propone % para cada pilar basado en tus cifras.
- **Hoja de Ruta**: Milestones a 3, 6, 12 meses con acciones concretas.
- **Principios Clave**: Lecciones de finanzas personales aplicadas a tu caso.

### 3. **Dashboard Empresarial**
- 💰 Métricas: ingresos, costos directos, gastos operativos, utilidad bruta y neta.
- 📊 Gráficos: estado de resultados, gastos por categoría, proyección de utilidades.
- 🎯 KPIs: margen bruto, margen neto, carga de nómina, carga financiera, reservas.
- 🚨 Alertas de rentabilidad y salud operativa.

### 4. **Plan Asesor Empresarial**
Análisis estructurado de:
- **Estructura de Costos**: Desglose y recomendaciones de optimización.
- **Gestión de Nómina**: Evaluación de peso en presupuesto.
- **Reservas y Reinversión**: Guía de distribución de utilidades.
- **Marketing y Crecimiento**: Benchmarks y estrategia de inversión.
- **5 Pilares Empresariales**: Costos directos, nómina, operación, reservas, excedente.

### 5. **Simulador de Ingresos** (Empresas)
Modela múltiples productos/servicios con:
- Nombre, tipo (físico/servicio/digital/suscripción).
- Precio de venta, costo unitario, costo variable (empaque, envío).
- Volumen de ventas por período (día/semana/mes/trimestre/año).
- Descuentos e impuestos aplicables.

**Resultados en tiempo real**:
- Precio neto, costo total, margen unitario, margen %.
- Contribución mensual por producto.
- Gráficos: desglose ingresos vs costos, proyección 12 meses.
- **Punto de equilibrio**: Unidades necesarias para cubrir costos fijos.
- **Escenarios**: Pesimista (70%), Base (100%), Optimista (150%).

---

## 🎨 Diseño y UX

### Temas
- **Tema Oscuro** (por defecto): Colores neutros, oro (#d4a853) como acento.
- **Tema Claro**: Versión clara del mismo sistema de diseño.
- **Toggle en la barra superior** para cambiar tema en tiempo real.

### Paleta de Colores
```
Verde (#22c55e)    → Positivo, ahorro, ganancia
Rojo (#ef4444)     → Negativo, deuda, pérdida
Ámbar (#f59e0b)    → Precaución, moderado
Oro (#d4a853)      → Acento principal
Azul (#3b82f6)     → Información, terciario
Púrpura (#8b5cf6)  → Vida, bienestar
Teal (#14b8a6)     → Saldo, neutral positivo
```

### Tipografía
- **Playfair Display** (serif): Títulos, números principales.
- **IBM Plex Mono** (monospace): Etiquetas, valores numéricos, KPIs.
- **Epilogue** (sans-serif): Cuerpo de texto, interfaz general.

### Responsive
- Adaptado para desktop (1200px+), tablet (768px-1199px), móvil (320px-767px).
- Grillas fluidas, navegación colapsable, touch-friendly.

---

## 🔧 Arquitectura Técnica

### Stack
- **HTML5**: Estructura semántica.
- **CSS3**: Sistema de diseño con variables CSS, flexbox, grid.
- **Vanilla JavaScript**: Sin dependencias externas (excepto Chart.js).
- **Chart.js 4.4.1**: Gráficos interactivos (doughnut, line, bar).
- **Fuentes Google Fonts**: Tipografía de calidad.

### Estructura de Datos

#### Estado Global
```javascript
let members = []; // Array de perfiles (personas y empresas)
let activeId = null; // ID del perfil actual
let darkMode = true; // Tema actual
```

#### Estructura de Perfil Personal
```javascript
{
  id: "abc123",
  name: "Juan Pérez",
  type: "personal",
  data: {
    ingresos: [{id, label, val}, ...],
    fijos: [{id, label, cat, val}, ...],
    variables: [{id, label, val}, ...],
  },
  charts: {
    score: Chart,    // Puntuación
    donut: Chart,    // Composición ingresos
    line: Chart,     // Proyección acumulada
    adv: Chart       // Asesor
  }
}
```

#### Estructura de Perfil Empresarial
```javascript
{
  id: "biz456",
  name: "Mi Empresa",
  type: "empresa",
  data: {
    ingresos: [{id, label, val}, ...],
    costos: [{id, label, val}, ...],
    gastos: [{id, label, cat, val}, ...],
    variables: [{id, label, val}, ...],
  },
  charts: { ... }
}
```

### Flujo de Cálculo

#### Para Personas
1. **Lectura de datos**: Suma de ingresos, gastos fijos y variables.
2. **Cálculo de saldo**: Ingreso total - (Fijos + Variables).
3. **Scoring**: Algoritmo que evalúa:
   - Tasa de gasto total (debe ser <80%).
   - Carga de deudas (<20% recomendado).
   - Tasa de ahorro (>10% saludable).
   - Variables (<22% de ingreso).
   - Margen disponible (>5%).
4. **Generación de asesor**: 
   - Define obligaciones (deudas + fijos obligatorios).
   - Propone ahorro recomendado (12% del ingreso).
   - Propone inversión recomendada (10% del ingreso).
   - Calcula "dinero de vida" para gastar sin culpa.
   - Genera hoja de ruta y principios personalizados.

#### Para Empresas
1. **Lectura de datos**: Ingresos, costos directos, gastos operativos, variables.
2. **Cálculo de márgenes**:
   - Margen Bruto = (Ingresos - Costos Directos) / Ingresos × 100%.
   - Margen Neto = (Utilidad Bruta - Gastos - Variables) / Ingresos × 100%.
3. **Scoring**: Evalúa margen neto, margen bruto, carga de nómina, carga financiera, reservas.
4. **Generación de asesor**:
   - Análisis de estructura de costos.
   - Gestión de nómina vs % de ingresos.
   - Recomendaciones de reservas e impuestos.
   - Hoja de ruta para rentabilidad.

#### Para Simulador
1. **Por cada producto**: Calcula margen unitario, contribución mensual.
2. **Agregado**: Suma ingresos, costos, contribución total.
3. **Punto de equilibrio**: Unidades = Costos Fijos / Margen Contribución Unitario.
4. **Escenarios**: Multiplica volumen actual × {70%, 100%, 150%} y recalcula.
5. **Proyecciones**: Línea de 12 meses acumulada.

---

## 🚀 Cómo Usar

### Instalación
1. Descarga `index.html`.
2. Abre en un navegador moderno (Chrome, Firefox, Safari, Edge).
3. No requiere servidor; funciona completamente en el navegador.

### Uso Básico

#### Crear un Perfil
1. Haz clic en "👤 Agregar persona" o "🏢 Agregar empresa".
2. Ingresa el nombre en el modal.
3. Se abre automáticamente la pestaña del nuevo perfil.

#### Ingresar Datos Financieros
1. En el **Dashboard**, completa ingresos, gastos fijos/variables (personas) o ingresos/costos/gastos (empresas).
2. Los gráficos y KPIs se actualizan en **tiempo real**.
3. Haz clic en "✕" para eliminar un ítem.
4. Usa "＋ Agregar" para añadir nuevos ítems.

#### Ver Plan Asesor
1. Navega a la pestaña **"🎯 Plan Asesor"** o **"🏦 Plan Asesor Empresarial"**.
2. Se genera automáticamente con:
   - Diagnóstico personalizado.
   - 4 pilares (personas) o 5 pilares (empresas).
   - Asignación recomendada de dinero.
   - Hoja de ruta con milestones.
   - Principios clave.

#### Simular Ingresos (Empresas)
1. Navega a **"🧮 Simulador de Ingresos"**.
2. Haz clic en "＋ Agregar producto".
3. Completa: nombre, tipo, precio, costo, cantidad.
4. Define costos fijos operativos.
5. Visualiza punto de equilibrio, escenarios y proyecciones.

#### Cambiar Tema
1. Haz clic en el toggle "🌙" en la esquina superior derecha.
2. La aplicación cambia a tema claro/oscuro instantáneamente.

---

## 📊 Fórmulas y Métrica Clave

### Puntuación Financiera Personal (0-100)
```
score = 100
si ingreso = 0:  score = 0
si (gastos_totales/ingreso) > 92%:  score -= 30
si (deudas/ingreso) > 30%:  score -= 20
si (ahorro/ingreso) < 10%:  score -= 20
si (variables/ingreso) > 22%:  score -= 8
si saldo < 0:  score -= 30
score = clamp(score, 0, 100)
```

### Rangos de Scoring
- **70-100**: Situación sólida ✦
- **45-69**: Situación moderada ▲
- **0-44**: Requiere atención ✗

### KPIs Empresariales

| KPI | Fórmula | Óptimo | Alerta |
|-----|---------|--------|--------|
| Margen Bruto | (Ing - Costos) / Ing × 100% | ≥40% | <25% |
| Margen Neto | (UB - Gastos) / Ing × 100% | ≥15% | <5% |
| Carga Nómina | Nómina / Ing × 100% | <35% | >50% |
| Carga Financiera | Deuda / Ing × 100% | <10% | >20% |
| Reservas | Reserva / Ing × 100% | ≥5% | <2% |

---

## 🎯 Lógica del Plan Asesor

### Personas: 4 Pilares
1. **Pilar 1 - Obligaciones**: No negociable. Incluye deudas, vivienda, familiar.
   - Fórmula: SUM(fijos) - SUM(ahorro planificado) - SUM(inversión planificada).
   
2. **Pilar 2 - Ahorro**: Recomendado 12% del ingreso.
   - Incluye fondo de emergencia, metas corto plazo, buffer.
   - Provisión: 55% emergencia, 30% meta CP, 15% buffer.

3. **Pilar 3 - Inversión**: Recomendado 10% del ingreso.
   - CDT/renta fija (40%), fondo diversificado (35%), ETF (15%), pensión voluntaria (10%).
   - Deducible en renta: hasta 30% del ingreso en AFC.

4. **Pilar 4 - Vida**: Lo sobrante después de pilares 1-3.
   - 25% alimentación variable, 20% entretenimiento, 15% ropa, 25% viaje, 15% social.
   - Importancia: Disfrutar sin culpa es clave para sostenibilidad del plan.

### Empresas: 5 Pilares
1. **Costos Directos**: <60% de ingresos.
2. **Nómina**: 25-40% de ingresos según industria.
3. **Operación**: Arriendo, servicios, marketing, otros.
4. **Reserva**: >5% de ingresos (impuestos 30%, fondo operativo, reinversión).
5. **Excedente**: Utilidad disponible para socios.

---

## 🔐 Persistencia de Datos

**Nota**: Actualmente **no hay persistencia automática**. Los datos se pierden al refrescar.

Para agregar persistencia, se puede:
1. Guardar en **localStorage** (navegador local).
2. Integrar con **backend** (API REST).
3. Usar **IndexedDB** para mayor capacidad.

Ejemplo localStorage:
```javascript
function saveMember(member) {
  const stored = JSON.parse(localStorage.getItem('members') || '[]');
  stored.push(member);
  localStorage.setItem('members', JSON.stringify(stored));
}

function loadMembers() {
  const stored = JSON.parse(localStorage.getItem('members') || '[]');
  members = stored;
}
```

---

## 📱 Funcionalidades Futuras

- [ ] **Persistencia**: LocalStorage o backend.
- [ ] **Exportar PDF**: Descargar plan asesor completo.
- [ ] **Integración Bancaria**: Conectar con Plaid/Soda para datos reales.
- [ ] **Múltiples Monedas**: Soportar USD, EUR, etc.
- [ ] **Análisis Histórico**: Comparar meses, evolución del score.
- [ ] **Metas Personalizadas**: Definir targets y trackearlos.
- [ ] **Notificaciones**: Alertas cuando se exceda presupuesto.
- [ ] **Compartir Panes**: Generar enlace compartible para ver asesor.
- [ ] **API Pública**: Para integraciones de terceros.
- [ ] **Mobile App**: React Native o Flutter.

---

## 🎓 Conceptos Financieros Aplicados

### Punto de Equilibrio
Número de unidades donde ingresos = costos totales.
```
PE = Costos Fijos / Margen Contribución Unitario
```
Indica el volumen mínimo para ser rentable.

### Margen de Contribución
Diferencia entre precio y costo variable.
```
MC = Precio - Costo Variable
```
Porcentaje de cada venta que cubre costos fijos y utilidad.

### Análisis de Sensibilidad
Escenarios (pesimista -30%, base, optimista +50%) muestran cómo cambios en volumen impactan utilidad.

### Scoring Dinámico
Algoritmo que evalúa múltiples indicadores y asigna una calificación numérica:
- Verde (70+): Saludable, mantener.
- Ámbar (45-69): Moderado, mejorable.
- Rojo (<45): Crítico, acción urgente.

---

## 🛠️ Desarrollo

### Estructura de Archivos
```
financial_assistant/
├── index.html          # Todo en uno: HTML + CSS + JS
└── README.md           # Este archivo
```

### Cómo Contribuir
1. Clona o descarga.
2. Abre `index.html` en editor (VS Code, etc.).
3. Modifica CSS en `<style>`, JavaScript en `<script>`.
4. Prueba en navegador (F12 para dev tools).

### Librerías Externas
- **Chart.js 4.4.1** (CDN): Gráficos.
- **Google Fonts** (CDN): Tipografía.

### Variables CSS Disponibles
```css
/* Colores dinámicos según tema */
--bg, --bg2, --bg3, --bg4
--text, --text2, --text3
--border, --border2, --border3
--gold, --green, --red, --amber, --blue, --purple, --teal

/* Tipografía */
--fs   (Playfair Display)
--fm   (IBM Plex Mono)
--fb   (Epilogue)

/* Espaciado */
--r    (14px, border-radius estándar)
--rs   (8px, border-radius small)
```

---

## 📞 Soporte

Este proyecto es de demostración/educativo.

Para issues:
1. Verifica console del navegador (F12 → Console).
2. Recarga la página.
3. Prueba en navegador diferente.

---

## 📄 Licencia

Proyecto de código abierto. Úsalo, modifícalo y distribúyelo libremente.

---

## 🏆 Créditos

**Concepto**: Asesor financiero personalizado con análisis en tiempo real.
**Diseño**: Sistema de diseño moderno, accesible, responsive.
**Tecnología**: HTML5 + CSS3 + Vanilla JS + Chart.js.
**Años**: 2024-2026.

---

**¡Que disfrutes organizando tus finanzas! 💰✨**
