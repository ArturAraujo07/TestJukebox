<template>
  
  <div class="container">
    <div class="row">
      <div class="col-sm-12">
        <form class="col-sm-12 col-md-12">
          <div class="form-group">
            <label for="name">Nome:</label>
            <input v-model.trim="people.name"
              type="text"
              class="form-control"
              id="name"
              placeholder="Digite seu nome"
            />
          </div>
          <div class="form-group">
            <label for="lastName">Sobrenome:</label>
            <input
              v-model.trim="people.surname"
              type="text"
              class="form-control"
              id="lastName"
              placeholder="Digite seu sobrenome"
            />
          </div>
          <div class="form-group">
            <label for="exampleInputEmail1">E-mail:</label>
            <input
              v-model="people.email"
              type="email"
              class="form-control"
              id="exampleInputEmail1"
              aria-describedby="emailHelp"
              placeholder="Digite seu e-mail"
            />
          </div>
          <div class="form-group">
            <label for="telephone">Telefone:</label>
            <input
              v-model="people.phone"
              type="text"
              class="form-control"
              id="telephone"
              placeholder="(DDD) 9xxxx-xxxx"
            />
          </div>
          <br />
          
          <div class="form-check form-check-inline">
            <input
              class="form-check-input"
              type="radio"
              name="pj"
              id="pj1"
              value="0"
              checked
              v-model="people.pj"
            />
            <label class="form-check-label" for="pj1"> CPF </label>
          </div>
          <div class="form-check form-check-inline">
            <input
              class="form-check-input"
              type="radio"
              name="pj"
              id="pj2"
              value="1"
              v-model="people.pj"
            />
            <label class="form-check-label" for="pj2"> CNPJ </label>
          </div>
          <br />
          <br />
          <div v-if="people.pj == 0" class="form-group" v-id="1">
            <label for="cpf">CPF</label>
            <input
              v-model="people.cpf"
              type="text"
              class="form-control"
              id="cpf"
              placeholder="xxx.xxx.xxx-xx"
            />
          </div>
          <div v-else-if="people.pj == 1" class="form-group" v-id="2">
            <label for="cnpj">CNPJ</label>
            <input
              v-model="people.cnpj"
              type="text"
              class="form-control"
              id="cnpj"
              placeholder="xx.xxx.xxx/xxxx.xx"
            />
          </div>
          <!-- <button type="button" class="btn btn-secundary">Editar</button> -->
          <button
            type="button"
            class="btn btn-primary"
            @click="salvar(people)"
          >
            Salvar
          </button>
        </form>
        <br/><br/>
      </div>

      <div class="col-sm-12">
        <div>
        <h3>Tabela</h3>
        <div v-if="this.formPeople[0]">
          <div
            class="card"
            v-for="(people, index) in formPeople"
            :key="index"
          >
            <div class="card-header">Informações pessoais</div>

            <ul class="list-group list-group-flush text-left">
              <br />

              <li class="list-group-item">
                <strong>Nome Completo: {{ totalName }}</strong>
              </li>
              <li class="list-group-item">
                <strong>E-mail: {{ people.email }}</strong>
              </li>
              <li class="list-group-item">
                <strong>Telefone: {{ people.phone }}</strong>
              </li>
              <li v-if="people.pj == 0" class="list-group-item">
                <strong>CPF: {{ people.cpf }}</strong>
              </li>
              <li v-if="people.pj == 1" class="list-group-item">
                <strong>CNPJ: {{ people.cnpj }}</strong>
              </li>
              <li class="list-group-item">
                <button
                  type="button"
                  class="btn btn-warning btn-sm col-sm-3 mr-2"
                  @click="editar(index)"
                >
                  Editar
                </button>
                <button
                  type="button"
                  class="btn btn-danger btn-sm col-sm-3"
                  @click="remover(index)"
                >
                  Excluir
                </button>
              </li>
            </ul>
          </div>
        </div>
        <div v-else><p>Preencha o formulário!</p></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    people: {
      name: "",
      surname: "",
      email: "",
      phone: "",
      pj: null,
      cpf: "",
      cnpj: "",
    },

    formPeople: [],
  }),

  watch: {
      1:function() {
        if(id == 1) {
          if(id == 1) {
          return people.cpf;
        } else {
          return people.cnpj;
        }
        }
      }
    },

  computed: {
    totalName() {
      return this.people.name + " " + this.people.surname
    },
  },

  methods: {
    salvar() {
      const people = Object.assign({}, this.people);
      this.formPeople.push(people);
    },

    editar(index){
      
      this.people = this.formPeople[index];
      
    },

    remover(index){
      this.formPeople.splice(index,1);      
    }
  },
};
</script>

<style>
</style>