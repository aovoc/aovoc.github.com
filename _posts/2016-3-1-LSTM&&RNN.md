---
layout: post
category : sequence learning
tagline: ""
tags : [sequence learning, deep learning]
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

# (vanilla) Recurrent Neural Network   
$$ h_t = f_W(h_{t-1}, x_t) $$   
$$ h_t = tanh(W_{hh}h_{t-1} +　W_{xh}x_t) $$   
$$ y_t = W_{hy}h_t $$   

# LSTM(长短期记忆人工神经网络)
是一种时间递归神经网络（RNN），适用于处理和预测时间序列中间隔和延迟比较长的重要事件。    
四个S函数单元     
input、forget、output.    
输入信息、忘记信息、输出信息     



$$ c_t^l = f \mult c_{t-1}^l + i \mult g $$   
$$ h_t^l = o \mult tanh(c_t^l) $$    


LSTM   
$$ c_t^l = f * c_{t-1}^l + ig $$  
$$ h_t^l = o * tanh(c_t^l) $$    
