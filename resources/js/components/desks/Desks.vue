<template>
<div class="container">
    <h1>Доски</h1>
    <div class="row">
        <div class="col-lg-4" v-for="desk in desks">
            <div class="card mt-3" >
                <router-link class="card-body" :to="{name:'show' , params:{deskId: desk.id}}">
                    <h5 class="card-title">{{desk.name}}</h5>
                </router-link>
                <button type="button" class="btn btn-danger mt-3" @click="deleteDesk(desk.id)">Удалить</button>
            </div>
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
export default {
    methods:{
        getAllDesk(){
            axios.get('/api/desks/')
                .then(response =>{
                    this.desks = response.data.data
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
        deleteDesk(id){
            if (confirm('Вы действительно хотите удалить доску?')){
                axios.post('/api/desks/'+id ,{
                    _method:'DELETE',
                    name: this.name,
                } )
                    .then(response =>{
                        this.desks = []
                        this.getAllDesk();
                    })
                    .catch(error=>{
                        console.log(error)
                        this.errored = true
                    })
                    .finally(()=>{
                        this.loading = false
                    })
            }

        }
    },
    data(){
        return{
            desks:[],
            errored:false,
            loading:true
        }
    },
    mounted() {
        this.getAllDesk();
    }
}
</script>


