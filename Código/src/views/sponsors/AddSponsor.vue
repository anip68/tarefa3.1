<template>
  <!-- Portfolio Section -->
  <section class="page-section">
    <b-container>
      <HeaderPage title="Adicionar patrocinador" />

      <!--FORM-->
      <b-row>
        <b-col cols="2"></b-col>
        <b-col>
          <form @submit.prevent="add">
            <!--input-box nome-->
            <div class="form-group">
              <input
                v-model="name"
                type="text"
                class="form-control form-control-lg"
                id="txtName"
                placeholder="escreve patrocinador"
                required
              />
            </div>
            <!--opcão-box tipo de patrocinador-->
            <div class="form-group">
              <select
                id="sltGroup"
                class="form-control form-control-lg"
                v-model="type"
                required
              >
                <option value>-- SELECIONA TIPO --</option>
                <option value="economico">ECONÓMICO</option>
                <option value="material">MATERIAL</option>
                <option value="humano">HUMANO</option>
              </select>
            </div>

            <!--text-box  fazer a discrição do patrocinador-->
            <div class="form-group">
              <textarea
                id="txtDescription"
                class="form-control form-control-lg"
                placeholder="escreve descrição"
                cols="30"
                rows="10"
                v-model="description"
                required
              ></textarea>
            </div>

            <!--input-box nome-->
            <div class="form-group">
              <div class="form-group">
                <input
                  v-model="montante"
                  type="text"
                  min="1"
                  max="10"
                  class="form-control form-control-lg"
                  id="txtMontante"
                  placeholder="escreve o montante"
                  required
                />
              </div>
            </div>

            <button type="submit" class="btn btn-outline-success btn-lg mr-2">
              <i class="fas fa-plus-square"></i> ADICIONAR
            </button>

            <router-link
              :to="{ name: 'listSponsors' }"
              tag="button"
              class="btn btn-outline-danger btn-lg">
              <i class="fas fa-window-close"></i> CANCELAR</router-link>
          
          </form>

        </b-col>
        <b-col cols="2"></b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import { ADD_SPONSOR } from "@/store/sponsors/sponsor.constants";
import HeaderPage from "@/components/HeaderPage.vue";
import router from "@/router";
import { mapGetters } from "vuex";

export default {
  name: "AddSponsor",
  components: {
    HeaderPage,
  },
  data: () => {
    return {
      name: "",
      type: "",
      description: "",
      montante: "",

      evaluation: [],
      comments: [],
    };
  },
  computed: {
    ...mapGetters("sponsor", ["getMessage"]),
  },
  methods: {

    teste(){
      console.log(this.$data.name);
    },
    add() {
      this.$store.dispatch(`sponsor/${ADD_SPONSOR}`, this.$data).then(
        () => {
          this.$alert(this.getMessage, "patrocinador adicionado!", "success");
          router.push({ name: "listSponsors" });
        },
        (err) => {
          this.$alert(`${err.message}`, "Erro", "error");
        }
      );
    },
  },
};
</script>
