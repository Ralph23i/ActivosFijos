<template>
  <div id="Departamento">
      <div class = "container">
      <h3>Departamentos</h3>
      <br>
      <form name="myform">
      <div class = "form-group">
          <label>Descripcion</label><br>
          <input type="text" v-model="cuerpos.Descripcion" class="form-control" placeholder="Ingrese la descripcion" ><br><br>
          <label id="caja">Estado</label>
          <input type="checkbox" v-model="cuerpos.Estado"><br><br>          
          <button v-on:click.prevent="post" class="btn btn-primary">Enviar</button><br><br>
      </div>
      </form>
      </div>
  </div> 
</template>

<script>
export default {
  name: 'Departamento',
  data () {
    return {
     descripcion:"",
     estado: false,
     id: null,
     modo: 'C',
     cuerpos: []
    }
  },

  methods:{
    post:function()
    {
    
      this.$http.put('http://localhost:61542/Api/Departamentos/' + this.id,{
        ID:this.id,
        Descripcion:this.cuerpos.Descripcion,
        Estado:this.cuerpos.Estado

      }).then(function(data){
        console.log(data);
        alert("Departamento editado exitosamente");
        window.location.href = "/Con";
      });
    
    }
  },

  created()
    {
        this.id = this.$route.params.id
        if(this.id != null){
          this.modo = 'E';
        this.$http.get('http://localhost:61542/Api/Departamentos/' + this.id).then(function(data){
           this.cuerpos = data.body;
          console.log(data);
        });
    }
    }

}
</script>

<style scoped>

#caja{
  padding-right: 5px;
}

</style>