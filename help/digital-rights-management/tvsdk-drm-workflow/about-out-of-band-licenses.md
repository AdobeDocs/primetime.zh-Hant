---
title: 帶外許可證概述
description: 帶外許可證概述
copied-description: true
exl-id: 31a9f097-74e8-41d0-9b9a-1c2a08d3e63a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 帶外許可證 {#out-of-band-licenses}

通過將許可證儲存在盤上和使用該許可證的儲存器中，也可獲得帶外許可證（不與黃金時段DRM許可證伺服器聯繫） `storeVoucher()` 的雙曲餘切值。

要在黃金時段播放加密視頻，各運行時需要獲取該視頻的許可證。 許可證包含視頻的解密密鑰，並由客戶已部署的黃金時段DRM許可證伺服器生成。

運行時通常通過向視頻的DRM元資料中指示的黃金時段DRM許可伺服器發送許可請求來獲得該許可(100) `DRMContentData` 類)。 應用程式可以通過調用 `DRMManager.loadVoucher()` 的雙曲餘切值。

`DRMManager.storeVoucher()` 允許應用程式發送其獲得的帶外許可證。 然後，運行時可以跳過許可請求過程，並使用轉發的許可來播放加密視頻。 在獲得帶外許可之前，仍需由Mighide DRM許可證伺服器生成許可證。 但是，您可以選擇在任何HTTP伺服器上托管許可證，而不是在Mighine DRM許可證伺服器上托管許可證。

`DRMManager.storeVoucher()` 還用於支援多個設備之間的許可證共用。 在黃金時段DRM 3.0之後，此功能稱為「設備域支援」。 如果您的部署支援此使用情形，則可以使用 `DRMManager.addToDeviceGroup()` 的雙曲餘切值。 如果某台電腦對給定內容具有有效的域綁定許可證，則應用程式可以使用 `DRMVoucher.toByteArray()` 方法，在其他電腦上，您可以使用 `DRMManager.storeVoucher()` 的雙曲餘切值。

## 關於設備註冊 {#about-device-registration}

建立時，所有黃金時段DRM許可證必須綁定到終端實體。 綁定是僅允許特定實體使用許可證的加密過程。 這對於防止任何任意設備都可以使用的&quot;浮動許可證&quot;是必要的。 對於黃金時段DRM要「預生成」許可證，這意味著這些預生成許可證的「目標」必須提前知道。 黃金時段DRM將其稱為「設備註冊」。

## 註冊設備 {#register-a-device}

假設您已執行了以下任務：

* 您已設定Mighine DRM伺服器SDK。
* 您已設定HTTP伺服器以發放預生成的許可證。
* 您已建立一個Mogifale應用程式來查看受保護的內容。

 設備註冊階段涉及以下操作：

1. 應用程式建立隨機生成的ID。
1. 應用程式調用 `DRMManager.authenticate()` 的雙曲餘切值。 應用程式必須在驗證請求中包含隨機生成的ID。 例如，在用戶名欄位中包括ID。
1. 步驟2中提到的操作將導致Mogine DRM向客戶伺服器發送驗證請求。 此請求包括設備證書：
   1. 伺服器從請求中提取設備證書和生成的ID並儲存。
   1. 客戶子系統預生成此設備證書的許可證，儲存它們並以將它們與生成的ID相關聯的方式授予對它們的訪問權。。
1. 伺服器以「成功」消息響應請求。
1. 應用程式儲存生成的ID。

在設備註冊後，應用程式使用生成的ID的方式與以前方案中使用設備ID的方式相同：
1. 應用程式將嘗試查找生成的ID。
1. 如果找到生成的ID，則應用程式將在下載預生成的許可證時使用生成的ID。 應用程式將將許可證發送至Mighine DRM客戶端，以供使用 `DRMManager.storeVoucher()` 的雙曲餘切值。。
1. 如果找不到生成的ID，應用程式將完成設備註冊過程。

## DRM工廠重置 {#drm-factory-reset}

當設備的用戶調用DRM出廠重置選項時，設備證書將被清除。 要繼續播放受保護的內容，應用程式必須再次完成設備註冊過程。 如果應用程式發送過時的預生成許可證，則Mighile DRM客戶端將拒絕該許可證，因為許可證已針對較舊的設備ID進行加密。

* FlashAPI: [DRMManager.resetDRMVouchers()](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/flash/net/drm/DRMManager.html#resetDRMVouchers())  — （只能響應某些不可恢復的DRM錯誤代碼而調用。）
* iOSAPI: [DRManager resetDRM](https://help.adobe.com/en_US/primetime/api/drm-apis/client/ios/interface_d_r_m_manager.html#a0dd6c9662428583196e0419d3ea69446)
* Android API: [DRMManager.resetDRM()](https://help.adobe.com/en_US/primetime/api/drm-apis/client/android/com/adobe/ave/drm/DRMManager.html#resetDRM(com.adobe.ave.drm.DRMOperationErrorCallback,%20com.adobe.ave.drm.DRMOperationCompleteCallback))
