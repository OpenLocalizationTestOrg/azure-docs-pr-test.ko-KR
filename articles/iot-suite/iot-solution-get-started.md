---
title: "MyDriving Azure IoT 예제: 빠른 시작 | Microsoft Docs"
description: "이 방법의 포괄적인 데모 응용 프로그램 시작 tooarchitect 스트림 분석, 기계 학습 및 이벤트 허브를 포함 하 여 Microsoft Azure를 사용 하 여 프로그램 IoT 시스템."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a>MyDriving IoT 시스템: 빠른 시작
MyDriving는 hello 디자인 및 구현 일반적인을 보여 주는 시스템 [사물 인터넷](iot-suite-overview.md) (IoT) 솔루션 장치에서 원격 분석을 수집 하는 hello 클라우드에서 해당 데이터를 처리 및 기계 학습 적용 됩니다. tooprovide 선택 응답 합니다. hello 데모 य ल फ와 자동차의 제어 시스템에서 정보를 수집 하는 어댑터에서 데이터를 사용 하 여 자동차 줄어들며에 대 한 데이터를 기록 합니다. 이 데이터 tooprovide 피드백 비교 tooother 사용자에서 구동 스타일에 사용합니다.

hello 실제 MyDriving의 목적은 사용자 고유의 IoT 솔루션을 만드는 시작 tooget입니다. 하지만 그 이전에 액세스할 수 있습니다 hello MyDriving 응용 프로그램 자체가-테스트 사용자 팀의 구성원으로 진행 합니다. 이렇게 하면 hello 앱 및 소비자를 근거 hello 시스템 경험 hello 아키텍처에 살펴보고 전에 됩니다. 또한, tooHockeyApp, 앱 tootest 사용자의 hello 알파, 베타 분포를 관리 하는 쿨 방법을 소개 합니다.

## <a name="use-hello-mobile-experience"></a>Hello 모바일 환경을 사용 하 여
Android, iOS 또는 Windows 10 장치를 사용 하는 경우 hello MyDriving 앱을 사용할 수 있습니다.

### <a name="android-and-windows-10-mobile-installation"></a>Android 및 Windows 10 Mobile 설치
장치에서:

1. 앱 개발을 허용합니다.
   
   * Android: **설정** > **보안**에서 **알 수 없는 원본**의 앱을 허용합니다.
   * Windows 10: **설정** > **업데이트** > **개발자용**에서 **개발자 모드**를 설정합니다.
2. [HockeyApp](https://rink.hockeyapp.net)에 등록 또는 로그인하여 베타 테스트 팀에 조인합니다. HockeyApp 앱 tootest 사용자의 초기 릴리스를 쉽게 toodistribute 있습니다.
   
   Windows 10을 사용 하는 경우 hello Edge 브라우저를 사용 합니다.
   
   빌드 2016 참석자 인 경우 इ न क hello 동일 hello Microsoft 단추 중 하나를 사용 하 여 hello 회의 대 한 등록 Microsoft 계정 전자 메일입니다. HockeyApp에 이미 등록되어 있습니다.
   
   ![HockeyApp 로그인 화면](./media/iot-solution-get-started/image1.png)
3. 다운로드 하 고 여기에서 hello 앱을 설치 합니다.
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   두 가지 항목이 있습니다. Hello 인증서를 설치 **신뢰할 수 있는 사용자**합니다. Hello 앱을 설치 합니다.

*Windows 10 Mobile에 hello 앱을 시작 하는 문제?* 휴대폰이 업데이트되었거나 너무 오래되었을 수 있습니다. Hello 최신 업데이트를 완료 했습니다 하거나 설치 해야 합니다.

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>iOS 설치
빌드 2016 다닌 경우 HockeyApp에서 테스트 팀의 구성원으로 hello 앱을 다운로드 합니다.

1. IOS 장치에서 로그인 너무[HockeyApp](https://rink.hockeyapp.net)합니다.
   Hello 회의에 등록 하는 동일한 Microsoft 계정 전자 메일을 hello hello Microsoft 로그인 단추 및 기호를 사용 하 여 중 하나를 사용 합니다. (Hello 전자 메일 및 암호 필드를 사용 하지 마십시오.)
   
   ![HockeyApp 로그인 화면](./media/iot-solution-get-started/image1.png)
2. Hello HockeyApp 대시보드에 MyDriving를 선택 하 고 다운로드 합니다.
3. Hello 베타 릴리스를 HockeyApp에 권한을 부여 합니다.
   
   a. 너무 이동**설정** > **일반** > **프로필 및 장치 관리 합니다.**
   
   b. Hello 신뢰 **비트 경기장 GmbH** 인증서입니다.

빌드 2016 참석 하지 않은 경우 있습니다를 빌드하고 배포 hello 앱 사용자가 직접:

1. Hello 코드 다운로드 [GitHub에서]합니다.
2. [Xamarin을 사용하여]빌드 및 배포합니다.

Hello에 자세한 내용을 보려면 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs)합니다.

## <a name="get-an-obd-adapter-optional"></a>OBD 어댑터 가져오기(선택 사항)
이 실제 사물 인터넷 시스템 수행 하는 hello 부분입니다! 없으면 hello 앱을 사용할 수 있지만 hello 실제 항목으로 더 재미 있게 되며 비용이 많이 드는 되지 않습니다.

온보드 진단 (OBD)는 자동차를 사용 하 여 tootune 차고 hello 및 홀수 소음 및 경고 램프 진단 하는 자동차의 hello 기능입니다. 자동차의 훌륭한 아주 오래 전부 아니면 hello 객실 hello 대시보드에서 플랩이 일반적으로 뒤의 어딘가에 소켓을 찾을 수 있습니다. Hello 오른쪽 연결선으로 hello 엔진의 성능 메트릭을 가져올 수 있으며 특정 조정 합니다. OBD 커넥터 hello 일반적인 위치에서 저렴 구입할 수 있습니다. 휴대폰에서 Bluetooth 또는 Wi-fi tooan 앱을 사용 하 여 연결 합니다.

이 예에서 여기 tooconnect 자동차 toohello 클라우드입니다. hello OBD의에서 직접 연결 hello tooyour 전화 않으며 릴레이로 작동 하는 앱입니다. 자동차의 원격 분석 직선 toohello MyDriving IoT 허브, 여기서는 처리 toolog도로 전송 하 고 구동 스타일을 평가 합니다.

tooconnect OBD 장치:

1. 자동차에 OBD 소켓이 있는지 확인합니다.
2. OBD 어댑터를 가져옵니다.
   
   * Android 또는 Windows 휴대폰을 사용하는 경우 Bluetooth 가능 OBD II 어댑터가 필요합니다. [BAFX Products 34t5 Bluetooth OBDII Scan Tool]을 사용했습니다.
   * iOS 휴대폰을 사용하는 경우 Wi-Fi 가능 OBD 어댑터가 필요합니다. [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]를 사용했습니다.
3. 와 함께 제공 되 OBD 어댑터 tooconnect 것 tooyour 전화 hello 지침을 따릅니다. Hello 다음을 염두에 두십시오.
   
   * Bluetooth 어댑터 hello 전화 hello에와 쌍이 되어야 합니다 **설정을** 페이지.
   * Wi-fi 어댑터 hello 범위 192.168.xxx.xxx는 주소가 있어야 합니다.
4. 자동차가 여러 대 있는 경우 각각 별도의 어댑터를 가져올 수 있습니다(최대 3개).

OBD 어댑터를 설정 하지 않은 경우 hello 앱 종료 및 toosimulate는 OBD 원하면 묻습니다 위치와 속도 hello 전화 GPS 수신기 toohello 다시 데이터로 여전히 송신할 수 있습니다.

Hello에 섹션 2.1, "IoT 장치"에 고유한 OBD 장치를 만들기 위한 옵션 및 hello 앱 hello OBD 어댑터의 데이터를 사용 하는 방법에 대 한 자세한 내용을 확인할 수 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs)합니다.

