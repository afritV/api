<template>
<div class="container">
    <div class="form-group">
        <input type="text" @blur="saveName()" v-model="name" class="form-control" :class="{ 'is-invalid': $v.name.$error }" >
        <div class="invalid-feedback" v-if="!$v.name.required">
            Обязательное поле
        </div>
    </div>
    <div class="alert alert-danger" role="alert" v-if="errored">
        Ошибка загрузки данных
    </div>
    <div class="text-center" v-if="loading" >
        <div class="spinner-border" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>
</div>
</template>

<script>
import { required } from 'vuelidate/lib/validators'

export default {
    methods:{
        saveName(){
            this.$v.$touch()
            if(this.$v.$anyError){
                return;
            }
            axios.post('/api/desks/' +this.deskId,{
                _method:'PUT',
                name: this.name,
            } )
                .then(response =>{


                })
                .catch(error=>{
                    console.log(error)
                    this.errored = true
                })
                .finally(()=>{
                    this.loading = false
                })
        }
    },
    props:[
        'deskId'
    ],
    data(){
        return{
            name:null,
            errored:false,
            loading:true
        }
    },
    mounted() {
        axios.get('/api/desks/'+this.deskId)
            .then(response =>{
                this.name = response.data.data.name
                console.log(response)

            })
            .catch(error=>{
                console.log(error)
                this.errored = true
            })
            .finally(()=>{
                this.loading = false
            })
    },
    validations:{
        name:{
            required
        }
    }
}
</script>

