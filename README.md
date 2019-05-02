# 百度搜索链接解密 & 百度收录查询 

百度的收录情况只给具体数字，却不说哪个被收录哪个没有。所以有必要根据百度搜索将所有链接提取出来。

[这里](https://blog.stackoverflow.club/article/baidu-search-link/)记录了一些开发过程。

# 使用方法

1. 在`src/get-link.py`中把`domin`改成你自己的域名
2. 运行`python get-link.py`，会有结果打印出来

![2358](http://images.stackoverflow.club/wiki/20190502/2358)

# 坑

1. 提取加密链接
观察网页发现，所有的加密链接都在`data-tools=\'(.*?)\'`里面，使用正则提取出来即可

2. 解密链接
模拟访问该加密链接，要么会返回一个自动跳转的js，要么在header中的location给出。要跳转的链接就是我们解密后的链接。

3. 翻页
网页是压缩过的，所有的换行符都删掉了。导致正则匹配`下一页`出现很大困难。贪婪模式和非贪婪模式都不好用，目前的措施是将`</a>`强制换为`</a>\n`, 即加上换行符。或许可以考虑使用html解析器，但是要测试速度差异。

# TODO
1. 做成api开放
2. 解决 访问次数会被强制断开的问题，目前是sleep 3秒。
