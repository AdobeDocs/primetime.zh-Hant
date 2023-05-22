---
title: 批准證書（帳戶或輔助管理員）
description: 批准證書（帳戶或輔助管理員）
copied-description: true
exl-id: 71e647a8-e325-4095-a0ac-775fb5898e9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 批准證書（帳戶或輔助管理員）{#approve-a-certificate-account-or-secondary-administrator}

1. 登錄到證書註冊站點。
1. 選擇 **[!UICONTROL Certificates]** 頁籤。
1. 查看請求以驗證請求是否有效。
1. 如果請求有效，請按一下 **[!UICONTROL Approve]**。

   您也可以添加註釋。 向請求者發送一封電子郵件，聲明請求已經由公司管理員之一批准。 此電子郵件的副本將發送給公司和Adobe管理員。

1. 如果請求無效，請按一下 **[!UICONTROL Reject]** 並在確認對話框中輸入注釋。

   向請求者發送一封電子郵件，指出該請求已被公司管理員之一拒絕。 此電子郵件的副本將發送給公司管理員。

當管理員批准證書請求時，Adobe會驗證請求者的身份。 Adobe在其配置檔案中列出的電話號碼與請求者聯繫。

Adobe管理員嘗試在三天內兩次聯繫請求者。 如果Adobe管理員無法與請求者聯繫，則他們會留下一條請求回叫的消息，或者他們提供再次呼叫的時間。 如果Adobe管理員無法聯繫請求者，則向管理員發送電子郵件。

>[!NOTE]
>
>只有帳戶和輔助管理員才能更改請求者的公司電話號碼和質詢短語。

如果驗證了請求者的身份，則請求者將收到包含PKCS#7檔案( [!DNL p7b])。

請求者可以從電子郵件正文中複製PKCS#7內容，並將其保存到檔案，或使用附加到電子郵件的檔案。 Adobe建議在保存PKSC#7檔案時，使用用於生成私鑰和CSR檔案的基名。

>[!NOTE]
>
>發送到請求者的檔案只包含證書。 檔案不包含私鑰資訊。
