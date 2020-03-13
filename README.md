# shadow--work
pcf,pcss,csm
pcf，pcss主要是来自GDC08中的软阴影技术，csm是用来对大规模场景阴影的渲染，主要是用在实验室的大型项目峨眉山的渲染中的阴影部分。
因为在家里，一直没能返回学校，所以回家以后又写了一遍代码，但是没有找到合适的场景应用，因此demo比较简单，笔记本的配置是用了6年的原价3000块的报废笔记本。

## 简介：

​	来自GDC08中的两种技术的实现与比较：

![0](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/0.png)

## pcf：

​		**对比了各种情况下的PCF的效果和效率**。

1. 普通的shadow map可以看到现在的走样情况是比较严重的，因为阴影只有1与0的区别，导致锯齿很明显。

   ![1581252257463](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcf1.png)



2. 可以使用sampler2Dshadow，来进行硬件级别的反走样。

![1581252444828](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcf2.png)



3. 3*3的点采样下的PCF。

![1581253588169](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcf3.png)







4. 加上随机旋转的点采样PCF。

   ![1581255940025](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcf4.png)





5. 集合3*3的pcf+随机旋转+线性采样

   ![1581256105808](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcf5.png)



6. 对5中的PCF稍作改进，在全部的阴影或者全部的非阴影中只是用2*2的采样核，其它地方使用3\*3的采样核，稍微提升了效率。

![1581256187233](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcf6.png)





## pcss：

​	首先是作为对比的3*3的PCF，可以明显看出来柱子的根部和头部的半影大小都是一样的。

![1581261149504](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcss1.png)



​	然后我们来看pcss，其中blocker search处的范围是16个泊松采样点。

​	lightSize = 1.0*(1.0/textureSize(shadowMapArray,0).x)。可以看出底部的半影要窄一些，然后头部的半影范围要大一些。

![1581261301205](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcss2.png)

​	下面分别是lightSize位3.0，5.0，7.0的情况，可以看出半影范围越来越大了。

![1581261502636](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcss3.png)



![1581261528325](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcss4.png)



![1581261553465](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/pcss5.png)

## csm result


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
