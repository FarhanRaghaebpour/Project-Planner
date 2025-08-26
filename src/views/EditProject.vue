<template>
  
<form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input v-model="title" type="text" required>
    <label>Details</label>
    <textarea v-model="details"></textarea>
    <button>Update project</button>
  </form>
</template>

<script>
export default {
    props: ['id'],
    data(){
        return{
            title: '',
            details: '',
            
        }
    },
    mounted(){
       fetch('data.json')
     .then(res => res.json())
     .then(data => console.log(data))
     .catch(err => console.error(err));
        
    },
    methods:{
        handleSubmit(){
            fetch('db.json', {
                method: 'PATCH',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify({
                    title: this.title,
                    details: this.details
                })
            }).then(() => {
                this.$router.push('/')

            }).catch(err => console.log(err.message))
        }

    }

}
</script>

<style>

</style>