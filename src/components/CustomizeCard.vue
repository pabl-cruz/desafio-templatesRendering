<script>
export default {
  name: 'CustomizableCard',
  data() {
    return {
      //variables y elementos dinamicos y estaticos de card
      card: {
        bgColor: '',
        txtColor: '',
        borderSize: '',
        text: '',
        typography: ['cursive', 'monospace', 'serif', 'sans-serif'],
        fontSelected: '',
        fontSize: ['8px', '18px', '40px'],
        fontSizeSelected: ''
      },
      //estados booleanos para mostrar/ocultar figura y texto
      isOpaque: false,
      isVisible: true
    }
  },
  methods:{
    opaque(){
        if (this.isOpaque == true){
            return 0.20;
        } else {
            return 1;
        }
    }
  }
}
</script>

<template>
  <div class="settings">
    <form>
      <div>
        <label for="bgColor">Color de fondo:</label>
        <input
          type="text"
          placeholder="introducir color de fondo de figura."
          v-model="card.bgColor"
        />
      </div>
      <br />
      <div>
        <label for="bgColor">Color de texto:</label>
        <input
          type="text"
          placeholder="introducir color del texto de la figura."
          v-model="card.txtColor"
        />
      </div>
      <br />
      <div>
        <input type="checkbox" v-model="isVisible" checked />
        <label for="showText">Mostrar texto</label>
      </div>
      <br />
      <div>
        <label for="borderRange">Ancho del borde:</label>
        <input
          type="range"
          name="borderRange"
          id="borderRange"
          min="1"
          max="50"
          v-model="card.borderSize"
        />
      </div>
      <br />
      <div>
        <label for="text">Contenido textual:</label>
        <br />
        <textarea
          id="text"
          rows="6"
          cols="30"
          v-model="card.text"
          placeholder="Introduzca el texto que quiere colocar en la tarjeta"
        ></textarea>
      </div>
      <br />
      <div>
        <label for="type">Tipografía:</label>
        <!--v-for en select que recorre todos las tipografias en typography y coloca el valor seleccionado en card.fontSelected-->
        <select name="type" id="type" v-model="card.fontSelected">
          <option v-for="type in card.typography" :value="type">{{ type }}</option>
        </select>
      </div>
      <br />
      <div>
        <input type="checkbox" name="opaque" id="opaque" v-model="isOpaque" />
        <label for="opaque">Opaco</label>
      </div>
      <br />
      <div>
        <label for="fontSize">Tamaño de letra:</label>
        <br />
        <!--valor de cada radio corresponde a indice en array fontSize-->
        <input type="radio" :value="card.fontSize[0]" v-model="card.fontSizeSelected" id="small" />
        <label for="small">Pequeño</label>
        <input
          type="radio"
          :value="card.fontSize[1]"
          v-model="card.fontSizeSelected"
          id="regular"
        />
        <label for="regular">Mediano</label>
        <input type="radio" :value="card.fontSize[2]" v-model="card.fontSizeSelected" id="large" />
        <label for="large">Grande</label>
      </div>
    </form>
  </div>
  <div
    class="box"
    :style="{
      backgroundColor: card.bgColor,
      color: card.txtColor,
      border: card.borderSize + `px solid black`,
      fontFamily: card.fontSelected,
      fontSize: card.fontSizeSelected,
      opacity: opaque(),
    }"
    :class="{
      empty: card.borderSize == false
    }"
  >
    <p v-if="card.text === ''">No hay texto</p>
    <p v-else v-show="isVisible">{{ card.text }}</p>
  </div>
</template>

<style scoped>
label {
  margin: 0.75rem 0.75rem 0.75rem 0;
}

.box {
  width: 350px;
  height: 550px;
  border-radius: 40px;
  display: flex;
}

.box p {
  text-align: center;
  justify-self: center;
  align-self: center;
  margin: auto;
}

.settings,
.box {
  margin: 1rem;
}

.settings {
  color: white;
  background-color: darkslategrey;
  padding: 2rem;
}
.empty {
  border: 1px dashed grey;
}
</style>
