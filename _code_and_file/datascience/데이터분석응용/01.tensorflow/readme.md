# Tensroflow 사용 방법 

> tf gpu 버전 사용하기 

```
nvidia 버전 확인
nvidia-smi 로 장치가 있는지 확인
cuda 릴리즈 버전 표를 확인하고 그것에 맞는 버전 설치
tensorflow-gpu 로 설치

jupyter notebook 사용시 
- 가상환경 접속 후 jupyter 설치
pip install jupyter 

- gpu 사용 가능여부 확인
tf.test.is_gpu_available()
```

> tf 다른 그래프 사용하기

```
g = tf.Graph()
with g.as_default():
    # 여기에서는 g를 기본 그래프로 인식
    pass

```

> tf 는 세션을 통해서 gpu를 사용

```
a = tf.constant(1.0)
b = tf.constant(2.0)
c = a+b
sess = tf.Session()
sess.run(c)
sess.close() # -> 세션 사용후 반드시 close 해야함
-> gpu 메모리상에 이미 올라가 있던 a,b,c 를 이용하여 계산
```

> 데이터를 입력 받는것을 가능하게 해주는 tf.placeholder

```
session이 실행되는 순간에 feeding이 되는 값들
- 사용 예
x = tf.placeholder(tf.float32)
with tf.Session() as sess:
    # feed_dict 를 통해서 데이터를 넣어줄 수 있음
    print(sess.run(x,feed_dict={x:1.0}))
- 제곱 값 구해보기
a = tf.placeholder(tf.float32)
b = a * a
with tf.Session() as sess:
    # feed_dict 를 통해서 데이터를 넣어줄 수 있음
    print(sess.run(b,feed_dict={a:2.0}))    
```

> 이후 설명은 jupyer 업로드 















