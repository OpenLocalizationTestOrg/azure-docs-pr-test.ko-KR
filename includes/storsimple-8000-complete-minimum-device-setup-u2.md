<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello 최소 StorSimple 장치 설치

   > [!NOTE]
   > Hello 최소 장치 설정 완료 되 면 hello 장치 이름을 변경할 수 없습니다.
   
1. Hello에서 장치의 hello 테이블 형식 목록에서 **장치** 블레이드를 선택 하 고 장치를 클릭 합니다. hello 장치는 한 **를 tooset 준비** 상태입니다. hello **장치 구성** 블레이드를 엽니다.

     ![StorSimple 최소 장치 설치 네트워크 인터페이스](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. Hello에 **장치 구성** 블레이드:
   
   1. 장치의 **이름** 을 제공합니다. hello 기본 장치 이름이 hello 장치 모델 및 일련 번호와 같은 정보를 반영합니다. 장치를 too64 문자 toomanage의 식별 이름에 할당할 수 있습니다.
   2. 집합 hello **시간대** hello 지리적 위치 장치 배포 되 고 있는 hello에 기반 합니다. 장치는 모든 예약된 작업에 대해 이 표준 시간대를 사용합니다.
   3. Hello에서 **DATA 0 설정**:

       1. 데이터 0 네트워크 인터페이스에서는 hello로 활성화 되는 네트워크 설정 (IP, 서브넷, 게이트웨이) hello 설치 마법사를 통해 구성 합니다. 또한 데이터 0은 클라우드뿐만 아니라 iSCSI에 대해서도 자동으로 활성화됩니다.

       2. Hello 컨트롤러 0에 대 한 IP 주소 및 컨트롤러 1 고정을 제공 합니다. **hello 컨트롤러 고정 IP 주소 필요 toobe 사용 가능한 Ip 액세스할 수 있는 hello 서브넷 내에서 hello 장치 IP 주소입니다.** Hello DATA 0 인터페이스에 대해 구성 된 4 hello 고정 IPv4 형식 hello에 제공 된 IP 주소 필요 toobe. IPv6 구성을 위한 접두사를 입력 하는 경우 고정 IP 주소는 hello은 이러한 필드에 자동으로 채워집니다.

            ![StorSimple 최소 장치 설치 네트워크 인터페이스](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            고정 IP 주소 hello 컨트롤러에 대 한 hello hello 업데이트 toohello 장치를 서비스에 사용 됩니다. 따라서 hello 고정 Ip는 라우팅 가능 하 고 수 tooconnect toohello 인터넷 이어야 합니다. Hello를 사용 하 여 라우팅할 수 있는 고정된 컨트롤러 Ip를 확인할 수 있습니다 [Test-hcsmconnection] [ Test] cmdlet. Microsoft 업데이트 서버 hello 하는 hello 다음 예제는 라우트된 toohello 인터넷 및 액세스할 수 있는 고정 컨트롤러 Ip 하는 방법을 보여 줍니다.

            ![라우팅 가능한 IP를 표시하는 Test-HcsmConnection](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. **확인**을 클릭합니다. hello 장치 구성을 시작합니다. Hello 장치 구성이 완료 되 면 알림이 표시 됩니다. 장치 상태 변경 사항을 너무 hello**온라인** hello에 **장치** 블레이드입니다.

    ![StorSimple 최소 장치 설치 네트워크 인터페이스](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
