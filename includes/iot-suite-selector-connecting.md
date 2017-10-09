> [!div class="op_single_selector"]
> * [Windows에서 C](../articles/iot-suite/iot-suite-connecting-devices.md)
> * [Linux에서 C](../articles/iot-suite/iot-suite-connecting-devices-linux.md)
> * [Node.JS](../articles/iot-suite/iot-suite-connecting-devices-node.md)
> 
> 

## <a name="scenario-overview"></a>시나리오 개요
이 시나리오에서는 원격 분석 toohello 원격 모니터링을 수행 하는 hello를 전송 하는 장치를 만들 [솔루션 미리 구성 된][lnk-what-are-preconfig-solutions]:

* 외부 온도
* 내부 온도
* 습도

간단한 설명을 위해 hello 장치에서 hello 코드 샘플 값을 생성 하지만 실제 센서 tooyour 장치를 연결 하 고 실제 원격 분석 보내기 tooextend hello 샘플 것이 좋습니다.

hello 장치 수 toorespond toomethods hello 솔루션 대시보드에서 호출 하 고 원하는 hello 솔루션 대시보드에 설정 된 속성 값 이기도 합니다.

toocomplete이이 자습서에서는 활성 Azure 계정이 필요 합니다. 계정이 없는 경우 몇 분 만에 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.

## <a name="before-you-start"></a>시작하기 전에
장치에 대한 코드를 작성하기 전에, 미리 구성된 원격 모니터링 솔루션을 프로비전하고 이 솔루션에 새로운 사용자 지정 장치를 프로비전해야 합니다.

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a>미리 구성된 사용자의 원격 모니터링 솔루션 프로비전
hello의 tooan 인스턴스 데이터를 전송 하는이 자습서에서 만드는 hello 장치 [원격 모니터링] [ lnk-remote-monitoring] 솔루션 미리 구성 합니다. 원격 Azure 계정에서 미리 구성 된 솔루션을 모니터링 하는 hello를 프로 비전 이미 하지 않은 경우 단계를 수행 하는 hello를 사용 합니다.

1. Hello에 <https://www.azureiotsuite.com/> 페이지  **+**  toocreate 솔루션입니다.
2. 클릭 **선택** hello에 **원격 모니터링** toocreate 솔루션 패널입니다.
3. Hello에 **원격 만들 모니터링 솔루션** 페이지에서 입력는 **솔루션 이름** 의 선택한 hello 선택 **지역** , toodeploy 한 hello Azure를 선택 합니다. 구독 toowant toouse 합니다. 그런 다음 **솔루션 만들기**를 클릭합니다.
4. Hello를 프로 비전 프로세스가 완료 될 때까지 기다립니다.

> [!WARNING]
> 미리 구성 하는 hello 솔루션 청구 가능한 Azure 서비스를 사용합니다. Tooremove 완료 되 면 구독에서 미리 구성 된 솔루션을 hello 반드시 tooavoid 불필요 한 비용이 있습니다. Hello를 방문 하 여 구독에서 미리 구성 된 솔루션을 완전히 제거할 수 <https://www.azureiotsuite.com/> 페이지.
> 
> 

Hello 모니터링 솔루션 원격 hello에 대 한 프로세스를 프로 비전 완료 되 면, 클릭 **시작** 브라우저에서 tooopen hello 솔루션 대시보드 합니다.

![솔루션 대시보드][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a>Hello 원격 모니터링 솔루션에서에서 장치를 프로 비전
> [!NOTE]
> 솔루션에 장치가 이미 프로비전되어 있으면 이 단계를 건너뜁니다. Hello 클라이언트 응용 프로그램을 만들 때 tooknow hello에 대 한 장치 자격 증명이 필요 합니다.
> 
> 

장치 tooconnect toohello 미리 구성 된 솔루션을 식별 해야 합니다 자체 tooIoT 허브 유효한 자격 증명을 사용 하 여 합니다. Hello 솔루션 대시보드에서 hello 장치 자격 증명을 검색할 수 있습니다. 이 자습서의 뒷부분에 나오는 클라이언트 응용 프로그램에 hello 장치 자격 증명을 포함 합니다.

hello 솔루션 대시보드에 전체 hello 다음 단계를 장치 tooyour 원격 모니터링 솔루션 tooadd 합니다.

1. Hello 왼쪽 아래 모퉁이의 hello 대시보드, 클릭 **장치 추가**합니다.
   
   ![장치 추가][1]
2. Hello에 **사용자 지정 장치** 에서 **새로 추가**합니다.
   
   ![사용자 지정 장치 추가][2]
3. **직접 나만의 장치 ID 정의**를 선택합니다. 같은 장치 ID를 입력 **mydevice**, 클릭 **ID 확인** tooverify 해당 이름을 이미와에 없는 사용 클릭 **만들기** tooprovision hello 장치입니다.
   
   ![장치 ID 추가][3]
4. 참고 hello 장치 자격 증명 (장치 ID, IoT 허브 호스트 이름 및 장치 키)를 확인 합니다. 클라이언트 응용 프로그램 모니터링 솔루션 원격 이러한 값 tooconnect toohello가 필요 합니다. **완료**를 클릭합니다.
   
    ![장치 자격 증명 보기][4]
5. Hello 솔루션 대시보드에 hello 장치 목록에서 장치를 선택 합니다. 그런 다음, hello **장치 세부 정보** 에서 **장치 사용**합니다. 현재 장치의 hello 상태는 **실행**합니다. 원격 모니터링 솔루션 hello 수 이제 장치에서 원격 분석을 수신 하 고 hello 장치에서 메서드를 호출 합니다.

[img-dashboard]: ./media/iot-suite-selector-connecting/dashboard.png
[1]: ./media/iot-suite-selector-connecting/suite0.png
[2]: ./media/iot-suite-selector-connecting/suite1.png
[3]: ./media/iot-suite-selector-connecting/suite2.png
[4]: ./media/iot-suite-selector-connecting/suite3.png

[lnk-what-are-preconfig-solutions]: ../articles/iot-suite/iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: ../articles/iot-suite/iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/