# TensorFlow_examples
包含学习TensorFlow过程当中涉及到的代码
1.simple_tensorflow利用TensorFlow的训练简单线性模型模拟加法，这个是非常简单的任务。这样能把注意力更好的放在TensorFlow的学习上，更容易理解TensorFlow的工作流程
训练的几个要素：
1.input:随机生成的x1，x2 label:y=x1+x2
2.模型：prect_y = Wx+b
3.损失函数：loss = (prect_y-y)^2 
4.使用GradientDescentOptimizer最为优化器，学习速率为0.1


Q1:tensor类型和variable类型的区别？
A:tensor是不可训练的，而variable是默认可以训练的。我们这里w,b都是需要训练的向量，所以应该为variable。x,y都为tensor。注意在词向量训练当中的input也应该设置variable已得到嵌入词向量。
Q2:参数更新的流程？
A:1.正向计算得到loss的值。2.对loss求w的偏导数w'=2(Wx-b-y)*x,w=w+lr*w';b'=2(Wx-b-y),b=b+lr*b',其中lr为学习率。这个步骤由优化器自动完成，我们只用给去学习率。
Q3:数据是否需要正则化，参数怎样设置？
A:可以做个试验，给出以下参数：range_random=10，lr=0.1,可以看出很快就能拟合。但如果rang_random=100、1000，则无法拟合。这个时候可以将lr调小几个数量级你会发现在循环多次后任然可以拟合。分析如下：若对w求导则，w'= 2(wx+b-y)*x 则更新后的update_w=lr*w'。对b求导：b=2(wx+b-y) update_b=lr*b'。一些书上说lr因设置为0.1，如果x的取值范围为（0,1000），则update_w的粒度为很大，或许理想的wi取值为（0,10）,这样永远无法拟合。所以需要将数据正则化。如果不正则化呢？当然也可以那么学习率lr则要设置的很小，update_w的粒度在wi范围了，而update_b的粒度则远小于bi，则造成了训练缓慢，难以拟合。综上，调参标准，将数据正则化，lr设置为0.1
