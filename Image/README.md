# from PIL import Image

> Image.open()
```
// 打开图片，不解释
from PIL import Image
im = Image.open("bride.jpg")
```
> Image.alpha_composite(im1, im2)
```
// 将两个图片进行融合，只有当至少有一个图包含透明部分的时候才能看出端倪，否则只能看到im2
im1 = Image.open('D:/data/pic32.PNG')
im2 = Image.open('D:/data/pic31.PNG')
image = Image.alpha_composite(im1, im2)
image.show()
```
> Image.blend(im1, im2, alpha)
```
// out = image1 * (1.0 - alpha) + image2 * alpha
// 也是一种图片融合的方法，类似于opencv中的addweighted
```
> Image.composite(image1, image2, mask)
```
// 另一种图片融合的方法
// 查看源码可知是把image1贴到image2上去，mask是控制粘贴的部位
// 相当于image2.paste(image1, None, mask)
im1 = Image.open('D:/data/pic31.PNG')
im2 = Image.open('D:/data/pic32.PNG')
mask = Image.open('D:/data/picmask.PNG')
r, g, b, a = mask.split()
image = Image.composite(im1, im2, b)
image2 = Image.composite(im1, im2, mask)
image.show()
image2.show()
```
> Image.eval(image, *args)
```
def fun(x):
    return abs(x - 255)


im1 = Image.open('D:/data/pic31.PNG')
image = Image.eval(im1, fun)
image.show()

image2 = Image.eval(im1, lambda x: abs(x-255))
image2.show()
```
> Image.merge(mode, bands)
```
// mode保存方式：参见https://pillow.readthedocs.io/en/stable/handbook/concepts.html#concept-modes
// bands通道：所有想要合并的通道
im1 = Image.open('D:/data/pic31.PNG')
r, g, b = im1.split()[:3]
image = Image.merge('RGB', (r, b, g)) # 这里特意交换了两个通道的合并顺序，测试以下
image.show()
```
> Image.new(mode, size, color=0)
```
# 初始化一块画布，默认是黑底
# size必须是(width, height)的元组， 如果是单通道的则color是一个数，否则需要以元组的形式
im1 = Image.new('1', (200, 200), 0)
im2 = Image.new('RGB', (200, 200), (0, 0, 255))
im1.show()
im2.show()
```
> Image.fromarray(obj, mode=None)
```
# 从np数组的形式获得图片，与np.asarray()相对
# 举个例子
from PIL import Image
import numpy as np
im = Image.open('hopper.jpg')
a = np.asarray(im)
im = Image.fromarray(a)
```
> Image.frombytes(mode, size, data, decoder_name='raw', *args)
```
# 先不学
```
> Image.fromstring(*args, **kw)
```
# 先不学
```
> Image.frombuffer(mode, size, data, decoder_name='raw', *args)
```
# 先不学
```
# Image 类以及方法
> .alpha_composite(im, dest=(0, 0), source=(0, 0))
```
im1 = Image.open('D:/data/pic31.PNG')
im2 = Image.open('D:/data/pic2.PNG')
im1.alpha_composite(im2)
im1.show()
// 将im2覆盖到im1上，这里不限制大小，基础画布就是im1，超过的部分不会出现在im2上
```
> .convert(mode=None, matrix=None, dither=None, palette=0, colors=256)
```
# 对图像的格式进行转化
im1 = Image.open('D:/data/pic31.PNG')
im2 = Image.open('D:/data/pic2.PNG')
im = Image.merge('RGB', im1.split()[:3])
im.show()
rgb2xyz = (
    0.412453, 0.357580, 0.180423, 0,
    0.212671, 0.715160, 0.072169, 0,
    0.019334, 0.119193, 0.950227, 0 )
out = im.convert("RGB", rgb2xyz)
out.show()
```
