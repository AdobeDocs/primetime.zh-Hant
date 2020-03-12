---
description: 'null'
seo-description: 'null'
seo-title: 核准憑證（帳戶或次要管理員）
title: 核准憑證（帳戶或次要管理員）
uuid: 5b95e2e8-abe9-4aef-bcb4-9b98ba6604d1
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# 核准憑證（帳戶或次要管理員）{#approve-a-certificate-account-or-secondary-administrator}

1. 登入憑證註冊網站。
1. 選擇選 **[!UICONTROL Certificates]** 項卡。
1. 請檢閱請求，以確認請求有效。
1. 如果請求有效，請按一下 **[!UICONTROL Approve]**。

   您也可以新增評論。 系統會寄送電子郵件給請求者，指出請求已經由公司管理員之一核准。 此電子郵件的副本會傳送給公司和Adobe管理員。

1. 如果請求無效，請按一下並 **[!UICONTROL Reject]** 在確認對話框中輸入注釋。

   系統會寄送電子郵件給請求者，指出請求已被公司管理員之一拒絕。 此電子郵件的副本會傳送給公司管理員。

當管理員核准憑證請求時，Adobe會驗證請求者的身分。 Adobe會以其個人資料中列出的電話號碼聯絡申請人。

Adobe管理員會嘗試在三天內連絡申請人兩次。 如果Adobe管理員無法聯絡請求者，會留出要求回電的訊息，或提供再次呼叫的時間。 如果Adobe管理員無法聯繫到請求者，系統會傳送電子郵件給管理員。

>[!NOTE]
>
>只有帳戶和次要管理員才能更改請求者的公司電話號碼和詢問片語。

如果驗證了請求者的身份，則請求者接收包含PKCS#7檔案( [!DNL p7b])的電子郵件。

請求者可以從電子郵件正文中複製PKCS#7內容，並將其保存到檔案或使用附加到電子郵件的檔案。 Adobe建議在保存PKSC#7檔案時，使用用於生成私鑰和CSR檔案的基本名稱。

>[!NOTE]
>
>發送給請求者的檔案只包含證書。 檔案不包含私密金鑰資訊。

