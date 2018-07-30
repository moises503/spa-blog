<template>
    <div class="form-contact">
        <transition name="fade" mode="out-in">
            <p v-if="sent">Tu mensaje ha sido recibido, te contactaremos pronto.</p>
            <form v-else @submit.prevent="submit">
                <div class="input-container container-flex space-between">
                    <input v-model="form.name" placeholder="Tu nombre" class="input-name">
                    <input v-model="form.email" type="email" placeholder="Email" class="input-email">
                </div>
                <div class="input-container">
                    <input v-model="form.subject" placeholder="Asunto" class="input-subject">
                </div>
                <div class="input-container">
                    <textarea v-model="form.message" cols="30" rows="10" placeholder="Tu mensaje"></textarea>
                </div>
                <div class="send-message">
                    <button class="text-uppercase c-green" :disabled="working">
                        <span v-if="working">
                            Enviando...
                        </span>
                        <span v-else>
                            Enviar mensaje
                        </span>
                    </button>
                </div>
            </form>
        </transition>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                sent: false,
                working: false,
                form: {
                    name: 'Moises',
                    email: 'hola@moises.me',
                    subject: 'Hola que hace',
                    message: 'Hola que mira'
                }
            }
        },
        methods:{
            submit(){
                this.working = true;
                axios.post('/api/messages', this.form)
                    .then(res => {
                        this.working = false;
                        this.sent = true;
                    })
                    .catch(errors =>{
                        this.sent = false;
                        this.working = false;
                    })
            }
        }
    }
</script>