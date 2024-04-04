# ko_whisper
fine tuning the whisper for korean

ChatGPT를 만들어서 서비스를 제공하는 OpenAI회사에서,
전세계 언어를 인식하는 것을 transformer기술을 이용해서 만든것이 whisper이다.

개발자중에 한국인이 포함되어,
whisper 홈페이지에 들어가면 친숙한 한글이 나온다.

https://openai.com/research/whisper

# 음성을 인식하는 기술을 쉽게 이해하는 방법 (교과서에도 안나오는 비유)
1) 우리가 말하는 음성(소리)은 음파라고 하고, 귀로 들리지는 않지만, 핸드폰에서 통신하는 것은 전파라고 한다.  "삐이"하는 소리는 1개의 주파수로 만들어진 음파이지만,
   
   ![image](https://github.com/calmroad/ko_whisper/assets/8465326/c8109ef4-bd49-46ef-a7ca-42e9ac1d676b)

   사람의 목소리는 성대에서 복수개의 주파수로 합성되어 만들어진다.

   ![image](https://github.com/calmroad/ko_whisper/assets/8465326/f8f1245b-fdb4-4ee0-a4ed-1f3f3e18724f)

2) 마이크나 전화기를 통해서 들어오는 음성은 위 그림과 같이 저장된다.  소리를 구분하기 위해서는 반드시, 구성하는 각각의 주파수를 찾아내야한다.  다행스럽게 FFT라는 알고리즘을 거치면 알수가 있다. 다음은 음파를 주파수로 변환한 그림이다.  스펙트럼이라고 한다.

   ![image](https://github.com/calmroad/ko_whisper/assets/8465326/4d08b053-fb8f-4bad-9d8f-89d5705b13b3)

3) 이렇게 변환한 데이타를, 시간에 따라 일정한 길이로 짤라서, 인식 알고리즘을 사용해서 원래의 글자를 찾아낸다.
4) 그럼, 인식 알고리즘은 어떻게 동작하는 걸까?  어렵게 생각할 필요가 없다. 스펙트럼 그림을 보면, 그림을 구성하는 색과 모양으로 구분할수 있으면 된다. 즉, 스펙트럼이라는 영상을 인식하는 알고리즘을 사용하면 된다.
5) 인식하는 알고리즘은 다양하게 많다. whisper 알고리즘을 보면, 30초 단위로 음성을 짤라서, 즉 30초단위로 만들어진 스펙트럼 영상을 입력해서, 글자를 알아내는 방식이다.
6) 이상은 음파로 인식하는 방식이고, 음파로 인식한 결과가 인식률이 많이 떨어져서, 후처리로 문장이 만들어지는 규칙을 이용하여 보정하는 기술이 추가되기도 한다.

# 음성인식의 어려움
1) 30초 길이의 음성 스펙트럼을 아무리 학습하더라도, 사람마다, 다양한 목소리가 존재하고, 심지어 본인의 목소리도 감기걸렸을때와 비교하면 다르다.
2) 전화를 통한, 음성인식은 전화망에서는 아날로그 음성을 코덱을 거쳐서 데이타로 변환해서,4kbps~64kbps, 8khz로 변환해서 전달되는데, 원음의 정보가 많이 손실되어진다.

# Whisper의 성능
- ChatGPT는 transformer기술을 이용해서 만들어졌고, 성능이 획기적이라는 기사가 많이 나온다. 하지만, whisper는 다음 그림처럼, 기존 다른 인식알고리즘과 비교해서 성능이 거기서 거기이다.

   ![image](https://github.com/calmroad/ko_whisper/assets/8465326/fb11221b-fa0e-4e22-86fa-e3973b5d4cd8)

# Whisper의 장점
- 다행인지는 모르겠지만, 전세계 웬만한 언어를 모두 인식해주도록 만들어졌고, 무료로 사용할수 있다.

# Whisper의 단점
- 다양한 크기로 사전 학습해둔 모델을 공개해주고 있지만, 실제 테스트를 해보면, 크다고 성능이 좋다고는 볼수 없다.
- python으로 되어 있어 무겁다.
- 
# Whisper의 성능 업그레이드(fine tuning)
- 성능을 개선할수 있도록 다른 AI 알고리즘처럼, fine tuning을 할수 있도록 제공해주고 있다. 
 https://github.com/huggingface/transformers/blob/v4.39.2/src/transformers/models/whisper

# whisper korean fine tunning 방법
