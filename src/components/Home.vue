<template>
  <div class="portafolio">
    <!-- Barra de navegación -->
    <nav class="navegacion">
      <div class="contenedor nav-contenido">
        <ul class="nav-lista">
          <li><a href="#sobre-mi">Sobre mí</a></li>
          <li><a href="#proyectos">Proyectos</a></li>
          <li><a href="#habilidades">Habilidades</a></li>
        </ul>
      </div>
    </nav>

    <!-- Encabezado -->
    <header class="portada">
      <div class="contenedor">
        <h1 class="portada-titulo">Andrés David Salgado Cala</h1>
        <p class="portada-subtitulo">Desarrollador Junior</p>
      </div>
    </header>

    <!-- Sobre mí -->
    <section class="sobre-mi" id="sobre-mi" v-reveal>
      <div class="contenedor">
        <h2 class="seccion-titulo">Sobre Mí</h2>
        <div class="sobre-contenido">
          <p class="sobre-texto">
            Soy un desarrollador junior, egresado del programa de Tecnología en
            Análisis y Desarrollo de Software. Me apasiona la programación y disfruto
            aprender cosas nuevas que me ayuden a crecer tanto personal como
            profesionalmente.
          </p>
          <p class="sobre-texto">
            Me considero una persona responsable, curiosa y con gran disposición para
            asumir nuevos retos. Busco oportunidades que me permitan seguir aprendiendo,
            aportar ideas frescas y formar parte de proyectos donde el trabajo en equipo
            y la innovación sean pilares fundamentales.
          </p>
        </div>
      </div>
    </section>

    <!-- Proyectos -->
    <section class="proyectos" id="proyectos" v-reveal>
      <div class="contenedor">
        <h2 class="seccion-titulo">Proyectos Realizados</h2>
        <p style="text-align: center;">Los siguientes proyectos los realicé durante mi etapa productiva en el SENA:</p>
        <div class="proyectos-grid">
          <article class="proyecto-tarjeta" v-for="proyecto in proyectos" :key="proyecto.id">
            <div class="proyecto-contenido">
              <h3 class="proyecto-titulo">{{ proyecto.titulo }}</h3>
              <p class="proyecto-descripcion">{{ proyecto.descripcion }}</p>
              <div class="proyecto-tecnologias">
                <span class="etiqueta-tecnologia" v-for="tecnologia in proyecto.tecnologias" :key="tecnologia">
                  {{ tecnologia }}
                </span>
              </div>
              <a v-if="proyecto.enlace" :href="proyecto.enlace" class="proyecto-enlace" target="_blank" rel="noopener">
                Ver Proyecto →
              </a>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- Habilidades -->
    <section class="habilidades" id="habilidades" v-reveal>
      <div class="contenedor">
        <h2 class="seccion-titulo">Lenguajes de Programación</h2>
        <div class="habilidades-grid">
          <div class="habilidad-item" v-for="habilidad in habilidades" :key="habilidad.nombre">
            <div class="habilidad-icono">{{ habilidad.icono }}</div>
            <h3 class="habilidad-nombre">{{ habilidad.nombre }}</h3>
            <div class="habilidad-nivel">
              <div class="barra-nivel">
                <div class="progreso-nivel" :style="{ width: habilidad.nivel + '%' }"></div>
              </div>
              <span class="porcentaje-nivel">{{ habilidad.nivel }}%</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Pie de página -->
    <footer class="pie" id="pie">
      <div class="contenedor">
        <p>&copy; 2025 Andrés David Salgado Cala. Todos los derechos reservados.</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Datos de proyectos
const proyectos = ref([
  {
    id: 1,
    titulo: 'Esfera AudioVisual',
    descripcion: 'Plataforma de comercio electrónico completa con carrito de compras, sistema de pagos y panel de administración.',
    tecnologias: ['Vue.js', 'Node.js', 'MongoDB', 'Stripe'],
    enlace: 'https://github.com/usuario/ecommerce'
  },
  {
    id: 2,
    titulo: 'Restaurante JuanMar',
    descripcion: 'Aplicación de gestión de tareas con funcionalidades de colaboración en tiempo real y notificaciones.',
    tecnologias: ['React', 'Firebase', 'Material-UI'],
    enlace: 'https://github.com/usuario/task-app'
  },
  {
    id: 3,
    titulo: 'Vivirelax',
    descripcion: 'Panel meteorológico interactivo con gráficos dinámicos y pronósticos de múltiples ciudades.',
    tecnologias: ['JavaScript', 'Chart.js', 'OpenWeather API'],
    enlace: 'https://github.com/usuario/weather-dashboard'
  },
  {
    id: 4,
    titulo: 'Blog Personal',
    descripcion: 'Blog personal con sistema de comentarios, categorías y optimización SEO.',
    tecnologias: ['Next.js', 'Markdown', 'Vercel'],
    enlace: null
  }
])

// Datos de habilidades
const habilidades = ref([
  { nombre: 'JavaScript', icono: 'JS', nivel: 90 },
  /*  { nombre: 'Vue.js', icono: 'Vue', nivel: 88 }, */
  /*   { nombre: 'Node.js', icono: 'Node', nivel: 80 }, */
  { nombre: 'Python', icono: 'Py', nivel: 75 },
  { nombre: 'SQL', icono: 'SQL', nivel: 85 }
])

