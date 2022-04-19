<template>
    <div class="bg-slate-800 text-white mt-20 ml-auto mr-auto h-96 rounded-md max-w-md">
        <Header />
        <Messages :messages="messages"  />
        <Submit @insert-message="insertMessage" />
    </div>        
    
</template>

<script>
    import Header from "./Header.vue"
    import Messages from "./Messages.vue"
    import Submit from "./Submit.vue"
    import questions from "../data/data.json" 

    export default {
        name: "Container",        
        methods: {
            randomId() {
                return Math.random();
            },
            insertMessage(message) {
                this.messages.push({
                    id: this.randomId,
                    message,
                    self:true
                })
                const index =  Math.floor(Math.random() * this.questions.length-1)
                //Reply message
                this.messages.push({
                    id: this.randomId,
                    message: this.questions[index],
                    self:false
                })
            }
        },
        data() {
            return {
                questions:questions,
                messages: [{
                  id: 1,  
                  message : "Hello, how are you?",
                  self: false
                }]
            }
        },
        components: {
            Header,
            Messages,
            Submit
        },
        mounted() {
            console.log("mounted")
        }
    }
</script>