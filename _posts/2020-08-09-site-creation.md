---
layout: single
title: 建站说明
---

本站基于`Jekyll` 使用 [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/docs/configuration/) 主题, 并做了一些改动:

- 固定上方横幅(mast header)  参考这个[issue](https://github.com/mmistakes/minimal-mistakes/issues/490)进行修改
- 固定上方横幅导致点击 anchor 滚动的时候标题被横幅覆盖, 参考这篇[博客](https://css-tricks.com/hash-tag-links-padding/)进行修改
- 文章及其他内容的日期改为最后修改的时间, 并且时间的格式改为 `%Y-%m-%d`, 获取页面最后的修改日期的插件为: `jekyll-last-modified-at`
- 将评论后端改为 [`LiveRe`][livere], 一家韩国的提供商, 并且支持在 `_config.yml` 中进行配置

## 遇到的坑

1. **无法展示左边的 `sidebar`**   
    需要将 wiki 的内容纳入 collections 中. 方法是在在 `_config.yml` 的配置:  
    ```yml
    collections:
        wiki:
            output: true
            permalink: /:collection/:path/
    ```  
    其他设置按照[官方文档](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#sidebars)操作即可


## TODO

- [ ] 分享到中文社交平台, 如微博, 微信等


[livere]: https://livere.com/