## Rxjava

### 写在前面

最近一直很纠结于学习什么，想学的东西太多，苦于时间不够，于是很焦虑，人就很浮躁，跟一些朋友聊了聊，终于能稳下心态了，按照我的预想，最近先把Android相关的几个常用库的用法与原理理解下，大体的捋一遍代码，然后把Android的基础知识夯实一下，最近两年做的业务居多，基础知识不系统，所以就Android相关知识系统的学习一下。

### Start

今天首先上网找了几个关于RxJava的帖子看了下，然后打开Android Studio，添加上RxJava的依赖，准备开始观摩这个经典的库，然后按照博客里的代码敲了下，发现没有*Observable.OnSubscribe*这个东西，我就奇了怪了，然后一想是不是版本的问题，看了下博客发表的时间是16年的8月份，我添加的依赖是:
```
compile 'io.reactivex.rxjava2:rxjava:2.0.0'
```
刚接触也不知道这个是什么时候的版本，那么怎么办呢，到[RxJava的release版本](https://github.com/ReactiveX/RxJava/releases)中查找一下对应的日期就好了嘛，于是上去一查，有两个大版本号1.x和2.x在同时进行，于是猜想这2.x并不是1.x的替代升级，而是有不同的侧重点才出现的一个新分支。于是我把依赖的版本号换成1.x的，然后就可以按照博客中的姿势开始学习了。

### What

那么什么是RxJava呢，在开始学一个东西之前，不弄明白它是啥它能干啥，那完全就是在摸瞎的学习，效率也是事倍功半，于是我广集各路大神的博客总结出了自己的一个观点：

实例代码：
```
        //创建一个被观察者，用于执行任务，执行完成之后，将执行结果公布给观察者们
        Observable<String> mObservable = Observable.create(new Observable.OnSubscribe<String>() {
            @Override
            public void call(Subscriber<? super String> subscriber) {
                // 这里写被观察者要执行的任务
                //...
                // 任务进行完后，把结果返回到观察者
                subscriber.onNext("Hello World");
                subscriber.onCompleted();

            }
        });

        // 创建观察者，将观察者注册到被观察者身上后，任务执行完会回调观察者中的方法
        Observer<String> mObserver = new Observer<String>() {
            @Override
            public void onCompleted() {
                Log.e("TAG","onCompleted()");
            }
            @Override
            public void onError(Throwable e) {}
            @Override
            public void onNext(String s) {
                Log.e("TAG",s);
            }
        };
        Observer<String> mObserver2 = new Observer<String>() {
            @Override
            public void onCompleted() {
                Log.e("TAG","onCompleted()222222222222");
            }
            @Override
            public void onError(Throwable e) {}
            @Override
            public void onNext(String s) {
                Log.e("TAG",s);
            }
        };
        // 注册观察者，
        mObservable.subscribe(mObserver);
        mObservable.subscribe(mObserver2);

```


### 参考
```

> https://www.daidingkang.cc/2017/05/19/Rxjava/
> http://www.jianshu.com/p/5e93c9101dc5
