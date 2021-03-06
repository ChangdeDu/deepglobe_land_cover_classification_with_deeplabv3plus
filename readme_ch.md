# DeepGlobe Land Cover Classification Challenge 土地利用分类竞赛

 ## 数据集
### 数据
* 训练数据集包括803张卫星图片，RGB格式，尺寸2448 * 2448
* 图像分辨率为50cm，由 DigitalGlobe's 卫星提供
* 可通过下载页点击"Starting Kit"下载数据。
* 可通过此 [百度云链接](https://pan.baidu.com/s/1kRSHGxmaeuBqACGcFaqhvw) 下载
 ### 标注

* 每张卫星图片有一张与之对应的标注图片。这张标注图片也是RGB格式，一共分为7类，每类对应的图像(R,G,B)编码对应关系如下：
    * 城市土地： 0，255，255，浅蓝色，人造建筑（可以忽略道路）
    * 农业用地： 255，255，0，黄色，农田，任何计划中（定期）的种植、农田、果园、葡萄园、苗圃、观赏性园艺以及养殖区
    * 牧场： 255，0，255，紫色，除了森林，农田之外的绿色土地，草地
    * 森林：0，255，0，绿色，任何土地上有x%的树冠密度。
    * 水系：0，0，255，深蓝色，江河湖海湿地
    * 荒地：255，255，255, 白色，山地，沙漠，戈壁，沙滩，没有植被的地方
    * 未知土地： 0，0，0，黑色，云层遮盖或其他因素
* 卫星图片和与其对应的标注图片的命名格式为\<id>_sat.jpg和\<id>_mask.png,\<id>是一个随机的整数。
* 需要注意：
    * 由于压缩，标注图像的值可能不是准确的目标颜色值。当转换到标签时，请将每个R/G/B通道按128阈值二值化。
    * 高分辨率卫星图像的土地覆被分割仍然是一个探索性的任务，由于标注多类分割的代价很大，标签还远远不够完善。此外，我们故意不标注道路，因为它已经包含在一个单独的道路提取挑战赛中。
### 评价指标
* 我们将采用像素级别的平均IoU分数作为评价指标。
    * IoU的定义是：交集/并集，公式：  预测准确的面积/(预测准确面积 + 没有预测出来的面积 + 预测错误的面积)
    * 平均IoU由各个类别的IoU取均值得到
* 需要注意的是"未知土地"(0,0,0)并不是一个真实的类别，在这个计算中也没有起到作用。所以有效的mIoU是前6个类别IoU的均值。

## 结果展示
<table border=0>
<tr>
    <td>
        <img src="/img/6399_sat.jpg" border=0 margin=1 width=512>
    </td>
    <td>
        <img src="/img/6399_mask.png" border=0 margin=1 width=512>
    </td>
</tr>
</table>

## 致谢
该代码部分借鉴了下面这个仓库。
- [rishizek's repo tensorflow-deeplab-v3-plus](https://github.com/rishizek/tensorflow-deeplab-v3-plus)
