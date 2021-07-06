<template>
    <div>{{news}}</div>
    <comment :newsId="newsId" :userName="userName"></comment>
    <template v-if="comments != null">
        <div v-for="comment in comments"
        :key="comment.commentId">
            <a href="#">{{comment.userName}}</a>&nbsp;
            <a href="#">{{comment.date}}</a>&nbsp;
            <a href="#">[ - ]</a>
        </div> 
    </template>
</template>
<script>
import Comment from './comment.vue'

export default({
    data() {
        return {
            userName: 'siqi',
            newsId: 'news1',
            news: null,
            comments: [],
        }
    },
    components: {
        Comment
    },
    created() {
        let data = JSON.parse(localStorage.getItem(this.newsId));
        this.news = data.content;
        this.comments = data.comments;
        // console.log(this.comments)
        /*
            数据结构
            key:newsId
            value: {
                content: String,
                comments: [{
                    pId: Number,
                    commentId: Number,
                    userName: String,
                    commentContent: String,
                    date: Date,
                    reply:[{
                        pId: Number
                        commentId: Number,
                        userName: String,
                        commentContent: String,
                        date: Date,
                    }]
                },
                {
                    pId: Number,
                    commentId: Number,
                    userName: String,
                    commentContent: String,
                    date: Date,
                    reply:[{
                        pId: Number
                        commentId: Number,
                        userName: String,
                        commentContent: String,
                        date: Date,
                    }]
                }]
            }
        */
    }
})
</script>
