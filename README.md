# Yii 2 开发网站流程记录

## 一、写作缘由

比较 **ASP.NET** 和 **PHP**，限于本人爱好，显然 **PHP**。
本着“站在巨人肩膀”的原则，选择框架*framework*，加快开发速度。
接触过 [Yii](https://github.com/yiisoft/yii)，为了跟上时代，选择[Yii 2.0](https://github.com/yiisoft/yii2)的高级版本 *advanced*。

自从2015年06月开始 [Yii 2 工作环境的搭建](http://www.yiichina.com/tutorial/437)，接触 Yii 2.0 快半年，感觉需要学习的东西很多，常常忘记，可以结合做网站，把他们记下来。

另外，[yiichina](http://www.yiichina.com) 网友号召开发一个完整的 Yii 2.0 教程，github 网友 [forecho](https://github.com/forecho) 建议采用 gitbook 制作 PDF 书籍。遂想利用 gitbook + markdown 写一本简易的书籍，把更多人的智慧集合起来。

本书在 Linux 操作系统 [Deepin 15](http://www.deepin.org/) 下编译制作并测试。

## 二、本书读者

本书适合期望使用 Yii 2.0 制作 Web 网站的初级开发者，读者需要具备基础的 HTML，JS 和 CSS 知识，并且了解 PHP 基本语法，最好也懂点 bash 的基本知识。在学习的过程中，建议读者注册一个 github.com 账号，建立一个学习笔记的代码仓库。

## 三、文章结构

初步计划分为三部分。

```
第一部分 开发环境的搭建
    基础知识部分
第二部分 开发的一般过程
第三部分 优秀教程选编
附录：
	代码规范：采用yii2核心代码的规范。
	搭建vagrant虚拟机测试平台
```

## 四、本书约定

- 中文和英文间留有空格。
- 命令行中，当前用户操作使用 $ 开头，root 用户操作，用 # 开头。
- 目录和文件使用斜体，比如 *./frontend/web/index.php*
- 变量名称使用代码形式，比如 `$model`
- 一段代码后的解释采用统一形式。**解释** 二字采用加粗，后面按序排列。
- 各章节的编号，采用 `ch-x-xx.md` 形式，用法 `ch-[1,2,3]-[01-99].md` 表示第几部分该部分的第几章。

## 五、示例代码

工作较忙，源码尚未发布，敬请期待。源码地址： https://github.com/bubifengyun/code-book-yii2-dev-process
代码将会采用分章节的形式设定 tag，方便查看不同的代码。

## 六、意见及反馈

欢迎提意见。

* 在 github 项目主页开 [issue](https://github.com/bubifengyun/book-yii2-dev-process/issues)
* yiichina 的 [bubifengyun](http://www.yiichina.com/user/29312)
* oschina [博客](http://my.oschina.net/bubifengyun) : http://my.oschina.net/bubifengyun
* 电子邮件：<a href="mailto:bubifengyun@sina.com?subject='Advice on book-yii2-dev-process'&body='advice'">bubifengyun@sina.com</a>
* QQ：402229566

## 七、版权声明

本书版权属于 @bubifengyun。
收编的优秀教程版权属于教程的原作者，原教程另有说明的遵守教程中的说明。
除特别声明外，本书中的内容使用 CC BY-SA 3.0 License（创作共用 署名-相同方式共享 3.0 许可协议）授权，
代码遵循 BSD 3-Clause License（3项条款的BSD许可协议）。

## 八、致谢

- [yiichina](http://www.yiichina.com) 网站的网友，感谢他们积累的丰富的教程资料，方便我更好的写作本文，
- [shi-yang](https://github.com/shi-yang/iisns/),
- [forecho](https://github.com/forecho),
- [魏曦](http://www.weixistyle.com)
- 其他没有提及到的朋友，没能在这里提上您的大名，表示由衷的歉意。

## 九、捐赠

如果您感觉本文写的不错，想给本人一点支持，除了上面的协助开发外，还可以捐赠一两块钱手机流量钱。
您的支持是将是我更新内容的一大动力，谢谢。下面分别是微信和支付宝。

<table>
<tbody>
<tr>
<td>
<img src="./images/readme_weixin.png" width="200" height="200"/>
</td>
<td>
<img src="./images/readme_zhifubao.png" width="200" height="200"/>
</td>
</tr>
</tbody>
</table>
