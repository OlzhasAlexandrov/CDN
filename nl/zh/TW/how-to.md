---

copyright:
  years: 2017, 2018
lastupdated: "2018-03-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 管理 CDN

請遵循下列準則，以瞭解如何管理 CDN 配置。

## 讓 CDN 成為執行中狀態

在建立 CDN 之後，它就會出現在 CDN 儀表板上。您可以在這裡看到 CDN 名稱、「原點」、「提供者」及狀態。  

 ![對映清單擷取畫面](images/mapping_list_cname.png)

**步驟 1：**

在您訂購 CDN 之後，需要與 DNS 提供者一起配置 **CNAME**。大部分 DNS 提供者都會指示您如何設定或變更 CNAME。

   * 在此期間，您的 CDN 狀態會顯示為 **CNAME 配置**。請與 DNS 提供者聯繫，以找出變更何時生效。

   ![CNAME 配置](images/cname-config.png)  

**步驟 2：**  

在您與 DNS 提供者一起配置 CNAME 之後，隨時都可以透過從 CDN 狀態右側的「溢位」功能表中選取**取得狀態**來檢查狀態。

  ![CNAME 取得狀態](images/cname-getstatus.png)  

**步驟 3：**  

CNAME 鏈結完成後，帳戶狀態會變更為*執行中*，並且可以開始使用 CDN。

恭喜！您的 CDN 現在正在執行。  

## 停止 CDN
只有在處於「執行中」狀態時，才能停止 CDN。

**步驟 1：**  

從「溢位」功能表（CDN 狀態右側的 3 個垂直點）中，按一下「停止 CDN」。
 ![「溢位」功能表](images/stop_cdn.png)

**步驟 2：**  

即會出現較大的對話框視窗，要求確認您要停止此服務。選取**確認**以繼續。

**步驟 3：**  

大約 5 到 15 秒之後，狀態應該會變更為「已停止」


## 啟動 CDN
只有在處於「已停止」狀態時，才能啟動 CDN  

**步驟 1：**  

從「溢位」功能表（此功能表顯示為 CDN 列右側的三個點）中，按一下「啟動 CDN」。
 ![「溢位」功能表](images/start_cdn.png)

**步驟 2：**  

即會出現較大的對話框視窗，要求確認您要啟動此服務。選取**確認**以繼續。

**步驟 3：**  

如果動作成功，則對話框會出現在畫面右上角，讓您知道它已成功，並且附有時間。

**步驟 4：**  

這個步驟會將「狀態」變更為「CNAME 配置」

**步驟 5：**  

從「溢位」功能表中，按一下「取得狀態」。這個步驟會將狀態變更為「執行中」。您的 CDN 將變成可操作。

## 刪除 CDN

若要刪除 CDN，請遵循下列步驟：

**附註**：從「溢位」功能表中選取`刪除`，只會刪除 CDN，並不會刪除您的帳戶。

**步驟 1：**  

從「溢位」功能表中，按一下「刪除」。

 ![刪除 CDN「溢位」功能表](images/delete_cdn.png)

**步驟 2：**  

即會出現較大的對話框視窗，要求確認您要刪除。按一下**刪除**以繼續。

**步驟 3：**  

這個步驟會將狀態變更為「刪除中」。從溢位功能表按一下「取得狀態」，並從 CDN 清單中移除列。

## 使用「存活時間」設定內容快取時間

在您的 CDN 執行之後，即可使用「存活時間 (TTL)」設定內容快取時間。特定檔案或目錄路徑的「存活時間」指出應該快取內容多久的時間。當您建立「CDN 對映」時，已建立 3600 秒的預設廣域 TTL。

**步驟 1：**  

在 CDN 頁面上，選取您的 CDN，以帶領您前往**概觀**頁面。

**步驟 2：**  

您可以使用箭頭或透過輸入新時間來調整時間。時間值是以秒為單位指定。例如，3600 秒等於 1 小時。可選擇的 `timeToLive` 的最小值是 30 秒，而最大值是 2147483647 秒。選取**儲存**按鈕，以設定時間快取時間。

  ![新增 TTL](images/adding-path.png)

**步驟 3：**

