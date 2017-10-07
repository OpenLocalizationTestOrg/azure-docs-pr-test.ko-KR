---
title: "StorSimple 장치 컨트롤러 aaaManage | Microsoft Docs"
description: "Toostop를 다시 시작, 종료 또는 StorSimple 장치 컨트롤러를 다시 설정 방법에 대해 알아봅니다."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4ee989d0-956f-4c14-951e-fd4e490ea09d
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/11/2016
ms.author: alkohli
ms.openlocfilehash: 9a86aa0f4a8fd96c36df206774972602c47a49a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-storsimple-device-controllers"></a>StorSimple 장치 컨트롤러 관리
## <a name="overview"></a>개요
이 자습서에서는 StorSimple 장치 컨트롤러에서 수행할 수 있는 hello 서로 다른 작업을 설명 합니다. StorSimple 장치에 hello 컨트롤러는 활성-수동 구성의 중복 (피어) 컨트롤러입니다. 지정된 된 시간에 컨트롤러를 하나만 활성 상태 이며 모든 hello 디스크 및 네트워크 작업을 처리 됩니다. hello 다른 컨트롤러는 수동 모드입니다. Hello 활성 컨트롤러에 오류가 발생 하는 경우 hello 수동 컨트롤러가 자동으로 활성화 됩니다.

이 자습서는 단계별 지침 toomanage hello 장치 컨트롤러를 사용 하 여 포함 된:

* **컨트롤러** hello 섹션 **유지 관리** hello StorSimple 관리자 서비스 페이지
* StorSimple용 Windows PowerShell입니다.

Hello StorSimple Manager 서비스를 통해 hello 장치 컨트롤러를 관리 하는 것이 좋습니다. StorSimple 용 Windows PowerShell을 사용 하 여는 작업을 수행할 수만, hello 자습서 게을 기록 합니다.

이 자습서를 읽은 후에 다음을 수행할 수 있습니다.

* StorSimple 장치 컨트롤러를 다시 시작 또는 종료
* StorSimple 장치 종료
* StorSimple 장치 toofactory 기본값은 다시 설정

## <a name="restart-or-shut-down-a-single-controller"></a>단일 컨트롤러 다시 시작 또는 종료
컨트롤러 다시 시작 또는 종료는 정상적인 시스템 작업의 일환으로 필요하지 않습니다. 단일 장치 컨트롤러에 대한 종료 작업은 실패한 장치 하드웨어 구성 요소가 교체를 필요로 하는 경우에 흔하게 발생합니다. 과도한 메모리 사용 또는 작동하지 않는 컨트롤러 때문에 성능이 영향을 받는 경우에도 컨트롤러를 다시 시작할 필요가 있습니다. Tooenable 원하는 hello 교체 컨트롤러를 테스트 하는 경우 성공적으로 컨트롤러를 사용 하는 교체 컨트롤러 toorestart를 할 수도 있습니다.

중단 tooconnected 초기자 hello 수동 컨트롤러를 사용할 수 없는 장치를 다시 시작 합니다. 수동 컨트롤러가 사용할 수 없거나 활성 hello를 다시 시작한 후 해제 된 경우 컨트롤러 서비스 및 가동 중지 시간 hello 중단 될 수 있습니다.

