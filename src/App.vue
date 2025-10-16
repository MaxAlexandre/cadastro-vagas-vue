<template>
  <div>
    <VagasFavoritas/>
    <Topo @navegar="componente = $event"/>
    <Alerta v-if="exibirAlerta" :tipo="alerta.tipoAlerta">
      <template v-slot:titulo>
        <h5>{{ alerta.titulo }}</h5>
      </template>
      <template v-slot:descricao>
        <p>{{ alerta.descricao }}</p>
      </template>
    </Alerta>
    <Conteudo :conteudo="componente"/>
  </div>
</template>

<script>
import Alerta from "@/components/comuns/Alerta.vue";
import Conteudo from './components/layouts/Conteudo.vue'
import Topo from './components/layouts/Topo.vue'
import VagasFavoritas from "@/components/comuns/VagasFavoritas.vue";

export default {
  data: () => ({
    componente: 'Home',
    exibirAlerta: false,
    alerta: {titulo: '', descricao: '', tipoAlerta: ''}
  }),
  name: 'App',
  components: {
    VagasFavoritas,
    Conteudo,
    Topo,
    Alerta
  },
  mounted() {
    this.emitter.on('alerta', (p) => {
      this.alerta = p
      this.exibirAlerta = true
      setTimeout(() => this.exibirAlerta = false, 5000)
    })
  }
}
</script>

<style scoped>

</style>
