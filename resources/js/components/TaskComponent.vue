<template>
    
            <div class="col-md-8 mt-4">
                <div class="card">
                    <div class="card-header">Task Form</div>

                    <div class="card-body">
                        <form action="./api/task" method="POST" @submit.prevent="addTask">
                            <div class="form-group">
                                <input type="text" name="title" v-model="title" placeholder="task Title" class="form-control">
                            </div>
                            <div class="form-group">
                                <input type="submit" class="btn btn-info" value="Add Task">
                            </div>    
                        </form>
                    </div>
                </div>
            </div>
       
</template>

<script>
    export default {
        data(){
            return{
                title:'',
            }
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods:{
            addTask(){
                if(this.title.trim().length > 0){
                    axios.post('./api/task',{title:this.title});
                    Event.$emit('refresh',{title:this.title});
                    this.title = '';
                }
                
            }
        }
    }
</script>
