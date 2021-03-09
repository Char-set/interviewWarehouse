1.工作中遇到的比较难的问题，项目中比较亮的点？


2.事件循环了解么？宏任务，微任务？单线程，为什么？怎么解决非阻塞问题（事件循环）？

    async function async1(){
        console.log('async1 start')
        await async2()
        console.log('async1 end')
    }

    async function async2(){
        console.log('async2')
    }

    console.log('script start')

    setTimeout(function(){
        console.log('setTimeOut')
    }, 0)

    async1()

    new Promise(function(resolve){
        console.log('promise1') 
        resolve()
    }).then(function(){
        console.log('promise2') 
    })

    console.log('script end')


3.现在有这么一个场景, 一个历史⻚面, 上面有若干按钮等点击逻辑, 每个按钮都有自己的click事件。现在新需求来了, 突然给每一个访问用户添加了banned这个属性, 如果为true, 则代表此用户被封禁了。被封禁用户不可操作⻚面上的任何内容, 点击⻚面内的任何一处, 都弹窗提示您已被封禁

    document.addEventListener('click',function(e) {

        if(banned) {
            alert('您已被封禁');e.stopPropagation();e.preventDefault();
        }

    },true)


4.防抖、节流用过么？什么是防抖、节流？工作中哪里用过么？


5.Promise



6.浏览器的缓存机制？

    缓存位置：

        Service Worker
        Memory Cache
        Disk Cache
        Push Cache

    缓存头、强缓存：



        Expires：缓存过期时间，用来指定资源到期的时间，是服务器端的具体的时间点

            会依赖本地时间，如果修改了本地时间，可能会造成缓存失效

        Cache-Control：

            max-age：max-age=xxx (xxx is numeric)表示缓存内容将在xxx秒后失效

            public：所有内容都将被缓存（客户端和代理服务器都可缓存）。

            s-maxage（单位为s)：同max-age作用一样，只在代理服务器中生效（比如CDN缓存）。比如当s-maxage=60时，在这60秒中，即使更新了CDN的内容，浏览器也不会进行请求。max-age用于普通缓存，而s-maxage用于代理缓存。s-maxage的优先级高于max-age。如果存在s-maxage，则会覆盖掉max-age和Expires header。

        
        Expires和Cache-Control两者对比：

            其实这两者差别不大，区别就在于 Expires 是http1.0的产物，Cache-Control是http1.1的产物，两者同时存在的话，Cache-Control优先级高于Expires；在某些不支持HTTP1.1的环境下，
            Expires就会发挥用处。所以Expires其实是过时的产物，现阶段它的存在只是一种兼容性的写法。
            强缓存判断是否缓存的依据来自于是否超出某个时间或者某个时间段，而不关心服务器端文件是否已经更新，这可能会导致加载文件不是服务器端最新的内容，那我们如何获知服务器端内容是否已经发生了更新呢？此时我们需要用到协商缓存策略。
    
    协商缓存：

        Last-Modified和If-Modified-Since

            浏览器在第一次访问资源时，服务器返回资源的同时，在response header中添加 Last-Modified的header，值是这个资源在服务器上的最后修改时间，浏览器接收后缓存文件和header；

            Last-Modified: Fri, 22 Jul 2016 01:47:00 GMT

            浏览器下一次请求这个资源，浏览器检测到有 Last-Modified这个header，于是添加If-Modified-Since这个header，值就是Last-Modified中的值；服务器再次收到这个资源请求，会根据 If-Modified-Since 中的值与服务器中这个资源的最后修改时间对比，如果没有变化，返回304和空的响应体，直接从缓存读取，如果If-Modified-Since的时间小于服务器中这个资源的最后修改时间，说明文件有更新，于是返回新的资源文件和200


        ETag和If-None-Match

            Etag是服务器响应请求时，返回当前资源文件的一个唯一标识(由服务器生成)，只要资源有变化，Etag就会重新生成。浏览器在下一次加载资源向服务器发送请求时，会将上一次返回的Etag值放到request header里的If-None-Match里，服务器只需要比较客户端传来的If-None-Match跟自己服务器上该资源的ETag是否一致，就能很好地判断资源相对客户端而言是否被修改过了。如果服务器发现ETag匹配不上，那么直接以常规GET 200回包形式将新的资源（当然也包括了新的ETag）发给客户端；如果ETag是一致的，则直接返回304知会客户端直接使用本地缓存即可。

    缓存机制：

        强制缓存优先于协商缓存进行，若强制缓存(Expires和Cache-Control)生效则直接使用缓存，若不生效则进行协商缓存(Last-Modified / If-Modified-Since和Etag / If-None-Match)，协商缓存由服务器决定是否使用缓存，若协商缓存失效，那么代表该请求的缓存失效，返回200，重新返回资源和缓存标识，再存入浏览器缓存中；生效则返回304，继续使用缓存。

7.浏览器输入URL后发生了什么

    合成url

    DNS域名解析

    建立TCP链接，三次握手

    发送HTTP请求，服务器处理请求，返回结果

    关闭TCP链接，四次挥手

    浏览器解析相应结果



6.new 操作符具体干了什么

    新建一个obj = {};

    将这个对象的constructor指向构建函数，为这个对象的_proto_ = 构造函数的 prototype

    用call Func.call(obj)，改变this指向

    返回 this;