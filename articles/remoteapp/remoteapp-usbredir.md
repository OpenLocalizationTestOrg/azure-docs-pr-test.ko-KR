---
title: "aaaHow Azure RemoteApp에서 USB 장치를 리디렉션할 수 있습니까? | Microsoft Docs"
description: "자세한 방법을 toouse Azure RemoteApp에서 USB 장치의 리디렉션."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Azure RemoteApp에서 USB 장치를 리디렉션하려면 어떻게 합니까?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

장치 리디렉션 Azure RemoteApp에서 hello 앱과 hello USB 장치 연결 된 tootheir 컴퓨터 또는 태블릿을 사용할 수 있도록 합니다. 예를 들어 Azure RemoteApp을 통해 Skype를 공유 하는 경우 사용자가 필요한 toobe 수 toouse 자신의 장치 카메라 합니다.

계속 진행 하기 전에 확인에 hello USB 리디렉션 정보를 읽을 [리디렉션을 사용 하 여 Azure RemoteApp에서](remoteapp-redirection.md)합니다. 그러나 hello 권장 nusbdevicestoredirect:s: * USB 웹 카메라 적합 하지 않은 하 고 일부 USB 프린터 또는 USB 다기능 장치에 대해 작동 하지 않을 수 있습니다. 설계 및 보안상의 이유로 Azure RemoteApp 관리자에 게에 tooenable 리디렉션 장치 클래스 GUID 또는 장치 인스턴스 ID입니다. 사용자가 해당 장치를 사용할 수 있습니다.

비슷한 접근 방식 tooredirect USB 프린터 및 기타 USB 다기능 장치 hello 리디렉션되지 않습니다에이 문서 웹 카메라 리디렉션에 대 한 설명, 있지만 사용할 수 있습니다 **nusbdevicestoredirect:s:*** 명령입니다.

## <a name="redirection-options-for-usb-devices"></a>USB 장치에 대한 리디렉션 옵션
Azure RemoteApp 원격 데스크톱 서비스에 대 한 hello 사용할 수 있는 것 처럼 USB 장치 리디렉션에 대 한 매우 비슷한 메커니즘을 사용 합니다. hello 기본 기술을 사용 하면 지정된 된 장치에 가장 높은 수준의 둘 다의 tooget hello에 대 한 hello 올바른 리디렉션 방법을 선택 하 고 hello를 사용 하 여 RemoteFX USB 장치 리디렉션 **usbdevicestoredirect:s:** 명령입니다. Toothis 명령은 4 개 요소:

| 처리 순서 | 매개 변수 | 설명 |
| --- | --- | --- |
| 1 |* |고급 리디렉션에 의해 선택되지 않은 모든 장치를 선택합니다. 참고: 설계상 USB 웹 카메라에 대해서는 *가 작동하지 않습니다. |
| {장치 클래스 GUID} |지정 된 hello와 일치 하는 모든 장치를 선택 합니다. 장치 설치 클래스입니다. | |
| USB\InstanceID |인스턴스 id입니다. 지정 된 hello에 대 한 지정 된 USB 장치를 선택 합니다. | |
| 2 |-USB\인스턴스 ID |Hello 지정 된 장치에 대 한 hello 리디렉션 설정을 제거합니다. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Hello 장치 클래스 GUID를 사용 하 여 USB 장치 리디렉션
두 가지 toofind hello 장치 클래스 리디렉션에 사용할 수 있는 GUID입니다. 

hello 첫 번째 옵션은 toouse hello [시스템 정의 장치 설치 클래스 사용 가능한 tooVendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx)합니다. Hello 장치 연결 된 toohello 로컬 컴퓨터에 가장 잘 맞는 hello 클래스를 선택 합니다. 디지털 카메라의 경우 이 클래스는 이미징 장치 클래스 또는 비디오 캡처 장치 클래스일 수 있습니다. Toodo 일부 실험 hello 장치 클래스 toofind hello 올바른 클래스 로컬로 hello를 사용 하는 GUID (우리의 사례 hello 웹 카메라)에서 USB 장치를 연결로 필요 합니다.

더 나은 방식으로 또는 hello 두 번째 옵션은 toofollow 이러한 단계 toofind hello 특정 장치 클래스 GUID:

1. Hello 장치 관리자를 열고 hello 장치를 마우스 오른쪽 단추로 클릭 하 고 리디렉션됩니다 찾습니다 다음 hello 속성을 엽니다.
   ![Hello 장치 관리자를 열려면](./media/remoteapp-usbredir/ra-devicemanager.png)
2. Hello에 **세부 정보** 탭, hello 속성 선택 **클래스 Guid**합니다. hello 값 표시 되는 hello 해당 유형의 장치에 대 한 클래스 GUID입니다.
   ![카메라 속성](./media/remoteapp-usbredir/ra-classguid.png)
3. 일치 하는 hello 클래스 Guid 값 tooredirect 장치를 사용 합니다.

예:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

여러 장치 리디렉션이 hello 결합할 수 동일한 cmdlet. 예를 들어: tooredirect 로컬 저장소와 USB 웹 카메라, cmdlet은 다음과 같습니다.

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

장치 리디렉션 클래스 GUID에 의해 설정 하는 경우 클래스 GUID hello에 지정한 컬렉션에 일치 하는 모든 장치가 리디렉션됩니다. 예를 들어 있는 경우 hello 로컬 네트워크에 있는 여러 컴퓨터 hello 동일 USB 웹 카메라, 모든 실행할 수 있습니다 단일 cmdlet tooredirect hello 웹 카메라의 합니다.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Hello 장치 인스턴스 ID를 사용 하 여 USB 장치 리디렉션
Hello를 사용할 수 있습니다 보다 세부적인 제어가 필요할를 줄이려는 경우 장치당 toocontrol 리디렉션 **USB\InstanceID** 리디렉션 매개 변수입니다.

이 방법의 가장 어려운 부분 hello를 발견 하 고 hello USB 장치 인스턴스 id입니다. Toohello 컴퓨터와 특정 USB 장치 hello 액세스할 필요 합니다. 그러고 나서 다음 단계를 수행합니다.

1. 에 설명 된 대로 원격 데스크톱 세션에서 장치 리디렉션 hello를 사용 하도록 설정 [사용 하는 방법 장치 및 리소스에 원격 데스크톱 세션?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. 원격 데스크톱 연결을 열고 **옵션 표시**를 클릭합니다.
3. 클릭 **다른 이름으로 저장** toosave hello 현재 연결 설정 tooan RDP 파일입니다.  
    ![Hello 설정을 RDP 파일로 저장](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. 파일 이름 및 위치, 예: MyConnection.rdp 및이 PC\Documents 선택한 hello 파일을 저장 합니다.
5. 열기 hello MyConnection.rdp 텍스트 편집기를 사용 하 여 파일 및 hello 인스턴스 ID를 찾을 원하는 tooredirect hello 장치입니다.

이제, hello 인스턴스 ID를 사용 하 여 hello cmdlet 뒤에:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>의견 보내기
또한 toorating에이 문서 및 설명 아래로 아래 변경할 수 있는 변경 내용을 toohello 문서 자체 알고 계십니까? 누락된 부분이 있나요? 잘못된 부분이 있나요? 혼동을 줄 수 있는 부분이 있나요? 위로 스크롤 및 클릭 **GitHub에서 편집** toomake 변경-것 나올지 검토를 위해 toous를 다음에 로그 오프 했습니다 되 면 확인할 수 있습니다 프로그램 변경 및 향상 바로 여기 합니다.

