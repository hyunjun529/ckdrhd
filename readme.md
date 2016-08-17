# ckdrhd[창공]

동국대 창의적공학설계 마인드스톰 샘플 코드, 삽질기


## 주의!

이 코드는 동작 예시입니다. 실제로는 조립하는게 반 이상이에요.


## 기본적인 설명

### 코드 짤 때 알아둘 것

1. 텍스트에디터는 다른거 쓰고 Bricx Command Center로는 컴파일하고 실행만 하는걸 추천합니다.
2. 베터리 상태, 경기장 조명, 조립 상태 등에 쉽게 대응할 수 있게 코드를 짭시다.
3. 상태는 되도록 전역변수로 관리하고 모터를 동작하는 것과 센서로 값을 읽는 것은 최대한 함수를 분리해서... 이건 나중에 배울꺼에요.
4. [공식 문서](http://bricxcc.sourceforge.net/nbc/nxcdoc/nxcapi/index.html)를 보면 좋습니다.
5. 더 많은 예시는 [공식 예제](http://bricxcc.sourceforge.net/nbc/nxcsamples/)에서 봅시다.

### Precedes & task

[Precedes](http://bricxcc.sourceforge.net/nbc/nxcdoc/nxcapi/group___command_module_functions_ga59bc18d456217192cffcfb1d0bef3863.html#ga59bc18d456217192cffcfb1d0bef3863)는 쓰레드로 실행합니다. [task](http://bricxcc.sourceforge.net/nbc/nxcdoc/nxcapi/task.html)는 while[1] 걸어서 계속 실행되게 만들어 주면 됩니다. 동시에 실행되니까 한 task에 모든 코드를 넣으려고 하지 마세요.

### 소리 재생에 관해서

[PlayFile](http://bricxcc.sourceforge.net/nbc/nxcdoc/nxcapi/group___sound_module_functions_ga44cdcc978853d615cc6fc27703e8d0cf.html#ga44cdcc978853d615cc6fc27703e8d0cf)로 소리 재생할 수 있긴 한데, 이거 파일을 어떻게 NXT에 넣는지 모르겠습니다. 근데 모든 기기에 공통으로 Woops.rso가 들어있었던거 같으니 그거 쓰시면 됩니다. 소리가 이상하게 재생되면 혹시 한 음성파일이 재생되는 동안 중복으로 재생하고 있는지 확인해보세요. [Wait](http://bricxcc.sourceforge.net/nbc/nxcdoc/nxcapi/group___command_module_functions_ga01e64d2250db0e5b41486e316228983f.html#ga01e64d2250db0e5b41486e316228983f)를 넣으면 해결할 수 있는 부분도 있습니다.

### 모터에 관해서

이거 배터리 잔량에 따라서 출력이 달라지거나, 조립 상태나 무게에 따라서도 달라지고 다루기 까다롭습니다. 모터 출력이나 동작에 문제가 생기면 마인드스톰 하드웨어적인 문제일 가능성이 있으니 주의. 그리고 경험상 여기에 넣을 값이 자주 바뀌게 되는데 전진, 후진 하나 그리고 속도 배율을 따로 매크로로 만들어서 쓰는게 편합니다.

### 터치 센서에 관해서

0, 1로만 들어옵니다. 잘 안 눌리면 앞에다 뭐 달아서 잘 눌리게 해주세요. 눌리고 있으면 계속 1이 나오니까 터치가 된 경우 Wait를 걸어서 일정시간 터치된 시간을 유지해주는 것도 괜찮은 방법입니다. Wait를 걸어줄 때는 센서를 감지하는 함수가 아니라 동작하는 함수에 걸어주는게 좋을겁니다.

### 빛 센서에 관해서

경기장 조명 상태에 따라서, 또 빛 센서와 바닥 사이에 높이에 따라서 측정값이 계속 달라집니다. 평균치를 찾으려 하지 말고 범위로 측정하는게 속 편해요. 아마도 시험 당일날에도 값을 바꿔야 할테니 이것도 매크로로 만들어둡시다. 바닥에서 5cm 벗어나면 정확도가 사라지는거 같았습니다. 라인트레이서를 할 때는 Wait를 걸 필요 없습니다. 또 빛 센서를 받는 것과 모터를 움직이는건 반드시 task분리하세요.

### 초음파 센서에 관해서

범위 엄청 좁아요. 기본은 cm이었던걸로 기억합니다. 또 값이 튑니다. 범위 엄청 좁아요. 사실상 센서는 막대기라고 생각하고 코드를 짜면 됩니다.

### 스마트폰 블루투스와 연결하는 것에 대해서

[NXT Remote Control GitHub](https://github.com/jfedor2/nxt-remote-control) 참고, 블루투스 값이 어떻게 전달되는지는 소스에 나와있으니 bluetoothState를 제어하면 될 꺼라고 예상만 해봅니다. 직접 해보진 않았고 하는걸 본 적은 있는데 그건 nxt 예제였던걸로 기억합니다.