> [!IMPORTANT]
> * **이렇게 하면 중복 손실과 가동 중지 시간 위험 가능성이 높아져서 실행 중인 컨트롤러를 물리적으로 제거하지 말아야 합니다.**
> * hello 다음 방법은 toohello StorSimple 물리적 장치에만 합니다. Toostart, 중지 및 다시 시작 hello 가상 장치를 참조 하는 방법에 대 한 내용은 [hello 가상 장치에 작동](storsimple-virtual-device-u2.md#work-with-the-storsimple-virtual-device)합니다.
> 
> 

StorSimple 용 hello hello StorSimple Manager 서비스 또는 Windows PowerShell의 Azure 클래식 포털을 사용 하 여 단일 장치 컨트롤러를 종료 하거나 다시 시작할 수 있습니다.

toomanage hello Azure 클래식 포털에서에서 하 여 장치 컨트롤러 수행 hello 단계를 수행 합니다.

#### <a name="toorestart-or-shut-down-a-controller-in-classic-portal"></a>toorestart 또는 클래식 포털에 있는 컨트롤러 종료
1. 너무 이동**장치 > 유지 관리**합니다.
2. 너무 이동**하드웨어 상태** 장치의 두 hello 컨트롤러의 hello 상태 인지 확인 하 고 **정상**합니다.
   
    ![StorSimple 장치 컨트롤러가 정상임을 확인](./media/storsimple-manage-device-controller/IC766017.png)
3. Hello hello 아래에서 **유지 관리** 페이지 **컨트롤러 관리**합니다.
   
    ![StorSimple 장치 컨트롤러 관리](./media/storsimple-manage-device-controller/IC766018.png)</br>
   
   > [!NOTE]
   > 표시 되지 않는 경우 **컨트롤러 관리**, tooinstall 업데이트 해야 합니다. 자세한 내용은 [StorSimple 장치 업데이트](storsimple-update-device.md)를 참조하세요.
   > 
   > 
4. Hello에 **컨트롤러 설정 변경** 대화 상자에서 다음 hello지 않습니다.
   
   1. Hello에서 **컨트롤러 선택** 드롭 다운 목록, 선택 hello 컨트롤러 toomanage 되도록 합니다. hello 옵션은 컨트롤러 0 및 컨트롤러 1입니다. 이러한 컨트롤러는 활성 또는 수동으로 식별됩니다.
      
      > [!NOTE]
      > 경우에 컨트롤러를 관리할 수 없습니다 사용할 수 없는 이거나 꺼져 있는데 아래 작업 hello 드롭 다운 목록에 나타나지 것입니다.
      > 
      > 
   2. Hello에서 **동작 선택** 드롭 다운 목록에서 선택 **컨트롤러 다시 시작** 또는 **컨트롤러를 종료**합니다.
      
       ![StorSimple 장치 수동 컨트롤러 다시 시작](./media/storsimple-manage-device-controller/IC766020.png)
   3. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-manage-device-controller/IC740895.png)에서도 확인할 수 있습니다.

Hello 컨트롤러를 종료 되거나 다시 시작 됩니다. hello에 적용 한 hello 선택에 따라 수행 되는 작업의 hello 세부 정보를 요약 하는 hello 표에서 **컨트롤러 설정 변경** 대화 상자.  

| 선택 번호 | 선택한 경우... | 발생합니다. |
| --- | --- | --- |
| 1. |Hello 수동 컨트롤러 다시 시작 합니다. |작업 toorestart hello 컨트롤러 만들어지고 hello 작업이 올바르게 만들어진 후 알림을 받게 됩니다. 그러면 시작 hello 컨트롤러를 다시 시작 합니다. 에 액세스 하 여 hello를 다시 시작 프로세스를 모니터링할 수 있습니다 **서비스 > 대시보드 > 작업 로그를 볼** 다음 특정 tooyour 서비스 매개 변수 별로 필터링 합니다. |
| 2. |Hello 활성 컨트롤러를 다시 시작 합니다. |다음 경고 hello 표시 됩니다: "hello 활성 컨트롤러를 다시 시작 하면 hello 장치 장애 조치 됩니다 toohello 수동 컨트롤러. 시겠습니까 toocontinue "? </br>이 작업을 tooproceed, 선택에 hello 다음 단계에 사용 되는 동일한 toothose toorestart hello 수동 컨트롤러 됩니다 (선택 번호 1 참조). |
| 3. |Hello 수동 컨트롤러를 종료 합니다. |Hello 메시지의 뒤에 표시 됩니다: "toopush 해야는 종료 완료 되 면 hello 전원 단추 컨트롤러 tooturn에 해당 합니다. 이 컨트롤러 아래로 tooshut 하 시겠습니까 "? </br>이 작업을 tooproceed, 선택에 hello 다음 단계에 사용 되는 동일한 toothose toorestart hello 수동 컨트롤러 됩니다 (선택 번호 1 참조). |
| 4. |Hello 활성 컨트롤러를 종료 합니다. |Hello 메시지의 뒤에 표시 됩니다: "toopush 해야는 종료 완료 되 면 hello 전원 단추 컨트롤러 tooturn에 해당 합니다. 이 컨트롤러 아래로 tooshut 하 시겠습니까 "? </br>이 작업을 tooproceed, 선택에 hello 다음 단계에 사용 되는 동일한 toothose toorestart hello 수동 컨트롤러 됩니다 (선택 번호 1 참조). |

