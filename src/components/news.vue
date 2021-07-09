<template>
    <div>{{news}}</div>
    <comment :newsId="newsId" :userName="userName"></comment>
    <show-comment v-if="comments.length != 0" :comments="comments" :userName="userName" :key="commentsNumber"></show-comment>
</template>
<script>
import Comment from './comment.vue'
import ShowComment from './showComment.vue'

export default({
    data() {
        return {
            userName: 'siqi',
            newsId: 'news1',
            news: null,
            comments: [],
            commentsNumber: 0
        }
    },
    components: {
        Comment,
        ShowComment
    },
    async created() {
        let data = await JSON.parse(localStorage.getItem(this.newsId));
        this.news = data.content;
        this.comments = data.comments;
        this.commentsNumber = data.commentsNumber
        /*
            数据结构
            {
                key:newsId
                value: {
                    content: String,
                    comments: [commentId]
                }
            }
            {
                key:commentId
                value: {
                    newsId: Number,
                    pId: Number,
                    commentId: Number,
                    userName: String,
                    commentContent: String,
                    date: Date,
                    reply:[commentId]
                }
            }

        */
    },
    methods: {
        showReplyComponent(commentId) {
            this.commentId = commentId;
            this.show = true;
        }
    }
})
</script>
