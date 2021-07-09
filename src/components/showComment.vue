<template>
    <div v-for="comment in commentsList"
    :key="comment.commentId">
        <a href="#">{{comment.userName}}</a>&nbsp;
        <a href="#">{{comment.date}}</a>&nbsp;
        <a href="#" v-on:click="showSubContent(comment.commentId)">[ - ]</a>
        <p>{{comment.content}}&nbsp;<button v-on:click="showReplyComponent(comment.commentId)">reply</button></p>
        <div style="margin-left:80px">
            <show-comment v-if="comment.replyComments.length != 0" :comments="comment.replyComments" :userName="userName"></show-comment>
        </div>    
    </div>
    <reply v-if="replyComponentShow" :commentId="commentId" :userName="userName" @cancel="cancel"></reply>
</template>   
<script>
import Reply from './reply.vue'

export default {
    props: {
        comments: {
            type: Array,
            requred: true
        },
        userName: {
            type: String,
            requred: true
        }
    },
    components: {
        Reply
    },
    data() {
        return {
            commentId: null,
            replyComponentShow: false,
            commentsList: [],
            show: true
        }
    },
    async created() {
        for (const item of this.comments) {
            let temp = await JSON.parse(localStorage.getItem(item));
            this.commentsList.push(temp);
        }
    },
    methods: {
        showReplyComponent(commentId) {
            this.commentId = commentId;
            this.replyComponentShow = true;
        },
        cancel (res) {
            this.replyComponentShow = res;
        },
        showSubContent (){

        }
    }
}
</script>