儲存之後，您可以使用「溢位」功能表選項來**編輯**或**刪除** TTL 設定（**附註**：無法變更 TTL 的路徑。如果變更「對映」路徑，則會自動更新 TTL 路徑）。

  ![編輯或刪除 TTL](images/edit-delete-ttl-setting.png)  

  * 內容符合多個規則時，會優先採用最近新增的配置。

  * 只能針對特定檔名或目錄設定 TTL 值。不支援正規表示式，因為它們可能會造成無法預期的行為。

## 新增原點路徑詳細資料

CDN 處於 *CNAME_Configuration* 或*執行中* 狀態時，即可新增「原點路徑」詳細資料。您可以選擇提供多個「原點伺服器」的內容。例如，可以從與視訊不同的伺服器遞送照片。「原點」可以根據「主伺服器」或 Object Storage。

**附註：**CDN 會為原點伺服器進行 URL 轉換。例如，如果原點 `xyz.example.com` 新增時路徑為 `/example/*`，當使用者開啟 URL `www.example.com/example/*` 時，CDN Edge Server 會從 `xyz.example.com/*` 擷取內容。

**步驟 1：**  

在 CDN 頁面上，選取您的 CDN，以帶領您前往**概觀**頁面。  

**步驟 2：**  

選取**原點**標籤，然後選取**新增原點**按鈕。這個步驟會開啟新的對話視窗，您可以在其中配置原點。  

   ![原點新增原點](images/add-origins.png)

**步驟 3：**  

您*必須* 提供路徑。路徑*必須* 以 CDN 路徑為字首開始，如果 CDN 建立時有路徑的話。  
  例如，如果 CDN 建立時路徑為 `/examplePath`，「原點」的路徑開頭必須為字首 `/examplePath/`。您可以選擇性地提供主機標頭。  
  
   ![原點新增原點](images/add-origin-path.png)

**步驟 4：**  

