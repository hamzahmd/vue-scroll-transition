<script setup lang="ts">
import ScrollTransition from './components/ScrollTransition.vue'
import SampleLogo from './components/SampleLogo.vue'
</script>

<template>
  <main class="bg-[#011D20] scroll-smooth">
    <div class="max-w-7xl mx-auto px-4">
      <div class="h-screen flex flex-col gap-6 justify-center items-center">
        <h2 class="text-2xl font-medium text-white">
          Vertical Slide-in (Default)
        </h2>
        <ScrollTransition> <SampleLogo /> </ScrollTransition>
      </div>

      <div class="h-screen flex flex-col gap-6 justify-center items-center">
        <h2 class="text-2xl font-medium text-white">
          Horizontal Right to Left
        </h2>
        <ScrollTransition transition="horizontalToLeft">
          <SampleLogo />
        </ScrollTransition>
      </div>

      <div class="h-screen flex flex-col gap-6 justify-center items-center">
        <h2 class="text-2xl font-medium text-white">
          Horizontal Left to Right
        </h2>
        <ScrollTransition transition="horizontalToRight">
          <SampleLogo />
        </ScrollTransition>
      </div>

      <div class="h-screen flex flex-col gap-6 justify-center items-center">
        <ScrollTransition
          as="h2"
          transition="horizontalToRight"
          class="text-2xl font-medium text-white"
        >
          With Delay
        </ScrollTransition>
        <ScrollTransition :more-delay="true">
          <SampleLogo />
        </ScrollTransition>
      </div>
    </div>
  </main>
</template>
