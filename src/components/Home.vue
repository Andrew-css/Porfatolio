<script setup>
import { ref } from 'vue';
import fotoPerfil from '../assets/fotoperfil.jpg';

// Importa tus imágenes de proyectos aquí
import img1 from '../assets/esferaaudiovisual.png';
import img2 from '../assets/juanmar.png';
import img3 from '../assets/vivirelax.png';
import img4 from '../assets/hotelesbarichara.png';

// Datos de proyectos
const proyectos = ref([
  {
    id: 1,
    titulo: 'Esfera AudioVisual',
    descripcion: 'Desarrollé un aplicativo web para promocionar salones de eventos con filtros de búsqueda y un módulo administrativo para su gestión.',
    tecnologias: ['Vue.js', 'Quasar', 'Node.js', 'MongoDB'],
    imagen: img1
  },
  {
    id: 2,
    titulo: 'Restaurante JuanMar',
    descripcion: 'Diseñé un aplicativo web para el restaurante JuanMar con módulo administrativo para gestionar reservas, menú y contenido.',
    tecnologias: ['Vue.js', 'Bootstrap', 'Node.js', 'MongoDB'],
    imagen: img2
  },
  {
    id: 3,
    titulo: 'Vivirelax',
    descripcion: 'Desarrollé la página web para el spa ViveRelax, integrando frontend, backend y un sistema administrativo para gestionar contenido y servicios.',
    tecnologias: ['Vue.js', 'Quasar', 'Node.js', 'MongoDB'],
    imagen: img3
  },
  {
    id: 4,
    titulo: 'Hoteles Barichara',
    descripcion: 'Desarrollé el Backend del sitio Hoteles Barichara para gestionar reservas y promocionar hoteles del municipio.',
    tecnologias: ['Node.js', 'MongoDB'],
    imagen: img4
  }
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

function scrollToSection(id) {
  const el = document.getElementById(id);
  if (el) {
    el.scrollIntoView({ behavior: 'smooth' });
  }
}

// Modal de imagen
const modalImagen = ref('');
const modalTitulo = ref('');

function abrirModalImagen(src, titulo) {
  modalImagen.value = src;
  modalTitulo.value = titulo;
}
</script>

<template>
  <div class="portafolio">
    <!-- Barra de navegación Bootstrap -->
    <nav class="navbar navbar-expand-lg navbar-dark navegacion fixed-top">
      <div class="container">
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
          aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse justify-content-center" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link text-white" href="#sobre-mi" @click.prevent="scrollToSection('sobre-mi')">Sobre mí</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-white" href="#proyectos"
                @click.prevent="scrollToSection('proyectos')">Proyectos</a>
            </li>
            <li class="nav-item">
              <a class="nav-link text-white" href="#habilidades"
                @click.prevent="scrollToSection('habilidades')">Lenguajes de Programación</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Encabezado -->
    <header class="portada">
      <div class="contenedor portada-contenido mt-3">
        <img :src="fotoPerfil" alt="Foto de perfil" class="portada-imagen" />
        <div>
          <h1 class="portada-titulo">Andrés David Salgado Cala</h1>
        </div>
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
            aportar ideas y formar parte de proyectos donde el trabajo en equipo
            y la innovación sean pilares fundamentales.
          </p>
        </div>
      </div>
    </section>

    <!-- Proyectos -->
    <section class="proyectos proyectos-bg" id="proyectos" v-reveal>
      <div class="contenedor">
        <h2 class="seccion-titulo" style="color: white;">Proyectos Realizados</h2>
        <p style="text-align: center; color: white;">Los siguientes proyectos los realicé durante mi etapa productiva en
          el SENA:</p>
        <div class="proyectos-grid">
          <article class="proyecto-tarjeta" v-for="proyecto in proyectos" :key="proyecto.id">
            <!-- Imagen del proyecto -->
            <img :src="proyecto.imagen" :alt="proyecto.titulo" class="img-fluid rounded mb-3 proyecto-img"
              style="cursor:pointer; max-height:180px; object-fit:cover;" data-bs-toggle="modal"
              data-bs-target="#modalImagenProyecto" @click="abrirModalImagen(proyecto.imagen, proyecto.titulo)" />
            <div class="proyecto-contenido">
              <h3 class="proyecto-titulo">{{ proyecto.titulo }}</h3>
              <p class="proyecto-descripcion">{{ proyecto.descripcion }}</p>
              <div class="proyecto-tecnologias">
                <span class="etiqueta-tecnologia" v-for="tecnologia in proyecto.tecnologias" :key="tecnologia">
                  {{ tecnologia }}
                </span>
              </div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- Modal Bootstrap para imagen de proyecto -->
    <div class="modal fade" id="modalImagenProyecto" tabindex="-1" aria-labelledby="modalImagenProyectoLabel"
      aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered modal-xl">
        <div class="modal-content bg-dark">
          <div class="modal-header border-0">
            <h5 class="modal-title text-white" id="modalImagenProyectoLabel">{{ modalTitulo }}</h5>
            <button type="button" class="btn-close btn-close-white" data-bs-dismiss="modal"
              aria-label="Cerrar"></button>
          </div>
          <div class="modal-body text-center">
            <img :src="modalImagen" :alt="modalTitulo" class="img-fluid rounded" />
          </div>
        </div>
      </div>
    </div>

    <!-- Lenguajes de Programación y Tecnologías -->
    <section class="habilidades" id="habilidades" v-reveal>
      <div class="contenedor">
        <h2 class="seccion-titulo">Lenguajes de Programación y Tecnologías</h2>
        <div class="habilidades-carousel-wrapper">
          <div class="habilidades-carousel">
            <span class="badge-habilidad js">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><rect width="32" height="32" rx="6" fill="#F7DF1E"/><path d="M19.5 23.9c.6 1.1 1.4 2 2.9 2 1.2 0 2-.6 2-1.4 0-1-0.8-1.3-2.2-1.9l-.8-.3c-2.3-.9-3.8-2-3.8-4.3 0-2.1 1.6-3.7 4.1-3.7 1.8 0 3.1.6 4 2.2l-2.2 1.4c-.5-.9-1-1.2-1.8-1.2-.8 0-1.3.5-1.3 1.2 0 .8.5 1.1 1.7 1.6l.8.3c2.7 1.1 4.2 2.1 4.2 4.5 0 2.6-2 4-4.7 4-2.6 0-4.2-1.2-5-2.7l2.3-1.3zm-8.2.2c.4.7.8 1.3 1.7 1.3.9 0 1.5-.3 1.5-1.7v-7.7h2.8v7.8c0 2.9-1.7 4.2-4.1 4.2-2.2 0-3.5-1.1-4.2-2.6l2.3-1.3z" fill="#222"/></svg>
              JavaScript
            </span>
            <span class="badge-habilidad vue">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M2 6h6.7L16 18.7 23.3 6H30L16 28 2 6z" fill="#41B883"/><path d="M2 6l14 22 14-22h-6.7L16 18.7 8.7 6H2z" fill="#41B883"/><path d="M8.7 6L16 18.7 23.3 6h-4.1L16 10.1 12.8 6H8.7z" fill="#35495E"/></g></svg>
              Vue.js
            </span>
            <span class="badge-habilidad node">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M16 2.7l12.5 7.2v12.2L16 29.3 3.5 22.1V9.9L16 2.7z" fill="#8CC84B"/><path d="M16 4.7l10.5 6.1v10.4L16 27.3 5.5 21.2V10.8L16 4.7z" fill="#fff"/><path d="M16 6.7l8.5 4.9v8.6L16 25.3 7.5 20.2v-8.6L16 6.7z" fill="#8CC84B"/><path d="M16 8.7l6.5 3.7v6.8L16 23.3l-6.5-3.7v-6.8L16 8.7z" fill="#fff"/><path d="M16 10.7l4.5 2.6v4.8L16 21.3l-4.5-2.6v-4.8L16 10.7z" fill="#8CC84B"/></g></svg>
              Node.js
            </span>
            <span class="badge-habilidad py">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M16.1 2c-2.2 0-4.2.2-6 1.1-2.7 1.2-3.2 3.7-3.2 6.2v2.7h12.3v1.4H6.9c-2.6 0-4.9 1.6-4.9 4.2v4.1c0 2.6 2.3 4.2 4.9 4.2h2.1v-3.1c0-2.8 2.3-5.1 5.1-5.1h7.2c2.2 0 4.2-.2 6-1.1 2.7-1.2 3.2-3.7 3.2-6.2V8.1c0-2.6-2.3-4.2-4.9-4.2h-2.1v3.1c0 2.8-2.3 5.1-5.1 5.1h-7.2z" fill="#3776AB"/><circle cx="10.5" cy="7.5" r="1.5" fill="#fff"/><path d="M15.9 30c2.2 0 4.2-.2 6-1.1 2.7-1.2 3.2-3.7 3.2-6.2v-2.7H12.8v-1.4h12.3c2.6 0 4.9-1.6 4.9-4.2v-4.1c0-2.6-2.3-4.2-4.9-4.2h-2.1v3.1c0 2.8-2.3 5.1-5.1 5.1h-7.2c-2.2 0-4.2.2-6 1.1-2.7 1.2-3.2 3.7-3.2 6.2v2.7c0 2.6 2.3 4.2 4.9 4.2h2.1v-3.1c0-2.8 2.3-5.1 5.1-5.1h7.2z" fill="#FFD43B"/><circle cx="21.5" cy="24.5" r="1.5" fill="#fff"/></g></svg>
              Python
            </span>
            <span class="badge-habilidad sql">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><ellipse cx="16" cy="8" rx="12" ry="5" fill="#336791"/><ellipse cx="16" cy="24" rx="12" ry="5" fill="#336791"/><ellipse cx="16" cy="16" rx="12" ry="5" fill="#336791"/><ellipse cx="16" cy="16" rx="12" ry="5" fill="#fff" fill-opacity=".2"/></svg>
              SQL
            </span>
            <span class="badge-habilidad mongo">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M16.5 2.5s.2 7.2 5.2 12.2c4.7 4.7 4.3 9.7 2.7 12.2-1.7 2.6-5.2 3.1-7.9 3.1-2.7 0-6.2-.5-7.9-3.1-1.6-2.5-2-7.5 2.7-12.2C16.3 9.7 16.5 2.5 16.5 2.5z" fill="#13AA52"/><path d="M16.5 2.5s.2 7.2 5.2 12.2c4.7 4.7 4.3 9.7 2.7 12.2-1.7 2.6-5.2 3.1-7.9 3.1-2.7 0-6.2-.5-7.9-3.1-1.6-2.5-2-7.5 2.7-12.2C16.3 9.7 16.5 2.5 16.5 2.5z" fill="#fff" fill-opacity=".1"/></g></svg>
              MongoDB
            </span>
            <span class="badge-habilidad bootstrap">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><rect width="32" height="32" rx="6" fill="#7952B3"/><path d="M11 8.5h7.2c2.7 0 4.3 1.2 4.3 3.5 0 1.5-.8 2.6-2.2 3v.1c1.8.3 2.8 1.5 2.8 3.2 0 2.5-1.8 3.7-4.7 3.7H11V8.5zm3.1 5.6h3.2c1.2 0 1.8-.5 1.8-1.5 0-1-.6-1.5-1.8-1.5h-3.2v3zm0 5.2h3.5c1.3 0 2-.5 2-1.6 0-1.1-.7-1.6-2-1.6h-3.5v3.2z" fill="#fff"/></svg>
              Bootstrap
            </span>
            <span class="badge-habilidad quasar">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><circle cx="16" cy="16" r="14" fill="#1976D2"/><path d="M16 7.5l2.6 5.3 5.9.9-4.2 4.1 1 5.8-5.3-2.8-5.3 2.8 1-5.8-4.2-4.1 5.9-.9L16 7.5z" fill="#fff"/></g></svg>
              Quasar
            </span>
            <!-- Duplicados para efecto infinito -->
            <span class="badge-habilidad js"><svg width="24" height="24" viewBox="0 0 32 32" fill="none"><rect width="32" height="32" rx="6" fill="#F7DF1E"/><path d="M19.5 23.9c.6 1.1 1.4 2 2.9 2 1.2 0 2-.6 2-1.4 0-1-0.8-1.3-2.2-1.9l-.8-.3c-2.3-.9-3.8-2-3.8-4.3 0-2.1 1.6-3.7 4.1-3.7 1.8 0 3.1.6 4 2.2l-2.2 1.4c-.5-.9-1-1.2-1.8-1.2-.8 0-1.3.5-1.3 1.2 0 .8.5 1.1 1.7 1.6l.8.3c2.7 1.1 4.2 2.1 4.2 4.5 0 2.6-2 4-4.7 4-2.6 0-4.2-1.2-5-2.7l2.3-1.3zm-8.2.2c.4.7.8 1.3 1.7 1.3.9 0 1.5-.3 1.5-1.7v-7.7h2.8v7.8c0 2.9-1.7 4.2-4.1 4.2-2.2 0-3.5-1.1-4.2-2.6l2.3-1.3z" fill="#222"/></svg>JavaScript</span>
            <span class="badge-habilidad vue"><svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M2 6h6.7L16 18.7 23.3 6H30L16 28 2 6z" fill="#41B883"/><path d="M2 6l14 22 14-22h-6.7L16 18.7 8.7 6H2z" fill="#41B883"/><path d="M8.7 6L16 18.7 23.3 6h-4.1L16 10.1 12.8 6H8.7z" fill="#35495E"/></g></svg>Vue.js</span>
            <span class="badge-habilidad node"><svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M16 2.7l12.5 7.2v12.2L16 29.3 3.5 22.1V9.9L16 2.7z" fill="#8CC84B"/><path d="M16 4.7l10.5 6.1v10.4L16 27.3 5.5 21.2V10.8L16 4.7z" fill="#fff"/><path d="M16 6.7l8.5 4.9v8.6L16 25.3 7.5 20.2v-8.6L16 6.7z" fill="#8CC84B"/><path d="M16 8.7l6.5 3.7v6.8L16 23.3l-6.5-3.7v-6.8L16 8.7z" fill="#fff"/><path d="M16 10.7l4.5 2.6v4.8L16 21.3l-4.5-2.6v-4.8L16 10.7z" fill="#8CC84B"/></g></svg>Node.js</span>
            <span class="badge-habilidad py"><svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M16.1 2c-2.2 0-4.2.2-6 1.1-2.7 1.2-3.2 3.7-3.2 6.2v2.7h12.3v1.4H6.9c-2.6 0-4.9 1.6-4.9 4.2v4.1c0 2.6 2.3 4.2 4.9 4.2h2.1v-3.1c0-2.8 2.3-5.1 5.1-5.1h7.2c2.2 0 4.2-.2 6-1.1 2.7-1.2 3.2-3.7 3.2-6.2V8.1c0-2.6-2.3-4.2-4.9-4.2h-2.1v3.1c0 2.8-2.3 5.1-5.1 5.1h-7.2z" fill="#3776AB"/><circle cx="10.5" cy="7.5" r="1.5" fill="#fff"/><path d="M15.9 30c2.2 0 4.2-.2 6-1.1 2.7-1.2 3.2-3.7 3.2-6.2v-2.7H12.8v-1.4h12.3c2.6 0 4.9-1.6 4.9-4.2v-4.1c0-2.6-2.3-4.2-4.9-4.2h-2.1v3.1c0 2.8-2.3 5.1-5.1 5.1h-7.2c-2.2 0-4.2.2-6 1.1-2.7 1.2-3.2 3.7-3.2 6.2v2.7c0 2.6 2.3 4.2 4.9 4.2h2.1v-3.1c0-2.8 2.3-5.1 5.1-5.1h7.2z" fill="#FFD43B"/><circle cx="21.5" cy="24.5" r="1.5" fill="#fff"/></g></svg>Python</span>
            <span class="badge-habilidad sql"><svg width="24" height="24" viewBox="0 0 32 32" fill="none"><ellipse cx="16" cy="8" rx="12" ry="5" fill="#336791"/><ellipse cx="16" cy="24" rx="12" ry="5" fill="#336791"/><ellipse cx="16" cy="16" rx="12" ry="5" fill="#336791"/><ellipse cx="16" cy="16" rx="12" ry="5" fill="#fff" fill-opacity=".2"/></svg>SQL</span>
            <span class="badge-habilidad mongo"><svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><path d="M16.5 2.5s.2 7.2 5.2 12.2c4.7 4.7 4.3 9.7 2.7 12.2-1.7 2.6-5.2 3.1-7.9 3.1-2.7 0-6.2-.5-7.9-3.1-1.6-2.5-2-7.5 2.7-12.2C16.3 9.7 16.5 2.5 16.5 2.5z" fill="#13AA52"/><path d="M16.5 2.5s.2 7.2 5.2 12.2c4.7 4.7 4.3 9.7 2.7 12.2-1.7 2.6-5.2 3.1-7.9 3.1-2.7 0-6.2-.5-7.9-3.1-1.6-2.5-2-7.5 2.7-12.2C16.3 9.7 16.5 2.5 16.5 2.5z" fill="#fff" fill-opacity=".1"/></g></svg>MongoDB</span>
            <span class="badge-habilidad bootstrap"><svg width="24" height="24" viewBox="0 0 32 32" fill="none"><rect width="32" height="32" rx="6" fill="#7952B3"/><path d="M11 8.5h7.2c2.7 0 4.3 1.2 4.3 3.5 0 1.5-.8 2.6-2.2 3v.1c1.8.3 2.8 1.5 2.8 3.2 0 2.5-1.8 3.7-4.7 3.7H11V8.5zm3.1 5.6h3.2c1.2 0 1.8-.5 1.8-1.5 0-1-.6-1.5-1.8-1.5h-3.2v3zm0 5.2h3.5c1.3 0 2-.5 2-1.6 0-1.1-.7-1.6-2-1.6h-3.5v3.2z" fill="#fff"/></svg>
              Bootstrap
            </span>
            <span class="badge-habilidad quasar">
              <svg width="24" height="24" viewBox="0 0 32 32" fill="none"><g><circle cx="16" cy="16" r="14" fill="#1976D2"/><path d="M16 7.5l2.6 5.3 5.9.9-4.2 4.1 1 5.8-5.3-2.8-5.3 2.8 1-5.8-4.2-4.1 5.9-.9L16 7.5z" fill="#fff"/></g></svg>
              Quasar
            </span>
          </div>
        </div>
      </div>
    </section>

    <!-- Pie de página -->
    <footer class="pie" id="pie">
      <div class="contenedor">
        <p>&copy; 2025 Andrés David Salgado Cala. Todos los derechos reservados.</p>
        <!-- Íconos de redes sociales -->
        <div class="redes-sociales mt-3">
          <a href="https://github.com/Andrew-css" target="_blank" rel="noopener" class="me-3 redes-icono" aria-label="GitHub">
            <svg width="28" height="28" fill="currentColor" viewBox="0 0 16 16">
              <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38
                0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52
                -.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2
                -3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64
                -.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08
                2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01
                1.93-.01 2.19 0 .21.15.46.55.38A8.013 8.013 0 0 0 16 8c0-4.42-3.58-8-8-8z"/>
            </svg>
          </a>
          <a href="https://www.linkedin.com/in/andr%C3%A9s-david-salgado-cala-901264248/" target="_blank" rel="noopener" class="redes-icono" aria-label="LinkedIn">
            <svg width="28" height="28" fill="currentColor" viewBox="0 0 16 16">
              <path d="M0 1.146C0 .513.526 0 1.175 0h13.65C15.474 0 16 .513 16 1.146v13.708c0
                .633-.526 1.146-1.175 1.146H1.175C.526 16 0 15.487 0 14.854V1.146zm4.943
                12.248V6.169H2.542v7.225h2.401zm-1.2-8.212c.837 0 1.358-.554 1.358-1.248
                -.015-.709-.521-1.248-1.342-1.248-.822 0-1.357.54-1.357 1.248 0 .694.52
                1.248 1.327 1.248h.014zm4.908 8.212h2.4V9.359c0-.215.016-.43.08-.584.175
                -.43.574-.877 1.244-.877.877 0 1.228.662 1.228 1.634v3.862h2.4V9.25c0
                -2.22-1.184-3.252-2.764-3.252-1.274 0-1.845.7-2.165 1.193v.025h-.016a5.6
                5.6 0 0 1 .016-.025V6.169h-2.4c.03.678 0 7.225 0 7.225z"/>
            </svg>
          </a>
        </div>
      </div>
    </footer>
  </div>
</template>

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
  background-color: #1a202c;
  color: white;
  padding: 5rem 0 6rem;
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

.portada-contenido {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
}

.portada-imagen {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  border: 4px solid #fff;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.10);
  background: #e2e8f0;
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
  background: #1a202c;
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
.proyectos-bg {
  background-color: #1a202c;
}

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

.redes-sociales {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
}
.redes-icono {
  color: #fff;
  transition: color 0.2s;
  display: inline-flex;
  align-items: center;
}
.redes-icono:hover {
  color: #667eea;
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

/* Responsive para portada */
@media (max-width: 768px) {
  .portada-contenido {
    flex-direction: column;
    gap: 1.5rem;
  }

  .portada-imagen {
    width: 90px;
    height: 90px;
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

.proyecto-img {
  width: 100%;
  max-width: 100%;
  transition: transform 0.2s;
}

.proyecto-img:hover {
  transform: scale(1.04);
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.18);
}

.habilidades-badges {
  display: flex;
  flex-wrap: wrap;
  gap: 1.2rem;
  justify-content: center;
  margin-top: 2.5rem;
}

.badge-habilidad {
  display: flex;
  align-items: center;
  gap: 0.7rem;
  background: #f3f4f6;
  color: #222;
  border-radius: 2rem;
  padding: 0.7rem 1.4rem;
  font-size: 1.1rem;
  font-weight: 600;
  box-shadow: 0 2px 8px rgba(0,0,0,0.04);
  transition: background 0.2s, color 0.2s, transform 0.2s;
  cursor: default;
}

.badge-habilidad svg {
  display: block;
}

.badge-habilidad.js { background: #f7df1e; color: #222; }
.badge-habilidad.vue { background: #41b883; color: #fff; }
.badge-habilidad.node { background: #8cc84b; color: #222; }
.badge-habilidad.py { background: #3776ab; color: #fff; }
.badge-habilidad.sql { background: #336791; color: #fff; }
.badge-habilidad.mongo { background: #13aa52; color: #fff; }
.badge-habilidad.bootstrap { background: #7952b3; color: #fff; }
.badge-habilidad.quasar { background: #1976d2; color: #fff; }

.badge-habilidad:hover {
  transform: translateY(-3px) scale(1.04);
  filter: brightness(1.08);
}

.habilidades-carousel-wrapper {
  overflow: hidden;
  width: 100%;
  padding: 10px;
  margin-top: 2.5rem;
}

.habilidades-carousel {
  display: flex;
  gap: 1.2rem;
  width: max-content;
  animation: carousel-move 25s linear infinite;
  will-change: transform;
}

@keyframes carousel-move {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.badge-habilidad {
  min-width: 180px;
  /* ...resto de tus estilos... */
}

/* Responsive: ajusta el tamaño de las badges en pantallas pequeñas */
@media (max-width: 768px) {
  .badge-habilidad {
    min-width: 140px;
    font-size: 0.95rem;
    padding: 0.5rem 1rem;
  }
  .habilidades-carousel {
    gap: 0.7rem;
  }
}
</style>