---
title: 快速入門
description: 快速入門
copied-description: true
exl-id: d29d141e-913c-4b9d-979c-91c486414071
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 快速入門 {#getting-started}

本檔案提供快速設定和部署Adobe Primetime DRM生態系統的步驟，該生態系統使用Progressive Download來發佈內容，並使用Primetime DRM Server for Protected Streaming來發佈授權。 以下指南提供每個步驟的其他詳細資訊：

* *使用Primetime DRM伺服器來保護內容*
* *使用Primetime DRM伺服器進行受保護的串流*

Primetime DRM Server for Protected Streaming是不含原始程式碼的最小功能伺服器。 如需具有完整Java來源的可修改伺服器，請參閱 *使用Primetime DRM參考實作* 指南。 如果您設定了「參照許可證」伺服器，它將取代 *設定和部署Primetime DRM Server for Protected Streaming （授權伺服器）* 步驟。

## 必要條件 {#prerequisites}

開始之前，請先完成下列工作：

* 取得兩部Windows或Linux電腦：

   * 一部電腦將成為License Server。
   * 一台電腦將成為Content Server。

* 在這兩部電腦上安裝下列應用程式：

   * Tomcat 6.0.18
   * Java 1.6

## 取得憑證 {#obtain-certificates}

SDK軟體交付後，指定的公司憑證管理員將會收到完成Adobe Primetime DRM憑證註冊程式的邀請。 如需詳細資訊，請參閱 *Primetime DRM憑證註冊指南*.

1. 管理員至少會指派一名個人擔任憑證請求者。
1. 憑證請求者會產生私密金鑰和CSR。
1. 請求者提交憑證請求。
1. 公司管理員核准該請求。
1. Adobe憑證管理員會確認提交。
1. 請求者會接收憑證、將憑證與私密金鑰繫結，然後部署憑證。 如所述。

   如需部署憑證的詳細資訊，請參閱 *部署Adobe Primetime DRM Server for Protected Streaming* 指南。
1. 每種憑證型別都必須完成步驟3到6。

   對於Primetime DRM生產版本，請求者必須針對License Server、Packaging及Transport憑證提出個別請求，這些憑證的有效期為兩年。

   使用Primetime DRM評估版或試用版的客戶只需要一個分別有效期為1年/90天的憑證。
