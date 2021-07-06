<template>
    <div>评论功能</div>
    <form id="comment" method="POST">
        <textarea name="comment" v-model="comments.commentContent"></textarea>
        <input type="button" value="add comment" v-on:click="submit()">
    </form>
</template>
<script>

export default({
    props: {
        newsId: {
            type: Number,
            required: true
        },
        userName: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            comments: {
                pId: 0,
                commentId: 0,
                userName: null,
                date: null,
                commentContent: null,
                replyComments: []
            }
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
    },
    methods: {
        submit() {
            let data = JSON.parse(localStorage.getItem(this.newsId));
            this.comments.userName = this.userName;
            this.comments.date = new Date();
            this.comments.commentId = data.commentsNumber + 1;
            data.comments.push(this.comments);
            data.commentsNumber = data.commentsNumber+1;
            // console.log(data.commentsNumber)
            localStorage.setItem(this.newsId, JSON.stringify(data));
        }
    }
})
</script>
