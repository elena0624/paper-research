# Memory-Augmented Monte Carlo Tree Search
* [原文](https://webdocs.cs.ualberta.ca/~mmueller/ps/2018/Chenjun-Xiao-M-MCTS-aaai18-final.pdf)  
* AAAI 2018 最佳論文
#### Abstract
* 提出基於memory的monte carlo tree search(M-MCTS)，其特點是可以利用online real time的generalization。
* 每一個entry多了一個memory去儲存特定state的資訊，並基於相似state的值去估算值。
* *在一般其況下比單純的Monte Carlo表現好(???)* (The memory based value approximation is better than the vanilla Monte Carlo estimation with high probability under mild conditions.)  
* 在Go的實驗中證實，在同樣數量的模擬下M-MCTS比MCTS好。
#### Introduction
* MCTS=>從起始狀態模擬各種結果，模擬結果的平均作為該狀態的價值。
* search tree=>引導模擬的方向，*應用"老虎機理論"來平衡exploration和exploitation*。
* 缺點: 平均值不夠有效，因為在有限的時間下可能會有high variance，導致search tree越來越失效。
* 所以有很多人想辦法要改進MCTS，如用DNN加入domain knowledge建立state value function─他們把這個DNN結合MCTS提供次經驗來提升搜索效率，是有效的。
* 總結來說ML的效用成功在於generalization(ex.相似的狀態共享資訊)。而generalizationed domain knowledge通常用function approximation代表，像DNN，都是offline的train。
* 目前大部分的研究都是關於離線學習的generalization，比較少online realtime的研究，而此篇的M-MCTS就是提供online的generalization方法，並在"GO"這個game中證實有效。
* 本篇架構: 前言=>memory架構理論介紹=>M-MCTS演算法=>相關研究及實驗結果=>結論+未來展望  
#### Preliminaries
* Setting:
  * S: 狀態
  * V()(s): s狀態的value(以s狀態為起點的模擬結果的平均reward)
  * V*(s): state s的true value
  * M-MCTS目的: 讓value estimations藉由memory更準確
  * approximate value estimation: given a memory *M* 以及 state *x*
    
