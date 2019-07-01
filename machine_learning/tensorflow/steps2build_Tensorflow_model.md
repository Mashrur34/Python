[toc]
## 数据清理
第一步先进行数据清理，需要分出模型的特征(Features)和标签(Labels)
然后把清洗好的数据分成**训练集**，**验证集**，**和测试集**
使用**sklearn**模组中内建函数进行数据分类

```py
from sklearn.model_selection import train_test_split
#首先把数据集先拆分成训练集（全）和测试集
x_train_all, x_test, y_train_all, y_test = train_test_split(Features , Labels, 
                                                            random_state = 1)
#然后把测试集（全）分成训练集和验证集
x_train, x_valid, y_train, y_valid = train_test_split(x_train_all , y_train_all,      
                                                            random_state = 2)
```

## 数据归一化来提升模型收敛速度（可选择）

```py
from sklearn.preprocessing import StandardScaler
#先创建一个StandardScaler对象
scaler = StandardScaler()
#调用fit方法，来对Features整体数据进行处理
scaler.fit(Features)
#然后调用transform 方法进行归一化操作
x_train = scaler.transform(x_train)
x_valid = scaler.transform(x_valid)
x_test = scaler.transform(x_test)
```


## 构建模型图
```py
model  = keras.models.Sequential([
     #输入层要增加一个参数 input_shape
     keras.layers.Dense(500, activation = 'relu',
                        input_shape = x_train.shape[1:]),
     # 隐藏层
     keras.layers.Dense(300, activation = 'tanh'),
     keras.layers.Dense(200, activation = 'relu'),
     #增加批归一化可以进一步提升模型准确度     
     keras.layers.BatchNormalization(),
     keras.layers.Dense(50, activation = 'tanh'),
     #输出层
     keras.layers.Dense(1)
])
```

## 编译模型
```py
model.compile(loss = 'mean_squared_error', optimizer = 'sgd')
# 定义callbacks
callbacks = [keras.callbacks.EarlyStopping(patience = 10, min_delta = 1e-5)]
```


## 训练模型
传入x_train 和 y_train 来训练模型
```py
hist = model.fit(x_train, y_train, epochs = 1000, 
validation_data = (x_valid, y_valid), 
callbacks = callbacks)
```


## 画出学习曲线
```py
def plot_learning_curve(history):
    pd.DataFrame(history.history).plot(figsize = (8 , 5))
    plt.grid(True)
    plt.gca().set_ylim(0 , 1)
    plt.show()
#调用学习曲线函数
plot_learning_curve(history = hist)
```


## 使用测试集来评估模型
```py
model.evaluate(x_test , y_test)
```
