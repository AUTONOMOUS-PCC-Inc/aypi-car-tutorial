<div align="center">

<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/tutorial-banner.svg" alt="바이브코딩 캠프 1회차 — 시뮬레이터에서 직접 운전하고, 그 기록으로 모델을 학습시켜, 운전대를 넘긴다" width="100%">

### 내가 운전한 대로 달리는 차를 만든다.

AUTONOMOUS PCC 바이브코딩 캠프 **1회차(자율주행)** 실습 저장소입니다.<br>
시뮬레이터에서 직접 운전해 데이터를 모으고, 그걸 흉내 내는 모델을 학습시켜, 자율주행을 돌립니다.

![Day](https://img.shields.io/badge/과정-1회차%20하루-0B1B33?style=for-the-badge)
![OS](https://img.shields.io/badge/환경-Windows-1E6FD9?style=for-the-badge)
![Env](https://img.shields.io/badge/conda-aypi--car-16A34A?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.9-1E6FD9?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-A3A3A3?style=for-the-badge)

[**시작하기**](#시작하기) · [**폴더 지도**](#폴더-지도) · [**하루 흐름**](#하루-흐름) · [**자주 막히는 곳**](#자주-막히는-곳) · [**만든 사람들**](#만든-사람들)

</div>

---

## 시작하기

> [!IMPORTANT]
> **수강생은 배포된 설치 안내서(PDF)를 따르세요.** 이 README는 "여기가 뭐 하는
> 저장소지" 싶을 때 보는 지도이고, 설치 절차의 정본은 안내서입니다.
> 설치는 내려받을 것이 많아 **수업 전에 미리** 끝내 두어야 합니다.

받는 것부터 하면 이렇습니다. 안내서 2단계와 같은 명령입니다.

```bat
git clone https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial.git
cd aypi-car-tutorial
git submodule update --init --recursive
```

- 마지막 줄을 빼면 `donkeycar`·`gym-donkeycar` 두 폴더가 **빈 채로** 남습니다. 등록만 하고 내려받지는 않기 때문입니다.
- 경로가 너무 깊으면 Windows에서 실패합니다 ([아래](#자주-막히는-곳) 참고). 안내서대로 `문서\GitHub` 아래에 두세요.

그다음은 안내서로 돌아가 conda 환경(`envs/aypi-car_for_windows.yml`)을 만드세요.

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
| `donkey` 명령을 찾을 수 없다 | `conda activate aypi-car` 를 안 했거나, 설치 후 이 폴더를 **옮겼습니다**. 옮겼다면 `donkeycar` 안에서 `pip install -e .` 를 다시 돌리세요 |
| `cudart64_110.dll` 경고가 아홉 줄쯤 뜬다 | **정상입니다.** GPU가 없어 CPU로 돌겠다는 알림일 뿐입니다. 인터넷의 "opencv를 지우라"는 조언은 **따르지 마세요** |
| `Could not connect to server. Is it running?` | 시뮬레이터가 켜지는 데 걸리는 시간보다 기다려 주는 시간이 짧아서입니다. `myconfig.py` 의 `GYM_CONF` 에서 `start_delay` 를 **15**로 올리세요 |
| 학습이 끝날 기미가 없다 | 원래 오래 걸립니다. 노트북 CPU로 몇천 장이면 수십 분입니다. 시작해 두고 **건드리지 말고** 기다리세요 |
| 시뮬레이터 창이 안 뜬다 | `myconfig.py` 의 `DONKEY_SIM_PATH` 경로를 확인하세요. `DonkeySimWin` 을 이 폴더 **바로 아래**에 풀었어야 합니다 |

그래도 안 되면 **에러 메시지 전체를 복사해서** 강사에게 보여 주세요. 마지막 줄만 보면 원인을 못 찾는 경우가 많습니다.

---

## 만든 사람들

|     PI     |     EL     |   EM   |    EM    |    EM    |    EM    |
|   :-----:   |   :-----:   | :------: |   :-----:   |   :-----:   |   :-----:   |
|   Sungho Park(Prof)    |   Aaron Yoon    |   Sungjoon Yang    |   Hoil Lee    |   Jeseok Oh    |   Kibum Yun    |

<!--
PI: Sungho Park
EL: Aaron Yoon
EM: Sungjoon Yang
EM: Hoil Lee
EM: Jeseok Oh
EM: Kibum Yun
-->

이 저장소는 [`YUNSUNGWOONG/DonkeyBro`](https://github.com/YUNSUNGWOONG/DonkeyBro)에서
이력 전체를 복제해 왔습니다. 원저자가 쓴 윈도우 설치 문서(0~11단계)는 그 저장소와,
[이 저장소의 복제 시점 커밋](https://github.com/AUTONOMOUS-PCC-Inc/aypi-car-tutorial/blob/d587dc3e1c48a752b31a3b5de4d550bfdba60c04/README.md)에
그대로 남아 있습니다. 수업은 conda 방식이라 그 문서를 따르지 않습니다.

## 라이선스

MIT &copy; [YUNSUNGWOONG](mailto:2170004487z@gmail.com)

전문은 [`LICENSE`](LICENSE)에 있습니다. 서브모듈 두 개도 각각 MIT이며 원 저작권 표기를
그대로 보존했습니다 — [donkeycar](https://github.com/AUTONOMOUS-PCC-Inc/donkeycar) (Will Roscoe),
[gym-donkeycar](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar) (Tawn Kramer · Roma Sokolkov · Leigh Johnson).

---

<div align="center">
<sub><strong>AUTONOMOUS PCC, Inc.</strong> · (주)오토노머스피씨씨 — 바이브코딩 캠프 1회차 실습</sub><br>
<sub><a href="https://github.com/AUTONOMOUS-PCC-Inc">github.com/AUTONOMOUS-PCC-Inc</a></sub>
</div>
