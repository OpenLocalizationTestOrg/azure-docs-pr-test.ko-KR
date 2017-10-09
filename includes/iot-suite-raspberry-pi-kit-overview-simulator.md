## <a name="overview"></a>개요

이 자습서의 단계를 수행 하는 hello를 완료 합니다.

- Hello 원격 모니터링 미리 구성 된 솔루션 tooyour Azure 구독의 인스턴스를 배포 합니다. 이 단계에서는 여러 Azure 서비스를 자동으로 배포하고 구성합니다.
- 컴퓨터 및 원격 모니터링 솔루션 hello와 장치 toocommunicate 사용자를 설정 합니다.
- Hello 샘플 장치 코드 tooconnect toohello 원격 모니터링 솔루션을 업데이트 하 고 hello 솔루션 대시보드에서 볼 수 있는 시뮬레이션 된 원격 분석.

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 활성 Azure 구독이 필요 합니다.

> [!NOTE]
> 계정이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다. 자세한 내용은 [Azure 무료 평가판][lnk-free-trial]을 참조하세요.

### <a name="required-software"></a>필수 소프트웨어

사용자 데스크톱 컴퓨터 tooenable 있습니다 tooremotely 액세스 hello 명령줄로 라스베리 Pi hello에에 SSH 클라이언트를 있어야 합니다.

- Windows에서는 SSH 클라이언트를 포함하지 않습니다. [PuTTY](http://www.putty.org/)를 사용하는 것이 좋습니다.
- 대부분의 Linux 배포판 및 Mac OS 명령줄 SSH 유틸리티 hello를 포함합니다. 자세한 내용은 [Linux 또는 Mac OS를 사용하는 SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md)를 참조하세요.

### <a name="required-hardware"></a>필수 하드웨어

데스크톱 컴퓨터 tooenable tooconnect 하면 원격으로 toohello 명령줄로 라스베리 Pi hello에 있습니다.

[Raspberry Pi 3용 Microsoft IoT 시작 키트][lnk-starter-kits] 또는 동등한 구성 요소입니다. 이 자습서에서는 hello hello 키트에서 다음 항목을 사용 합니다.

- Raspberry Pi 3
- MicroSD 카드(NOOBS 포함)
- USB 미니 케이블
- 이더넷 케이블

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/