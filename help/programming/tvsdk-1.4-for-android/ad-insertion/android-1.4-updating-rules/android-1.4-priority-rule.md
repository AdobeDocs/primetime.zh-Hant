---
description: 優先順序規則會定義廣告創作元素的優先順序，這些廣告創作元素將會從VAST/VMAP回應中選取來播放。
keywords: 優先順序規則；創意選擇規則
title: 優先順序規則
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# 優先順序規則{#priority-rules}

優先順序規則會定義廣告創作元素的優先順序，這些廣告創作元素將會從VAST/VMAP回應中選取來播放。

**表1:優先順序規則具有下列屬性和可能的值：**

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> Key</th> 
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
   <td> 小寫mime類型的陣列，它定義了必須選擇來源創作元素才能播放的優先順序。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 項目</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 主機</span></td> 
   <td>目前僅支援<span class="codeph">主機</span>。 當定義<span class="codeph">與</span>和<span class="codeph">值</span>屬性時，必須存在此屬性。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 多重</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> -等於</li> 
     <li><span class="codeph"> ne</span> - not equals</li> 
     <li><span class="codeph"> co</span> - contains</li> 
     <li><span class="codeph"> nc</span> -不包含</li> 
     <li><span class="codeph"> sw</span> -開頭為</li> 
     <li><span class="codeph"> ew</span> -結尾為</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 優先順序</span></td> 
   <td>值必須始終為<span class="codeph"> priority</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td> <p>TVSDK將使用來源創意素材的<span class="codeph">項目</span>上的<span class="codeph">符合</span>屬性，並比對此陣列中定義的值</p> </td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 串流</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td></td> 
   <td> <p>值可以是<span class="codeph"> vod</span>或<span class="codeph"> live</span></p> </td> 
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

