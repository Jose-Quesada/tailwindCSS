---
icon: lucide/sparkles
---

# 05. Tipografía, Colores OKLCH, Gradientes y Efectos Visuales

El refinamiento visual distingue una interfaz amateur de un producto digital profesional. Tailwind CSS 4.0 incorpora herramientas de vanguardia para tipografía editorial equilibrada, gradientes multidimensionales y efectos de desenfoque (*Glassmorphism*).

---

## ✍️ 1. Tipografía Moderna y Control Editorial

Tailwind ofrece una escala tipográfica completa basada en unidades relativas (`rem`):

```text
text-xs: 0.75rem (12px)  |  text-sm: 0.875rem (14px)  |  text-base: 1rem (16px)
text-lg: 1.125rem (18px) |  text-xl: 1.25rem (20px)   |  text-2xl: 1.5rem (24px)
text-3xl: 1.875rem (30px)|  text-4xl: 2.25rem (36px)  |  text-6xl: 3.75rem (60px)
```

### Novedades Cruciales en v4: `text-balance` y `text-pretty`

Uno de los problemas clásicos en maquetación web son los títulos con una sola palabra huérfana en la última línea:

```html
<!-- SIN text-balance: La última palabra puede quedar sola abajo -->
<h1 class="text-3xl font-extrabold text-slate-900">
  Aprende Desarrollo de Interfaces con Tailwind 4
</h1>

<!-- CON text-balance: El navegador reparte las palabras de forma armónica -->
<h1 class="text-3xl font-extrabold text-slate-900 text-balance">
  Aprende Desarrollo de Interfaces con Tailwind 4
</h1>

<!-- CON text-pretty: Optimiza el flujo de lectura en párrafos largos evitando viudas -->
<p class="text-slate-600 text-sm leading-relaxed text-pretty mt-3">
  El nuevo motor Oxide compila a velocidad nativa sin requerir un pipeline complejo de PostCSS.
</p>
```

### Truncado de Texto y Pinzamiento de Líneas (`line-clamp`)

Cuando se muestran resúmenes de noticias o productos, es vital evitar que textos excesivamente largos desborden la tarjeta:

```html
<!-- Corta el texto exactamente en la línea 2 y añade puntos suspensivos (...) -->
<p class="text-slate-600 text-sm line-clamp-2">
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam.
</p>
```

---

## 🎨 2. Paletas de Color, Modificadores de Opacidad y Gradientes

### Modificador de Opacidad con Barra Inclinada (`/`)

En lugar de definir clases separadas para cada nivel de transparencia, en Tailwind cualquier color admite una barra inclinada con el porcentaje deseado:

```html
<!-- Fondo Sky 500 al 20% de opacidad -->
<div class="bg-sky-500/20 border border-sky-500/40 text-sky-900 p-4 rounded-lg">
  Alerta informativa con fondo translúcido y borde nítido.
</div>
```

### Gradientes de Texto con `bg-clip-text`

Uno de los patrones visuales más populares en landings SaaS es el texto con gradiente metálico o multicolor:

```html
<h2 class="text-4xl sm:text-6xl font-black tracking-tight text-center">
  Diseñado para la velocidad
  <span class="block bg-gradient-to-r from-sky-400 via-teal-300 to-emerald-400 bg-clip-text text-transparent">
    Motor Oxide en Rust
  </span>
</h2>
```

---

## 💎 3. Sombras, Anillos y Efecto Glassmorphism

El efecto de cristal esmerilado (*Glassmorphism*) se consigue combinando un fondo translúcido (`bg-*/70`) con desenfoque de fondo (`backdrop-blur-*`) y un borde sutil:

```html
<div class="relative min-h-[300px] flex items-center justify-center bg-gradient-to-tr from-slate-900 via-indigo-950 to-slate-900 p-8 rounded-2xl overflow-hidden">
  <!-- Círculos luminosos decorativos de fondo -->
  <div class="absolute -top-10 -left-10 w-48 h-48 bg-sky-500/30 rounded-full blur-3xl"></div>
  <div class="absolute -bottom-10 -right-10 w-48 h-48 bg-purple-500/30 rounded-full blur-3xl"></div>

  <!-- Tarjeta con Glassmorphism -->
  <div class="relative z-10 p-6 max-w-sm w-full bg-white/10 backdrop-blur-xl border border-white/20 rounded-2xl shadow-2xl text-white">
    <div class="flex items-center gap-3">
      <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-sky-400 to-indigo-600 flex items-center justify-center font-bold">
        ⚡
      </div>
      <div>
        <h4 class="font-bold text-base">Rendimiento Extremo</h4>
        <p class="text-xs text-slate-300">Compilación < 10ms</p>
      </div>
    </div>
    <p class="mt-4 text-xs text-slate-200 leading-relaxed text-pretty">
      El reemplazo de Node.js por Rust garantiza tiempos de respuesta instantáneos en la recarga de módulos de Vite.
    </p>
    <button class="mt-5 w-full py-2.5 px-4 bg-white/20 hover:bg-white/30 active:scale-[0.98] border border-white/30 text-white font-semibold text-xs rounded-xl transition-all shadow-sm">
      Explorar benchmarks
    </button>
  </div>
</div>
```

---

## 🕶️ 4. Transformaciones 3D Nativas en Tailwind 4

Tailwind 4 incorpora soporte nativo para perspectiva y rotación tridimensional:

```html
<div class="perspective-1000 flex justify-center py-10">
  <div class="w-64 h-40 bg-gradient-to-br from-indigo-500 to-sky-600 rounded-2xl shadow-xl p-6 text-white transform rotate-x-12 -rotate-y-12 hover:rotate-0 transition-transform duration-500">
    <p class="text-xs uppercase tracking-widest text-indigo-200">Tarjeta 3D</p>
    <p class="text-xl font-bold mt-2">Interactiva</p>
    <p class="text-xs text-indigo-100 mt-4">Pasa el ratón para nivelar</p>
  </div>
</div>
```
