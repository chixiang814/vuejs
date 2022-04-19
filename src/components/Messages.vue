<template>
    <div id="messageContainer" class="overflow-auto h-72">
            <div class="flex m-1 mt-3" v-for="(item) in messages" :key="item">
                <img src="../assets/ppl.jpg" alt="" v-show="!item.self" class="rounded-full mt-1 ml-2 h-8 w-8 object-cover">
                <div class="bg-slate-600 w-fit h-fit p-1 rounded-md ml-2 cursor-pointer" v-show="!item.self">{{item.message}}</div>
                <div class="bg-slate-700 w-fit h-fit p-1 rounded-md ml-auto cursor-pointer" v-show="item.self">{{item.message}}</div>
            </div>
    </div>
</template>

<script>
export default {
    name: "Messages",
    props: {
        messages:Array
    },
     methods : {
        scrollToBtm: function() {
            var container = this.$el;
            container.scrollTop = container.scrollHeight;
        }
    },updated() {
        this.scrollToBtm()
    }, mounted() {
        this.scrollToBtm()
    }
}
</script>