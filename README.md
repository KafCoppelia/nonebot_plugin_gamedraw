# nonebot_plugin_gamedraw

## 介绍
基于爬取wiki实现自动更新的抽卡插件（阴阳师爬取自官网）

  明日方舟：区分了限定，且自动更新当前的up池或即将到来的up池（包括概率提升和权值）  
  赛马娘：混合抽卡  
  原神：混合抽卡  
  坎公骑冠剑：混合抽卡  
  公主连结（国/台）：只区分了节日限定  
  碧蓝航线：区分了限定/科研（大概）  
  命运-冠位指定（FGO）：区分了限定  
  阴阳师：区分了联动限定（手动区分了...）
<br>

抓取的资料包含角色的属性等，如果你希望做一个查看角色武器资料的话或许可以帮上忙）

## 目前支持的抽卡
* 原神
* 明日方舟
* 赛马娘
* 坎公骑冠剑
* 公主连结（国/台）
* 碧蓝航线
* 命运-冠位指定（FGO）
* 阴阳师

## 命令
### 抽卡命令
'   .* ?方舟[1-9|一][0-9]{0,2}[抽|井]'    
'   .* ?原神[1-9|一][0-9]{0,2}[抽|井]'    
'   .* ?马娘卡?[1-9|一][0-9]{0,2}[抽|井]'    
'   .* ?坎公骑冠剑武?器?[1-9|一][0-9]{0,2}[抽|井]'  
'   .* ?(pcr|公主连结|公主连接|公主链接|公主焊接)[1-9|一][0-9]{0,2}[抽|井]'  
'   .* ?碧蓝航?线?(轻型|重型|特型)池?[1-9|一][0-9]{0,2}[抽]'  
'   .* ?fgo[1-9|一][0-9]{0,2}[抽]'  
'   .* ?阴阳师[1-9|一][0-9]{0,2}[抽]'  
<br>

#### 注：
赛马娘分为 赛马娘N抽（抽马），赛马娘卡N抽（抽卡）  
坎公骑冠剑分为 坎公骑冠剑N抽（角色池），坎公骑冠剑武器N抽（武器池）  
碧蓝航线分为 碧蓝航线轻型 碧蓝航线重型 碧蓝航线特型，对应3个池子  

### 其他命令
'重置原神抽卡'（重置保底）  
'重载方舟卡池'  

### 更新命令
'更新明日方舟信息'  
'更新原神信息'  
'更新赛马娘信息'  
'更新赛坎公骑冠剑信息'  
'更新pcr信息'  
'更新碧蓝航线信息'  
'更新fgo信息'  
'更新阴阳师信息'  

## 使用
  ```
  1.是否需要变更资源路径嘛？（默认路径 data/draw_card/）
    如果需要变更路径，在.env文件中添加DRAW_PATH绝对路径【注：如果你的项目开启了debug冷重载，建议更换路径！】
    示例：
      DRAW_PATH = "D:/xxx/data/draw_card/"
   
  2.是否需要关闭某些抽卡呢？（即不下载资源不使用对应抽卡命令）
    如果需要关闭某些卡池，在.env文件中添加对应的卡池FLAG并设置为False
    # 不添加或不设置默认为True
    
    PRTS_FLAG = False       # 明日方舟
    GENSHIN_FLAG = False    # 原神
    PRETTY_FLAG = False      # 赛马娘
    GUARDIAN_FLAG = False   # 坎公骑冠剑
    PCR_FLAG = False        # 公主连结
    AZUR_FLAG = False       # 碧蓝航线
    FGO_FLAG = False        # 命运-冠位指定（FGO）
    ONMYOJI_FLAG = False    # 阴阳师
  
  3.是否需要更改一些其他配置呢？（不添加或不设置默认为 False）
    在.env文件中添加对应 属性 并设置为True
    
    PCR_TAI = True          # 公主连结使用台服卡池（即添加国服未时装角色）删除原pcr.json文件再重启bot自动更新即可
    
  4.在bot入口文件添加
    nonebot.load_plugin("nonebot_plugin_gamedraw")
  ```
    
## 更新：
### 2021/5/31
  * 将 明日方舟 获取额外数据（招募方式）改为异步多任务访问
  * 为 碧蓝航线 抽卡图片添加头像外框（更清晰的显示品质）【注：若之前已存在azur.json，删除该文件重启即刻下载头像框图片（不下载抽卡也不会报错）】   
  * 每日自动更新改为异步多任务
  * 命运-冠位指定（FGO）！！！
  * 阴阳师！！！
### 2021/5/29
  * 碧蓝航线 重新区分了 限定（大部分应该都区分了）
### 2021/5/28
  * 感谢 [AdamXuD](https://github.com/AdamXuD) 的pr，修复 2021/5/27 更新后的 bug：因重复字符串 "base64://" 导致图片无法发送
  * 修复当处于Windows系统时，下载图片的名称若包含 \/:*?"<>| 导致报错（现会将字符串中的禁止字符删除）
### 2021/5/27
  * 公主连结区分国服/台服
  * 启动时下载资源改为异步多任务下载（提速！）
  * 碧蓝航线！！！
### 2021/5/26
  * 添加更改路径的配置
  * 添加卡池的开关的配置
  * 公主连结！！！
### 2021/5/24
  * 修复了明日方舟文本资料 某些角色的获取途径 含有html文本的信息
  * 坎公骑冠剑！！！
### 2021/5/23
  * 修复明日方舟卡池无法区分 商店限定 的问题 [issues #3](https://github.com/HibiKier/nonebot_plugin_gamedraw/issues/3)
### 2021/5/21
  * 将抽卡方法向py3.9以下兼容 [issues #2](https://github.com/HibiKier/nonebot_plugin_gamedraw/issues/2)
### 2021/5/19
  * 实现 [issues #1](https://github.com/HibiKier/nonebot_plugin_gamedraw/issues/1) 提供的比较完善的抽卡逻辑）感谢# [@Jerry-FaGe](https://github.com/Jerry-FaGe)
### 2021/5/18
  * 明日方舟实现爬取游戏公告自动更新当前的up卡池
  

## 注意
1.第一次启动会下载信息和图片资源<br>
2.默认资源路径是data/draw_card/  <br>
3.含有定时任务，大部分情况不需要手动触发更新命令<br>
4.若图片缺失，抽卡时则会以全黑的头像替代（一般是正式服还未上线的角色或物品）<br>
5.如果 明日方舟 更新时获取额外数据 "获取途径" 中途结束，且没有报错也没有生成prts.json，也许是网络问题，更换网络再次尝试<br>
<br>

## Todo

  * 各池子的UP（大概）

## 效果
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/0.png)
![](https://raw.githubusercontent.com/HibiKier/nonebot_plugin_gamedraw/main/docs/CM85%40%5B6TG%25%25SEZ5%24T%7DH5A73.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/1.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/2.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/3.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/5.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/6.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/prc.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/azur.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/fgo.png)
![](https://github.com/HibiKier/nonebot_plugin_gamedraw/blob/main/docs/yys.png)

