# Memory-Augmented Monte Carlo Tree Search
* [原文](https://webdocs.cs.ualberta.ca/~mmueller/ps/2018/Chenjun-Xiao-M-MCTS-aaai18-final.pdf)  
* AAAI 2018 最佳論文
#### Abstract
* 提出基於memory的monte carlo tree search(M-MCTS)，其特點是可以利用online real time的generalization。
* 每一個entry多了一個memory去儲存特定state的資訊，並基於相似state的值去估算值。
* *在一般其況下比單純的Monte Carlo表現好(???)*
* 在Go的實驗中證實，在同樣數量的模擬下M-MCTS比MCTS好。
