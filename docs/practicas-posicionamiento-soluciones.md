---
icon: lucide/check-check
title: "Soluciones — Prácticas de Posicionamiento en Tailwind CSS 4.0"
description: "Código fuente resuelto al 100% con clases de Tailwind CSS 4.0 para las prácticas de posicionamiento: capas, badges, tooltips, sticky headers, fixed banners, FABs y flexbox con status dot."
modulo: "LMH (0373) / DIW (0615) / DI (0488)"
unidad: 4
---

# Soluciones · Prácticas de Posicionamiento en Tailwind CSS 4.0

<div class="badges">
  <span class="badge badge-v4">Tailwind CSS 4.0</span>
  <span class="badge badge-theme">Solucionario Técnico</span>
  <span class="badge badge-oxide">Uso Docente / Referencia</span>
  <span class="badge badge-ra">RA 2 / RA 3</span>
</div>

> [!IMPORTANT] Archivo de Solución Oficial
> Este documento contiene las soluciones de referencia completas y funcionales maquetadas con **Tailwind CSS 4.0**. Está concebido como material de consulta docente y guía de corrección. Si eres alumno, intenta resolver primero los ejercicios en [**`practicas-posicionamiento.md`**](practicas-posicionamiento.md).

---

## 🎯 Solución Práctica 1: Tarjeta Comercial con Capas, Badges y Tooltip Flotante

### Código Resuelto en Tailwind CSS 4.0

```html title="solucion-01-tarjeta-posicionamiento.html"
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Solución Práctica 1 — Tarjeta Comercial en Tailwind 4</title>
  <link rel="stylesheet" href="/src/style.css">
</head>
<body class="bg-slate-100 min-h-screen flex items-center justify-center p-4 font-sans text-slate-800">

  <!-- CONTENEDOR PRINCIPAL: Sin overflow-hidden para no recortar el tooltip emergente -->
  <article class="w-full max-w-xs mx-auto bg-white rounded-2xl border border-slate-200 shadow-md">
    
    <!-- ZONA MULTIMEDIA: Bloque contenedor de coordenadas cartesianas (relative) -->
    <div class="relative aspect-square w-full rounded-t-2xl bg-gradient-to-br from-slate-100 to-slate-200 flex items-center justify-center">
      
      <!-- 1. Insignia de descuento absoluta en la esquina superior izquierda -->
      <span class="absolute top-3 left-3 z-10 px-2.5 py-1 text-xs font-black uppercase tracking-wider text-white bg-rose-600 rounded-full shadow-md shadow-rose-600/30">
        -25% HOY
      </span>

      <!-- 2. Botón flotante absoluto en la esquina superior derecha con tooltip reactivo -->
      <div class="group relative absolute top-3 right-3 z-10">
        <button
          type="button"
          class="size-9 rounded-full bg-white/90 backdrop-blur-sm border border-slate-200/80 shadow flex items-center justify-center text-slate-400 hover:text-rose-500 hover:scale-110 active:scale-95 transition-all"
          aria-label="Guardar en favoritos"
        >
          <svg class="size-5" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
          </svg>
        </button>

        <!-- Tooltip flotante centrado: aparece al posar el cursor sobre el grupo -->
        <span
          role="tooltip"
          class="pointer-events-none absolute bottom-full left-1/2 -translate-x-1/2 mb-2 px-2.5 py-1 text-[11px] font-semibold text-white bg-slate-900 rounded-md whitespace-nowrap opacity-0 group-hover:opacity-100 transition-opacity duration-150 shadow-lg"
        >
          Añadir a mi lista
          <!-- Pequeño puntero triangular inferior del tooltip -->
          <span class="absolute top-full left-1/2 -translate-x-1/2 border-4 border-transparent border-t-slate-900"></span>
        </span>
      </div>

      <!-- Icono central representativo del producto -->
      <div class="text-7xl select-none transform transition-transform hover:scale-105 duration-200">
        🎧
      </div>
    </div>

    <!-- CUERPO DE LA TARJETA (FLUJO NORMAL) -->
    <div class="p-5">
      <span class="text-xs font-bold text-slate-400 uppercase tracking-wider">
        AudioPro Elite
      </span>
      <h2 class="text-base font-bold text-slate-900 mt-1 leading-snug">
        Auriculares Studio Wireless Pro ANC
      </h2>
      
      <!-- Valoración con estrellas -->
      <div class="flex items-center gap-1.5 mt-2">
        <span class="text-amber-400 text-sm">★★★★★</span>
        <span class="text-xs font-medium text-slate-500">(142 valoraciones)</span>
      </div>

      <!-- Bloque de precios -->
      <div class="flex items-baseline gap-2 mt-4">
        <span class="text-xl font-black text-slate-900">149,99€</span>
        <span class="text-xs font-medium text-slate-400 line-through">199,99€</span>
      </div>

      <!-- Botón de compra interactivo -->
      <button
        type="button"
        class="w-full mt-4 py-2.5 px-4 bg-blue-600 hover:bg-blue-700 active:scale-[0.98] text-white text-sm font-semibold rounded-xl shadow-sm transition-all focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-600"
      >
        Añadir a la Cesta
      </button>
    </div>

  </article>

</body>
</html>
```

