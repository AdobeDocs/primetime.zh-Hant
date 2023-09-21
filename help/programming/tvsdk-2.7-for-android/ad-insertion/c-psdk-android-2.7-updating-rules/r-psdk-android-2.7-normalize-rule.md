---
description: 標準化規則會定義URL轉換，以套用至從VAST/VMAP回應取得的來源創意URL。
keywords: 標準化規則；創意選取規則
title: 標準化規則
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 標準化規則 {#normalize-rules}

標準化規則會定義URL轉換，以套用至從VAST/VMAP回應取得的來源創意URL。

## 標準化規則有下列屬性和可能的值：

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"> 索引鍵</th> 
   <th class="entry"> 型別</th> 
   <th class="entry"> 值</th> 
   <th class="entry"> 說明</th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> type</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 標準化</span></td> 
   <td>值必須一律為 <span class="codeph"> 標準化</span>.</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 專案</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 主機</span></td> 
   <td>目前僅適用 <span class="codeph"> 主機</span> 支援。 此屬性必須存在於 <span class="codeph"> 符合</span> 和 <span class="codeph"> 值</span> 屬性已定義。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 符合</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td>TVSDK會使用 <span class="codeph"> 符合</span> 上的屬性 <span class="codeph"> 專案</span> 並將與此陣列中定義的值進行比對。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 尋找</span></td> 
   <td><span class="codeph"> 規則運算式</span></td> 
   <td></td> 
   <td> 要套用至來源創作URL的規則運算式，以比對。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> replace</span></td> 
   <td><span class="codeph"> 規則運算式</span></td> 
   <td></td> 
   <td> 根據相符專案套用至要取代的來源創意URL的規則運算式。</td> 
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
