---
title: "Azure 로그 통합 aaaGet 시작 | Microsoft Docs"
description: "Tooinstall hello Azure 로그 통합 서비스 및 Azure 저장소, Azure 감사 로그 및 Azure 보안 센터 경고에서 로그 통합 방법에 대해 알아봅니다."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Azure 로그 통합과 Azure 진단 로깅 및 Windows 이벤트 전달
Azure 로그 (AzLog) 통합 하면 Azure 리소스에서 toointegrate 원시 로그 온-프레미스 보안 정보 및 이벤트 관리 SIEM () 시스템에 있습니다. 이러한 통합 가능한 toohave 모든 자산에 대 한 통합된 보안 대시보드를 사용 하면, 온-프레미스 또는 hello 클라우드에서 집계할 수 있도록 상관 관계를 설정, 분석 및 응용 프로그램와 관련 된 보안 이벤트에 대 한 경고입니다.
>[!NOTE]
Azure 로그 통합에 대 한 자세한 내용은 hello를 검토할 수 있습니다 [Azure 로그 통합 개요](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview)합니다.

이 문서는 hello hello Azlog 서비스 설치에 집중 하 고 Azure 진단을 hello 서비스 통합 하 여 Azure 로그 통합을 시작 하는 데 도움이 됩니다. Azure 로그 통합 서비스 hello 수 toocollect Azure IaaS에서 배포 된 가상 컴퓨터에서 Windows 보안 이벤트 채널 hello에서 Windows 이벤트 로그 정보 있게 됩니다. 이 매우 유사한 너무 "이벤트 전달"을 사용 하 여 있을 온-프레미스입니다.

>[!NOTE]
>Azure 로그 통합 toohello에 hello 기능 toobring hello 출력 SIEM hello SIEM 자체에서 제공 됩니다. Hello 문서를 참조 하세요 [SIEM 온-프레미스와 Azure 로그 통합 통합](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) 자세한 정보에 대 한 합니다.

운영 체제 이상 hello Windows Server 2008 r 2를 사용 하는 물리적 또는 가상 컴퓨터에 매우 명확한-toobe hello Azure 로그 통합 서비스를 실행 (Windows Server 2012 R2 또는 Windows Server 2016은 기본 설정).

hello 물리적 컴퓨터는 온-프레미스를 실행할 수 있습니다 (또는 호스팅 서비스 공급자 사이트에서). 해당 가상 컴퓨터에 온-프레미스 수 toorun hello Azure 로그 통합 서비스는 가상 컴퓨터를 선택 하면 Microsoft Azure와 같은 공용 클라우드 또는 합니다.

실제 hello 또는 hello Azure 로그 통합 서비스를 실행 하는 가상 컴퓨터 네트워크 연결 toohello Azure 공용 클라우드에서 필요 합니다. 이 문서의 단계 hello 구성에 자세히 설명 합니다.

## <a name="prerequisites"></a>필수 조건
AzLog hello 설치에는 최소한 다음 항목 hello이 필요 합니다.
* **Azure 구독**. 아직 구독이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)을 등록할 수 있습니다.
* A **저장소 계정** Windows Azure 진단 로깅에 사용할 수 있는 (미리 구성 된 저장소 계정을 사용 하거나 새로 만들 수 있습니다 – 됩니다에 대해서도 설명 방법을 tooconfigure hello이 문서의 뒷부분에 나오는 저장소 계정)
  >[!NOTE]
  시나리오에 따라 저장소 계정이 필요하지 않을 수도 있습니다. Hello에 대 한 Azure 진단 시나리오 필요한이 문서에서 설명 합니다.
