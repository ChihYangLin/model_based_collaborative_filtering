# Model-based Collaborative Filtering
#### 以模型為基礎的協同過濾，是先用歷史資料得到一個模型，再用此模型進行預測，常用的有KNN最近鄰居法, SVD矩陣分解法等等。
#### 用python的surprise套件，此套件支持多個推薦的演算法模型
## 實作步驟
* 整理資料成三個欄位，顧客ID、商品ID、商品評分
  * 評分產生參考論文：大數據分析應用於零售商的推薦系統2018年/大同大學/陸建寰
  
  ![image](https://github.com/ChihYangLin/model_based_collaborative_filtering/blob/master/demo_photos/rating.png)
  
  * 固定模型找出最佳評分權重
  
  ![image](https://github.com/ChihYangLin/model_based_collaborative_filtering/blob/master/demo_photos/weight.png)

* 帶入最佳的評分權重，使用python的surprise套件，在多個模型裡，找出RMSE最小的模型。
  * SVD, SlopeOne, CoClustering, NMF, NormalPredictor, BaselineOnly, KNNBaseline等模型
  ![image](https://github.com/ChihYangLin/model_based_collaborative_filtering/blob/master/demo_photos/model_rmse.png)
  
* KNNBaseline為RMSE最小的模型，以此模型出發來調參數，來得到RMSE更小的優化模型。
  * KNNBaseline有最主要的三個參數可以調整
    * 鄰近方法: user_based(使用者) 或 item_based(商品)
    * 相似度的計算方式: cosine similarity(餘弦相似度), pearson(皮爾森相關係數), msd, pearson_baseline
    * 誤差優化：ALS(交替最小二乘法), SGD(隨機梯度下降法)
    ```
    sim_options = {'name': 'cosine', 'user_based': True}
    bsl_options = {'method': 'als', 'n_epochs': 20}
    algo = KNNBaseline(40, 1, sim_options=sim_options, bsl_options=bsl_options)
    ```
* 輸出模型














