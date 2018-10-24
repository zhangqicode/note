一个有趣的 iOS 项目 [Changeset](https://github.com/osteslag/Changeset)

主要功能是计算两个数组之间的元素差异，即如何从一个数组经过一系列最小化的操作变为另一个数组。

定义了一组操作：additions, deletions, substitutions, and moves，即增加、删除、替换、移动四种操作。

输入一个原数组，一个目标数组，输出的是一个操作集使得，原数组变为目标数组。

主要使用场景是 tableview 或 collectionview 数据集变化后，给界面提供动画效果。项目中还提供了 UIKit 的扩展，可以很方便的让 tableView 和 collectionView 使用操作集实现动画变更。

项目是用 swift 写成的，代码中的核心是，如何比较两个数组并产生最小化的操作集。

这个问题与最小公共子序列问题有一定的相似性，代码中的核心算法也是使用的动态规划的思路完成的。