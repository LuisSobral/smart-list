<template>
  <div class="h-full">
    <header class="h-10 relative">
      <nuxt-link to="/">
        <img class="absolute inset-0 m-auto" :src="require('@/static/images/logo.png')" />
      </nuxt-link>
    </header>
    <main class="min-h-screen py-16">
      <Nuxt />
    </main>
    <base-button fab>
      <img :src="require('@/static/images/add.png')" />
    </base-button>
    <footer>
      <div class="container mx-auto py-4 border-t border-gray-300">
        <p class="text-center">
          @2021. BLIP Todos os direitos reservados |
          <span class="font-bold">Termos de Uso</span>
        </p>
      </div>
    </footer>
  </div>
</template>

<style lang="scss">
body {
  overflow-x: hidden;
}
</style>

<style lang="scss" scoped>
header {
  background-color: $bg-header;
}

main,
footer {
  background-color: #f5f8f9;
}

footer {
  color: #939da5;
}
</style>
>
