<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>hello 직렬 콘솔을 통해 tooconnect
1. 직렬 케이블 toohello 장치 (직접 또는 USB 직렬 어댑터를 통해)에 연결 합니다.
2. 열기 hello **제어판**를 연 다음 hello **장치 관리자**합니다.
3. Hello 다음 그림에에서 표시 된 대로 hello COM 포트를 식별 합니다.
   
     ![직렬 콘솔을 통해 연결](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. PuTTY를 시작합니다. 
5. Hello 오른쪽 창에서 변경 hello **연결 유형** 너무**직렬**합니다.
6. Hello 오른쪽 창에서 hello 적절 한 COM 포트를 입력 합니다. Hello 직렬 구성 매개 변수가 다음과 같이 설정 되어 있는지 확인 합니다.
   
   * 속도: 115,200
   * 데이터 비트: 8
   * 정지 비트: 1
   * 패리티: 없음
   * 흐름 제어: 없음
     
     이러한 설정은 hello 다음 그림에에서 표시 됩니다.
     
     ![PuTTY 설정](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Hello 기본 흐름 제어 설정이 작동 하지 않으면 hello 흐름 제어 tooXON/XOFF를 설정 해 보십시오.
     > 
     > 
7. 클릭 **열려** toostart 직렬 세션입니다.

