<template>
    
            <div class="col-md-8 mt-4">
                <div class="card">
                    <div class="card-header">Task Form</div>

                    <div class="card-body">
                        <form action="./api/task" method="POST" @submit.prevent="addTask">
                            <div class="form-group">
                                <input type="text" name="title" v-model="title" placeholder="task Title" class="form-control">
                                <div class="invalid-feedback" v-show="errors.title">
                                    {{getError('title')}}
                                </div>
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
                errors:[],
            }
        },
        mounted() {
            console.log('Component mounted.')
        },
        methods:{
            addTask(){
                    // display validation error from server
                    axios.post('./api/task',{title:this.title})
                    .then(function () {
                        // handle success
                        Event.$emit('refresh',{title:this.title});
                        this.title = '';
                    })
                    .catch(error=> this.errors = error.response.data.errors) 

                // if not empty take the action
                // if(this.title.trim().length > 0){
                //     axios.post('./api/task',{title:this.title});
                //     Event.$emit('refresh',{title:this.title});
                //     this.title = '';
                // }
                
            },
            getError(fieldName){
                if(this.errors[fieldName]){
                    return this.errors[fieldName][0]
                }
            }
        }
    }
</script>
<style>
    .invalid-feedback {
        display: inline;
    }
</style>