#### <a name="toorestart-or-shut-down-a-controller-in-windows-powershell-for-storsimple"></a>toorestart 또는 StorSimple 용 Windows PowerShell에서 컨트롤러 종료
Hello 다운 tooshut 단계를 수행 하거나 hello Azure 클래식 포털에서에서 StorSimple 장치에서 단일 컨트롤러를 다시 시작 합니다.

1. 원격 컴퓨터에서 텔넷 세션 또는 직렬 콘솔 hello 사용 하 여 액세스 hello 장치입니다. TooController 0을 연결 하거나 다음 hello로 컨트롤러 1의 단계를 [PuTTY를 사용 하 여 장치 직렬 콘솔 tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console)합니다.
2. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.
3. Hello 배너 메시지에 너무 연결 된 hello 컨트롤러 기록해 (컨트롤러 0 또는 컨트롤러 1)와 활성 hello 인지 hello 수동 (대기) 컨트롤러 인지 합니다.
   
   * hello 프롬프트 형식에서 단일 컨트롤러 아래로 tooshut:
     
       `Stop-HcsController`
     
       에 연결 되어 있는 hello 컨트롤러 종료 됩니다. Hello 활성 컨트롤러를 중지 하는 경우 다음이 장애 조치 됩니다 toohello 수동 컨트롤러 종료 되기 전에.
   * toorestart hello 프롬프트에서 컨트롤러를 입력 합니다.
     
       `Restart-HcsController`
     
       에 연결 되어 있는 hello 컨트롤러 다시 시작 됩니다. Hello 활성 컨트롤러를 다시 시작 하면 hello를 다시 시작 전에 toohello 수동 컨트롤러를 통해 실패 합니다.

## <a name="shut-down-a-storsimple-device"></a>StorSimple 장치 종료
이 섹션에서는 어떻게 tooshut는 실행 또는 원격 컴퓨터에서 실패 한 StorSimple 장치입니다. 두 hello 장치 컨트롤러를 종료 한 후 장치 기능이 비활성화 됩니다. Hello 물리적으로 이동 하는 장치나 서비스에서 제거 됩니다. 장치 종료 수행 됩니다.

> [!IMPORTANT]
> Hello 장치를 종료 하기 전에 hello 장치 구성의 hello 상태를 확인 합니다. 너무 이동**장치 > 유지 관리 > 하드웨어 상태** hello에 대 한 구성 요소를 모두의 hello LED 상태가 녹색 인지 확인 합니다. 정상 장치만이 녹색 상태가 됩니다. 장치가 종료 하 tooreplace 오작동 구성 요소, 오류 (빨간색) 나타납니다 또는 저하 (노란색) 상태에 대 한 개별 구성 요소의 hello 합니다.
> 
> 

#### <a name="tooshut-down-a-storsimple-device"></a>StorSimple 장치 아래로 tooshut
1. 사용 하 여 hello [다시 시작 하거나 컨트롤러를 종료](#restart-or-shut-down-a-single-controller) 프로시저 tooidentify 및 장치에서 hello 수동 컨트롤러를 종료 합니다. StorSimple 용 Windows PowerShell 또는 hello Azure 클래식 포털에서에서이 작업을 수행할 수 있습니다.
2. 활성 컨트롤러 hello 아래로 단계 tooshut 위에 hello를 반복 합니다.
3. 이제 해야 hello에 toolook hello 장치의 백플레인에서. Hello 두 명의 컨트롤러를 완전히 종료 후 hello 두 hello 컨트롤러 상태 led가 빨간색으로 깜박입니다. 플립 hello 전원 전원 및 냉각 모듈 (Pcm) 모두 스위치가이 이번에 완전히 tooturn hello이 장치를 해야 할 경우 toohello OFF 위치입니다. Hello 장치 수 없도록 해제 해야 합니다.

<!--#### tooshut down a StorSimple device in Windows PowerShell for StorSimple

1. Connect toohello serial console of hello StorSimple device by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-serial-console).

1. In hello serial console menu, verify from hello banner message that hello controller you are connected toois hello passive controller. If you are connected toohello active controller, disconnect from this controller and connect toohello other controller.

1. In hello serial console menu, choose option 1, **log in with full access**.

