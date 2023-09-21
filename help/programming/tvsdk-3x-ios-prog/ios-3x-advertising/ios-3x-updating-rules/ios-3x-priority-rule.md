---
description: 優先順序規則會定義從VAST/VMAP回應中選取要播放的廣告創意的優先順序。
keywords: 優先順序規則；創意選取規則
title: 優先順序規則
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 優先順序規則 {#priority-rules}

優先順序規則會定義從VAST/VMAP回應中選取要播放的廣告創意的優先順序。

## 「優先順序」規則具有下列屬性和可能的值：

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>索引鍵</b></th> 
   <th class="entry"><b>型別</b></th> 
   <th class="entry"><b>值</b></th> 
   <th class="entry"><b>說明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 優先順序</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td> 一個小寫mime型別陣列，定義必須選取來源創意才能播放的優先順序。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 專案</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 主機</span></td> 
   <td>目前僅適用 <span class="codeph"> 主機</span> 支援。 此屬性必須存在於 <span class="codeph"> 符合</span> 和 <span class="codeph"> 值</span> 屬性已定義。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 符合</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 多個</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span>  — 等於</li> 
     <li><span class="codeph"> 新</span>  — 不等於</li> 
     <li><span class="codeph"> co</span>  — 包含</li> 
     <li><span class="codeph"> nc</span>  — 不包含</li> 
     <li><span class="codeph"> sw</span>  — 開頭為</li> 
     <li><span class="codeph"> 新</span>  — 結尾為</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 優先順序</span></td> 
   <td>值必須一律為 <span class="codeph"> 優先順序</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td> <p>TVSDK會使用 <span class="codeph"> 符合</span> 上的屬性 <span class="codeph"> 專案</span> 並將與此陣列中定義的值進行比對</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 串流</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td></td> 
   <td> <p>值可以是 <span class="codeph"> vod</span> 或 <span class="codeph"> 即時</span></p> </td> 
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
