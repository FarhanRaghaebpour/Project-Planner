<template>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input v-model="title" type="text" required>
    <label>Details</label>
    <textarea v-model="details"></textarea>
    <button>Add project</button>
  </form>
</template>

<script>
export default {
    data(){
        return{
            title: '',
            details: ''
        }
    },
    methods:{
        handleSubmit(){
          fetch('db.json')
            .then(res => res.json())
            .then(projects => {
              let maxId = 0;
              if(projects.length) {
                maxId = Math.max(...projects.map(p => p.id));
              }
              let project = {
                id: maxId + 1,
                title: this.title,
                details: this.details,
                complete: false
              }
              fetch('db.json',{
                method: 'POST',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify(project)
              }).then(() => {
                this.$router.push('/')
              }).catch(err => console.log(err.message))
            })
        }
    }

}
</script>

<style>
form{
    background: white;
    padding: 20px;
    border-radius: 10px;

}

label{
    display:block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
}
input{
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-align: border-box;
}
textarea{
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;

}
form button{
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
}

</style>