1. At hello prompt, type:

    `Stop-HCSController`

    This should shut down hello current controller. tooverify whether hello shutdown has finished, check hello back of hello device. hello controller status LED should be solid red.

1. Repeat steps 1 through 4 tooconnect toohello active controller and then shut it down.

1. After both hello controllers are completely shut down, hello status LEDs on both should be blinking red. If you need tooturn off hello device completely at this time, flip hello power switches on both Power and Cooling Modules (PCMs) toohello OFF position.-->

## <a name="reset-hello-device-toofactory-default-settings"></a>Hello 장치 toofactory 기본 설정으로 초기화
> [!IMPORTANT]
> 장치 toofactory 기본 설정을 tooreset 해야 할 경우 Microsoft 지원에 문의 합니다. 아래에서 설명 하는 hello 절차는 Microsoft 기술 지원 서비스와 함께에 사용 해야 합니다.
> 
> 

이 절차에서는 설명 방법을 tooreset StorSimple 용 Windows PowerShell을 사용 하 여 Microsoft Azure StorSimple 장치 toofactory 기본 설정 합니다.
장치를 초기화 합니다. 기본적으로 hello 전체 클러스터에서 모든 데이터와 설정이 제거 됩니다.

Microsoft Azure StorSimple 장치 toofactory 기본 설정을 hello 단계 tooreset 다음을 수행 합니다.

