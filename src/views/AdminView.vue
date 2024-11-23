<template>
    <div>
        <div v-if="showForm">
        <h1 class="text-center mx-auto my-5">Ingresa tus datos</h1>
            <b-form @submit="onSubmit" class="w-50 text-center mx-auto">

                <b-form-group id="input-group-1" label="Nombre completo:" label-for="input-1" class="text-white text-start mb-3">
                    <b-form-input
                    id="input-1"
                    v-model="form.name"
                    placeholder="Nombre"
                    required
                    ></b-form-input>
                </b-form-group>

                <b-form-group id="input-group-2" label="Contraseña:" label-for="input-2" class="text-white text-start mb-3">
                    <b-form-input
                    id="input-2"
                    type="password"
                    v-model="form.password"
                    placeholder="Ingresa tu Contraseña:"
                    required
                    ></b-form-input>
                </b-form-group>

                <b-button type="submit" variant="success" class="mt-4">Ingresar</b-button>
            </b-form>
        </div>

        <!--segunda vista-->
        <div v-else class="">
            <div class="d-flex gap-3">
                <aside class="bg-dark col-2 d-none d-md-block">
                    <div class="text-center pt-5 mx-auto">
                        <img src="@/assets/perfil.png" alt="Imagen perfil" class="text-center mx-auto" />
                        <h5 class="text-secondary mt-3">Bienvenid@ <br> <span class="small text-light">{{form.name}}</span></h5>
                    </div>
                </aside>

                <!--derecha-->
                <div class="col-9 px-5 div-right">
                    <div class="pt-5 pb-3">
                        <h2 class="">Resumen de tu cuenta</h2>
                        <h4 class="">Le has dado like al juego <span class="fw-bold text-dark"></span></h4>
                    </div>
                    
                    <div class="border border-secondary p-4 w-75">
                        <p class="fs-5">¿Deseas comprar coins para este juego?</p>

                        <div class="text-center mb-4 mx-auto">
                            <button @click="addCoins" :disabled="form.coins >= 60" class="mt-3 btn btn-warning">
                            <i class="bi bi-coin"></i> Agregar coins
                            </button>
                            
                            <hr>
                            <p class="fs-5">Cantidad de coins comprados</p>
                        </div>

                        <!--progreso-->
                        <div
                            class="progress text-center mx-auto"
                            role="progressbar"
                            aria-label="Basic example"
                            aria-valuenow="form.coins"
                            aria-valuemin="0"
                            aria-valuemax="100"
                            >
                            <div
                            :class="
                                form.coins < 20
                                    ? 'progress-bar bg-success'
                                    : form.coins < 50
                                    ? 'progress-bar bg-warning'
                                    : 'progress-bar bg-danger'
                            "
                            :style="`width: ${form.coins}%`"
                            >{{form.coins}} %</div>
                        </div>
                        <p v-if="maxCoins" class="text-secondary mt-2 mb-0">{{maxCoins}}</p>
                    </div>

                    <!--box colores-->
                    <div class="d-flex flex-wrap justify-content-start my-4">
                        <div class="bg-warning p-3 fs-4" style="flex: 1 1 30%;">
                            <p>% de finalización del juego</p>
                            <hr>
                            <p class="fs-5">17%><i class="bi bi-star-half"></i> </p>
                        </div>
                        <div class="bg-success p-3 fs-4" style="flex: 1 1 30%;">
                            <p class="fs-5">Logros en el juego</p>
                            <hr>
                            <p>166<i class="bi bi-trophy-fill ms-2"></i></p>
                        </div>
                        <div class="bg-info p-3 fs-4" style="flex: 1 1 30%;">
                            <p class="fs-5">Recompensas</p>
                            <hr>
                            <p>200 🥈</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "AdminView",
    data() {
        return {
            form: {
                name: '',
                password: '',
                coins: 0,
            },
            showForm: true,
            isFormValid: false,
            maxCoins: 'Llegaste al maximo de tu credito',
        };
    },
    methods: {
        onSubmit(event) {
            event.preventDefault();
            if (this.form.name && this.form.password) {
                this.isFormValid = true;
                this.showForm = false;
            } else {
                alert("Debes ingresar todos los datos.");
            }
        },
        addCoins() {
            if (this.form.coins < 60) {
                this.form.coins += 5;
            }
        },
    },
    
};
</script>










<style>
aside {
    min-height: 100vh;
}
    aside img {
        width: 100px;
        display: block;
    }
</style>