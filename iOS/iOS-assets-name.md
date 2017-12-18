## iOS 图片资源命名规范

### 图片文件命名采用 `type_location_identifier(_state)` 规则，只需要@2x和@3x图片,不需提供1x的图。

> 示例：icon_tabbar_home_normal@2x  icon_tabbar_home_highlighted@2x 
>
> icon_profile_setting@3x 

#### type缩略前缀可用如下例子  ***必填参数***

- icon
- btn
- bg
- line
- logo
- pic
- img

#### location代码位置 功能模块 （如首页、 我的、……）***必填参数*** 

#### identifier 主要作用就是用来描述图片的用途，如一个用于设置按钮的图片，这一部分就可以写为 setting。当一个单词无法准确描述用途时，也可用多个单词采用驼峰命名 ***必填参数***

#### state是可选的，可选项是下列之一

- normal
- highlighted
- selected
- disabled



> 除了上述主要内容外，还有一些其他的基本要求：
>
> - 命名使用英文并且全小写，找不到合适英文单词时才考虑使用拼音，禁止中文字符。
> - 单词间用 _ 分隔而不是其他符号

## 相关icon apple官方推荐尺寸设置

https://developer.apple.com/ios/human-interface-guidelines/icons-and-images/app-icon/



## apple官方 人机交互设计指南

https://developer.apple.com/ios/human-interface-guidelines/overview/themes/



