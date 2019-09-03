# enilu Blog

 本博客模板克隆自：https://github.com/qiubaiying/qiubaiying.github.io
 感谢[qiubaiying](https://github.com/qiubaiying)

 ## 备忘
 这里说明本博客做的特殊调整
 - 博客使用了gittalk做评论插件，需要针对每篇博客创建issue来保存评论，建立issue的时候需要根据url来做issue的标签label。但是github的label长度有限制，因此本博客issue的label都截取url标题的前四十位，如下所示：
 	```
	http://reading.enilu.cn/2019/09/01/如何阅读一本书/
	上面url encoder后内容为：
	http://reading.enilu.cn/2019/09/01/%E5%A6%82%E4%BD%95%E9%98%85%E8%AF%BB%E4%B8%80%E6%9C%AC%E4%B9%A6-%E8%AF%BB%E4%B9%A6%E7%AC%94%E8%AE%B0/
	则取其日期(2019/09/01/)之后的前40位做issue的label：
	%E5%A6%82%E4%BD%95%E9%98%85%E8%AF%BB%E4%
	同时修改了_layouts/post.html中的gittalk id取值方式：
	id: (location.pathname).split("/")[4].substring(0, 40)
	```
## License

遵循 MIT 许可证。有关详细,请参阅 [LICENSE](https://github.com/qiubaiying/qiubaiying.github.io/blob/master/LICENSE)。
