<template>
    
            <div class="col-md-8 mt-4">
                <div class="card">
                    <div class="card-header">Task list</div>

                    <div class="card-body">
                        <ul>
                            <li v-for="task in tasks" :key="task.index">{{task.title}}</li>
                        </ul>
                    </div>
                </div>
            </div>
       
</template>

<script>
    export default {
        data(){
            return{
                tasks:[],
            }
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods:{
            
        },
        created(){
            Event.$on('refresh',(title)=>{
                this.tasks.push(title)
                //axios.get('./api/task').then(response => this.tasks = response.data)
            })
            axios.get('./api/task').then(response => this.tasks = response.data)        
                         
            
        }
    }
</script>
