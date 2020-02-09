---
typora-copy-images-to: pcfAndPcss_pictureSet
---

# pcfAndPcss result

## 简介：

​	来自GDC08中的两种技术的实现与比较：

![0](https://github.com/cr-tg/shadow--work/blob/master/pcfAndPcss_pictureSet/0.png)

## pcf：

​		**对比了各种情况下的PCF的效果和效率**。

1. 普通的shadow map可以看到现在的走样情况是比较严重的，因为阴影只有1与0的区别，导致锯齿很明显。

   ![1581252257463](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcf1.png)



2. 可以使用sampler2Dshadow，来进行硬件级别的反走样。

![1581252444828](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcf2.png)



3. 3*3的点采样下的PCF。

![1581253588169](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcf3.png)







4. 加上随机旋转的点采样PCF。

   ![1581255940025](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcf4.png)





5. 集合3*3的pcf+随机旋转+线性采样

   ![1581256105808](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcf5.png)



6. 对5中的PCF稍作改进，在全部的阴影或者全部的非阴影中只是用2*2的采样核，其它地方使用3\*3的采样核，稍微提升了效率。

![1581256187233](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcf6.png)





## pcss：

​	首先是作为对比的3*3的PCF，可以明显看出来柱子的根部和头部的半影大小都是一样的。

![1581261149504](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcss1.png)



​	然后我们来看pcss，其中blocker search处的范围是16个泊松采样点。

​	lightSize = 1.0*(1.0/textureSize(shadowMapArray,0).x)。可以看出底部的半影要窄一些，然后头部的半影范围要大一些。

![1581261301205](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcss2.png)

​	下面分别是lightSize位3.0，5.0，7.0的情况，可以看出半影范围越来越大了。

![1581261502636](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcss3.png)



![1581261528325](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcss4.png)



![1581261553465](E:\工作项目\csm\shadow--work\pcfAndPcss_pictureSet\pcss5.png)

