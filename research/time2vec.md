<h2>Time2Vec</h2>

  -  RNN베이스 모델은 squential data를 다루는데 뛰어난 결과를 나타내지만, time-series data를 다루는데 특화되있는 것은 아님.
  -  data를 preprocessing하여 feature를 추출 > 손수(hand-crafting)작업하기 떄문에 시간, 노력과 비용이 많이 필요
  -  Time2Vec은 새로운 모델을 제시하는 것이 아니라 Time-series data의 represnetation을 하는 방법을 새로 만든 것이다.
  -  (our goal is not to propose a new model for time series analysis, but instead to propose a representation f time in the form of a vector embedding that can be used by many models.)
  -  기존 모델 + Time2Vec와 기존 모델을 비교하였을 때 얼마나 성능이 향상되었는지를 실험적으로 보여준다.

### Notation

scalar값은 소문자로 vector값은 bold체 소문자, matrix는 bold체 대문자로 표현한다. r[i]r[i]은 rr벡터의 ii번째 값을 의미한다. 2가지 벡터의concatenation은 r⊙sr⊙s로 표현한다.

### Representation

Time2Vec은 3가지 중요한 요소가 포함되도록 디자인 되었다.

1. 주기적과 비주기적 패턴들을 파악할 수 있도록한다.
2. time rescaling에 대해서 불변해야 한다.
3. 다른 모델들과 결합할 수 있도록 충분히 단순화 할 수 있어야 한다.
   저자가 왜 위의 3가지를 담아야 한다고 생각했는지 알아보자

**Periodicity(1번)**
Time series data는 패턴이 주기적 일 수 있고, 비주기적 일 수 있다. 중요한 것은 시간이 지나가면서 변해가는 데이터의 주기나 비주기적 패턴을 파악하여 Neural Net에 feed할 수 있어야 한다. 예를 들어 계절이나 피아노 반주곡 같이 주기적 패턴으로 나타나는 것이 있지만, 나이가 많아질록 발병확률이 높아지는 질병처럼 비주기적 패턴이 있다. 이러한 주기적 비주기적 time패턴은 더 좋은 치료법이나 시간대를 나타내는 다른 feature과 구별해야 한다. **(Such periodic and non-periodic patterns distinguish time from other features calling for better treatment and a better representation of time.)** 즉, 특정시점의 feature를 찾는 것이 아니라 전체적인 시간흐름에서 우리에게 필요한 주기적 feature, 비 주기적 feature를 찾는 것이 이 논문의 목적이다.

 

**Invariable to Time Rescaling(2번)**
만약 다른 scales(day, week, etc..)로 측정되도라도, scale에 상관없이 time represtation에 중요한 정보들은 불변해야 한다. 논문에서는 **class CC에 관해서 모델M1∈CM1∈C와 scalar α>0α>0라면, τατα로 행동하는 M2∈CM2∈C이 동시에 기존 τsτs행동하는 M1M1이 있다.** 이러하게 나와있지만, 수식을 보면 이해가 금방간다. 예를 들어 time interval이 하루인 데이터의 feature ττ값갖고 이때 wt=αwt=α의 값을 갖는다. 이 데이터의 scale을 7일로 증가 시키게 되면 ττ는 유지가 되고, ^wt=wt7w^t=wt7을 가지게 될 것이다. 나중에 실험에서 나오겠지만, 실제로 여러가지 데이터를 time interval 7일로 두었을 때, 2π72π7와 비슷한 값이 어렵다. 즉, 이 모델의 목적은 time-sries data에서 고유값, 고유벡터를 추출하는 것으로 볼 수 있다.

 

**Simplicity(3번)**
기존의 time representation은 다른 데이터와 결합하기 어려운 점이 있지만, 이 모델은 다른 데이터와 결합이 되면서 다른 모델과도 결합하여 사용 할 수 있다.

### Time2Vec

