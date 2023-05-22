---
description: 本節介紹配置輸入的語法，強調有效和無效的輸入選項，並說明如何解釋省略的可選欄位。
title: RBOP語法
exl-id: 311194ec-e59b-4145-b22b-6983e212fcab
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# RBOP語法 {#rbop-grammar}

本節介紹配置輸入的語法，強調有效和無效的輸入選項，並說明如何解釋省略的可選欄位。

基於解析度的輸出保護語法被定義為規則序列，其中每個規則可以具有多個有效形式：

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## 應用語法規則 {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>為幫助提高語法的可讀性，以下屬性不會反映在語法中，但仍然保持true:

1. 對象內定義的對的順序不固定；因此，對的任何排列都是有效的。

   例如，如果我們定義了這樣的對象：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   則以下結構也視為有效：=

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. 對於對象中的每對，假定給定對象的給定實例中只存在該對的1個實例。

   例如，如果我們定義了這樣的對象：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   則以下實例將無效，因為有兩個實例 `foo` 同一對象中的對：

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   同樣，有兩個對象，例如：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   及：

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   有效，因為它們是同一對象的獨立實例。

1. 對於可以選擇一個或多個字串序列的定義，將字串視為集，在集中，重複條目被視為單個條目。 比如說， `["foo", "bar", "foo", "baz"]` 等於 `["foo", "bar", "baz"]`

1. 為了定義數字，在規則之間使用空格(例如， `Digit Digits`)，但應用規則時不應使用此空間。

   例如，如果我們表示 *一百二十三* 根據NonZeroInteger規則，它應表示為 `123` 而 `1 2 3`，即使規則包含NonZeroDigit和Digits之間的空格。

1. 有些規則允許多個表單。 在這些情況下，不同的形式被 `'|'` 字元。

   例如，此規則：

   ```
   Foo ::= "A" | "B" | "C"
   ```

   意味著 `Foo` 可以替換為&quot;A&quot;、&quot;B&quot;或&quot;C&quot;。 這不應與跨多行的表格混淆；這個功能可讓更長的表格更易讀。

## 《語法》 {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

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

## 語義：合法但無效的配置 {#section_709BE240FF0041D4A1B0A0A7544E4966}

的 *輸出保護配置示例* 主題提供了一個有效的配置及其語義。 中的上一節 *這個* 主題介紹了配置的語法規則。 雖然語法有助於確保句法正確性，但有語法上合法的配置在語義上不正確（即它們不是邏輯配置）。 本節介紹以下配置： *句法* 合法 *語義* 錯誤。 請記住，本節中的示例已簡化為說明所討論情形所需的最小結構。

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
