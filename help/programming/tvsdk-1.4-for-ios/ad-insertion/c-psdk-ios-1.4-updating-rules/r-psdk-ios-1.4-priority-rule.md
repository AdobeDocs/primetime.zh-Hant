---
description: 該優先順序規則定義將從VAST/VMAP響應中選擇用於回放的廣告創意的優先順序順序。
keywords: 優先順序規則；創意選擇規則
title: 優先順序規則
exl-id: 927815fc-1910-43cc-9e83-e57e9659dd23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 優先順序規則{#priority-rules}

該優先順序規則定義將從VAST/VMAP響應中選擇用於回放的廣告創意的優先順序順序。

## 優先順序規則具有以下屬性和可能的值：

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> 鍵</th> 
   <th class="entry"> 類型</th> 
   <th class="entry"> 值</th> 
   <th class="entry"> 說明</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 優先順序</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td> 小寫mime類型的陣列，它定義了必須選擇源建立才能播放的優先順序。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 物料</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 主機</span></td> 
   <td>僅當前 <span class="codeph"> 主機</span> 支援。 當 <span class="codeph"> 匹配</span> 和 <span class="codeph"> 值</span> 屬性。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 匹配</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 多</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> 情</span>  — 等於</li> 
     <li><span class="codeph"> 紐</span>  — 不等於</li> 
     <li><span class="codeph"> 協</span>  — 包含</li> 
     <li><span class="codeph"> 數控</span>  — 不包含</li> 
     <li><span class="codeph"> 軟</span>  — 開頭</li> 
     <li><span class="codeph"> 新</span>  — 結尾</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 類型</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 優先順序</span></td> 
   <td>值必須始終為 <span class="codeph"> 優先順序</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td> <p>TVSDK將使用 <span class="codeph"> 匹配</span> 屬性 <span class="codeph"> 物料</span> 建立源，並與此陣列中定義的值匹配</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 流</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td></td> 
   <td> <p>值可以是 <span class="codeph"> 視頻</span> 或 <span class="codeph"> 活</span></p> </td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                    "
<b>type</b>": "
<b>priority</b>",
                    "
<b>stream</b>": "vod",
                    "
<b>priority</b>": [
                        "application/x-mpegurl",
                        "application/vnd.apple.mpegurl",
                        "application/x-shockwave-flash",
                        "video/mp4",
                        "video/m4v",
                        "video/x-flv",
                        "video/webm"
                    ]
                },
                {
                    ...
                },
            ]
        }
    }
}
```
