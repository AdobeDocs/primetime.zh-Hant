---
description: 優先順序規則會定義廣告創作元素的優先順序，這些廣告創作元素將會從VAST/VMAP回應中選取來播放。
keywords: priority rule;creative selection rules
seo-description: 優先順序規則會定義廣告創作元素的優先順序，這些廣告創作元素將會從VAST/VMAP回應中選取來播放。
seo-title: 優先順序規則
title: 優先順序規則
uuid: 6aa5822a-a3c0-49b2-b25b-0308a784e405
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

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
   <td>目前僅支 <span class="codeph"> 援主機</span> 。 當符合併定義值屬性 <span class="codeph"> 時</span> , <span class="codeph"></span> 必須存在此屬性。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 多重</span></td> 
   <td>可能的值：
    <ul id="ul_tnf_2hx_hz"> 
     <li><span class="codeph"> eq</span> —— 等於</li> 
     <li><span class="codeph"> ne</span> —— 不等於</li> 
     <li><span class="codeph"> co</span> —— 包含</li> 
     <li><span class="codeph"> nc</span> —— 不包含</li> 
     <li><span class="codeph"> sw</span> —— 開始於</li> 
     <li><span class="codeph"> ew</span> —— 結尾為</li> 
    </ul></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 優先順序</span></td> 
   <td>值必須始終為優 <span class="codeph"> 先</span></td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td> <p>TVSDK會在來源創 <span class="codeph"> 作項目上使</span> 用 <span class="codeph"> 「符合」屬性</span> ，並比對此陣列中定義的值</p> </td> 
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