### Disección Técnica Paso a Paso

1. **`relative` en `.product-media`:** Establece el marco de referencia espacial. Sin esta clase, los elementos hijos con `absolute` buscarían el siguiente ancestro posicionado o el `<html>`, dispersándose por la pantalla.
2. **`group` + `group-hover:opacity-100`:** Permite que el hover sobre el botón despierte la visibilidad del tooltip sin necesidad de JavaScript ni hacks de selectores adyacentes.
3. **Centrado del Tooltip con `left-1/2 -translate-x-1/2`:** Aplica la fórmula matemática universal de centrado absoluto: desplaza el ancla al 50% horizontal del padre y retrocede el 50% de la propia anchura del tooltip mediante traslación negativa.
4. **Por qué NO usar `overflow-hidden` exterior:** Si añades `overflow-hidden` a la tarjeta principal, el tooltip que se proyecta por encima de la tarjeta con `bottom-full` quedará recortado físicamente por el navegador.

---

## 📌 Solución Práctica 2: Barra Superior Adhesiva y Banner Fijo de Consentimiento (Sticky vs Fixed)

### Código Resuelto en Tailwind CSS 4.0

```html title="solucion-02-sticky-fixed.html"
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Solución Práctica 2 — Sticky vs Fixed en Tailwind 4</title>
  <link rel="stylesheet" href="/src/style.css">
</head>
<body class="bg-slate-50 min-h-screen font-sans text-slate-800">

  <!-- 1. CABECERA ADHESIVA (POSITION: STICKY) -->
  <header class="sticky top-0 z-30 w-full bg-slate-900/95 backdrop-blur-md border-b border-slate-800 shadow-lg">
    <div class="max-w-4xl mx-auto px-4 py-3 flex items-center justify-between gap-4">
      
      <!-- Logotipo de la academia -->
      <a href="#" class="flex items-center gap-2 font-bold text-sky-400 hover:text-sky-300 transition-colors">
        <span class="text-xl">⚡</span>
        <span class="text-base tracking-tight text-white font-extrabold">DominIA Academy</span>
      </a>

      <!-- Navegación principal -->
      <nav class="hidden sm:flex items-center gap-6 text-sm font-medium text-slate-300" aria-label="Navegación principal">
        <a href="#" class="text-sky-400 font-semibold">Inicio</a>
        <a href="#" class="hover:text-white transition-colors">Artículos</a>
        <a href="#" class="hover:text-white transition-colors">Lecciones</a>
        <a href="#" class="hover:text-white transition-colors">Recursos</a>
      </nav>

      <!-- Zona de acciones con campana e insignia numérica absoluta -->
      <div class="flex items-center">
        <button
          type="button"
          class="relative p-2 text-slate-300 hover:text-white rounded-lg hover:bg-slate-800 transition-colors"
          aria-label="3 notificaciones pendientes"
        >
          <svg class="size-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
          </svg>
          <!-- Insignia absoluta superpuesta con ring protector -->
          <span class="absolute top-1 right-1 size-4 rounded-full bg-rose-600 text-white text-[10px] font-bold flex items-center justify-center ring-2 ring-slate-900">
            3
          </span>
        </button>
      </div>

    </div>
  </header>

  <!-- 2. CONTENIDO PRINCIPAL: pb-32 garantiza holgura contra la barra fija de cookies -->
  <main class="max-w-4xl mx-auto px-4 py-8 pb-32">
    
    <header class="mb-8">
      <h1 class="text-3xl font-extrabold text-slate-900 tracking-tight">
        Guía Maestra: Sticky vs Fixed en Tailwind CSS
      </h1>
      <p class="mt-2 text-base text-slate-600">
        Aprende la diferencia operativa entre elementos anclados al flujo y fijados a la ventana gráfica.
      </p>
    </header>

    <!-- Cuadrícula de tarjetas comparativas -->
    <section class="grid grid-cols-1 md:grid-cols-2 gap-6 my-8">
      
      <!-- Tarjeta 1: Sticky -->
      <article class="bg-white rounded-2xl p-6 border border-slate-200 border-t-4 border-t-blue-600 shadow-sm flex flex-col justify-between">
        <div>
          <h2 class="text-lg font-bold text-blue-600 mb-2">1. Comportamiento Sticky</h2>
          <p class="text-sm text-slate-600 leading-relaxed mb-4">
            El elemento fluye con el scroll natural hasta alcanzar el umbral <code>top-0</code>, donde se congela. Requiere que su contenedor ancestro mantenga altura visible en pantalla.
          </p>
        </div>
        <div>
          <span class="inline-block px-2.5 py-1 text-xs font-mono font-bold text-blue-700 bg-blue-50 rounded-md border border-blue-100">
            sticky top-0 z-30
          </span>
        </div>
      </article>

      <!-- Tarjeta 2: Fixed -->
      <article class="bg-white rounded-2xl p-6 border border-slate-200 border-t-4 border-t-amber-600 shadow-sm flex flex-col justify-between">
        <div>
          <h2 class="text-lg font-bold text-amber-600 mb-2">2. Comportamiento Fixed</h2>
          <p class="text-sm text-slate-600 leading-relaxed mb-4">
            Se extrae por completo del flujo del documento y se ancla respecto a la ventana física de la pantalla. No se desplaza jamás con el scroll, ignorando a los padres.
          </p>
        </div>
        <div>
          <span class="inline-block px-2.5 py-1 text-xs font-mono font-bold text-amber-700 bg-amber-50 rounded-md border border-amber-100">
            fixed bottom-0 inset-x-0
          </span>
        </div>
      </article>

    </section>

    <!-- Bloques de lectura para garantizar recorrido de scroll holgado -->
    <section class="space-y-6">
      <div class="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm">
        <h3 class="text-base font-bold text-slate-900 mb-2">3. Profundizando en el Mecanismo de Sticky</h3>
        <p class="text-sm text-slate-600 leading-relaxed">
          A diferencia de <code>fixed</code>, un elemento <code>sticky</code> respeta su hueco inicial en el documento y no requiere trucos de compensación superior en el <code>body</code>. Al alcanzar la coordenada indicada, pasa a comportarse como fijo hasta que su contenedor padre finaliza.
        </p>
      </div>

      <div class="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm">
        <h3 class="text-base font-bold text-slate-900 mb-2">4. El Funcionamiento Inmutable de Fixed</h3>
        <p class="text-sm text-slate-600 leading-relaxed">
          Los elementos <code>fixed</code> se posicionan siempre respecto al <em>Viewport</em> (la ventana del navegador). Por este motivo son la solución indicada para barras fijas de consentimiento, ventanas modales emergentes y botones flotantes de acción.
        </p>
      </div>

      <div class="bg-white rounded-2xl p-6 border border-slate-200 shadow-sm">
        <h3 class="text-base font-bold text-slate-900 mb-2">5. La Jerarquía de Capas con z-index</h3>
        <p class="text-sm text-slate-600 leading-relaxed">
          La cabecera adhesiva (<code>z-30</code>) y los elementos fijos inferiores (<code>z-40</code> y <code>z-50</code>) declaran niveles de apilamiento escalonados para evitar que elementos ordinarios los tapen durante la navegación.
        </p>
      </div>
    </section>

  </main>

  <!-- 3. BOTÓN FLOTANTE VOLVER ARRIBA (POSITION: FIXED CON CENTRADO VECTORIAL) -->
  <a
    href="#"
    class="fixed bottom-24 right-6 z-40 size-12 rounded-full bg-blue-600 hover:bg-blue-500 active:scale-95 text-white shadow-xl shadow-blue-600/30 flex items-center justify-center transition-all hover:-translate-y-1"
    title="Volver al principio"
    aria-label="Volver al principio"
  >
    <svg class="size-5" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
      <path d="M12 19V5M5 12l7-7 7 7"/>
    </svg>
  </a>

  <!-- 4. BANNER FIJO INFERIOR DE COOKIES (POSITION: FIXED A ANCHO COMPLETO) -->
  <aside
    class="fixed bottom-0 inset-x-0 z-50 w-full bg-slate-900/95 backdrop-blur-md border-t border-slate-800 text-white shadow-2xl"
    role="region"
    aria-label="Aviso de privacidad"
  >
    <div class="max-w-4xl mx-auto px-4 py-3.5 flex flex-col sm:flex-row items-center justify-between gap-4">
      <p class="text-xs sm:text-sm text-slate-300 leading-relaxed text-center sm:text-left">
        🍪 Utilizamos cookies técnicas para garantizar el funcionamiento del aula.
      </p>
      <div class="flex-shrink-0 w-full sm:w-auto">
        <button
          type="button"
          class="w-full sm:w-auto px-5 py-2 text-xs font-bold text-white bg-emerald-600 hover:bg-emerald-500 rounded-lg shadow-sm transition-colors whitespace-nowrap active:scale-95"
        >
          Aceptar todas
        </button>
      </div>
    </div>
  </aside>

</body>
</html>
```

