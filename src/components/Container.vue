<template>
    <div class="bg-slate-800 text-white mt-20 ml-auto mr-auto h-96 rounded-md max-w-md">
        <Header  />
        <Messages :messages="messages"  />
        <Submit  @insert-message="insertMessage" />
    </div>        
    
</template>

<script>
    import Header from "./Header.vue"
    import Messages from "./Messages.vue"
    import Submit from "./Submit.vue"
    import questions from "../data/data.json" 

    export default {
        name: "Container",
         async created() {
            this.messages = await this.fetchData();
        },        
        methods: {
            randomId() {
                return Math.random();
            },
            async insertMessage(message) {
                await this.insertToDb({message, self:true})
                const index =  Math.floor(Math.random() * (this.questions.length-1))
                await this.insertToDb({message:this.questions[index],self:false})
            },
            async fetchData() {
                const res = await fetch(`api/chats`);
                const data = await res.json()
                return data
            },
            async insertToDb({message, self}){ 
            const res = await fetch("api/chats", {
                method: 'POST',
                headers:{
                    'Content-Type': 'application/json',            
                },
                body:JSON.stringify({
                     id: this.randomId(),
                     message,
                    self})
            })

            const data = await res.json();
            this.messages = [...this.messages, data]
        }
        },
        data() {
            return {
                questions:questions,
                messages: null
            }
        },
        components: {
            Header,
            Messages,
            Submit
        }
    }
</script>