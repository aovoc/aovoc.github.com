---
layout: post
category : attention
tagline: ""
tags : [tensorflow]
---
# tf.train.batch和tf.train.shuffle_batch

返回batch的样本和样本标签  

顺序输出batch:
>$ tf.train.batch([example, label], batch_size=batch_size, capacity=capacity)  

乱序输出batch:
>$ tf.train.shuffle_batch([example, label], batch_size=batch_size, capacity=capacity, min_after_dequeue  
  
* 要保证 *min_after_dequeue < capacity* 

# sess.run()
**每次执行sess.run()之后batch会更新，debug找了好久... T T**