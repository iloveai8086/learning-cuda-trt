# 知识点
1. 对于yolov5的封装，主要考虑以下：
    - 希望调用者是线程安全的，可以随意进行commit，而不用考虑是否冲突
    - 希望结果是懒加载的，也就是需要的时候才等待，不需要的时候可以不等待
        - 由promise与future配合实现
        - 这样的灵活度和效率性能都是最好的
    - 希望最大化利用GPU，如何利用呢？需要尽可能的使得计算密集
        - 实际体现就是抓取一个批次，一次性进行推理
        - 这在内部的消费者模型里面，一次抓一批