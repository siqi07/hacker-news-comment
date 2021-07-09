1. 第一次运行需要添加news的初始数据,在App.vue的created()中添加
   ```
    let data = {
      content: "this is new1",
      comments: [],
      commentsNumber: 0
    };
    localStorage.setItem('news1',JSON.stringify(data));
   ```
