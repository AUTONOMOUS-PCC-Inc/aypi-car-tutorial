<div align="center">

<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/tutorial-banner.svg" alt="바이브코딩 캠프 1회차 — 시뮬레이터에서 직접 운전하고, 그 기록으로 모델을 학습시켜, 운전대를 넘긴다" width="100%">

### 내가 운전한 대로 달리는 차를 만든다.

AUTONOMOUS PCC 바이브코딩 캠프 **1회차(자율주행)** 실습 저장소입니다.<br>
시뮬레이터에서 직접 운전해 데이터를 모으고, 그걸 흉내 내는 모델을 학습시켜, 자율주행을 돌립니다.

![Day](https://img.shields.io/badge/과정-1회차%20하루-0B1B33?style=for-the-badge)
![OS](https://img.shields.io/badge/환경-Windows-1E6FD9?style=for-the-badge)
![Env](https://img.shields.io/badge/conda-donkeybro-16A34A?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.9-1E6FD9?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-A3A3A3?style=for-the-badge)

[**시작하기**](#시작하기) · [**폴더 지도**](#폴더-지도) · [**하루 흐름**](#하루-흐름) · [**자주 막히는 곳**](#자주-막히는-곳) · [**원저자 문서**](#원저자의-설치-문서-참고용) · [**만든 사람들**](#만든-사람들)

</div>

---

## 시작하기

> [!IMPORTANT]
> **수강생은 배포된 설치 안내서(PDF)를 따르세요.** 이 README는 "여기가 뭐 하는
> 저장소지" 싶을 때 보는 지도이고, 설치 절차의 정본은 안내서입니다.
> 설치는 내려받을 것이 많아 **수업 전에 미리** 끝내 두어야 합니다.

받는 것부터 하면 이렇습니다. 안내서 2단계와 같은 명령입니다.

```bat
git clone https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial.git DonkeyBro
cd DonkeyBro
git submodule update --init --recursive
```

- 폴더 이름을 `DonkeyBro`로 만드는 건 **의도한 것**입니다. 안내서의 나머지 경로가 그 이름을 씁니다.
- 마지막 줄을 빼면 `donkeycar`·`gym-donkeycar` 두 폴더가 **빈 채로** 남습니다. 등록만 하고 내려받지는 않기 때문입니다.
- 경로가 너무 깊으면 Windows에서 실패합니다 ([아래](#자주-막히는-곳) 참고). 안내서대로 `문서\GitHub` 아래에 두세요.

그다음은 안내서로 돌아가 conda 환경(`envs/donkeybro_for_windows.yml`)을 만드세요.

---

## 폴더 지도

받고 나면 폴더가 여럿입니다. 하루 종일 "지금 어느 폴더에 있어야 하지"가 가장 자주 막히는 지점이라, 먼저 봐 두면 좋습니다.

<div align="center">
<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/tutorial-layout.svg" alt="폴더 지도 — 클론에 따라오는 폴더, 직접 내려받는 폴더, 직접 만드는 폴더를 색으로 구분" width="100%">
</div>

라이브러리 두 개는 **서브모듈**이라 각자 자기 저장소가 있습니다. 무슨 일을 하는지는 각 폴더의 README에 있습니다 — [donkeycar](https://github.com/AUTONOMOUS-PCC-Inc/donkeycar) · [gym-donkeycar](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar).

---

## 하루 흐름

<div align="center">
<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/donkeycar-pipeline.svg" alt="6단계 흐름: 설치 · 차량 생성 · 데이터 수집 · 학습 · 자율주행 · 바이브코딩 과제" width="100%">
</div>

| 단계 | 하는 일 | 결과물 |
|:--:|---|---|
| 1 | conda 환경을 만들고 `donkeycar`를 설치 | `donkey` 명령이 돈다 |
| 2 | `donkey createcar`로 내 차를 만든다 | `cars/mycar` |
| 3 | 시뮬레이터를 띄우고 **직접 운전**한다 | `data/` — 사진 + 내 조향값 |
| 4 | 그 기록으로 모델을 학습시킨다 | `models/mypilot.h5` |
| 5 | 모델에게 운전대를 넘긴다 | 한 바퀴, 또는 충돌 |
| 6 | 모델이 **나와 가장 다르게 판단한 순간**을 찾는다 | 사진 10장 |

3단계가 가장 중요합니다. **모델은 네 운전을 흉내 낼 뿐**이라, 네가 안 가 본 상황은 모델도 모릅니다. 5단계에서 차가 코너를 못 돌면 대개 모델이 멍청해서가 아니라 그 코너 데이터가 부족한 겁니다. 6단계가 그 자리를 찾아내는 과제입니다.

---

## 자주 막히는 곳

| 증상 | 원인과 해결 |
|---|---|
| `donkeycar`·`gym-donkeycar` 폴더가 비어 있다 | 서브모듈을 안 받았습니다. 이 폴더 맨 위에서 `git submodule update --init --recursive`. `git submodule init` 만으로는 **안 받아집니다** |
| clone 중 `Filename too long` | 경로가 너무 깊습니다 (Windows 경로 길이 제한). `문서\GitHub` 처럼 **짧은 경로**에 받으세요. OneDrive 하위 깊은 폴더가 자주 걸립니다 |
| `donkey` 명령을 찾을 수 없다 | `conda activate donkeybro` 를 안 했거나, 설치 후 이 폴더를 **옮겼습니다**. 옮겼다면 `donkeycar` 안에서 `pip install -e .` 를 다시 돌리세요 |
| `cudart64_110.dll` 경고가 아홉 줄쯤 뜬다 | **정상입니다.** GPU가 없어 CPU로 돌겠다는 알림일 뿐입니다. 인터넷의 "opencv를 지우라"는 조언은 **따르지 마세요** |
| `Could not connect to server. Is it running?` | 시뮬레이터가 켜지는 데 걸리는 시간보다 기다려 주는 시간이 짧아서입니다. `myconfig.py` 의 `GYM_CONF` 에서 `start_delay` 를 **15**로 올리세요 |
| 학습이 끝날 기미가 없다 | 원래 오래 걸립니다. 노트북 CPU로 몇천 장이면 수십 분입니다. 시작해 두고 **건드리지 말고** 기다리세요 |
| 시뮬레이터 창이 안 뜬다 | `myconfig.py` 의 `DONKEY_SIM_PATH` 경로를 확인하세요. `DonkeySimWin` 을 이 폴더 **바로 아래**에 풀었어야 합니다 |

그래도 안 되면 **에러 메시지 전체를 복사해서** 강사에게 보여 주세요. 마지막 줄만 보면 원인을 못 찾는 경우가 많습니다.

---

## 원저자의 설치 문서 (참고용)

아래는 이 프로젝트를 만든 분이 쓴 원본 설치 문서입니다. **3~5단계가 `virtualenv` 방식**이라
수업의 conda 방식과 다르고, 두 방식을 섞으면 패키지 버전이 꼬입니다.
수업을 따라가는 중이라면 열지 말고, 배경이 궁금할 때만 펼쳐 보세요.

<details>
<summary><b>원본 문서 펼쳐 보기</b> — 윈도우 설치 0~11단계</summary>

<br>

<p align="center">
  <img src="./images/common/donkeybro.png">
</p>

### ※프로젝트 구축방법(윈도우 버전)

#### 기본적으로 설치되어 있어야 할 프로그램

1. Vscode([링크](https://code.visualstudio.com/download))
2. Git([링크](https://git-scm.com/))
3. Msys([링크](https://www.msys2.org/))
4. Miniconda(3.9)([링크](https://docs.anaconda.com/miniconda/miniconda-other-installer-links/))

<br>

|     vscode     |     git     |   msys   |    miniconda   |
|   :--------:   |  :--------: | :------: |   :-----:   |
|   ![vscode]    |   ![git]    | ![msys]  |  ![miniconda]  |

<br>

#### 0. msys 설치후,  환경설정 해주기

셋업파일을 다운로드 받고 설치해준다.

이후 아래 명령어를 작성해준다.

```shell
pacman -Suy
pacman -S wget unzip mingw-w64-ucrt-x86_64-hdf5 mingw-w64-ucrt-x86_64-ffmpeg
```



#### 1. 파이썬 설치후, 가상환경 구축하기

파이썬은 무조건 3.9.12버전을 설치해주어야 한다. 만약 다른 버전이 설치되어 있더라도 해당 버전으로 바꾸어주어야 하니 설치해주자.

(물론 3.7, 3.8에서도 동작하지만 저작자와 맞추기 위함이다. 그리고 3.10이상에서는 잔오류가 많이 발생하게 된다.)

<div>
	<img src="./images/common/README/image-20240229191848799.png" alt="image-20240229191848799" style="zoom:100%"/>
</div>

이후 아래와 같이 설치한다.

![image-20240229193031719](images/common/README/image-20240229193031719.png)

Next!

![image-20240229193045326](images/common/README/image-20240229193045326.png)

아래와 같이 세가지를 체크해주고, 설치경로를 다음과 같이 `C:\Python\Python3_9_12` 맞춰준다.

![image-20240229193057292](images/common/README/image-20240229193057292.png)

이렇게 깔리면 아래와 같이 구조가 잡히게 된것이다.

![image-20240229193616533](images/common/README/image-20240229193616533.png)

이후 수동으로 환경변수(사용자변수)를 잡아주자.

![image-20240229193849567](images/common/README/image-20240229193849567.png)






#### 2. DonkeyBro 프로젝트 설치하기
<!-- ## 2. donkeycar_projects 설치하기 -->
다음과 같이 C드라이브 바로 아래에 DonkeyBro프로젝트를 생성한다.

```
cd C:\
```



해당([링크](https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial))로 git clone을 해준다.

```shell
git clone https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial.git DonkeyBro
cd DonkeyBro
```

서브모듈(donkeycar, gym-donkeycar)을 받아온다.

```shell
git submodule update --init --recursive
```

> `git submodule init` 만 치면 폴더가 **빈 채로** 남는다. 등록만 하고 내려받지는
> 않기 때문이다. 위 명령을 써야 실제로 파일이 들어온다.
>
> 처음부터 한 번에 받으려면 `git clone --recurse-submodules <URL>` 을 쓰면 된다.
>
> ⚠ `git submodule update --remote` 는 쓰지 말 것. 수업이 고정해 둔 버전을 버린다.



#### 3. 가상환경 구축하기

cmd창에서 DonkeyBro로 와주고, 가상환경 패키지 및 가상환경 구축을 해준다.

```shell
pip install virtualenv
virtualenv env
```

![image-20240229194919138](images/common/README/image-20240229194919138.png)

이후 가상환경에 접속해준다.
```shell
cd env/Scripts
activate
cd ..
cd ..
```

![image-20240229195007561](images/common/README/image-20240229195007561.png)

아래 것들을 설치해준다.

```shell
python.exe -m pip install --upgrade pip
pip install --upgrade wheel setuptools
```





#### 4. donkeycar/gym-donkeycar 의존성 패키지 설치하기

DonkeyBro에 들어가면 donkeycar가 있을것이다. cmd창으로 여기를 들어가준다. 그리고 서브패키지를 설치해준다.

```shell
cd donkeycar
pip install -e .
cd ..
```

DonkeyBro에에 들어가면 gym-donkeycar가 있을것이다. cmd창으로 여기를 들어가준다. 그리고 서브패키지를 설치해준다.

```shell
cd gym-donkeycar
pip install -e .
cd ..
```



#### 5. library_sheet에서 의존성 패키지 설치하기

DonkeyBro에에 들어가면 library_sheet가 있을것이다. cmd창으로 여기를 들어가준다. 그리고 서브패키지를 설치해준다.

```shell
cd library_sheet
pip install -r requirements_dynamic.txt
pip install -r "requirements_for_windows(3.9).txt"
cd ..
```





#### 6. donkeysim(시뮬레이터) 설치하기(가상환경에서 돌릴경우에만)

파워셀을 키고 아래와 같이 zip파일을 다운받고 압축을 풀어주자.

```shell
curl -O -L https://github.com/tawnkramer/gym-donkeycar/releases/download/v22.11.06/DonkeySimWin.zip
tar -zxvf DonkeySimWin.zip
```



#### 7. cars안에 mycar 생성하고 실행해보기

1)`DonkeyBro` 아래에 `cars`라는 폴더를 만들어줍니다.

(차량들을 모아둘, 비유하자면 일종의 주차장 같은 겁니다.)

```shell
mkdir cars
cd cars
```

2)이제 기본 차량을 만들어줍니다.

```shell
donkey createcar --path mycar
cd mycar
```

3)이제 mycofnig.py파일에 들어가 다음과 같이 수정해줍니다.

수정전>

![image-20240301004548797](images/common/README/image-20240301004548797.png)

수정후>

![image-20240301005014869](images/common/README/image-20240301005014869.png)

4)현재 mycar디렉토리에서 다음 명령어를 적어줍니다.

```shell
python manage.py drive
```

<웹브라우저에 localhost:8887이라고 적어주세요.>(아래그림: 웹브라우저와 콘솔창)

![image-20240301005206853](images/common/README/image-20240301005206853.png)

(아래그림: 시뮬레이션 화면)

![image-20240301005245170](images/common/README/image-20240301005245170.png)

![image-20240301005245170](images/common/README/gif1.gif)

#### 8. cars안에 car_dl, car_cv 생성하기

이번에는 두가지 각각 다른 템플릿이 탑재된 차량템플릿을 적용해서, 차량을 생성해보겠습니다.

### Template(1): Computer-Vision

```shell
donkey createcar --template=cv_control --path car_cv
```

### Template(2): Path-Follow(DeepLearning)

```shell
donkey createcar --template=path_follow --path car_dl
```

최종적으로 아래와 같이 아키텍처를 구축하게 됩니다.

![image-20240301102542781](images/common/README/image-20240301102542781.png)

#### 9. 카메라로 데이터 수집하기(Data collection)

python manage.py drive로 주행을 하게 되면 동작에 따라 실시간으로 데이터를 수집하게 됩니다.

최소 10바퀴정도를 돌려서 학습데이터셋을 수집합니다.



#### 10. driving model 훈련시키기(Train Data)

tensorflow를 통해 훈련을 시키기 위해서는 msvcp140.dl파일이 필요하며, 이는 Microsoft Visual C++ Redistributable 패키지에 포함되어 있다.([관련사이트](https://learn.microsoft.com/ko-kr/cpp/windows/latest-supported-vc-redist?view=msvc-170))<br>
컴퓨터 설정에 맞춰 둘중 하나를 설치해서 실행해준다.<br>
64비트일 경우: [`vc_redist.x64.exe`](https://aka.ms/vs/17/release/vc_redist.x64.exe)<br>
32비트일 경우: [`vc_redist.x86.exe`](https://aka.ms/vs/17/release/vc_redist.x86.exe)<br>

설치가 다 완료되면 아래 순서를 진행해준다.<br>
mycar디렉토리를 보면 train.py가 있습니다. 이를 활용하여 두가지 방식중 하나를 복붙해서 훈련을 시켜준다.<br>

```shell
### python 명령어를 사용하는 경우
python train.py --tubs=./data --model=./models/mypilot.h5
### donkey 명령어를 사용하는 경우
donkey train -tub ./data -model ./models/mypilot.h5
```



#### 11. 훈련모델을 사용해서 자율주행하기(Auto-Driving)

위 명령어를 통해 학습을 시키면 mypilot.h5라는 h5포맷의 AI파일 생성될 뿐만 아니라 .tflite 포맷의 AI파일도 생성된다.이후에 해당 학습된 모델을 사용하기 위해서는 다음과 같다.

- h5파일을 사용할 경우

```shell
### python 명령어를 사용하는 경우
python manage.py drive --model ./models/mypilot.h5
### donkey 명령어를 사용하는 경우(이거는 시도해보지 않았다)
donkey manage -model ./models/mypilot.h5
```

- tflite파일을 사용할 경우

```shell
### python 명령어를 사용하는 경우
python manage.py drive --model ./models/mypilot.tflite --type tflite_linear
### donkey 명령어를 사용하는 경우(이거는 시도해보지 않았다)
donkey manage -model ./models/mypilot.tflite -type tflite_linear
```





<br>

#### 개선점

<p align="justify">
  아직 강화학습(ddqn)에 대한 부분과, docker를 통해 VirtualLeague를 구축하는 부분에 대해서는
  좀 더 공부해야 할 부분이다.
</p>
<br>
</details>

---

## 만든 사람들

|     PI     |     EL     |   EM   |    EM    |    EM    |    EM    |
|   :-----:   |   :-----:   | :------: |   :-----:   |   :-----:   |   :-----:   |
|   Sunho Park(Prof)    |   Sungwoong Yun    |   Sungjoon Yang    |   Hoil Lee    |   Jeseok Oh    |   Kibum Yun    |

<!--
PI: Sunho Park
EL: Sungwoong Yun
EM: Sungjoon Yang
EM: Hoil Lee
EM: Jeseok Oh
EM: Kibum Yun
-->
## 라이선스

MIT &copy; [YUNSUNGWOONG](mailto:2170004487z@gmail.com)

전문은 [`LICENSE`](LICENSE)에 있습니다. 서브모듈 두 개도 각각 MIT이며 원 저작권 표기를
그대로 보존했습니다 — [donkeycar](https://github.com/AUTONOMOUS-PCC-Inc/donkeycar) (Will Roscoe),
[gym-donkeycar](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar) (Tawn Kramer · Roma Sokolkov · Leigh Johnson).

<!-- Stack Icon Refernces -->

[vscode]: ./images/stack/vscode.svg
[git]: ./images/stack/git.svg
[msys]:  ./images/stack/msys2.svg
[miniconda]:  ./images/stack/miniconda.svg

---

<div align="center">
<sub><strong>AUTONOMOUS PCC, Inc.</strong> · (주)오토노머스피씨씨 — 바이브코딩 캠프 1회차 실습</sub><br>
<sub><a href="https://github.com/AUTONOMOUS-PCC-Inc">github.com/AUTONOMOUS-PCC-Inc</a></sub>
</div>
