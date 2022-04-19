<template>
    <div class="flex mt-2 w-full">
        <input type="text" :value="message" v-on:keyup.enter="emitValue($event)" @input="updateMessage($event.target.value)" class="bg-slate-500 pl-2 rounded ml-2 w-full">
        <button @click="emitValue($event)" class="bg-slate-500 hover:bg-slate-700 text-white ml-2 rounded p-1 mr-2 text-sm w-8"><i class="fa fa-paper-plane" aria-hidden="true"></i></button>
    </div>
</template>

<script>
export default {
    name:"Submit",
    data() {
         return {
             message: ""
         }
    },
    emits: ['insert-message'],
    methods:{
        updateMessage:function(msg) {
            this.message = msg
        }, 
        emitValue(e) {
            console.log(this.message)
            if (this.message) {
                this.$emit('insert-message', this.message)
                this.message = "";
            }
        }        
    }    
}
</script>