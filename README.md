# Parsely


## Introduce Organization (URL)
https://github.com/12come


## Project Repository
https://github.com/12come/Parsely


## Project Objective
단어 암기는 영어 학습에서 가장 중요하면서도 번거로운 영역이다. 또한 대부분의 영어 학습자들이 단어-뜻만 반복적으로 암기한다는 점도 기존 영어 학습의 한계로 지적되고 있다. 따라서 숏폼을 통해 사용자의 감각을 자극하고 사용자가 쉽게 반복할 수 있도록 돕는 방법을 제시한다. 숏폼의 간편성을 기반으로 단어 접근을 늘리고 이미지와 음성을 통해 다양한 자극을 주는 영단어 학습 서비스를 제시한다.


## Member & Stack
- 조수빈 | python 
- 김윤선 | python
- 양가현 | python


## Scenario
1. DB에서 단어 랜덤 5개 추출
2. 단어를 기반으로 스크립트, 이미지, 음성 제작
3. 스크립트, 이미지, 음성 합성하여 동영상 제작
4. 영상을 사용자에게 전달


## Architecture
<img width="750" src="https://github.com/12come/Parsely/assets/109792191/be8a46ce-f418-4bf7-98f3-535b5940f740"/>

https://github.com/12come/Parsely/assets/109792191/be8a46ce-f418-4bf7-98f3-535b5940f740

## Tutorial
#### Script
1. 
#### Image
1. Hugging Face (https://huggingface.co)에 로그인하여 User Setting>Access Token에 들어가 토큰을 복사한다.
2. https://colab.research.google.com/drive/1Iy-xW9t1-OQWhb0hNxueGij8phCyluOh#scrollTo=R-xAdMA5wxXd 를 실행한다.
3. 실행 결과 나온 사이트에 프롬프트를 입력한다.
4. 이미지를 다운 받고, 영상 처리를 위해 제목을 %2d.{확장자명}으로 저장한다. 
#### Audio
1. https://colab.research.google.com/drive/1iCCSseo_UxRXPCk5CfEoeVWsDmii-yYX?usp=sharing 를 실행한다.
2. 구글 코랩 환경을 설정한다. (하드웨어 가속기: GPU, GPU 유형: T4)
3. 음성을 합성하고 싶은 텍스트 파일을 준비하고 경로를 코드에 복사한다. 
4. [런타임]-[모두 실행] 또는 Ctrl+F9를 눌러 전체 코드를 실행한다.
5. 코드가 정상적으로 실행되면 합성한 음성 파일이 다운로드 된다(.zip)
#### Video
1. output 폴더를 다운 받는다.
2. FFmpeg를 설치한다.

        brew install ffmpeg
    
3. 터미널에 다음을 차례로 입력한다.
        
        # 이미지로 영상 합성 (-t 50: 영상 소요 시간 50초)
        ffmpeg -f concat -safe 0 -i Downloads/output/init.txt -vsync vfr -t 50 -pix_fmt yuv420p Downloads/output/output.mp4
        
        # 음성 합치기 
        ffmpeg -f concat -safe 0 -i Downloads/output/tmp.txt -c copy Downloads/output/output.wav
        
        # 영상에 음성 입히기
        ffmpeg -i Downloads/output/output.mp4 -i Downloads/output/output.wav -c:v copy -c:a aac -strict/experimental -map 0:v:0 -map 1:a:0 -shortest Downloads/output/final.mp4

4. 실행결과 final.mp4가 동일 경로에 저장된다. 


## TODO
#### Database
  - [ ] DB 구축
  - [ ] DB에서 단어 랜덤으로 5개 추출
  - [ ] DB와 Script파트 연결
#### Script
  - [ ]  
#### Image + Video
  - [x] FFmpeg 커맨드 작성 및 샘플 영상 제작
  - [ ] 파일 제목 전처리
  - [ ] init.txt 작성
  - [ ] FFmpeg 커맨드 파일 작성
  - [ ] 영상 사이즈 조절
  - [ ] 영상 디자인
  - [ ] 음성 타임 스탬프로 영상과 음성 싱크 맞추기
  - [ ] Stable Diffusion API 사용
#### Audio
  - [x] 텍스트를 문장 단위로 구분하여 음성 합성
  - [x] output 폴더에 합성한 음성 저장
  - [x] .zip 으로 압축하여 로컬 pc로 다운로드
  - [ ] 다양한 화자의 목소리로 합성을 할 수 있도록 다른 speech dataset을 준비하여 모델 학습


## Reference
- <https://chat.openai.com/>
- <https://catalog.ngc.nvidia.com/orgs/nvidia/resources/tacotron_2_and_waveglow_for_pytorch>
- <https://developer-kade.tistory.com/131>
- https://subyecho.tistory.com