// Directiva personalizada para animaciones
const vReveal = {
  mounted(el) {
    el.classList.add('reveal')
    const observer = new IntersectionObserver(
      entries => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            entry.target.classList.add('reveal-visible')
            observer.unobserve(entry.target)
          }
        })
      },
      { threshold: 0.2 }
    )
    observer.observe(el)
  }
}
</script>


<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
  /* Scroll suave */
}



.portafolio {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  line-height: 1.6;
  color: #2d3748;
  background-color: #ffffff;
}

/* Navegación */
.navegacion {
  position: fixed;
  top: 0;
  width: 100%;
  background: #1a202c;
  color: white;
  padding: 1rem 0;
  z-index: 1000;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.nav-contenido {
  display: flex;
  justify-content: center;

}

.nav-logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: white;
}

.nav-lista {
  display: flex;
  list-style: none;
  gap: 2rem;
}

.nav-lista a {
  color: white;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav-lista a:hover {
  color: #667eea;
}

/* Ajustar el padding del header para compensar el nav fijo */
.portada {
  background: linear-gradient(135deg, #667eea 0%, #414141 100%);
  color: white;
  padding: 8rem 0 6rem;
  /* más espacio arriba */
  text-align: center;
  /* compensar altura nav */
}

.portada-titulo {
  font-size: 3.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  letter-spacing: -0.02em;
}

.portada-subtitulo {
  font-size: 1.5rem;
  font-weight: 300;
  opacity: 0.9;
}

/* Secciones */
section {
  padding: 5rem 0;
}

.seccion-titulo {
  font-size: 2.5rem;
  font-weight: 600;
  text-align: center;
  margin-bottom: 3rem;
  color: #1a202c;
  position: relative;
}

.seccion-titulo::after {
  content: '';
  position: absolute;
  bottom: -0.5rem;
  left: 50%;
  transform: translateX(-50%);
  width: 4rem;
  height: 3px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 2px;
}

/* Sobre mí */
.sobre-mi {
  background-color: #f7fafc;
}

.sobre-contenido {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

.sobre-texto {
  font-size: 1.125rem;
  margin-bottom: 1.5rem;
  color: #4a5568;
  line-height: 1.8;
}

/* Proyectos */
.proyectos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.proyecto-tarjeta {
  background: white;
  border-radius: 12px;
  padding: 2rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  transition: all 0.3s ease;
  border: 1px solid #e2e8f0;
}

.proyecto-tarjeta:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

.proyecto-titulo {
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #1a202c;
}

.proyecto-descripcion {
  color: #4a5568;
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.proyecto-tecnologias {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.etiqueta-tecnologia {
  background: #edf2f7;
  color: #4a5568;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.875rem;
  font-weight: 500;
}

.proyecto-enlace {
  display: inline-flex;
  align-items: center;
  color: #667eea;
  text-decoration: none;
  font-weight: 600;
  transition: color 0.3s ease;
}

.proyecto-enlace:hover {
  color: #764ba2;
}

/* Habilidades */
.habilidades {
  background-color: #f7fafc;
}

.habilidades-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

.habilidad-item {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.habilidad-item:hover {
  transform: translateY(-2px);
}

.habilidad-icono {
  width: 4rem;
  height: 4rem;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 1.125rem;
  margin: 0 auto 1rem;
}

.habilidad-nombre {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: #1a202c;
}

.habilidad-nivel {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.barra-nivel {
  flex: 1;
  height: 8px;
  background: #e2e8f0;
  border-radius: 4px;
  overflow: hidden;
}

.progreso-nivel {
  height: 100%;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 4px;
  transition: width 0.3s ease;
}

.porcentaje-nivel {
  font-weight: 600;
  color: #4a5568;
  font-size: 0.875rem;
  min-width: 3rem;
}

/* Pie de página */
.pie {
  background: #1a202c;
  color: white;
  padding: 2rem 0;
  text-align: center;
}

/* Responsive */
@media (max-width: 768px) {
  .portada-titulo {
    font-size: 2.5rem;
  }

  .portada-subtitulo {
    font-size: 1.25rem;
  }

  .seccion-titulo {
    font-size: 2rem;
  }

  section {
    padding: 3rem 0;
  }

  .portada {
    padding: 4rem 0;
  }

  .proyectos-grid {
    grid-template-columns: 1fr;
  }

  .habilidades-grid {
    grid-template-columns: 1fr;
  }

  .habilidad-nivel {
    flex-direction: column;
    gap: 0.5rem;
  }

  .barra-nivel {
    width: 100%;
  }
}

@media (max-width: 480px) {
  .contenedor {
    padding: 0 1rem;
  }

  .portada-titulo {
    font-size: 2rem;
  }

  .proyecto-tarjeta,
  .habilidad-item {
    padding: 1.5rem;
  }
}

/* Animaciones */

.reveal {
  opacity: 0;
  transform: translateY(50px);
  transition: all 0.8s ease;
}

.reveal-visible {
  opacity: 1;
  transform: translateY(0);
}

/* Animaciones específicas */
.proyecto-tarjeta.reveal {
  transform: scale(0.95);
}

.proyecto-tarjeta.reveal-visible {
  transform: scale(1);
}

.habilidad-item.reveal {
  transform: translateY(30px) rotate(-2deg);
}

.habilidad-item.reveal-visible {
  transform: translateY(0) rotate(0);
}
</style>
