---
seo-title: 快速入門
title: 快速入門
uuid: 2002cf94-c8a7-4820-a560-6d9f7f33ee97
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# 快速入門 {#getting-started}

本檔案提供快速設定和部署Adobe Primetime DRM生態系統的步驟，該生態系統使用漸進式下載來散發內容，而Primetime DRM Server則用於受保護的串流以進行授權散發。 以下指南提供了每個步驟的其他詳細資訊：

* *使用Primetime DRM Server保護內容*
* *使用Primetime DRM Server進行受保護的串流*

Primetime DRM Server for Protected Streaming是功能最小且不包含原始碼的伺服器。 有關具有完整Java來源的可修改伺服器，請參 *閱使用Primetime DRM參考實施指南* 。 如果您設定「參考授權伺服器」，會取代「設 *定並部署Primetime DRM伺服器以進行受保護串流（授權伺服器）」步驟* 。

## 必要條件 {#prerequisites}

開始之前，請完成下列工作：

* 取得兩部Windows或Linux電腦：

   * 其中一部電腦是授權伺服器。
   * 其中一部電腦是Content Server。

* 在兩部電腦上安裝下列應用程式：

   * Tomcat 6.0.18
   * Java 1.6

## 取得憑證 {#obtain-certificates}

在SDK軟體交付後，指定的公司認證管理員將會收到完成Adobe Primetime DRM認證註冊程式的邀請。 如需詳細資訊，請參 *閱Primetime DRM憑證註冊指南*。

1. 管理員指派至少一人擔任認證請求者。
1. 證書請求者生成私鑰和CSR。
1. 請求者提交證書請求。
1. 公司管理員會核准請求。
1. Adobe認證管理員會確認提交。
1. 請求者接收證書，用私鑰綁定證書，並部署證書。 如中所述。

   如需有關部署憑證的詳細資訊，請參 *閱「部署Adobe Primetime DRM Server for Protected Streaming* 」指南。
1. 必須針對每個憑證類型完成步驟3至6。

   對於Primetime DRM Production版本，請求者必須對有效期為兩年的授權伺服器、封裝和傳輸憑證個別提出要求。

   使用Primetime DRM評估版或試用版的客戶只需要一份有效期分別為1年/90天的憑證。