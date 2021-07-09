<template>
    <div>{{news}}</div>
    <comment :newsId="newsId" :userName="userName"></comment>
    <show-comment v-if="comments.length != 0" :comments="comments" :userName="userName" :key="commentsNumber"></show-comment>
    <!-- <div id="showComment">

    </div> -->
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
        // for (const item of data.comments) {
        //     let temp = await JSON.parse(localStorage.getItem(item))
        //     this.commentsList.push(temp);
        // }
        // console.log(this.comments)
        // this.DFS(this.commentsList)
        // console.log(this.commentsList)
        // console.log(this.comments)
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
        /* 
            深度遍历json，如果回复为空，跳出，如果回复不为空，遍历
        */
        // DFS (commentsList) {     //dom插入
        //     for (const item of commentsList) {  //遍历
        //         let html = "" 
        //         console.log(item)

        //         if(item.replyComments){    //有子节点
        //             let replyList = [];
        //             for (const item of item.replyComments) {
        //                 let temp = JSON.parse(localStorage.getItem(item))
        //                 replyList.push(temp);
        //             }
        //             this.DFS (replyList);
        //         }
        //     } 
        // }
    }
})
</script>
