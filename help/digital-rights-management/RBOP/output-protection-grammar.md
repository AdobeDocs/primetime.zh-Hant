---
description: 本節涵蓋設定輸入的文法，強調有效及無效的輸入選項，並說明如何解譯省略的選用欄位。
title: RBOP文法
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# RBOP文法 {#rbop-grammar}

本節涵蓋設定輸入的文法，強調有效及無效的輸入選項，並說明如何解譯省略的選用欄位。

以解析度為基礎的輸出保護文法定義為一連串規則，每個規則可以有多個有效的形式：

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## 套用文法規則 {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>為了協助改善文法的可讀性，下列屬性並未反映在文法中，但仍成立：

1. 物件中定義的配對順序不是固定的；因此，配對的任何排列都是有效的。

   例如，如果我們定義一個物件，如下所示：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   則以下結構也視為有效： =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. 對於物件內的每個配對，假設給定物件的給定執行個體內只存在該配對的1個執行個體。

   例如，如果我們定義一個物件，如下所示：

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   則下列例項會無效，因為其中有兩項 `foo` 在相同物件中的配對：

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

1. 對於可能選擇一或多個字串序列的定義，請將字串視為集合，其中重複專案視為單一專案。 例如， `["foo", "bar", "foo", "baz"]` 相當於 `["foo", "bar", "baz"]`

1. 定義數字時，規則之間會使用空格， `Digit Digits`)，但套用規則時不應使用這類空格。

   例如，如果我們表示數字 *一百二十三* 根據NonZeroInteger規則，其應表示為 `123` 而非 `1 2 3`，即使規則在NonZeroDigit和Digits之間包含空格。

1. 部分規則允許多個表單。 在這些情況下，不同的表單會由 `'|'` 字元。

   例如，此規則：

   ```
   Foo ::= "A" | "B" | "C"
   ```

   表示例項屬於 `Foo` 可取代為「A」、「B」或「C」。 請勿將此與跨越多行的表單混淆；此功能可讓較長的表單更容易閱讀。

## 語法 {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

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

## 語義：合法但無效的設定 {#section_709BE240FF0041D4A1B0A0A7544E4966}

此 *輸出保護設定範例* 主題呈現了有效的設定及其語意意義。 中的上一節 *此* 主題說明設定的文法規則。 雖然文法有助於確保語法正確，但語法上合法的設定在語義上不正確（也就是說它們不合邏輯）。 本節介紹以下組態： *語意上* 法律，但 *語義* 不正確。 請記住，本節中的範例已簡化為說明所討論情境所需的最低結構。

* 以相同的畫素計數定義多個畫素限制是無效的。

  ```
  {  
    "pixelConstraints":  
      [  
        { "pixelCount": 720 }  
      ]  
   }  
  ```

* 畫素計數不得超出指定的最大畫素解析度。

  ```
  { 
    "maxPixel": 720, 
    "pixelConstraints": 
      [ 
        {"pixelCount": 1080} 
      ] 
  } 
  ```
