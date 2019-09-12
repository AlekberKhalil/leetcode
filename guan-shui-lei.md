# 灌水类

[Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water)   和 [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water)   ii

都是不断找最低点做标杆开始（二维就是左右，四维就是所有外围边），再和标杆的右边/左边/四维比较，有更低点，res+=高度差. 同时更新标杆为更大值。

二维2个标杆，四维始终一堆外围做标杆。围水需要边界，就是标杆存在意义。

可以发现继续比较下去的**标杆**都是取更大的Height. 只有高度差累积，没有\*宽度，所以宽度都是算1这个情况

