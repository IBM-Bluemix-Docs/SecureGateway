---

copyright:
  years: 2015, 2018
lastupdated: "2018-08-10"

---

# 執行用戶端的需求

## 系統需求
{: #system}

下列環境支援「Secure Gateway 用戶端」：

| 名稱 | 版本          |
| ------------- | ----------- |
| Windows Desktop |7、8.1、10 及更高版本|
| Windows Server |2012 R2 及更高版本|
| Red Hat Linux |6.5 及更高版本|
| CentOS |7.2 及更高版本|
| SuSE Linux |11.0<sup>*</sup> 及更高版本|
| Ubuntu Linux |14.04 (LTS) 及更高版本|
| Power Machine | ppc64el 架構 |
| Ubuntu Z-Linux | - |
| AIX |7.1 及更高版本|
|Mac OS X|10.10 (Yosemite) 及更高版本|
|Docker|1.7.0 及更高版本，所有支援的作業系統|

<sup> * </sup>- SLES 11 支援僅與 Service Pack 4 搭配使用

<b>附註：</b>目前只有 64 位元環境支援原生用戶端安裝。

## 網路需求
{: #network}

「Secure Gateway 用戶端」會使用出埠的埠 443 及埠 9000 來連接至 npm 登錄及 {{site.data.keyword.Bluemix}} 環境：
- 適用於 npm 安裝的埠 443
  - 在安裝期間，安裝程式將連接至 npm 登錄，並執行 `npm install` 以安裝「Secure Gateway 用戶端」所需的相依關係。安裝之前，請確定要在其上安裝用戶端的機器可以連接至 npm 登錄網站。依預設，npm 配置成使用 npm, Inc. 的公用登錄，網址為 `https://registry.npmjs.org`。<br><br>
如果您的環境中有 npm 企業伺服器，請將 npm 企業伺服器上的所有「Secure Gateway 用戶端」相依關係都設為白名單。如需相依關係清單，請參閱 `<Installation_directory>\ibm\securegateway\client\package.json` 檔案。<br><br>

- 適用於閘道鑑別的埠 443


  |地區| 主機  |
  | --  | --  |
  | 美國南部  | sgmanager.ng.bluemix.net  |
  | 美國東部  | sgmanager.us-east.bluemix.net  |
  | 英國  | sgmanager.eu-gb.bluemix.net  |
  | 德國  | sgmanager.eu-de.bluemix.net  |
  | 雪梨  | sgmanager.au-syd.bluemix.net  |


- 埠 9000

  可在閘道配置中找到之 SG 閘道的節點，每個閘道不在相同節點上，請在每次建立閘道時，確認節點的主機名稱


請務必檢查或修改可能會適用的其他防火牆及「IP 表格」規則。如果您的網路管理者需要特定 IP，請[與支援中心聯絡，以為您的環境要求這些項目](./securegateway_troubleshooting.html#support)。


## 判定硬體需求
{: #hardware}

執行「Secure Gateway 用戶端」之機器的規格大部分取決於將通過每個連線的資料流量。每個用戶端實例都是個別的處理程序，各提供最多 250 個並行連線。若要大致估計機器需要支援的平均最大值，請判定通過用戶端的平均交易大小（要求及回應），然後將它調整為 250 個並行交易。假設此數字已結合要求及回應大小，則用戶端不應該超過這個記憶體覆蓋區。如需更精準的預估，應該使用混合的要求大小及回應大小，更恰當地模擬現實交易情境。

針對執行單一「Secure Gateway 用戶端」實例的情況，我們建議最少使用 2 個核心及 4 GB 的記憶體。

若為將在相同機器上執行多個用戶端實例的 HA 情境，我們建議最少使用 4 個核心及 8 GB 的記憶體。