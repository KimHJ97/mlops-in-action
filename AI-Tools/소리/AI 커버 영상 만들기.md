# AI 커버곡 만들기

 - 관련 영상: https://www.youtube.com/watch?v=a5fxyMKQxR8

<br/>

## 만드는 방법

### 1. 목소리 학습시키기

AI 노래를 만들기 위해서는 부르고자 하는 가수의 목소리를 학습해야 한다.  
목소리의 음색을 잘 뽑아내기 위해서는 MR와 Vocal(목소리)를 분리시켜야 한다.  

#### 1-1. Ultimate Vocal Remover을 목소리 분리

 - MR와 Vocal 분리
    - Select Input, Select Output 선택
    - MDX-NET MODEL: Kim Vocal 1
    - GPU Conversion, Vocals Only
 - 세부 음향
    - Select Input: 분리 작업한 보컬 목소리 선택
    - MDX-NET MODEL: Karaoke 2
    - GPU Conversion, Vocals Only
 - 리버브 제거
    - Select Input: 분리 작업한 소리 선택
    - MDX-NET MODEL: Reverb HQ
    - GPU Conversion, No Other Only

이후 만들어진 생목소리를 zip 파일로 압축

<br/>

#### 1-2. RCV 코랩 사이트

가수 음성 트레이닝 학습을 위한 RVC v2 Disconnected colab을 이용한다.  
 - https://colab.research.google.com/drive/1XIPCP9ken63S7M6b5ui1b36Cs17sP-NS#scrollTo=ZodNcumpg-JM
    - 자신의 Drive로 복사한다.
```
1. Run me first! 클릭
 - 순차적으로 코드 수행

2. Initial Setup
 - experiment_name: 가수명
 - model_architecture: v2
 - target_sample_rate: 40k

3. Load Dataset
 - dataset: 가수 목소리 ZIP 파일 구글 드라이브로 업로드

4. 순차적으로 코드를 실행

5. 아래 두 항목은 실행하지 않는다.
Load preprocessed dataset files from Google Drive (for resuming)
Import Model from Drive to Notebook (for resuming)

6. Training
 - save_frequency: 10
 - total_epochs: 250
 - batch_size: 16

7. 이후 코드를 모두 실행하면 rvcDisconnected 하위 폴더에
*.index(목소리 데이터)와 *.pth(메인 트레이닝) 파일이 생성된다.
```
<br/>

### 2. 목소리 합성하기

목소리를 합성시켰다면 부르고 싶은 노래로 합성을 해준다.  
 - https://www.tryreplay.io/
```
1. 목소리 학습 압축 파일을 model에 끌어놓는다.
2. 부르고 싶은 노래 파일을 유튜브 링크로 넣어준다.
3. 노래를 부를 가수를 선택해준다.

4. 스크롤을 내리고 Setting
 - Stem Method
    - UVR-MDX-NET Voc FT (pth)
 - Advanced Settings
    - Index Ratio: 1
```

