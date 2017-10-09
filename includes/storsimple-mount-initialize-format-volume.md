<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, 초기화 및 볼륨 포맷
1. Hello Microsoft iSCSI 초기자를 시작 합니다.
2. Hello에 **iSCSI 초기자 속성** 창의 hello에 **검색** 탭을 클릭 **포털 검색**합니다.
3. Hello에 **대상 포털 검색** 대화 상자에서 사용할 수 있는 iSCSI 네트워크 인터페이스의 hello IP 주소를 제공 하 고 클릭 **확인**합니다. 
4. Hello에 **iSCSI 초기자 속성** 창의 hello에 **대상** 탭, 찾기 hello **대상 검색**합니다. hello 장치 상태에 표시 되어야 **비활성**합니다.
5. Hello 대상 장치를 선택한 다음 클릭 **연결**합니다. Hello 상태도 변경 해야 hello 장치가 연결 된 후**연결 됨**합니다. (Hello Microsoft iSCSI 초기자를 사용 하는 방법에 대 한 자세한 내용은 참조 [iSCSI 초기자 설치 및 구성 하는 Microsoft][1]).
6. Windows 호스트에서 hello Windows 로고 키 + X를 클릭 한 다음 **실행**합니다. 
7. Hello에 **실행** 대화 상자에서 **Diskmgmt.msc**합니다. 클릭 **확인**, 및 hello **디스크 관리** 대화 상자가 표시 됩니다. hello 오른쪽 창에는 호스트에서 hello 볼륨이 표시 됩니다.
8. Hello에 **디스크 관리** 창의 hello 탑재 된 볼륨이 표시 됩니다 hello 다음 그림에에서 나와 있는 것 처럼 합니다. 발견 된 hello 볼륨을 마우스 오른쪽 단추로 클릭 (hello 디스크 이름 클릭)를 클릭 하 고 **온라인**합니다.
   
     ![볼륨 포맷 초기화](./media/storsimple-mount-initialize-format-volume/HCS_InitializeFormatVolume-include.png) 
9. Hello 볼륨을 마우스 오른쪽 단추로 클릭 (hello 디스크 이름 클릭)를 다시 클릭 하 고 **초기화**합니다.
10. 단순 볼륨 tooformat hello 다음 단계를 수행 합니다.
    
    1. Hello 볼륨 선택 마우스 오른쪽 단추로 클릭 (hello 오른쪽 영역 클릭)를 클릭 하 고 **새 단순 볼륨**합니다.
    2. Hello 새 단순 볼륨 마법사에서 hello 볼륨 크기와 드라이브 문자를 지정 하 고 hello 볼륨은 NTFS 파일 시스템으로 구성 합니다.
    3. 64KB 할당 단위 크기를 지정합니다. 이 할당 단위 크기 hello StorSimple 솔루션에에서 사용 되는 hello 중복 제거 알고리즘와 잘 작동 합니다.
    4. 빠른 포맷을 수행합니다.

![동영상 사용 가능](./media/storsimple-mount-initialize-format-volume/Video_icon.png) **동영상 사용 가능**

toowatch toomount, 초기화, 및 서식과 StorSimple 볼륨을 클릭 하는 방법을 보여 주는 비디오에서 [여기](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/)합니다.

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
