<template>
    <div>
        <div>
            <form id="forms" method="POST" @submit="createBurger">
                <div class="input-container">
                    <label for="nome">Nome do Produto</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome" >
                </div>
                <div class="input-container">
                    <label for="quantidade">Qauntidade de itens</label>
                    <input type="number" id="quantidade" name="quantidade" v-model="quantidade" >                
                </div>
                <div class="input-container">
                    <label for="valor">Valor</label>
                    <input type="number" pattern="[0-9]+([,\.][0-9]+)?" id="valor" name="valor" v-model="valor" >                
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Salvar Produto">
                </div>
            </form>
        </div>
    </div>

</template>

<script>
import { useVuelidate } from '@vuelidate/core'
import { required, email } from '@vuelidate/validators'

    export default{
        name: "form",
        setup () {
    return { v$: useVuelidate() }
  },
        data() {
            return {
                nome: null,
                quantidade: null,
                valor: null               
                }
        },
        methods: {
   
          async createBurger(e) {
            
            e.preventDefault()
            const data = {
              nome: this.nome,
              quantidade: this.quantidade,
              valor: this.valor        
            }
            const dataJson = JSON.stringify(data)    

             const req = await fetch("http://localhost:8080/api/produto", {
                method: "POST",
                headers: { "Content-Type" : "application/json" },
                body: dataJson
             });
             const res = await req.json()
                console.log(res, "ass")
                this.msg = "Pedido realizado com sucesso!"
                // clear message
                setTimeout(() => this.msg = "", 3000)
                  // limpar campos               
    }
  },
  validations () {
    return {
      nome: { required }, // Matches this.firstName
      quantidade: { required }, // Matches this.lastName      
    }
  }  
}
    

</script>

<style>
    #forms{
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

    label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }

    .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }


</style>