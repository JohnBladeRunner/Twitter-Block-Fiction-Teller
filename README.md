<div align="center">
   <a href="https://trendshift.io/repositories/1501" target="_blank">
      <img src="https://trendshift.io/api/badge/repositories/1501" alt="daymade%2FTwitter-Block-Porn | Trendshift" style="height: 35px;"/>
   </a>
</div>

## Twitter-Block-Porn

受不了评论区黄推了? 打开[共享黑名单](https://twitter.com/i/lists/1677334530754248706)，用 [Twitter-Block-Porn](https://greasyfork.org/zh-CN/scripts/470359-twitter-block-porn) 插件一键批量拉黑黄推，手机上也能生效，普通人拉黑受益的是自己，大V拉黑受益的是所有人。

## 功能

- 共享黑名单，一键拉黑所有黄推诈骗犯，被黄推提前拉黑了也能生效

  ![image](https://github.com/daymade/Twitter-Block-Porn/assets/4291901/b56331b2-368f-4716-b916-2654aefc9bca)

- 熟悉的小蓝鸟又飞回来了! 将 Logo 还原为 Twitter 原始的小鸟。 效果: 

  ![替换 logo](https://greasyfork.org/rails/active_storage/blobs/redirect/eyJfcmFpbHMiOnsibWVzc2FnZSI6IkJBaHBBeC9BQVE9PSIsImV4cCI6bnVsbCwicHVyIjoiYmxvYl9pZCJ9fQ==--f05c18d96183f1c8de51bcd322b9dd476e555da0/F14jEjkWIAEg3wS.png?locale=zh-CN)

## 使用方式

1. 打开脚本[主页](https://greasyfork.org/zh-CN/scripts/470359-twitter-block-porn)，安装脚本

   <img width="547" alt="image" src="https://github.com/daymade/Twitter-Block-Porn/assets/4291901/15d98829-8615-4ef7-9fbf-c2297cac8b23">

2. 用电脑打开列表，点击跳转到 [列表①](https://twitter.com/i/lists/1677334530754248706) [列表②](https://twitter.com/i/lists/1683810394287079426)，或者直接点击插件图标可以跳转到各个黑名单

   <img width="256" alt="image" src="https://github.com/daymade/Twitter-Block-Porn/assets/4291901/2cc2baa9-e116-4d91-b8fa-6c5b1be887ac">
3. 在推特**列表**的页面，点列表**封面图下方**的查看成员（members），打开列表成员弹框

   <img width="591" alt="image" src="https://github.com/daymade/Twitter-Block-Porn/assets/4291901/a7f015a1-a34f-4dc6-9ad5-46d7c8655239">

4. 在弹框的右上角有"全部屏蔽"按钮

   <img width="603" alt="image" src="https://github.com/daymade/Twitter-Block-Porn/assets/4291901/a1b5f482-f579-4764-9978-8feb0f1df970">

### 风险提示

请节制操作避免风控，建议屏蔽多个列表要间隔一段时间操作，隔天再拉黑更安全。

1. 不管是手动还是自动，如果一天 block 超过500个左右，就会被 Twitter 强制登出，需要重新登录。
2. 这个插件呢，它并没有用到任何黑科技，和手动 block 是完全一样的实现，可以理解脚本只是帮你点击了屏蔽按钮。

## Roadmap

- [ ] 短时间内屏蔽多次时提示用户隔天再操作，记录上一次屏蔽时间。
- [ ] 拉黑的批量操作改成前端入queue，在后台缓慢拉黑，期间显示进度
- [ ] 跟踪列表的更新，持续自动拉黑offset以后的新账号
- [ ] 增加举报功能

参见 [路线图](https://github.com/users/daymade/projects/3)

## 贡献方式

参见 [贡献方式.md](https://github.com/daymade/Twitter-Block-Porn/blob/master/CONTRIBUTING.md)

## 支持

### 捐助

- 💝 请我喝蜜雪冰城😋 **[buymeacoffee.com/finetuning](https://www.buymeacoffee.com/finetuning)**
- 👤 需要匿名请发送到 `0x3eccE113CA05350B2CefeE97b429EA1d3CBCd267`，我嘴很严

### 打分/评价

⭐⭐⭐⭐⭐ 在 [Greasy Fork](https://greasyfork.org/zh-CN/scripts/470359-twitter-block-porn/feedback#post-discussion) 给我打分

## 源码地址

[https://github.com/daymade/Twitter-Block-Porn](https://github.com/daymade/Twitter-Block-Porn)

方便的话给个免费的 STAR 吧 (*╹▽╹*) !

## 实现原理

1. 怎么批量 Block 账号?

   抓包可以看出来在用户点击拉黑某个账号时，会向 twitter 服务器发送 `/1.1/blocks/create.json` 请求，用 js 携带用户自己的 cookie 模拟这个请求，就可以达到自动拉黑的效果。

2. `/1.1/blocks/create.json` 需要 id 参数，怎么查询账号的 id?

   ```
   # 填入你在 https://developer.twitter.com 申请的 API KEY，替换 XXX
   export TWITTER_API_KEY="XXX"

   # 调用推特开发者 API，修改 screen_name 为你要查询的用户名，可传入多个用逗号分隔
   curl -s -X GET "https://api.twitter.com/1.1/users/lookup.json?screen_name=va77735,annegaga09" \
      -H "Authorization: Bearer $TWITTER_API_KEY" \
      | jq '[.[] | .id_str]'
   ```

3. 怎么自动识别诈骗黄推? 

   使用 https://github.com/daymade/Block-Pornographic-Replies 插件，用关键字识别

4. 怎么批量管理 twitter 的 List，自动将诈骗账号添加到 List?

    魔改了 https://github.com/daymade/Block-Pornographic-Replies 插件，代码见 https://github.com/slarkvan/Block-Pornographic-Replies/compare/main...daymade:Block-Pornographic-Replies:main

## 👨‍💻贡献者/Contributors

我们欢迎任何形式的贡献，无论是提交错误报告，提出改进意见，或者是提供代码和文档。我们都欣赏你的帮助。

贡献者列表：

<a href="https://github.com/daymade/Twitter-Block-Porn/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=daymade/Twitter-Block-Porn" />
</a>

## 致谢

- 感谢 [@奥莉𝗢𝗹𝗹𝗶𝗲](https://twitter.com/MissOllie2020) 无私捐赠一个月蜜雪冰城, 祝富婆生意兴隆, 和00后如胶似漆!
- 感谢 [Manjusaka_Lee](https://github.com/Zheaoli) 无私捐赠 50 杯蜜雪冰城, 祝老板事业有成, 单元测试全绿!
- 感谢 [@taresky](https://twitter.com/taresky) [@kefan_ManesLAB](https://twitter.com/kefan_ManesLAB) [@tennisatw](https://twitter.com/tennisatw) [@hengdm](https://twitter.com/hengdm) [@betajerks](https://twitter.com/betajerks) [@yum_707](https://twitter.com/yum_707) 等 	𝕏 友的投喂!
- 感谢 [@aoxu](https://twitter.com/Blind___Gamer) 数十日如一日提供了很多高质量黑名单
- 感谢 [albaz64](https://github.com/albaz64) 提供了还原被替换 logo 的思路
- 感谢 [E011011101001](https://github.com/E011011101001) 的原始代码，本仓库 forked from [Twitter-Block-With-Love](https://github.com/E011011101001/Twitter-Block-With-Love)

---
李老师最可爱
<pre>
                                                                                                   
                                                                                                   
                                                                        ....*...                   
                                                                        .*,@@\..                   
            ..*......  .                ..  .   ......................*.,@@^@@..                   
            .,@@@].... .                   ..   .......*..*........ **,@@`..=@^.                   
            .=@^.[@@\`......    ........*...,]]@@@@@@@@@@@@@@@@@@]].,@@/... =@@.                   
            ..@^....,\@\....    ...**]/@@@@@/[[......*...........[\@@`....  .@@`..                 
            ..\@    ..,@@\...*.,]@@@@[`......@@.....,@@`....                .=@\....               
            ..@@    .....\@]@@@/[..........,@@@@`.*.@/\@`...                .*@@....               
            ../@        ...[*...        ...=@@*,@\.=@^*@@...                ..=@^...               
            ..@/        .....           ...@@@...\@@@...\@**                ...@@`..               
            ..\@                        ..=@@@....,[`....@@*..      ....*.**...=@\..               
            ../@                        ..=@@^............`..       ...,@@`.....@@`*               
            ..=@. ..                    ..=@.`..                    .,@@/...  ..=@\.               
            ..=@....                    ........                  ../@@`....   ..@@*               
            ..=@....    .   ............                       ..................=@^....    ....   
            ..=@^..      ...*]]]]]]*.*..                       ...................@@....    ..*.   
            ..*@^...      ...\@@@@@@@`..        .   . .   ..    .....,O@O`**......=@^....,]@@@@.   
            ...@^...    .   ...... .....         ........       . ..*@@@@@`......./@@@@/[`*.....   
  ..**.........@@...   .....*]]`..            .../@@@@@^. .         .....**.**]@@/`\@`..           
 ...\@@@`......@@...   ...*=@@@/..             ..\@@@@@`.               ...,@[.....=@^*.           
    ....[@@@@]]/@...........[/`*        ......*...,@@/..*....*..........    ...,...,@@..........   
     .........*=@/[\@@@@@/@]*..*.       ..*..]]@@@@@@@@@@@@@@@@@@\`...*.    ...*,[@@@@@@@@@@@@@.   
................@^.......... ........*]]@@@@\@^.... ........,@@@^,[@@@@\.*..      ..*@\.........   
 ......*......]]@@@@@@@@/*..    ..*,@/[..,@\@@..    .......,]/@@@@@@@@@@@...       ..@@*           
...@@@@@@@@@[[[`\@..            .*=@`..*...,[`...,]]@@@@@@@@[[[`..           . ......,@\.......    
............ ...=@..            .*.[@@@@@@@@@@@@@@/*.............            ...\@@\]]@@.......    
                *@^.........        ......  ......                            .......,\@@@@@@\].   
                .=@...../@*.         ..                                          .. ..=@^.......   
           ......=@`.]@/`*..                                                        ..=@^...       
          . ..*,]/@@/`......                                                        ..=@^...       
    ......,/@@@/`*=@....                                                        ......=@^. .       
    ..,/@@/`..*...,@^*..                                                        ...**]/@`..        
     .....      ..*\@...                                                        ...@@@@@^...       
                ...,@^..                                                        ..*,[@@@`...       
                   .\\.....*.*..                                ........,]]]*.........=@^.......   
                   .=@@@@@@@@`..                                ...**/@@/`...*...,/@@@@@\.....*.   
                    .@/[[`*... .            ..,`........        .*/@@`....      .,[[\@@@@@@@/@@*   
                    .@@*.......             ..,\@@@\*...        .,@^....   .    ................   
                    .@@@@@@@\...   .    . . ......*[@\`. . ... ..@@.    ....  ..            ..     
                    .@@@/[[[[...        .............\@`....  ..=@^*.........               .  .   
                    .=@.....    ..]`......]@@@\*.]/@@@@@^*.....=@^,]`.*,@@]`..**    ..........=`   
                    .=@^....    ..[@@]]@@/[*.*@@^@@@@/\@`......@@@@@^@@@@.[@@@@.    ...*]@@@`@@.   
                    ..@@@\`.....    ....     ..=@@@`...     ...\@`.@@@@@/...    .....*./@\.,\@@.   
                    ..@@@@@@@`*.            ....*,`*..      ........[`......    ...*@@@@@@......   
                    .*@@@@@@[\`.                                                ...,@@@@@@`.       
                    ..\@***.....                                                .. ...../@^.       
                                                                                                   
                                                                                                   </pre>