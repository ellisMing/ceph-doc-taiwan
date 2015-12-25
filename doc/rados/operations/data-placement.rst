==============
 資料放置概念
==============

Ceph 透過 RADOS 叢集動態地儲存、複製與重新平均資料物件。很多不同使用者因為不同目的，來把物件儲存在不同的儲存池 pool 裡，而它們都座落於無數的OSD上，所以 Ceph 的操作要求一些資料放置的規劃。Ceph 的資料放置規劃概念主要有以下：

- **儲存池（Pool）：** Ceph 在 pools 裡面儲存資料，它是物件儲存的邏輯群組。Pools 管理著 Placement groups 的數量、replicas 的數量、pool 的 ruleset。要在 Pools 裡面存資料，使用者必須經過驗證、且具有合適權限。最後能夠建立一個快照的 pool。詳細可參考 `儲存池`_\ 。

- **放置群組（Placement Group）：** Ceph 把物件映射到放置群組（PG），PG 是一種邏輯的物件 pool 片段，這些物件會組成一個群組後，再存到 OSD 中。PG 減少了各物件存入對應的 OSD 時 metadata 的數量，更多的 PG（如：每個 OSD 有 100 個群組）可以使負載平衡更好。詳細可參考 `放置群組`_\ 。

- **CRUSH 狀態圖（CRUSH Map）：** CRUSH 是一個重要的部分，它驅使 Ceph 能伸縮自如，且沒有效能瓶頸、沒有擴展限制、沒有單點故障（SPOF）問題，它為 CRUSH 演算法提供了叢集的物理拓樸，以此來確定一個物件的資料以及它的副本應該在哪裡、如何跨故障區域的儲存，以提升資料安裝。詳細可參考 `CRUSH Map`_\ 。

起初安裝測試叢集時，可以使用預設值。但開始規劃一個大型的 Ceph 叢集，做資料放置操作的時候，會涉及 Pools、Placement Groups 與 CRUSH Maps。如果遇到難題，也可找 `Inktank`_ 來提供技術協助。


.. _儲存池: ../pools
.. _放置群組: ../placement-groups
.. _CRUSH Map: ../crush-map
.. _Inktank: http://www.inktank.com
