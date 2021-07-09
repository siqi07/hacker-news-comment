<template>
    <div>回复功能</div>
    <form id="reply" method="POST">
        <textarea name="reply" v-model="comments.content"></textarea>
        <button value="cancel" @click="cancel">cancel</button>
        <input type="button" value="reply" v-on:click="reply()">
    </form>
</template>
<script>
export default {
    props: {
        commentId: {
            type: String,
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
                pId: null,
                commentId: 0,
                userName: null,
                date: null,
                content: null,
                replyComments: []
            },
            replyComponentShow: false
        }
        /*
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
    created() {
        
    },
    methods: {
        async reply() {
            let data = await JSON.parse(localStorage.getItem(this.commentId));    //获取父节点数据
            let news = await JSON.parse(localStorage.getItem(data.newsId));
            this.comments.pId = this.commentId;
            this.comments.newsId = data.newsId;
            this.comments.userName = this.userName;
            this.comments.date = new Date();
            this.comments.commentId = "comment" + (news.commentsNumber + 1);
            data.replyComments.push(this.comments.commentId);    //父节点中添加子节点的id
            news.commentsNumber = news.commentsNumber+1;         //总的回复数+1
            // console.log(data.commentsNumber)
            await localStorage.setItem(data.newsId, JSON.stringify(news));
            await localStorage.setItem(this.commentId,JSON.stringify(data));
            await localStorage.setItem(this.comments.commentId,JSON.stringify(this.comments));
            this.reload();
        },

        cancel() {
            this.$emit('cancel', this.replyComponentShow)
        }
    }
}
</script>