選取**伺服器**或 **Object Storage**。

  * 如果您已選取**伺服器**，請以 IPv4 位址或_主機名稱_ 輸入原點伺服器。建議提供主機名稱並提供完整網域名稱 (FQDN)。視您在 CDN 建立期間選取哪個通訊協定而定，也請提供 HTTP 埠及（或）HTTPS 埠。如果您使用 HTTPS 埠，原點伺服器位址**必須**是_主機名稱_，而非 IP 位址。
  
       ![新增原點伺服器](images/add-origin-server-default.png)

  * 如果您已選取 **Object Storage**，請提供「端點」、「儲存區名稱」及 HTTPS 埠。您可以選擇性地指定可用於 CDN 服務中的副檔名。如果未指定任何項目，則容許所有副檔名。
  
       ![新增原點物件儲存空間](images/add-origin-object-storage.png)

  * 伺服器及 Object Storage 配置的**最佳化**及**快取金鑰**選項是相同的。
  
    * 從下拉功能表選擇**最佳化**選項。預設選項是**一般 Web 遞送**，或者您也可以選擇**大型檔案**或**隨選視訊**最佳化。**一般 Web 遞送**允許 CDN 提供最多 1.8GB 的內容，而**大型檔案**最佳化允許下載從 1.8GB 到 320GB 的檔案。**隨選視訊**會將您的 CDN 最佳化以便遞送分段的串流格式。[大型檔案最佳化](about.html#large-file-optimization-)和[隨選視訊](about.html#video-on-demand-)的特性說明提供進一步的資訊。
    
        ![效能配置選項](images/performance-config-options.png)
    
    * 從下拉功能表選擇**快取金鑰**選項。預設選項是 **Include-all**。如果您選取 **Include specified** 或 **Ignore specified**，您**必須**輸入要包含或忽略的查詢字串，並以空格區隔。例如，輸入 `uuid=123456` 作為單一查詢字串，或輸入 `uuid=123456 issue=important` 作為兩個查詢字串。您可以在特性說明中找到[快取金鑰查詢引數](about.html#ignore-query-args-in-cache-key-feature-)的詳細資訊。
    
        ![快取金鑰選項](images/cache-key-options.png)
    
**附註**：使用者介面所顯示的「通訊協定」和「埠」選項將符合在訂購 CDN 時所選取的值。例如，如果在訂購 CDN 時選取了 **HTTP 埠**，則在新增原點時將只會顯示 **HTTP 埠**選項。

**步驟 5：**  

選取**新增**按鈕，以新增「原點路徑」。

  **附註**：當您提供 Object Storage 原點路徑的副檔名時，URL 與原點路徑相同的 TTL 設定會將範圍設成包括所有具有這些所指定副檔名的檔案。例如，如果您建立 `/example` 的原點路徑，並指定副檔名 "jpg png gif"，則 TTL 路徑 `/example` 的 TTL 值範圍會包括 `/example` 目錄及其子目錄下的所有 JPG/PNG/GIF 檔案。

**步驟 6：**  

新增之後，您可以使用「溢位」功能表選項來**編輯**或**刪除**「原點」。

  ![編輯或刪除原點](images/edit-delete-origin.png)

## 清除已快取的內容

在您的 CDN 執行之後，即可從「供應商」的伺服器中清除已快取的內容。  

**步驟 1：**  

在 CDN 頁面上，選取您的 CDN，以帶領您前往**概觀**頁面。

**步驟 2：**  

選取**清除**標籤。

   ![清除頁面](images/purge_tab.png)

**步驟 3：**  

輸入標準 Unix 路徑語法以指出您要清除的檔案，然後選取**清除**按鈕。目前只容許清除單一檔案。

**步驟 4：**  

清除之後，活動會列在**清除活動**下。您可以使用「溢位」功能表選項，來**重做清除**，或者將路徑設為**我的最愛**。

   ![清除活動](images/purge-activity.png)

   **附註：**如果超過 15 次清除，則每 15 天都會自動修整「清除活動」。

## 更新 CDN 配置詳細資料

在您的 CDN 執行之後，即可更新 CDN 配置詳細資料。

**步驟 1：**

在 CDN 頁面上，選取您的 CDN，以帶領您前往**概觀**頁面。

**步驟 2：**  

選取**設定**標籤。即會顯示您的 CDN 配置詳細資料。

   ![「設定」標籤](images/settings-tab.png)

  對於**伺服器**，可以變更下列欄位：
   * 主機標頭
   * 原點伺服器位址
   * HTTP/HTTPS 埠
   * 提供過時內容
   * 遵循標頭
   * 最佳化選項
   * 快取查詢

  對於 **Object Storage**，可以變更下列欄位：
   * 主機標頭
   * 端點
   * 儲存區名稱
   * HTTPS 埠
   * 容許的副檔名
   * 提供過時內容
   * 遵循標頭
   * 最佳化選項
   * 快取查詢

**步驟 3：**  

更新**原點**或**其他原點**詳細資料（必要的話），然後按一下右下角的**儲存**按鈕，以更新 CDN 配置詳細資料。

   ![「儲存」按鈕](images/save-button.png)


## 配置 CDN 的 IBM Cloud Object Storage

若要充分運用 IBM Cloud Object Storage 中所儲存的物件，您必須設定儲存區中每一個物件的 "acl" 內容值（亦即，存取控制清單）來進行 "public-read" 存取。

請參閱「IBM Cloud Object Storage 開發人員中心」(https://developer.ibm.com/cloudobjectstorage/) 的「工具」小節，以安裝任何必要的用戶端或工具。本手冊假設您已安裝正式 AWS 指令行介面，其與 IBM Cloud Object Storage S3 API 相容。

下列程式碼範例示範如何使用指令行介面來設定儲存區中所有物件的 "public-read" 存取權。

```
$ export ENDPOINT="YOUR_ENDPOINT"
$ export BUCKET="YOUR_BUCKET"
$ KEYS=( "$(aws --endpoint-url "$ENDPOINT" s3api list-objects --no-paginate --query 'Contents[].{key: Key}' --output text --bucket "$BUCKET")" )
$ for KEY in "${KEYS[@]}"
  > do
  >   aws --endpoint-url "$ENDPOINT" s3api put-object-acl --bucket "$BUCKET" --key "$KEY" --acl "public-read"
  > done
```
