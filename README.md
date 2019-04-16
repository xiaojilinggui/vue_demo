# vue_demo

> A Vue.js project

## 更新内容

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# 安装PubSub
npm install --save pubsub-js

使用PubSub 制作删除
详细地址https://www.npmjs.com/package/pubsub-js

PubSubJS具有同步解耦，因此主题是异步发布的。这有助于保持程序的可预测性，因为在消费者处理主题时，不会阻止主题的创建者。
Basic example
// create a function to subscribe to topics
var mySubscriber = function (msg, data) {
    console.log( msg, data );
};
 
// add the function to the list of subscribers for a particular topic
// we're keeping the returned token, in order to be able to unsubscribe
// from the topic later on
var token = PubSub.subscribe('MY TOPIC', mySubscriber);
 
// publish a topic asynchronously
PubSub.publish('MY TOPIC', 'hello world!');
 
// publish a topic synchronously, which is faster in some environments,
// but will get confusing when one topic triggers new topics in the
// same execution chain
// USE WITH CAUTION, HERE BE DRAGONS!!!
PubSub.publishSync('MY TOPIC', 'hello world!');

 mounted(){
    //订阅消息 箭头函数指向this
    PubSub.subscribe('deleteTodo',(msg,index)=>{
      this.deleteTodo(index)
    })
  },

deleteItem(){
      const{todo,index,deleteTodo} = this
      if(window.confirm(todo.title)){
        // deleteTodo(index)
        //发布消息
        PubSub.publish('deleteTodo',index)
      }
    }