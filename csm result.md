# csm result

[TOC]

  之前的截图，在峨眉山场景中的应用。
  峨眉山远景：
  ![csmFar](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/csmFar.bmp)
  峨眉山近景：
  ![csmNear](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/csmNear.bmp)
​	因为是在家里重做的demo，没有合适的场景模型，因此做了一个场景将摄像机划分后的视锥体以及light的视锥体都可视化了出来。这样也能证明算法的正确性。


​	如下图绿色的代表视锥体，不同的视锥体之间，用绿色的深浅来区分。

![1581129926472](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/1581129926472.png)





​	然后是4个将相机视锥体包含的红色光源视锥体，光源的类型是平行光，因此投影矩阵是长方体。



![1581129989210](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/1581129989210.png)



![1581130014408](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/1581130014408.png)

![1581130055840](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/1581130055840.png)

![1581130092315](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/1581130092315.png)





​	第一个视锥下的渲染效果，与之对比的是一个固定视锥，两者光源的初始近远平面都为0.1，7.5。

​	普通的shadow map:

![1581130779706](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/1581130779706.png)

CSM：下面的4个长发形是4个连续的视锥体形成的阴影图。只不过第3个，4个的相机视锥体中没有物体，因此是无阴影的。

![1581130810304](https://github.com/cr-tg/shadow--work/blob/master/csm_pictureSet/1581130810304.png)













