## <a name="use-hello-app"></a>Hello 응용 프로그램을 사용 하 여
Hello 응용 프로그램을 시작 합니다. 초기 퀵 스타트 toowalk는 작동 방법 안내 합니다.

### <a name="track-your-trips"></a>사용자의 주행을 추적합니다.
Hello 레코드 단추 (hello hello 화면 맨 아래에 빨간색 원이 큰) toostart 여행을 누르고 다시 tooend입니다.

![여정 추적에 대 한 hello 레코드 단추 그림](./media/iot-solution-get-started/image2.png)

여행을 시작할 때마다 없는 OBD 장치인 경우 묻는 toouse hello 시뮬레이터 하려는 경우.

이동의 hello 끝 tap hello 중지 단추 수행 요약 합니다.

![주행 요약의 예](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>주행을 검토합니다.
![지난 주행의 예](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>프로필을 검토합니다.
![운전 스타일 프로필의 예](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>테스트 사용자 의견을 보냅니다.
사용자 고유의 IoT 시스템 MyDriving toohelp 신속 작성 했기 때문에 얼마나 잘 작동 하는 방법에 대 한 사용자의 toohear 확실히 하려고 합니다. 다음의 경우 알려주세요.

* 문제 또는 도전 과제가 발생했습니다.
* 만들 때와 더 적합 한 tooyour 시나리오 있는 확장 지점이 있습니다.
* 특정 요구를 보다 효율적인 방식으로 tooaccomplish 찾을 있습니다.
* MyDriving 또는 이 설명서를 개선하기 위한 다른 제안이 있습니다.

자체 hello MyDriving 앱 내에서 기본 제공 hello HockeyApp 피드백 메커니즘을 사용할 수 있습니다: iOS 및 Android 지정 휴대폰은 흔들기 하거나 hello를 사용 하 여 **피드백** 메뉴 명령입니다. 그러면 스크린샷에 자동으로 연결되어 말하는 내용을 알 수 있습니다. 및 모든 든 충돌 인 HockeyApp 수집 hello 크래시 로그 tootell us에 대 한 합니다. Hello 통해 피드백을 제공할 수 있습니다 [HockeyApp 포털]합니다.

또한 [GitHub의 문제점]을 제출하거나 아래에 의견을 남길 수도 있습니다(en-US 버전).

의견에 귀 toohearing에서 있습니다!

## <a name="next-steps"></a>다음 단계
* Hello 탐색 [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs) म 한 설계 및 구축 방법 toounderstand hello 전체 MyDriving 시스템입니다.
* [사용자 고유의 시스템을 만들고 배포](iot-solution-build-system.md) 합니다. hello [MyDriving 참조 가이드](http://aka.ms/mydrivingdocs) 수도 있는 할 hello 대부분의 사용자 지정 영역을 통해 안내 합니다.

[GitHub에서]: https://github.com/Azure-Samples/MyDriving
[Xamarin을 사용하여]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS
[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp 포털]: https://rink.hockeyapp.org
[GitHub의 문제점]: https://github.com/Azure-Samples/MyDriving/issues
