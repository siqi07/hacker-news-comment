<template>
    <div>评论功能</div>
    <form id="comment" method="POST">
        <textarea name="comment" v-model="comments.content"></textarea>
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
    inject: ['reload'],
    data() {
        return {
            comments: {
                newsId: null,
                pId: 'comment0',
                commentId: 0,
                userName: null,
                date: null,
                content: null,
                replyComments: []
            }
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
        }
    },
    methods: {
        async submit() {
            let data = await JSON.parse(localStorage.getItem(this.newsId));
            // console.log(data);
            this.comments.newsId = this.newsId;
            this.comments.userName = this.userName;
            this.comments.date = new Date();
            this.comments.commentId = "comment" + (data.commentsNumber + 1);
            data.comments.push(this.comments.commentId);
            data.commentsNumber = data.commentsNumber+1;
            // console.log(data.commentsNumber)
            await localStorage.setItem(this.newsId, JSON.stringify(data));
            await localStorage.setItem(this.comments.commentId,JSON.stringify(this.comments));
            this.reload();
        }
    }
})
</script>
