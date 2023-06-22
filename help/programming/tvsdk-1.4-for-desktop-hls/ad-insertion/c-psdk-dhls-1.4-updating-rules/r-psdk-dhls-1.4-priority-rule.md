---
description: 優先順序規則會定義從VAST/VMAP回應中選取要播放的廣告創意的優先順序。
keywords: 優先順序規則；創意選擇規則
title: 優先順序規則
exl-id: a045e102-1c16-46b5-8322-0bcab086ac67
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 優先順序規則{#priority-rules}

優先順序規則會定義從VAST/VMAP回應中選取要播放的廣告創意的優先順序。

## 優先順序規則具有下列屬性和可能的值：

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> 金鑰</th> 
   <th class="entry"> 型別</th> 
   <th class="entry"> 值</th> 
   <th class="entry"> 說明</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 優先順序</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td> 一個小寫MIME型別陣列，定義必須選取來源創意內容才能播放的優先順序。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 個專案</span></td> 
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
     <li><span class="codeph"> ew</span>  — 結尾為</li> 
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
   <td> <p>TVSDK會使用 <span class="codeph"> 符合</span> 上的屬性 <span class="codeph"> 個專案</span> 和符合此陣列中定義的值</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 串流</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td></td> 
   <td> <p>值可以是 <span class="codeph"> vod</span> 或 <span class="codeph"> live</span></p> </td> 
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