### Disección Técnica Paso a Paso

1. **`sticky top-0 z-30` en el Header:** La barra no extrae el elemento del flujo inicial, de modo que el título principal empieza exactamente después del header sin requerir `pt-*` artificial en el `body`.
2. **`fixed bottom-0 inset-x-0 z-50` en el Banner:** La combinación `inset-x-0` (`left: 0; right: 0`) junto con `bottom-0` y `w-full` garantiza que el banner abarque el 100% exacto de la pantalla, evitando el colapso a anchuras mínimas.
3. **`pb-32` en el contenedor del artículo:** Respaldo vital de diseño. Como el banner es `fixed`, flotará por encima del contenido; el margen inferior reservado asegura que el usuario pueda scrollear hasta ver el último párrafo completo.
4. **Centrado geométrico del FAB con SVG:** En lugar de caracteres de texto como `'↑'` (cuyas fuentes de sistema sufren desviaciones de métricas verticales), el icono SVG con `flex items-center justify-center` en una caja `size-12 rounded-full` ofrece simetría matemática perfecta.

---

## 🧭 Solución Práctica 3: Ficha de Perfil Profesional y Barra de Herramientas (Flexbox + Posicionamiento)

### Código Resuelto en Tailwind CSS 4.0

```html title="solucion-03-flexbox-perfil.html"
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Solución Práctica 3 — Ficha de Perfil en Tailwind 4</title>
  <link rel="stylesheet" href="/src/style.css">
</head>
<body class="bg-slate-100 min-h-screen p-4 sm:p-6 flex items-center justify-center font-sans text-slate-800">

  <main class="w-full max-w-xl mx-auto space-y-6">

    <!-- 1. BARRA SUPERIOR: Flexbox con efecto Push automático mediante ms-auto -->
    <header class="flex items-center gap-3 bg-white p-4 rounded-2xl border border-slate-200 shadow-sm">
      <span class="text-xl">⚙️</span>
      <h3 class="text-sm font-bold text-slate-900 tracking-tight">Panel de Desarrollador</h3>
      
      <!-- Este botón absorbe todo el espacio sobrante hacia la izquierda mediante ms-auto -->
      <button
        type="button"
        class="ms-auto px-3.5 py-1.5 text-xs font-semibold text-rose-600 hover:text-white bg-rose-50 hover:bg-rose-600 rounded-lg transition-colors border border-rose-200/60"
      >
        Cerrar Sesión
      </button>
    </header>

    <!-- 2. TARJETA DE PERFIL (FLEXBOX + BADGE ABSOLUTA) -->
    <article class="bg-white p-6 rounded-2xl border border-slate-200 shadow-md">
      
      <div class="flex items-start gap-4">
        <!-- AVATAR CIRCULAR: shrink-0 previene deformación + relative para anclar status-dot -->
        <div class="relative size-14 shrink-0">
          <img
            class="size-14 rounded-full object-cover border-2 border-slate-200 shadow-sm"
            src="https://images.unsplash.com/photo-1573496359142-b8d87734a5a2?w=160&h=160&fit=crop&crop=face"
            alt="Foto de perfil de Alejandra"
          >
          <!-- Indicador de conexión verde absoluto con halo blanco (ring-2) -->
          <span
            class="absolute bottom-0 right-0 size-3.5 rounded-full bg-emerald-500 ring-2 ring-white"
            title="Usuario en línea"
          ></span>
        </div>

        <!-- BLOQUE DE INFORMACIÓN: min-w-0 permite que truncate funcione en Flexbox -->
        <div class="min-w-0 flex-1">
          <h2 class="text-base sm:text-lg font-bold text-slate-900 truncate" title="Alejandra Gómez de la Torre de la Vega y Montesdeoca">
            Alejandra Gómez de la Torre de la Vega y Montesdeoca
          </h2>
          <p class="text-xs font-medium text-sky-600 truncate mt-0.5">
            Ingeniera Cloud Architect & Principal SRE
          </p>
          <p class="text-xs text-slate-500 mt-1">
            📍 Madrid, España · Remoto
          </p>
        </div>
      </div>

      <!-- Resumen biográfico con text-pretty para evitar huérfanas -->
      <p class="mt-4 text-xs sm:text-sm text-slate-600 leading-relaxed text-pretty">
        Especialista en escalabilidad horizontal de clústeres Kubernetes, diseño de infraestructuras multirregión resilientes y arquitectura de microservicios de alto tráfico.
      </p>

      <!-- 3. COMPETENCIAS TÉCNICAS CON FLEX-WRAP -->
      <div class="mt-5">
        <h4 class="text-xs font-bold text-slate-400 uppercase tracking-wider mb-2.5">
          Competencias Clave
        </h4>
        <div class="flex flex-wrap gap-2">
          <span class="px-2.5 py-1 bg-slate-100 text-slate-700 text-xs font-medium rounded-md hover:bg-slate-200 transition-colors">Kubernetes</span>
          <span class="px-2.5 py-1 bg-slate-100 text-slate-700 text-xs font-medium rounded-md hover:bg-slate-200 transition-colors">Terraform</span>
          <span class="px-2.5 py-1 bg-slate-100 text-slate-700 text-xs font-medium rounded-md hover:bg-slate-200 transition-colors">AWS EKS</span>
          <span class="px-2.5 py-1 bg-sky-50 text-sky-700 border border-sky-200 text-xs font-semibold rounded-md">Tailwind CSS 4.0</span>
          <span class="px-2.5 py-1 bg-slate-100 text-slate-700 text-xs font-medium rounded-md hover:bg-slate-200 transition-colors">Go</span>
          <span class="px-2.5 py-1 bg-slate-100 text-slate-700 text-xs font-medium rounded-md hover:bg-slate-200 transition-colors">OpenTelemetry</span>
          <span class="px-2.5 py-1 bg-slate-100 text-slate-700 text-xs font-medium rounded-md hover:bg-slate-200 transition-colors">CI/CD Pipelines</span>
        </div>
      </div>

      <!-- Botones de acción inferiores -->
      <div class="mt-6 pt-5 border-t border-slate-100 flex flex-col sm:flex-row gap-3">
        <button
          type="button"
          class="flex-1 py-2 px-4 bg-slate-900 hover:bg-slate-800 text-white text-xs font-semibold rounded-xl shadow-sm transition-colors text-center"
        >
          Ver Proyectos Activos
        </button>
        <button
          type="button"
          class="flex-1 py-2 px-4 bg-slate-100 hover:bg-slate-200 text-slate-700 text-xs font-semibold rounded-xl transition-colors text-center"
        >
          Enviar Mensaje
        </button>
      </div>

    </article>

  </main>

</body>
</html>
```

### Disección Técnica Paso a Paso

1. **`ms-auto` en `.btn-logout`:** Aplica `margin-inline-start: auto`. En un contenedor flex horizontal, un margen automático absorbe todo el espacio positivo disponible en ese eje, empujando limpiamente el elemento hacia el extremo contrario sin requerir espaciadores vacíos (`<div class="grow"></div>`).
2. **`shrink-0` en el contenedor del avatar:** Evita que el algoritmo de flexión comprima el avatar si el texto adyacente es muy largo.
3. **`min-w-0` en el bloque de texto:** Los elementos flex tienen por defecto `min-width: auto`. Sin `min-w-0`, el navegador se niega a contraer la caja de texto, rompiendo el comportamiento de `truncate` y provocando desbordamiento horizontal.
4. **`ring-2 ring-white` en `.status-dot`:** El halo blanco perimetral separa el punto verde del borde de la foto del avatar, garantizando contraste y legibilidad con cualquier fondo de imagen.
