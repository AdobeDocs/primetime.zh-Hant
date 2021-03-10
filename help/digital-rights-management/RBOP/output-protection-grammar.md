---
description: 本節介紹配置輸入的語法，強調有效和無效的輸入選項，並說明如何解釋省略的可選欄位。
title: RBOP語法
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---


# RBOP語法{#rbop-grammar}

本節介紹配置輸入的語法，強調有效和無效的輸入選項，並說明如何解釋省略的可選欄位。

基於解析度的輸出保護語法被定義為規則序列，其中每個規則可以有多個有效形式：

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## 應用語法規則{#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>為協助改善語法的可讀性，下列屬性不會反映在語法中，但仍然成立：

1. 對象中定義的對的順序沒有固定；因此，對的任何排列都是有效的。

   例如，如果我們定義了如下對象：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   則下列結構也會被視為有效：=

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. 對於對象內的每對，假定該對的1個實例僅存在於給定對象的給定實例內。

   例如，如果我們定義了如下對象：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   則下列實例將無效，因為同一對象中有兩對`foo`對：

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   同樣地，有兩個物件，例如：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   和：

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   有效，因為它們是相同物件的獨立例項。

1. 對於可以選擇一個或多個字串序列的定義，請將字串視為一個集，其中重複條目被視為單個條目。 例如，`["foo", "bar", "foo", "baz"]`等效於`["foo", "bar", "baz"]`

1. 在定義數字時，規則之間會使用空格（例如`Digit Digits`），但套用規則時不應使用此類空格。

   例如，如果我們根據NonZeroInteger規則表示數字&#x200B;*123*，則應將其表示為`123`，而不是`1 2 3`，即使規則包含NonZeroDigit和Digits之間的空格。

1. 有些規則允許多個表單。 在這些情況下，不同的形式會以`'|'`字元分隔。

   例如，此規則：

   ```
   Foo ::= "A" | "B" | "C"
   ```

   表示`Foo`的例項可以取代為&quot;A&quot;、&quot;B&quot;或&quot;C&quot;。 這不應與跨越多行的表格混淆；這項功能可讓更長的表格更容易閱讀。

## 語法{#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## 語義：合法但無效的配置{#section_709BE240FF0041D4A1B0A0A7544E4966}

*示例輸出保護配置*&#x200B;主題提供了有效的配置及其語義。 *this*&#x200B;主題的上一節介紹了配置的語法規則。 雖然語法有助於確保句法正確性，但有一些語法上合法的配置在語義上不正確（即，它們不是邏輯配置）。 本節介紹的配置&#x200B;*語法*&#x200B;合法，但語義&#x200B;*語義*&#x200B;不正確。 請記住，本節中的示例已簡化為說明所討論方案所需的最小結構。

* 定義具有相同像素計數的多個像素約束是無效的。

   ```
   {  
     "pixelConstraints":  
       [  
         { "pixelCount": 720 }  
       ]  
    }  
   ```

* 像素計數不得超過指定的最大像素解析度。

   ```
   { 
     "maxPixel": 720, 
     "pixelConstraints": 
       [ 
         {"pixelCount": 1080} 
       ] 
   } 
   ```
