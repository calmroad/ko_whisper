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

2) 마이크나 전화기를 통해서 들어오는 음성은 위 그림과 같이 저장된다.  소리를 구분하기 위해서는 반드시, 구성하는 각각의 주파수를 찾아내야한다.  다행스럽게 FFT라는 알고리즘을 거치면 알수가 있다. 다음은 음파를 주파수로 변환한 그림이다.

   ![image](https://github.com/calmroad/ko_whisper/assets/8465326/4d08b053-fb8f-4bad-9d8f-89d5705b13b3)

3) 이렇게 변환한 데이타를, 시간에 따라 일정한 길이로 짤라서, 인식 알고리즘을 사용해서 원래의 글자를 찾아낸다.
4) 
5) 