Time2Vec는 위에 3가지 모든 것을 담을 수 있다. 즉, 주기적 비주기적 패턴과 scale에 상관없는 불변성 마지막으로 여러모델과 결합할 수 있는 단순함(simplicity)까지 있다고 한다.
t2v(τ)[i]={wiτ+bi,if i=0F(wiτ+bi),if 1≤i≤kt2v(τ)[i]={wiτ+bi,if i=0F(wiτ+bi),if 1≤i≤k

이 논문에서는 FF는 sin함수를 사용하였지만 다른 함수도 충분히 활용가능하다고 한다. vector를 만드는데 학습이 가능한 wiwi,bibi때문에 다른 모델들과 쉽게 결합 할 수 있다**(3번)**.
또, 저자가 sin function을 정한 이유는 주기적 패턴에 대해서 캡쳐할 수 있고, 내부에 들어있는 linear function으로 비주기적 패턴을 캡쳐 할 수 있다고 한다(1번). 만약 ww가 2π72π7라면 일주일의 주기(scale이 day인 경우)를 가지는 패턴을 가지게 될 것이다. 저자가 sin을 function으로 사용하는 이유는 transformer모델을 인용했다고 한다. 여기서 positional embedding(PE)을 사용하게 되는데, 언어의 길이는 다양한데 아무리 같은 word라도 서로 다른 position을 가지고 있어 word에 대한 position정보를 정의하기 위해 사용하고 있다[Attetion is all you need참고].
PE=⎧⎨⎩sin(j10000)kd,if j is evencos(j10000)kd,if j is oddPE={sin⁡(j10000)kd,if j is evencos⁡(j10000)kd,if j is odd
위의 공식은 positional embedding의 공식인데, 저 의미는 affine 즉, 좌표평면에서 이동을 나타내지만, 이와 다르게 sin을 단순히 사용한 것은 가변적인 position을 나타내는 것이 아니라 time2vec고정된 값에서 tiem에 대한 continuous한 feature를 나타내고 싶어했기 때문이다. Periodicity에서 말한 것처럼 특정시점에 대한 정보가 아니라 전체적인 흐름에서 주기적 패턴을 나타내고 싶어했던 것이다.

t = 0시점은 function은 단순히 linear function인데, 비주기적 패턴을 파악하기 위해 남겨두었다고 한다. 첫번째 layer는 ττ대신에 linear한 함수를 씀으로써 sin함수와는 구별된 feature를 나타내게 된다. 시간의 진행(progression)에 따른 정보를 그대로 담고 있기 때문에 비주기적 패턴을 파악 할 수 있고, extrapolation의 도움을 주는데 사용 될 수 있다고 하는데 사실 직관적으로 확 와닿지는 않는다.

### Experiments & Results

여기서 model을 2가지로 나누어서 비교를 하고 있는데, LSTM+Time2VecLSTM+Time2Vec과 LSTM+TLSTM+T이다. 전자는 LSTM에 들어갈 데이터를 time2vec을 통해서 데이터를 전처리한 모델이고, 후자는 기본 LSTM을 나타낸다. 그 외에도 LSTM1, LSTM2 등.. 모델이 있는데 이 부분에 대한 상세한 구조는 논문을 확인해주길 바란다.

이제 실험을 통해서 5가지 질문에 대한 대답을 찾아볼 것이다.
**Q1:Time2Vec은 좋은 representation인가?**
**Q2:Time3Vec은 다른 architecture와 사용될수 있으며 performance를 향상시키는가?**
**Q3:sin함수는 어떤 것을 학습하는가?**
**Q4:Time2vec공식을 사용하여 비주기적 패턴에 대해 비슷한 효과를 낼 수 있는가?**
**Q5:sin함수가 학습하는 값은 fixed한 속성을 지니는가?**

\1. On the effectiveness of Time2Vec



![img](https://blog.kakaocdn.net/dn/9Q2ln/btqKwq1LDDD/4W6quhJjqEUq9NbOu4EWrK/img.png)



왼쪽 사진은 여러가지의 Squential data를 통해서 실험을 해보았지만, 이 테스트데이터 중에서 N_TIDIGTS18은 long time hozien과 long squence를 가지지만 부분의 경우에는 performance가 향상되었고, 악화된 경우는 전혀 없다는 것을 보여준다(**Q1해결**). 반면에 오른쪽 사진 여러 다른 모델(TLSTM1,2,3)에도 적응 할 수 있는 representation이라는 것을 보여준다.(**Q2해결**)

\2. Time2Vec는 무엇을 학습하는가(**Q3**)?



![img](https://blog.kakaocdn.net/dn/cUtkBv/btqKBOUMJ1r/xvisA7KgHWBaHpdoDEpweK/img.png)



위에서 말했듯이 **sin함수를 쓴 Time2Vec는 주기적인 패턴을 표현하고 있다.** time inteval을 7 day기준으로 데이터셋을 time2vec로 구해 봤을 때, 대부분 α2π7α2π7와 근접한 값이 산출되었고, π2π2를 shift한 결과 값이 주로 나온다고 한다. 왼쪽에 있는 사진은 이것을 fully connected layer를 통해서 classification한것을 보여주고 있다. 이 파동이 의미있는 이유는 주어진 데이터 안에서의 generalization뿐 아니라 패턴을 학습하기 때문에 주어진 데이터 외에서의 패턴 볼수 있는 extrapolation으로 사용될 수 있다고 말한다.
또, **Time2Vec은 고정된 frequencies를 가져다 준다.** data는 항상 제자리이고 이것을 조작하는 model들의 feature값들이 다르게 나올 텐데, data represnetation이 일정하지 않는다면 나쁜 성능을 보여주게 될 것이다. 위에서도 말한 것처럼 time inteval이 day,week 또는 year에 주기이든 상관없이 feature들의 속성을 고정된 채로 있어 더 좋은 성능을 가져다준다.(**Q5**)

오른쪽 사진은 비주기적 패턴을 학습시켰을 경우와 학습시키지 않았을 경우를 나타내고 있다. 결과적으로 비주기적 패턴을 학습시킨 것이 더 좋은 성능을 내고 있다.(**Q4**)