* **두 시스템**: hello Azure 로그 통합 서비스를 실행 하는 컴퓨터 및 모니터링 됩니다 아니며 보낸 toohello Azlog 서비스 컴퓨터의 로깅 정보를 포함 하는 컴퓨터입니다.
   * 으로 실행 하는 VM이는 toomonitor –를 원하는 컴퓨터는 [Azure 가상 컴퓨터](../virtual-machines/virtual-machines-windows-overview.md)
   * Hello Azure 로그 통합 서비스를 실행 하는 컴퓨터 이 컴퓨터는 SIEM에 나중에 가져올 수 있는 모든 hello 로그 정보를 수집 합니다.
    * 이 시스템은 온-프레미스 또는 Microsoft Azure에 위치할 수 있습니다.  
    * X64 실행 toobe 필요한 버전의 Windows server 2008 R2 SP1 이상이.NET 4.5.1이 설치 되어 있고 합니다. 다음 hello 문서에서 설치한 hello.NET 버전을 확인할 수 있습니다 [하는 방법:.NET Framework 버전은 설치 확인](https://msdn.microsoft.com/library/hh925568)  
    Azure 진단 로깅에 사용 되는 연결 toohello Azure 저장소 계정이 있어야 합니다. 이 문서의 뒷부분에서 이 연결을 확인하는 방법에 대한 지침을 제공합니다.

간단히 살펴보려면 hello는 hello Azure 포털을 사용 하 여 가상 컴퓨터를 만드는 과정에 대 한 hello 아래 동영상을 살펴보세요.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>배포 고려 사항
Azure 로그 통합을 테스트 하는 동안에 hello 최소 운영 체제 요구 사항을 충족 하는 모든 시스템을 사용할 수 있습니다. 그러나 프로덕션 환경 hello에 대 한 부하를 내부 또는 외부 조정 tooplan이 필요할 수 있습니다.

이벤트 볼륨 높을 경우 hello Azure 로그 통합 서비스 (실제 또는 가상 컴퓨터 마다 인스턴스가 하나씩)의 여러 인스턴스를 실행할 수 있습니다. 또한 WAD (Windows) 및 구독 tooprovide toohello 인스턴스 수가 hello에 대 한 Azure 진단 저장소 계정 용량에 따라 균형을 로드할 수 있습니다.
>[!NOTE]
이 이번에 없으므로 tooscale azure 인스턴스 통합 컴퓨터 (예: 컴퓨터의 경우 hello Azure 로그 통합 서비스를 실행 하는)를 기록 하는 경우 또는 저장소 계정 또는 구독에 대해 구체적으로 제시 합니다. 확장 결정은 이러한 각 영역에서의 성능 관찰을 기반으로 해야 합니다.

Hello Azure 로그 통합 서비스 toohelp hello 옵션 tooscale 성능을 향상 시킬 수도 있습니다. 다음 성능 매트릭이 hello toorun hello Azure 로그 통합 서비스를 선택 하는 hello 컴퓨터를 크기 조정에서 수행할 수 있습니다.
* 8-프로세서(코어) 컴퓨터에서는 Azlog 통합자의 인스턴스 하나가 하루에 약 2400만 이벤트를 처리할 수 있습니다(~1M/시간).

* 4-프로세서(코어) 컴퓨터에서는 Azlog 통합자의 인스턴스 하나가 하루에 약 150만 이벤트를 처리할 수 있습니다(~62.5K/시간).

## <a name="install-azure-log-integration"></a>Azure 로그 통합 설치
Azure 로그 통합 tooinstall 해야 toodownload hello [Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) 설치 파일입니다. Hello 설치 루틴을 통해 실행 하 고 원격 분석 정보 tooMicrosoft tooprovide 할지를 결정 합니다.  

![원격 분석 확인란이 선택된 설치 화면](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> Microsoft toocollect 원격 분석 데이터를 허용 하는 것이 좋습니다. 이 옵션을 선택 취소하여 원격 분석 데이터의 컬렉션을 해제할 수 있습니다.
>


hello Azure 로그 통합 서비스가 설치 되어 있는 hello 컴퓨터에서 원격 분석 데이터를 수집 합니다.  

수집된 원격 분석 데이터는 다음과 같습니다.

* Azure 로그 통합 실행 중에 발생하는 예외
* 쿼리 및 처리 된 이벤트의 hello 수에 대 한 메트릭
* 어떤 Azlog.exe 명령줄 옵션이 사용되었는지에 대한 통계

hello 설치 프로세스는 hello 비디오 아래에서 다룹니다.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>사후 설치 및 유효성 검사 단계
기본 설치 루틴 hello를 완료 한 후 준비 단계 tooperform 사후 설치 및 유효성 검사 단계 넌:
1. 관리자 PowerShell 창을 열고 너무**c:\Program Files\Microsoft Azure 로그 통합**
2. tootake 필요한 hello 첫 번째 단계는 AzLog Cmdlet 가져온 tooget hello입니다. Hello 스크립트를 실행 하 여 할 수 있습니다 **LoadAzlogModule.ps1** (공지 hello "입니다. \"에서 다음 명령을 hello). **.\LoadAzlogModule.ps1**을 입력하고 **Enter** 키를 누릅니다.  
아래 hello 그림에 표시 하는 것과 같이 표시 됩니다. </br></br>
![원격 분석 확인란이 선택된 설치 화면](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. 이제 tooconfigure AzLog toouse 특정 Azure 환경에 필요 합니다. "Azure 환경"은 Azure 클라우드 데이터 센터와 toowork 원하는의 hello "type"입니다. 지금은 여러 Azure 환경의 있을 때는 hello 현재 관련 옵션은 **azure 클라우드** 또는 **AzureUSGovernment**합니다.   관리자 권한 PowerShell 환경에서 현재 **c:\program files\Microsoft Azure Log Integration\** 위치인지 확인합니다. </br></br>
    한 번 hello 명령을 실행합니다. </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud``(Azure Commercial의 경우)

      >[!NOTE]
      Hello 명령이 성공 하는 경우 한 피드백이 수신 되지 않습니다.  사용 하려는 경우 toouse hello 미국 정부 Azure 클라우드, **AzureUSGovernment** (에 대 한 이름 변수-hello) 미국 정부 클라우드 hello에 대 한 합니다. 현재 다른 Azure 클라우드는 지원되지 않습니다.  
4. 시스템을 모니터링 하려면 먼저 Azure 진단에 대 한 hello hello 저장소 계정의 이름으로 사용에서 해야 합니다.  Hello Azure 포털 이동 너무**가상 컴퓨터** 모니터링 하는 hello 가상 컴퓨터를 찾습니다. Hello에 **속성** 섹션에서 선택 **진단 설정을**합니다.  클릭 **에이전트** 메모 hello 저장소 계정 이름 지정 합니다. 이후 단계에서 이 계정 이름이 필요합니다.
![Azure 진단 설정](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Azure 진단 설정](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      모니터링 된 가상 컴퓨터를 만드는 동안 설정 되지 않은 경우 주어 집니다 hello 옵션 tooenable 위와 같이 것입니다.
5. 이제 우리 주의 백 toohello Azure 로그 통합 컴퓨터 전환 우리 합니다. Tooverify 있다고 hello 시스템에서 저장소 계정을 연결 toohello 설치한 Azure 로그 통합이 필요 합니다. hello 물리적 컴퓨터 또는 서비스 toohello 저장소 계정 tooretrieve 정보 각각 hello에 구성 된 대로 Azure 진단에 의해 기록에 액세스 해야 하는 Azure 로그 통합 hello를 실행 중인 가상 컴퓨터 시스템을 모니터링 합니다.  
  1. [여기](http://storageexplorer.com/)에서 Azure Storage 탐색기를 다운로드할 수 있습니다.
  2. Hello 설치 루틴 예행
  3. Hello 설치가 끝나면 **다음** hello 확인란 및 **시작 Microsoft Azure 저장소 탐색기** 확인 합니다.  
  4. TooAzure에 로그인 합니다.
  5. Azure 진단 구성 hello 저장소 계정을 볼 수 있는지 확인 합니다.  
![저장소 계정](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. 저장소 계정에는 몇 가지 옵션이 있습니다. 그중 하나가 **테이블**입니다. **테이블**에 **WADWindowsEventLogsTable**이 표시되어야 합니다. </br></br>
   ![저장소 계정](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Azure 진단 로깅 통합
이 단계에서는 hello Azure 로그 통합 서비스 tooconnect toohello 저장소 계정을 hello 로그 파일이 포함 된를 실행 하는 hello 컴퓨터를 구성 합니다.
toocomplete이이 단계를 몇 가지 들겠지만 필요 합니다.  
* **FriendlyNameForSource:** hello Azure 진단에서 toostore 정보를 가상 컴퓨터를 구성 하는 toohello 저장소 계정에 적용할 수 있도록 하는 친숙 한 이름
* **: StorageAccountName** hello Azure 진단 프로그램을 구성할 때 지정한 hello 저장소 계정 이름입니다.  
* **StorageKey:** 이 가상 컴퓨터에 대 한 hello Azure 진단 정보 저장 된 hello 저장소 계정에 대 한 hello 저장소 키입니다.  

다음 단계 tooobtain hello 저장소 키 hello를 수행 합니다.
 1. Toohello 찾아보기 [Azure 포털](http://portal.azure.com)합니다.
 2. Hello Azure의 hello 탐색 창에서 콘솔 toohello 아래로 스크롤하여 클릭 **더 많은 서비스입니다.**

 ![추가 서비스](./media/security-azure-log-integration-get-started/more-services.png)
 3. 입력 **저장소** hello에 **필터** 입력란. **저장소**를 입력한 뒤 나타나는 **저장소 계정**을 클릭합니다.

   ![필터 상자](./media/security-azure-log-integration-get-started/filter.png)
 4. 저장소 계정 목록이 표시 됩니다 tooLog 저장소를 할당 하는 hello 계정에 두 번 클릭 합니다.

   ![저장소 계정 목록](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. 클릭 **선택키가** hello에 **설정을** 섹션.

  ![액세스 키](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. 복사 **key1** hello 다음 단계를 위해 액세스할 수 있는 안전한 위치에 저장 합니다.

   ![두 개의 액세스 키](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. Azure 로그 통합 설치한 hello 서버에서 관리자 권한 명령 프롬프트 (관리자 권한 명령 프롬프트 창을 여기 사용 하는지 참고, 하지 관리자 권한 PowerShell 콘솔)를 엽니다.
 8. 너무 이동**c:\Program Files\Microsoft Azure 로그 통합**
 9. ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> `` 실행 </br> 예를 들어 ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` XML hello 이벤트에서를 구독 ID tooshow hello 싶으면, hello 구독 ID toohello 친숙 한 이름을 추가: ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` 또는 예를 들어``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Too60 분을 기다린 하 후 ग द ृ hello hello 저장소 계정에서 가져온 키를 누릅니다. 열기 tooview **이벤트 뷰어 > 전역 로그 > 전달 된 이벤트** hello Azlog 통합자에 합니다.

여기 위에서 다룬 hello 단계를 통과 하는 비디오를 볼 수 있습니다.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>그렇다면 데이터는 hello 이벤트 전달 폴더에 표시 되지?
하는 경우 1 시간 후 데이터가 표시 되지 않는 hello에 **전달 된 이벤트** 다음 폴더:

1. Hello 컴퓨터 실행 중인 hello Azure 로그 통합 서비스를 확인 하 고 Azure에 액세스할 수 있는지 확인 합니다. tootest 연결을 시도 tooopen hello [Azure 포털](http://portal.azure.com) hello 브라우저에서 합니다.
2. Hello 사용자 계정이 확인 **Azlog** hello 폴더에 대 한 쓰기 권한이 **users\Azlog**합니다.
  <ol type="a">
   <li>**Windows 탐색기** 를 엽니다.</li>
  <li> 너무 이동**c:\users** </li>
  <li> 마우스 오른쪽 단추로 **c:\users\Azlog** 를 클릭합니다.</li>
  <li> **보안**  을 클릭합니다.</li>
  <li> 클릭 **NT Service\Azlog** hello 계정에 대 한 hello 사용 권한을 확인 하 고 있습니다. Hello 계정이이 탭에 없는 경우 또는 hello 적절 한 권한이 없는 경우 현재는이 탭에서 hello 계정 권한을 부여할 수를 표시 합니다.</li>
  </ol>
3.Hello 명령에서 추가 hello 저장소 계정이 확인 **Azlog 소스 추가** hello 명령을 실행할 때 표시 됩니다 **Azlog 원본 목록**합니다.
4. 너무 이동**이벤트 뷰어 > 전역 로그 > 응용 프로그램** hello Azure 로그 통합에서 toosee 오류가 발생 하는 경우 보고 합니다.


Hello 설치 및 구성 하는 동안 모든 문제를 실행 하면을 개시 하세요는 [지원 요청](../azure-supportability/how-to-create-azure-support-request.md)선택, **로그 통합** 지원을 요청 하는 hello 서비스로 합니다.

또 다른 지원 옵션은 hello [Azure 로그 통합 MSDN 포럼](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration)합니다. 여기 hello 커뮤니티와 질문, 대답, 팁 및 요령 tooget 가장 Azure 로그 통합 hello 방식에서 서로 지원할 수 있습니다. 또한 hello Azure 로그 통합 팀이이 포럼을 모니터링 하 고을 활용해 서 때마다는 데 도움이 됩니다.

## <a name="next-steps"></a>다음 단계
Azure 로그 통합에 대해 자세히 toolearn hello 다음 문서를 참조 하십시오.

* [Azure 로그에 대한 Microsoft Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 로그 통합에 대한 세부 정보, 시스템 요구 사항 및 설치 지침을 다운로드할 수 있습니다.
* [소개 tooAzure 로그 통합](security-azure-log-integration-overview.md) -이 문서에서는 소개 tooAzure 로그 통합의 주요 기능 및 작동 방식입니다.
* [구성 단계를 파트너](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) –이 블로그 게시물을 보면 tooconfigure Azure Splunk, HP ArcSight 및 IBM QRadar 파트너 솔루션과 통합 toowork를 로그 하는 방법은 합니다. 이 어떻게 tooconfigure hello SIEM 구성 요소에 대 한 우리의 현재 지침입니다. 먼저 SIEM 공급업체에 추가 세부 정보를 확인하세요.
* [Azure 로그 통합 FAQ(질문과 대답)](security-azure-log-integration-faq.md) - 이 FAQ는 Azure 로그 통합에 대한 질문에 답변합니다.
* [보안 센터를 통합 합니다. Azure와 경고 로그 통합](../security-center/security-center-integrating-alerts-with-log-integration.md) -이 문서에서는 어떻게 toosync 보안 센터 경고, 로그 분석으로 Azure 진단 및 Azure 활동 로그에서 수집 하는 가상 컴퓨터 보안 이벤트와 함께 또는 SIEM 솔루션을 추가 합니다.
* [Azure 진단 및 Azure 감사 로그에 대 한 새로운 기능](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) –이 블로그 게시물 tooAzure 감사 로그를 소개 하 고 Azure 리소스의 hello 작업을 파악할 수 있는 기타 기능입니다.
