<template>
    <div class="calculadora" onselectstart='return false'>
        <div class="operacion">{{operacion}}</div>
        <div class="resultado">{{resultado}}</div>
        <div @click="borrar()" class='btn oscuro'>C</div>
        <div @click="signo()" class='btn oscuro'>+/-</div>
        <div @click="porcentaje()" class='btn oscuro'>%</div>
        <div @click="dividir()" class='btn operador'>/</div>
        <div @click="agregar(7)" class='btn'>7</div>
        <div @click="agregar(8)" class='btn'>8</div>
        <div @click="agregar(9)" class='btn'>9</div>
        <div @click="multiplicar()" class='btn operador'>*</div>
        <div @click="agregar(4)" class='btn'>4</div>
        <div @click="agregar(5)" class='btn'>5</div>
        <div @click="agregar(6)" class='btn'>6</div>
        <div @click="restar()" class='btn operador'>-</div>
        <div @click="agregar(1)" class='btn'>1</div>
        <div @click="agregar(2)" class='btn'>2</div>
        <div @click="agregar(3)" class='btn'>3</div>
        <div @click="sumar()" class='btn operador'>+</div>
        <div @click='agregar(0)' class='btn cero btn-abajo'>0</div>
        <div @click='puntoDecimal()' class='btn btn-abajo'>.</div>
        <div @click='igual()' class='btn operador btn-abajo'>=</div>
    </div>
</template>

<script>
export default {
  data () {
    return {
      resultado: 0,
      operadorClick: false,
      operador: null,
      anterior: null,
      operacion: ' ',
      puntito: false
    }
  },
  mounted () {
      window.addEventListener('keyup', this.handleKeyboard);
  },
  methods: {
    handleKeyboard(){
        if(event.keyCode === 27) this.resultado = 0;            // Borrar
        if(event.keyCode === 49) this.agregar(1);               // 1
        if(event.keyCode === 50) this.agregar(2);               // 2
        if(event.keyCode === 51) this.agregar(3);               // 3
        if(event.keyCode === 52) this.agregar(4);               // 4
        if(event.keyCode === 53) this.agregar(5);               // 5
        if(event.keyCode === 54) this.agregar(6);               // 6
        if(event.keyCode === 55) this.agregar(7);               // 7
        if(event.keyCode === 56) this.agregar(8);               // 8
        if(event.keyCode === 57) this.agregar(9);               // 9
        if(event.keyCode === 48) this.agregar(0);               // 0
        if(event.keyCode === 106) this.multiplicar();           // *
        if(event.keyCode === 107) this.sumar();                 // +
        if(event.keyCode === 109) this.restar();                // -
        if(event.keyCode === 110 || event.keyCode === 190 || event.keyCode === 188) this.puntoDecimal();          // ,
        if(event.keyCode === 111) this.dividir();               // /
        if(event.keyCode === 13) this.igual();                  // =
    },
    borrar () {
        this.resultado = 0;
        this.operadorClick = false;
        this.operador = null;
        this.anterior = null;
        this.puntito = false;
        this.operacion = ' ';
    },
    mostrarOperacion(op){
        this.operacion = op;
    },
    signo () {
        this.mostrarOperacion('+/-');
        this.resultado =
            this.resultado < 0
            ? (this.resultado = this.resultado - this.resultado * 2)
            : (this.resultado = this.resultado - this.resultado * 2)
    },
    porcentaje () {
        this.mostrarOperacion('%');
        this.resultado = this.resultado / 100
    },
    agregar (numero) {
        if (this.operadorClick && !this.puntito) {
            this.resultado = numero
            this.operadorClick = false
        } else {
            if (this.operadorClick && this.puntito) {
                this.resultado = '' + this.resultado + numero
                this.puntito = false
                this.operadorClick = false
            } else {
                this.resultado =
                    this.resultado === 0
                    ? (this.resultado = numero)
                    : '' + this.resultado + numero
            }
        }
    },
    puntoDecimal () {
        if(Number.isInteger(this.resultado)){
            let resultado = this.resultado;
            // Agregamos el punto decimal
            this.resultado = resultado + '.'
        }

        // if(this.operadorClick) {
        //     this.resultado = '0.'
        //     this.puntito = true
        // }
    },
    dividir () {
        this.mostrarOperacion('/')
        this.operador = (a, b) => a / b
        this.anterior = this.resultado
        this.operadorClick = true
    },
    multiplicar () {
        this.mostrarOperacion('*')
        this.operador = (a, b) => a * b
        this.anterior = this.resultado
        this.operadorClick = true
    },
    restar () {
        this.mostrarOperacion('-')
        this.operador = (a, b) => a - b
        this.anterior = this.resultado
        this.operadorClick = true
    },
    sumar () {
        this.mostrarOperacion('+')
        this.operador = (a, b) => a + b
        this.anterior = this.resultado
        this.operadorClick = true
    },
    igual () {
        this.mostrarOperacion('=')
        this.resultado = this.operador(Number(this.anterior), Number(this.resultado))
        this.anterior = null      
        this.operadorClick = true
    }
  }
}
</script>

<style scoped>
.calculadora {
	margin: 0 auto;
	width: 80vw;
	font-size: 2rem;
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	grid-auto-rows: minmax(10vh, auto);
	-webkit-box-shadow: -3px 3px 15px hsla(0, 0%, 7%, .4);
	box-shadow: -3px 3px 15px hsla(0, 0%, 7%, .4);
	line-height: 10vh
}

.operacion{
    background: #020C0E;
    color: #fff;
}

.resultado {
	grid-column: 2/5;
	background: #020C0E;
	color: #fff;
	border-top: 0;
	font-size: 2.5rem;
	cursor: default;
	overflow: hidden;
	text-overflow: ellipsis;
	padding: 0 1rem;
	text-align: right;
}

.cero {
	grid-column: 1/3
}

.btn {
	background: #d4d4d2;
	cursor: pointer
}

.btn:active {
	outline: none;
	background: #2f2f31;
	color: #fff;
	box-shadow: inset 0 0 5px rgba(0, 0, 0, .5);
	-moz-box-shadow: inset 0 0 5px rgba(0, 0, 0, .5);
	-webkit-box-shadow: inset 0 0 5px rgba(0, 0, 0, .5)
}

.btn-abajo {
	border-bottom: 0
}

.operador {
	background: #f49e3f;
	color: #fff
}

.oscuro {
	background: #424345;
	color: #fff
}

@media only screen and (min-width:0px) {
	.calculadora {
		width: 100%;
		grid-auto-rows: minmax(14vh, auto);
		line-height: 14vh
	}
}

@media only screen and (min-width:768px) {
	.calculadora {
		width: 100%;
		grid-auto-rows: minmax(8.5vh, auto);
		line-height: 7.5vh
	}
}

@media only screen and (min-width:1024px) {
	.calculadora {
		width: 80%;
        grid-auto-rows: minmax(10.5vh, auto);
	}
}

@media only screen and (min-width:1280px) {
	.calculadora {
		width: 20vw
	}
}

@media only screen and (min-width:1600px) {
	.calculadora {
		width: 15vw
	}
}
</style>