### <a name="tooreset-hello-device-toodefault-settings-in-windows-powershell-for-storsimple"></a>tooreset hello 장치 toodefault 설정을 Windows PowerShell에서 StorSimple 용
1. Hello 장치 직렬 콘솔을 통해 액세스 합니다. 연결 된 toohello 활성 컨트롤러는 hello 배너 메시지 tooensure를 확인 합니다.
2. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다.
3. Hello 프롬프트에서 다음 명령 tooreset hello 전체 클러스터, 모든 데이터, 메타 데이터 및 컨트롤러 설정이 제거 hello를 입력 합니다.
   
    `Reset-HcsFactoryDefault`
   
    tooinstead 단일 컨트롤러를 다시 설정, hello를 사용 하 여 [Reset-hcsfactorydefault](http://technet.microsoft.com/library/dn688132.aspx) hello 사용 하 여 cmdlet `-scope` 매개 변수.)
   
    hello 시스템에는 여러 번 다시 부팅 됩니다. Hello 재설정 성공적으로 완료 되 면 알림이 표시 됩니다. Hello 시스템 모델에 따라 분이 지나야 45-60 8100 장치에 대 한 및 8600 toofinish 60 ~ 90 분이이 프로세스입니다.
   
   > [!TIP]
   > * 이전 hello를 사용 하거나 업데이트 1.2를 사용 하는 경우 `–SkipFirmwareVersionCheck` 매개 변수 tooskip hello 펌웨어 버전 확인 (그렇지 않은 경우 펌웨어 불일치 오류 나타납니다: tooa hello 펌웨어 버전 불일치로 인해 공장 재설정을 계속할 수 없습니다. )을 참조하세요.
   > * hello 정부 포털에서 업데이트 1 또는 1.1 실행 되 고 (전 업데이트 1과 함께 제공 된 교체 컨트롤러를 성공적으로 단일 또는 이중 컨트롤러 교체를 수행 했는지 여부를 지정 하는 StorSimple 장치에 대 한 hello 공장 재설정 프로시저가 실패할 수도 있습니다. 소프트웨어)입니다. 하면 이런 경우가 hello 공장 기본 설정 이미지 hello 전 업데이트 1 소프트웨어에 대 한 SHA1 파일이 존재 하지 않는 hello 컨트롤러에 있는지에 대 한 유효성을 검사 합니다. 이 팩터리가 오류를 다시 설정, tooassist Microsoft 지원에 문의 표시 되 면 hello로 하면 다음 단계입니다. 이 문제는 업데이트 1 또는 이후 소프트웨어와 hello 팩터리에서 선적 된 교체 컨트롤러와 표시 되지 않습니다.
   > 
   > 

## <a name="questions-and-answers-about-managing-device-controllers"></a>장치 컨트롤러를 관리하는 방법에 대한 질문 및 답변
이 섹션에서는 요약할 hello 자주 묻는 질문 중 일부 StorSimple 장치 컨트롤러 관리 관련 항목입니다.

**Q.** 장치에서 컨트롤러를 hello 둘 다 하는 경우 어떤 일이 생기를 다시 시작 하거나 hello 활성 컨트롤러 종료는 정상 상태이 고 기능으로 설정 하 고 있습니까?

**A.** 장치에서 hello 컨트롤러가 모두 정상 상태이 고 켜져 있는데 경우, 메시지가 표시 됩니다에 대 한 확인 합니다. 선택할 수 있습니다.

* **Hello 활성 컨트롤러를 다시 시작** – 활성 컨트롤러를 다시 시작에서 않도록 hello 장치 toofail toohello 수동 컨트롤러를 통해 알림을 받게 됩니다. hello 컨트롤러 다시 시작 됩니다.
* **활성 컨트롤러 종료** – 활성 컨트롤러를 종료하면 가동이 중지된다는 알림이 표시됩니다. Toopush hello 장치 tooturn hello 컨트롤러의 전원 단추를 hello 해야 합니다.

**Q.** Hello 내 장치의 수동 컨트롤러가 사용할 수 없거나 해제 하는 경우 해제 및 다시 시작 하거나 hello 활성 컨트롤러를 종료 하려면 어떻게 됩니까?

**A.** Hello 장치의 수동 컨트롤러가 사용할 수 없는 이거나 꺼져 하 고 하기로 합니다.

* **Hello 활성 컨트롤러를 다시 시작** – 알려 hello 서비스의 임시 중단에서 hello 작업을 계속 하면 및 확인을 위해 나타납니다.
* **활성 컨트롤러 종료** – 알려는 hello 작업을 계속 하면 가동이 중단, 및가 toopush hello 전원 단추에 하나 또는 두 컨트롤러 tooturn hello 장치에 필요 합니다. 확인하라는 메시지가 표시됩니다.

**Q.** hello 컨트롤러 다시 시작 또는 종료에 실패 한 경우 tooprogress?

**A.** 다음 경우 롤러를 다시 시작하거나 종료하는 데 실패할 수 있습니다.

* 장치 업데이트를 진행 중입니다.
* 컨트롤러 다시 시작이 이미 진행 중입니다.
* 컨트롤러 종료가 이미 진행 중입니다.

**Q.** 컨트롤러를 다시 시작하거나 종료하는 경우 어떻게 확인합니까?

**A.** Hello hello 유지 관리 페이지에서 컨트롤러의 상태를 확인할 수 있습니다. hello 컨트롤러의 상태는 컨트롤러를 다시 시작 하거나 종료 되었는지 여부를 나타냅니다. 또한 hello 경고 페이지 hello 컨트롤러를 다시 시작 하거나 종료 하는 경우 정보 제공 알림이 포함 됩니다. hello 컨트롤러 다시 시작 및 종료 작업 hello 작업 로그에 기록 됩니다. 작업 로그에 대 한 자세한 내용은 이동 너무[hello 작업 로그를 볼](storsimple-service-dashboard.md#view-the-operations-logs)합니다.

**Q.** 컨트롤러 장애 조치의 결과로 모든 영향 toohello I/o는 무엇입니까?

**A.** 초기자와 활성 컨트롤러 간의 TCP 연결이 hello 컨트롤러 장애 조치를 설정 하지만 hello 수동 컨트롤러가 작업 다시 설정 됩니다. 이 작업의 hello 동안 임시 (30 초 미만) 일시 중지 hello 장치와 초기자 간의 I/O 활동이 있을 수 있습니다.

**Q.** 종료 및 제거 된 후 내 컨트롤러 tooservice를 반환 하는 방법

**A.** 컨트롤러 tooservice tooreturn 삽입 해야 hello 섀시 안으로 설명 된 대로 [StorSimple 장치에서 컨트롤러 모듈 교체](storsimple-controller-replacement.md)합니다.

## <a name="next-steps"></a>다음 단계
* 이 자습서에 나열 된 hello 절차를 사용 하 여 확인할 수 없는 StorSimple 장치 컨트롤러와 모든 문제를 발생 하는 경우 [Microsoft 지원에 문의](storsimple-contact-microsoft-support.md)합니다.
* hello StorSimple Manager 서비스를 사용 하 여에 대 한 더 toolearn 너무 이동[사용 하 여 StorSimple 장치를 StorSimple Manager 서비스 tooadminister hello](storsimple-manager-service-administration.md)합니다.

