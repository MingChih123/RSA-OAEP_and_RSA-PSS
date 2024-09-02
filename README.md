# 資訊安全
主題：RSA-OAEP 跟 RSA-PSS 先加密再簽名 與 先簽名後加密  
組員：  
1102924 李名智  
1102932 林微訢  
1102943 顏莉諭  
1102966 邱翊銨  
1103478 林虹佑  
## 摘要
本專案主要介紹RSA-OAEP 跟 RSA-PSS，以python實作、比較先簽名在加密以及先加密再簽名之差別。
## Optimal Asymmetric Encryption Padding(OAEP) 概念
OAEP 是一種費斯妥演算法，他透過添加隨機性元素將確定性方案（傳統 RSA）轉變成機率性方案，且確保對手無法反轉陷門單向排列，所以無法恢復明文的任一部份，也不會造成資訊洩漏。  

## Probabilistic signature scheme（PSS）概念
PSS 是由 RSASA（RSA 數字簽名法）演化而來，因為 RSASA 容易被選擇密文攻擊，所以加入 padding 讓明文的轉換多一些隨機性，讓它比較沒辦法被預測。  
由於此簽章方案使用隨機數據，因此輸入的兩個簽名是不同的，並且都可以用來驗證原始資料，且 PSS 無法從簽章中恢復原來的簽章。   
它的特性有：  
1. 是隨機的，因此每次都會產生不同的簽名值。  
2. 無法從 PSS 簽名中提取訊息摘要值，只能根據已知的訊息進行驗證。  
3. PSS 具有安全性證明且比 PKCSV1_5 更健壯。

## RSA-OAEP 跟 RSA-PSS 先簽名再加密 
### 實作流程
![image](https://github.com/user-attachments/assets/19ef0d1b-b3ee-4766-8ba8-0df3cdc677ef)
[圖片來源](https://www.yisu.com/jc/457729.html)
### 實作結果圖
![image](https://github.com/user-attachments/assets/b37fa48e-75fd-4e21-b966-7d48f1792015)

## RSA-OAEP 跟 RSA-PSS 先加密再簽名
### 實作流程
![image](https://github.com/user-attachments/assets/688c21a1-e586-4de2-8c7f-606fc025722f)
[圖片來源](https://www.yisu.com/jc/457729.html)
### 實作結果圖
![image](https://github.com/user-attachments/assets/7a2dedd2-42cf-4205-8ffa-9b547f75879e)

## 比較差異
### 先簽名再加密
- 分塊加密(因明文簽署後長度太長)
- 確保訊息在傳輸過程中不被竄改且來源可信
- 傳統上是使用這一種
### 先加密再簽名
- 要很信任傳輸渠道安全

若主要關注訊息的機密性，並且信任傳輸渠道安全，則可以先加密再簽名。  
傳統上，數位簽名是基於明文訊息生成的，因為簽名是用來驗證訊息完整性和來源的真實性。  
對密文進行簽名可能會導致一些安全風險，例如可能泄露加密密鑰或者導致安全性降低。  
為了確保安全性和避免潛在的風險，傳統上仍然建議在加密之前對明文進行簽名，而不是對密文進行簽名。  
