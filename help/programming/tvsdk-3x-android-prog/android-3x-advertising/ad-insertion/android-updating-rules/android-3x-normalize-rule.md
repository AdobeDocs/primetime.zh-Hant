---
description: 規範化規則定義URL轉換以應用於從VAST/VMAP響應獲得的源建立URL。
keywords: 規範化規則；創意選擇規則
title: 規範化規則
exl-id: 731e0cfd-cabd-4e34-a01e-537c23be6a2d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 規範化規則 {#normalize-rules}

規範化規則定義URL轉換以應用於從VAST/VMAP響應獲得的源建立URL。

<table id="table_ljp_tgx_hz">  
 <thead> 
  <tr> 
   <th class="entry"><b>鍵</b></th> 
   <th class="entry"><b>類型</b></th> 
   <th class="entry"><b>值</b></th> 
   <th class="entry"><b>說明</b></th>
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td><span class="codeph"> 類型</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 規範</span></td> 
   <td>值必須始終為 <span class="codeph"> 規範</span>。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 物料</span></td> 
   <td><span class="codeph"> 字串</span></td> 
   <td><span class="codeph"> 主機</span></td> 
   <td>僅當前 <span class="codeph"> 主機</span> 支援。 當 <span class="codeph"> 匹配</span> 和 <span class="codeph"> 值</span> 屬性。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 匹配</span></td> 
   <td></td> 
   <td></td> 
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
   <td><span class="codeph"> 值</span></td> 
   <td><span class="codeph"> 陣列</span></td> 
   <td></td> 
   <td>TVSDK將使用 <span class="codeph"> 匹配</span> 屬性 <span class="codeph"> 物料</span> 建立源，並與此陣列中定義的值匹配。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 查找</span></td> 
   <td><span class="codeph"> 規則運算式</span></td> 
   <td></td> 
   <td> 要應用於要匹配的源建立URL的規則運算式。</td> 
  </tr> 
  <tr> 
   <td><span class="codeph"> 替換</span></td> 
   <td><span class="codeph"> 規則運算式</span></td> 
   <td></td> 
   <td> 要應用於源建立URL以基於匹配替換的規則運算式。</td> 
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
