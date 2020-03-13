---
description: 標準化規則定義URL轉換，以套用至從VAST/VMAP回應取得的來源創意URL。
keywords: normalize rule;creative selection rules
seo-description: 標準化規則定義URL轉換，以套用至從VAST/VMAP回應取得的來源創意URL。
seo-title: 標準化規則
title: 標準化規則
uuid: e2a11466-41a3-44ba-abec-1a541df6c1a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 標準化規則{#normalize-rules}

標準化規則定義URL轉換，以套用至從VAST/VMAP回應取得的來源創意URL。

## 標準化規則具有下列屬性和可能的值：

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
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 標準化</span></td> 
   <td>值必須一律為正 <span class="codeph"> 規化</span>。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 項目</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 主機</span></td> 
   <td>目前僅支 <span class="codeph"> 援主機</span> 。 當符合併定義值屬性 <span class="codeph"> 時</span> , <span class="codeph"></span> 必須存在此屬性。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> values</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td>TVSDK會在來源創 <span class="codeph"> 作項目上使</span> 用 <span class="codeph"> 「符合」屬性</span> ，並比對此陣列中定義的值。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> find</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> 要套用至來源創意URL以符合的規則運算式。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 替換</span></td> 
   <td><span class="codeph"> regex</span></td> 
   <td></td> 
   <td> 要套用至來源創意URL以根據符合來取代的規則運算式。</td> 
  </tr> 
 </tbody> 
</table>

```
{
    "ads": {
        "rules": {
            "default": [
                {
                ...
                }
                {
                    "
<b>type</b>": "
<b>normalize</b>",
                    "
<b>item</b>": "host",
                    "
<b>matches</b>": "ew",
                    "
<b>values</b>": [
                        "redirector.gvt1.com"
                    ],
                    "
<b>find</b>": "videoplayback/(.*?)/expire/.*?/(.*?)/signature/.*?/",
                    "
<b>replace</b>": "videoplayback/$1/expire//$2/signature//"
                }                
            ]
        }
    }
}
```

