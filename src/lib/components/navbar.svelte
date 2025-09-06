<script>
    import { goto } from '$app/navigation';
    import { browser } from '$app/environment';
    let menuAbierto = false;
    let token = null;
    let video = "/images/asosi.mp4"
  
    function toggleMenu() {
      menuAbierto = !menuAbierto;
    }
  
    function logout() {
      if (browser) {
        localStorage.removeItem('token');
        goto('/');
      }
    }
  
    // Verifica si hay token (solo en cliente)
    if (browser) {
      token = localStorage.getItem('token');
    }
  </script>
  
  <nav class="bg-indigo-900 text-white px-4 py-3 shadow-md flex flex-col items-center">
    <p>Asosiacion Siempre a tu Lado</p>
    <div class="container mx-auto flex items-center justify-between mt-4">
      <a href="/" class="font-bold">ASATL</a>
  
      <!-- Botón hamburguesa (visible solo en móvil) -->
      <button class="md:hidden focus:outline-none" on:click={toggleMenu}>
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
            d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>
      <button class="bg-rose-600 p-2 text-white font-bold rounded-xl">Donar </button>
  
      <!-- Enlaces (pantallas grandes) -->
      <ul class="hidden md:flex space-x-6">
        
        <li><a href="#servicios" class="hover:text-yellow-300">Servicios</a></li>
        <li><a href="/aboutus" class="hover:text-yellow-300">Conócenos</a></li>
        {#if token}
          <li><button on:click={logout} class="hover:text-yellow-300">Cerrar sesión</button></li>
        {/if}
      </ul>
    </div>
  
    <!-- Enlaces (pantallas pequeñas) -->
    {#if menuAbierto}
      <ul class="md:hidden flex flex-col mt-2 space-y-2 px-2 pb-4 animate-slide-down">
       
        {#if token}
        <li><a href="/dashboard" class="block text-left hover:text-yellow-300">Mi perfil</a></li>
          <li><button on:click={logout} class="block text-left hover:text-yellow-300">Cerrar sesión</button></li>
        {/if}
        {#if !token}
        <li><a href="/login" class="block hover:text-yellow-300">Iniciar sesión</a></li>
        {/if}
        <li><a href="/registro" class="block hover:text-yellow-300">Registrarme</a></li>
        <li><a href="/services" class="block hover:text-yellow-300">Servicios</a></li>
        <li><a href="/aboutus" class="block hover:text-yellow-300">Conócenos</a></li>
        
      </ul>
    {/if}
  </nav>
  
  <style>
    @keyframes slideDown {
      from {
        opacity: 0;
        transform: translateY(-10px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }
  
    .animate-slide-down {
      animation: slideDown 0.3s ease-out forwards;
    }
  </style>
  