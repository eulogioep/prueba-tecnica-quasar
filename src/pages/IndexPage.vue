<template>
  <q-page padding>
    <!-- Sección donde se muestra la selección de la plataforma de juegos -->
    <!-- Nota: en html5 <section></section> es equivalente a un <div> (https://developer.mozilla.org/es/docs/Web/HTML/Element/section) -->
    <section class="q-pa-md cabecera">
      <p class="text-h6">
        Selecciona una plataforma para mostrar los juegos gratuitos disponibles:
      </p>
      <!-- Componente predefinido en Quasar que muestra las propiedades establecidas en la variable "platforms". El valor seleccionado se guarda en la variable "platform" -->
      <q-select
        outlined
        v-model="platform"
        :options="platforms"
        option-value="id"
        option-label="desc"
      >
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-select>
    </section>

    <!-- Sección que muestra el número de juegos encontrados -->
    <section class="items-found">
      <p v-if="data.length > 0" class="q-pt-xs text-center">
        <b>{{ data.length }}</b> juegos encontrados.
      </p>
      <p v-else class="q-pt-xs text-center">
        <em>Selecciona una plataforma para buscar los juegos</em>
      </p>
    </section>

    <!-- Sección donde se carga el listado de juegos disponibles -->
    <section class="q-mt-xl items">
      <!-- Nota 1: <article></article> es equivalente a un <div> https://developer.mozilla.org/es/docs/Web/HTML/Element/article -->
      <!-- Nota 2: Bucle FOR directamente en HTML con Vue.js (https://es.vuejs.org/v2/guide/list.html) -->
      <article v-for="item in data" :key="item.id" class="item">
        <!-- Ejemplo del contenido de un item que devuelve el API:<template>
        {
          "id": 521,
          "title": "Diablo Immortal",
          "thumbnail": "https://www.freetogame.com/g/521/thumbnail.jpg",
          "short_description": "Built for mobile and also released on PC, Diablo Immortal fills in the gaps between Diablo II and III in an MMOARPG environment.",
          "game_url": "https://www.freetogame.com/open/diablo-immortal",
          "genre": "MMOARPG",
          "platform": "PC (Windows)",
          "publisher": "Blizzard Entertainment",
          "developer": "Blizzard Entertainment",
          "release_date": "2022-06-02",
          "freetogame_profile_url": "https://www.freetogame.com/diablo-immortal"
        }
      -->
        <a href="{{ item.freetogame_profile_url }}" class="item-link">
          <q-chip
            _outline
            color="secondary"
            text-color="white"
            icon="sports_esports"
            class="chip chip-platform"
            >{{ item.genre }}</q-chip
          >

          <!-- Foto del juego - En Vue.js se utiliza :atributo, en este caso el atributo es 'src' por lo que se utiliza
          :src="nombre_variable" para que el atributo tome el valor de forma dinámica a partir de la variable -->
          <img :src="item.thumbnail" class="item-image" />

          <div class="info">
            <!-- Título del juego - En Vue.js se utiliza {{ nombre_variable }} para mostrar un valor en la página -->
            <div class="text-h6">
              <b>{{ item.title }}</b>
            </div>
            <div class="developer">{{ item.developer }}</div>

            <!-- Descripción corta del juego -->
            <p class="description">{{ item.short_description }}</p>

            <!-- Información adicional del juego -->
            <div class="additional-info">
              <q-chip
                outline
                color="primary"
                text-color="white"
                icon="devices"
                class="chip"
                >{{ item.platform }}</q-chip
              >
            </div>
          </div>
        </a>
      </article>
      <q-inner-loading :showing="loading">
        <q-spinner-gears size="50px" color="primary" />
      </q-inner-loading>
    </section>
  </q-page>
</template>

<script>
import { defineComponent, ref, watch } from "vue";
import { api } from "boot/axios";
import { useQuasar } from "quasar";
export default defineComponent({
  name: "IndexPage",
  setup() {
    const $q = useQuasar();
    const platform = ref(null);
    const data = ref([]);
    const loading = ref(false);

    const loadData = () => {
      loading.value = true;
      const params = new URLSearchParams([
        ["platform", platform.value.id],
        ["sort-by", "alphabetical"],
      ]);
      api
        .get("/api/games", {
          params,
          headers: {
            "X-RapidAPI-Key":
              "67d9436ce8msh5a7f6cb557501a3p1efcadjsn7e754104fc3a",
            "X-RapidAPI-Host": "free-to-play-games-database.p.rapidapi.com",
          },
        })
        .then((response) => {
          data.value = response.data;
          loading.value = false;
        })
        .catch(() => {
          $q.notify({
            color: "negative",
            position: "top",
            message: "Error al recuperar datos",
            icon: "report_problem",
          });
          loading.value = false;
        });
    };
    watch(platform, (newvalue, oldvalue) => {
      //console.log('filter by ', newvalue)

      loadData();
    });
    return {
      data,
      platform,
      platforms: [
        { id: "all", desc: "Mostrar todos" },
        { id: "pc", desc: "Ver juegos para PC" },
        { id: "browser", desc: "Ver juegos para Navegador web" },
      ],
      loading,
    };
  },
});
</script>
<!--No aplico el Estilo CSS en el archivo app.scss porque el planteamiento es que cada página tenga su propio estilo-->
<style scoped>
.cabecera {
  border: 1px solid #dedede;
}

.items-found {
  margin-top: 12px;
}

.items {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap; /*De la fila, corta los items hasta el ancho de la pantalla*/
  gap: 24px; /*Separación entre los items*/
}

.item {
  position: relative;
  width: calc(
    25% - 24px
  ); /*% para dividir en 4 los componentes de la pantalla. -24px para compensar el gap del contenedor*/
  background-color: #f7f7f7;
}
.item:hover .text-h6 {
  text-decoration: underline;
}

.item a.item-link {
  height: 100%;
  text-decoration: none;
}

.item img.item-image {
  width: 100%;
  vertical-align: bottom;
}

.item .info {
  padding: 16px;
}

.item .text-h6 {
  margin: 0;
  color: #2b2b2b;
}
.item .developer {
  margin-bottom: 16px;
  font-size: 12px;
  color: #999;
}

.item .description {
  color: #333;
}
.item .chip {
  font-size: 12px;
}
.item .chip-platform {
  position: absolute;
  top: 8px;
  right: 8px;
  border: solid 2px white;
  box-shadow: 0 0 2px 4px rgb(0 0 0 / 20%);
}
</style>
