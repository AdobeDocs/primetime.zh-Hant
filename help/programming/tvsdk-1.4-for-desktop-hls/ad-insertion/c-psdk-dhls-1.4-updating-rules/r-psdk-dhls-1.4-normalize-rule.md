---
description: 標準化規則定義URL轉換，以套用至從VAST/VMAP回應取得的來源創意URL。
keywords: 標準化規則；創意選擇規則
title: 標準化規則
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

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
   <td>值必須始終為<span class="codeph"> normalize</span>。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 項目</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 主機</span></td> 
   <td>目前僅支援<span class="codeph">主機</span>。 當定義<span class="codeph">與</span>和<span class="codeph">值</span>屬性時，必須存在此屬性。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> matches</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td>TVSDK將使用來源創意素材的<span class="codeph">項目</span>上的<span class="codeph">符合</span>屬性，並比對此陣列中定義的值。</td> 
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

