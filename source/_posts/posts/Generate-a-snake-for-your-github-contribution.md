---
title: 为你的Github首页生成一条可爱的小蛇
author: 紫源君
email: 
readmore: true
date: 2022-09-11 20:42:07
updated: 
description: 
tags: Github
categories: 分享
---
### _默认样式_
<div class="box"><img src="https://raw.githubusercontent.com/Tru-tru/Tru-tru/output/github-contribution-grid-snake.svg" class="cover" alt="Tru-tru's Github Contributions" loading="eager">
</div>
<!-- more -->

---

### _暗黑蛇_ 
![github-contribution-grid-snake-dark](https://raw.githubusercontent.com/Tru-tru/Tru-tru/output/github-contribution-grid-snake-dark.svg)

### _多彩蛇_
![github-contribution-grid-snake-ocean](https://github.com/Tru-tru/Tru-tru/raw/output/github-contribution-grid-snake-ocean.svg)

### 配置方法
1. 将[配置文件](https://github.com/Tru-tru/Tru-tru/blob/main/.github/workflows/snake.yml)导入你的仓库中的<strong><code>.github/workflows</code></strong>文件夹中 ~~（没有就创建一个）~~
<details><summary>点击打开相关配置</summary>
```yml
name: generate animation

on:
  # run automatically every Monday
  schedule:
    - cron: "0 0 * * 1"
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the main branch
  push:
    branches:
      - main



jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    
    steps:
      # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v2
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
            dist/github-contribution-grid-snake-ocean.svg?color_snake=orange&color_dots=#bfd6f6,#8dbdff,#64a1f4,#4b91f1,#3c7dd9

      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
</details>

2. 在相应的你想要小蛇出现的地方，引用生成的 <strong><code>output</code></strong> 分支下的图片`raw`链接文件即可

### 原仓库链接

> https://github.com/Platane/snk

<!-- Q.E.D. -->
