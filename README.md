# High-Performance-Sorting-System-Parallel-Asynchronous-Computing-Analysis

# 排序演算法效能分析 (Multi-processing & Multi-threading)

本專案為旨在探討不同資料規模 ($N$) 與切割份數 ($K$) 下，單線程、多程序 (Multiprocessing) 與多線程 (Multithreading) 對排序效率的影響 。

## 🛠 開發環境
**編輯器**：Visual Studio Code (VScode) 

---

## 🚀 實作方法與執行流程

### 執行流程圖
本程式會先讀取資料夾內檔案，並根據使用者輸入的 $K$ 值切割資料，最後選擇排序方法執行。

```mermaid
graph TD
    Start([程式開始]) --> InputName[輸入檔案名稱]
    InputName --> Exist{檔案是否存在?}
    Exist -- NO --> InputName
    Exist -- YES --> InputK[輸入切成幾份 K]
    InputK --> CheckSize{份數 < 資料數?}
    CheckSize -- NO --> End([程式結束])
    CheckSize -- YES --> InputMethod[輸入方法編號]
    
    InputMethod --> M1{方法 1?}
    M1 -- YES --> RunM1[執行方法 1]
    
    InputMethod --> M2{方法 2?}
    M2 -- YES --> RunM2[執行方法 2]
    
    InputMethod --> M3{方法 3?}
    M3 -- YES --> RunM3[執行方法 3]
    
    InputMethod --> M4{方法 4?}
    M4 -- YES --> RunM4[執行方法 4]
    
    RunM1 --> Output[輸出排序後的結果]
    RunM2 --> Output
    RunM3 --> Output
    RunM4 --> Output
    Output --> End
```

## 方法說明


   方法一：對完整資料進行泡沫排序（無切割）。 

   
   方法二：將資料切割後，先分別進行泡沫排序，再做合併排序 。方法三 (Multiprocessing)：利用 multiprocessing.Pool 創建 $k$ 個進程並行            執行泡沫排序，最後進行兩兩合併排序直到完成 。 

   方法三 (Multiprocessing)：利用 multiprocessing.Pool 創建 $k$ 個進程並行執行泡沫排序，最後進行兩兩合併排序直到完成 。

   
   方法四 (Multi-threading)：為每一份切割資料創建一個 thread 執行泡沫排序，並使用 join() 等待所有線程完成後再進行合併排序 。

## 結果與討論: (單位為秒)


![系統架構圖](images/tables.png)

不同對於 N 值變化(資料筆數): 
    實驗發現在 N 值越大時，不同方法之間的時間差異越明顯。N=1 萬時，方法一、二、三、四所執行時間並無太大的差異，但在 N=10 萬開始，就可以明顯看出不同方法的時間差異。


對於 K 值變化(切成幾份): 
    資料切越多份，執行時間越短。Process 或 thread 分工執行，使效率增加，方法三的執行時間大部分比其他方法來的短。
