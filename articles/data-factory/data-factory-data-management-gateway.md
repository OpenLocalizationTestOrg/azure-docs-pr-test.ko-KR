---
title: "데이터 팩토리에 대 한 관리 게이트웨이 aaaData | Microsoft Docs"
description: "Hello와 온-프레미스 데이터 게이트웨이 toomove 데이터 설정 클라우드입니다. 데이터 toomove Azure Data Factory에서에서 데이터 관리 게이트웨이 사용 합니다."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>데이터 관리 게이트웨이
hello 데이터 관리 게이트웨이 클라우드 및 온-프레미스 데이터 저장소 간의 온-프레미스 환경 toocopy 데이터에 설치 해야 하는 클라이언트 에이전트입니다. hello 온-프레미스 데이터를 Data Factory에서 지 원하는 저장소 hello에 나열 된 [지원 되는 데이터 원본](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 섹션.

이 문서는 hello에 hello 연습 보완 [온-프레미스와 클라우드 간 데이터 이동 데이터 저장소](data-factory-move-data-between-onprem-and-cloud.md) 문서. Hello 연습 hello 게이트웨이 toomove 데이터는 온-프레미스 SQL Server 데이터베이스 tooan Azure blob에서 사용 하는 파이프라인을 만듭니다. 이 문서는 데이터 관리 게이트웨이 hello에 대 한 깊이 있는 자세한 정보를 제공합니다. 

Hello 게이트웨이를 여러 온-프레미스 컴퓨터를 연결 하 여 데이터 관리 게이트웨이 확장할 수 있습니다. 노드에서 동시에 실행할 수 있는 데이터 이동 작업의 수를 늘려 강화할 수 있습니다. 이 기능은 단일 노드가 있는 논리 게이트웨이에서도 사용할 수 있습니다. 자세한 내용은 [Azure Data Factory에서 데이터 관리 게이트웨이 확장](data-factory-data-management-gateway-high-availability-scalability.md) 문서를 참조하세요.

> [!NOTE]
> 현재, 게이트웨이 데이터 팩터리에서 hello 복사 작업 및 저장된 프로시저 작업을 지원합니다. 사용자 지정 활동 tooaccess 온-프레미스 데이터 원본에서 가능한 toouse hello 게이트웨이 없습니다.      

## <a name="overview"></a>개요
### <a name="capabilities-of-data-management-gateway"></a>데이터 관리 게이트웨이의 기능
데이터 관리 게이트웨이 hello를 다음 기능을 제공 합니다.

* 모델 온-프레미스 데이터 원본 및 클라우드 데이터 원본 내 같은 데이터 팩터리 hello 및 데이터를 이동 합니다.
* 모니터링 및 hello Data Factory 페이지에서 게이트웨이 상태에 대 한 가시성을 사용한 관리를 위한 유리의 단일 창이 있어야 합니다.
* Tooon 온-프레미스 데이터 원본 액세스를 안전 하 게 관리 합니다.
  * 변경 내용이 없습니다 toocorporate 방화벽이 필요합니다. 게이트웨이 아웃 바운드 HTTP 기반 연결 tooopen 더욱 인터넷 합니다.
  * 인증서를 사용하여 온-프레미스 데이터 저장소에 대한 자격 증명을 암호화합니다.
* 데이터를 효율적으로 이동-병렬, 복원 력 있는 toointermittent 네트워크 문제 자동 다시 시도 논리와 데이터를 전송 합니다.

### <a name="command-flow-and-data-flow"></a>명령 흐름 및 데이터 흐름
온-프레미스와 클라우드 간 복사 활동 toocopy 데이터를 사용 하면 온-프레미스 데이터 원본 toocloud에서 그 반대의 게이트웨이 tootransfer 데이터 hello 활동에 사용 합니다.

다음은 대 한 높은 수준의 데이터 흐름 hello와 단계 데이터 게이트웨이 사용 하 여 복사에 대 한 요약: ![게이트웨이 사용 하 여 데이터 흐름](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. 데이터 개발자 hello 중 하나를 사용 하는 Azure 데이터 팩터리에 대 한 한 게이트웨이 만듭니다 [Azure 포털](https://portal.azure.com) 또는 [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx)합니다.
2. 데이터 개발자 hello 게이트웨이 지정 하 여 온-프레미스 데이터 저장소에 대 한 연결 된 서비스를 만듭니다. 연결 된 서비스를 hello 설정, 데이터 개발자 hello 자격 증명 설정 응용 프로그램 toospecify 인증 유형 및 자격 증명 사용 합니다.  hello 자격 증명 설정 hello 데이터와 통신 하는 응용 프로그램 대화 상자 tootest 연결과 hello 게이트웨이 toosave 자격 증명을 저장 합니다.
3. 게이트웨이는 hello 클라우드에서 hello 자격 증명을 저장 하기 전에 hello 인증서 (데이터 개발자가 제공) hello 게이트웨이에 연결 된 hello 자격 증명을 암호화 합니다.
4. 데이터 팩터리 서비스는 일정 및 공유 Azure 서비스 버스 큐를 사용 하는 컨트롤 채널을 통해 작업의 관리에 대 한 hello 게이트웨이와 통신 합니다. 복사 활동 작업 toobe 시작 하면 데이터 팩터리에 자격 증명 정보와 함께 hello 요청을 대기 합니다. 게이트웨이는 hello 작업 hello 큐 폴링 후 시작 합니다.
5. hello 게이트웨이 hello 인증서 동일 하 고 다음 적절 한 인증 유형 및 자격 증명으로 toohello 온-프레미스 데이터 저장소를 연결로 hello 자격 증명을 해독 합니다.
6. hello 게이트웨이 온-프레미스 저장소 tooa 클라우드 저장소에서 또는 그 반대로 hello 데이터 파이프라인에서 hello 복사 작업은 구성 하는 방법에 따라 데이터를 복사 합니다. 이 단계에 대 한 hello 게이트웨이 직접 보안 (HTTPS) 채널을 통해 Azure Blob 저장소와 같은 클라우드 기반 저장소 서비스와 통신합니다.

### <a name="considerations-for-using-gateway"></a>게이트웨이 사용을 위한 고려 사항
* 데이터 관리 게이트웨이의 단일 인스턴스를 여러 온-프레미스 데이터 소스에 사용할 수 있습니다. 그러나 **단일 게이트웨이 인스턴스에서 동 점된 tooonly 하나의 Azure 데이터 팩터리** 및 다른 데이터 팩터리와 공유할 수 없습니다.
* 단일 컴퓨터에 **데이터 관리 게이트웨이 인스턴스를 하나만** 설치할 수 있습니다. Tooaccess 온-프레미스 데이터 소스를 필요로 하는 두 개의 데이터 팩터리 있다고 가정해 보겠습니다 tooinstall 게이트웨이 두 온-프레미스 컴퓨터에 필요 합니다. 즉, 게이트웨이 동 점된 tooa 특정 데이터 팩터리
* hello **게이트웨이 toobe hello hello 데이터 원본으로 동일한 컴퓨터에 필요 하지 않습니다**합니다. 그러나 게이트웨이 자세히 toohello 데이터 원본이 있으면 hello 게이트웨이 tooconnect toohello 데이터 원본에 대 한 hello 시간을 줄입니다. Hello 해당 호스트 온-프레미스 데이터 원본 하나에서 다른 컴퓨터에 hello 게이트웨이 설치 하는 것이 좋습니다. Hello 게이트웨이 및 데이터 소스가 서로 다른 컴퓨터에서을 hello 게이트웨이가 데이터 소스를 사용 하 여 리소스에 대 한 경합 하지 않습니다.
* 사용할 수 있습니다 **toohello 연결 하는 서로 다른 컴퓨터에서 여러 게이트웨이 동일한 온-프레미스 데이터 원본**합니다. 예를 들어 두 데이터 팩터리 하지만 hello 모두 hello 데이터 팩터리와 같은 온-프레미스 데이터 원본 등록을 처리 하는 두 게이트웨이 할 수 있습니다.
* 컴퓨터에 **Power BI** 시나리오를 처리할 게이트웨이가 이미 설치된 경우 **별도의 Azure Data Factory용 게이트웨이**를 다른 컴퓨터에 설치하세요.
* **Express 경로**를 사용할 때도 게이트웨이를 사용해야 합니다.
* **Express 경로**를 사용하더라도 데이터 소스는 방화벽으로 보호되는 온-프레미스 데이터 소스로 취급해야 합니다. Hello 서비스와 hello 데이터 원본 간의 hello 게이트웨이 tooestablish 연결 기능을 사용 합니다.
* 수행 해야 **hello 게이트웨이 사용 하 여** hello 데이터 저장소에 hello 클라우드 중인 경우에는 **Azure IaaS VM**합니다.

## <a name="installation"></a>설치
### <a name="prerequisites"></a>필수 조건
* 지원 되는 hello **운영 체제** 버전은 Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 r 2입니다. 설치의 hello 데이터 관리 게이트웨이 도메인 컨트롤러에서 현재 지원 되지 않습니다.
* .NET Framework 4.5.1 이상이 필요합니다. Windows 7 컴퓨터에 게이트웨이를 설치하는 경우 .NET Framework 4.5 이상을 설치하세요. 자세한 내용은 [.NET Framework 시스템 요구 사항](https://msdn.microsoft.com/library/8z6watww.aspx)을 참조하세요.
* 권장 hello **구성** hello 게이트웨이 컴퓨터 2ghz 이상, 4 개 코어, 8GB RAM 및 디스크 80 GB에 대 한 합니다.
* Hello 호스트 컴퓨터 최대 절전 모드로 전환 하는 경우 hello 게이트웨이 toodata 요청 응답 하지 않습니다. 따라서 적절 한 구성 **전원 관리 옵션** hello 게이트웨이 설치 하기 전에 hello 컴퓨터에 있습니다. Hello 컴퓨터가 구성 된 toohibernate 이면 hello 게이트웨이 설치 메시지는 메시지를 표시 합니다.
* Hello 컴퓨터 tooinstall의 관리자 여야 하 고 hello 데이터 관리 게이트웨이 성공적으로 구성 해야 합니다. 추가 사용자 toohello를 추가할 수 있습니다 **데이터 관리 게이트웨이 사용자** 로컬 Windows 그룹입니다. 이 그룹의 hello 구성원은 수 toouse hello **데이터 관리 게이트웨이 구성 관리자** 도구 tooconfigure hello 게이트웨이 합니다.

특정 빈도에 활동을 실행을 발생 복사, hello hello 컴퓨터에서 리소스 사용 (CPU, 메모리) 따르는 hello 같은 최고 및 유휴 시간 패턴입니다. 리소스 사용률도에 따라 달라 집니다 hello 양의 데이터를 이동 합니다. 여러 복사 작업이 진행 중인 경우 사용량이 많은 시간 동안 리소스 사용량이 증가하는 것을 볼 수 있습니다.

### <a name="installation-options"></a>설치 옵션
다음 방법으로 hello에 데이터 관리 게이트웨이 설치할 수 있습니다.

* Hello에서 MSI 설치 패키지를 다운로드 하 여 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=39717)합니다.  hello MSI tooupgrade 사용 되는 기존 데이터 관리 게이트웨이 toohello 최신 버전을 유지 하는 모든 설정 될 수도 있습니다.
* 수동 설치에서 **데이터 게이트웨이 다운로드 및 설치** 링크 또는 빠른 설치에서 **이 컴퓨터에 직접 설치**를 클릭합니다. 빠른 설치를 사용하는 단계별 지침은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요. hello 수동 단계 toohello 다운로드 센터를 이동합니다.  다운로드 하 고 hello 게이트웨이 다운로드 센터에서 설치에 대 한 hello 지침은 hello 다음 섹션에 나와 있습니다.

### <a name="installation-best-practices"></a>설치 모범 사례입니다.
1. Hello 컴퓨터는 최대 절전 모드 없음 있도록 hello 게이트웨이에 대 한 hello 호스트 컴퓨터에 전원 관리 옵션을 구성 합니다. Hello 호스트 컴퓨터 최대 절전 모드로 전환 하는 경우 hello 게이트웨이 toodata 요청 응답 하지 않습니다.
2. Hello 게이트웨이에 연결 된 hello 인증서를 백업 합니다.

### <a name="install-hello-gateway-from-download-center"></a>다운로드 센터에서 hello 게이트웨이 설치 합니다.
1. 너무 이동[Microsoft 데이터 관리 게이트웨이 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=39717)합니다.
2. 클릭 **다운로드**, 선택 hello 적절 한 버전 (**32 비트** vs. **64비트**)을 선택하고 **다음**을 클릭합니다.
3. Hello 실행 **MSI** 직접 또는 tooyour 하드 디스크를 저장 하 고 실행 합니다.
4. Hello에 **시작** 페이지에서 한 **언어** 클릭 **다음**합니다.
5. **수락** 클릭 하 고 최종 사용자 사용권 계약을 hello **다음**합니다.
6. 선택 **폴더** tooinstall 게이트웨이 hello 및 클릭 **다음**합니다.
7. Hello에 **준비 tooinstall** 페이지 **설치**합니다.
8. 클릭 **마침** toocomplete 설치 합니다.
9. Hello Azure 포털에서에서 hello 키를 가져옵니다. Hello에 대 한 단계별 지침은 다음 섹션을 참조 하십시오.
10. Hello에 **레지스터 게이트웨이** 페이지 **데이터 관리 게이트웨이 구성 관리자** 다음 단계 hello 수행 하 여 컴퓨터에서 실행 합니다.
    1. Hello 텍스트에 hello 키를 붙여 넣습니다.
    2. 필요에 따라 **표시 게이트웨이 키** toosee hello 키 텍스트입니다.
    3. **Register**를 클릭합니다.

### <a name="register-gateway-using-key"></a>키를 사용하여 게이트웨이 등록
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Hello 포털에 이미 논리 게이트웨이 만들지 않은 경우
toocreate hello에서 hello 포털 및 get hello 키에서 게이트웨이 **구성** 페이지 hello에 연습에서 단계 수행 [온-프레미스와 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Hello 포털에서 hello 논리 게이트웨이 이미 만든 경우
1. Azure 포털에서 탐색 toohello **Data Factory** 페이지를 클릭 하 여 **연결 된 서비스** 바둑판식으로 배열입니다.

    ![Data Factory 페이지](media/data-factory-data-management-gateway/data-factory-blade.png)
2. Hello에 **연결 된 서비스** 페이지를 선택 하는 hello 논리 **게이트웨이** hello 포털에서 생성 합니다.

    ![논리 게이트웨이](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. Hello에 **데이터 게이트웨이** 페이지 **데이터 게이트웨이 다운로드 및 설치**합니다.

    ![다운로드 링크 hello 포털에서](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. Hello에 **구성** 페이지 **다시 만든 후 키**합니다. 신중 하 게 읽은 후 hello 경고 메시지에서 예를 클릭 합니다.

    ![키 다시 만들기](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Toohello 키 다음 복사 단추를 클릭 합니다. hello 키는 복사한 toohello 클립보드 합니다.

    ![키 복사](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>시스템 트레이 아이콘/알림
hello 다음 이미지에서는 hello 중 일부 볼 수 있는 트레이 아이콘

![시스템 트레이 아이콘](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Hello 시스템 트레이 아이콘/알림 메시지 위로 커서를 이동 하면 팝업 창의 hello 게이트웨이/업데이트 작업의 hello 상태에 대 한 세부 정보 표시 됩니다.

### <a name="ports-and-firewall"></a>포트 및 방화벽
Tooconsider 해야 하는 두 개의 방화벽이: **회사 방화벽** hello 중앙 라우터 hello 조직에서 실행 되 고 **Windows 방화벽** 여기서 hello 디먼 hello 로컬 컴퓨터에 구성 된 게이트웨이가 설치 되어 있습니다.  

![방화벽](./media/data-factory-data-management-gateway/firewalls2.png)

Hello 다음을 구성 해야 회사 방화벽 수준에서 도메인 및 아웃 바운드 포트:

| 도메인 이름 | 포트 | 설명 |
| --- | --- | --- |
| *.servicebus.windows.net |443, 80 |데이터 이동 서비스 백 엔드와 통신에 사용됨 |
| *.core.windows.net |443 |Azure Blob를 사용하여 준비된 복사에 사용됨(구성된 경우)|
| *.frontend.clouddatahub.net |443 |데이터 이동 서비스 백 엔드와 통신에 사용됨 |


Windows 방화벽 수준에서 이러한 아웃바운드 포트를 일반적으로 사용할 수 있습니다. 그렇지 않은 수 구성 hello 도메인과 포트 그에 따라 게이트웨이 컴퓨터에 있습니다.

> [!NOTE]
> 1. 소스에 따라 toowhitelist 추가 도메인 및 아웃 바운드 포트에 있을 수 있습니다 싱크를 / Windows/회사 방화벽입니다.
> 2. 일부 클라우드 데이터베이스에 대 한 (예: [Azure SQL 데이터베이스](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure 데이터 레이크](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access)등), 해당 방화벽 구성에 게이트웨이 컴퓨터의 IP 주소 toowhitelist 할 수 있습니다.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>원본 데이터 저장소 tooa 싱크 데이터 저장소에서 데이터를 복사 합니다.
Hello 회사 방화벽을 hello 게이트웨이 컴퓨터에서 Windows 방화벽 hello 방화벽 규칙을 올바르게 사용할 수 있고 자체 hello 데이터 저장소를 확인 합니다. 이러한 규칙을 사용 하면 hello 게이트웨이 tooconnect tooboth 원본 및 싱크를 성공적으로 수 있습니다. Hello 복사 작업에 포함 되는 각 데이터 저장소에 대 한 규칙을 사용 하도록 설정 합니다.

예를 들어 toocopy에서 **온-프레미스 데이터 저장소 tooan Azure SQL 데이터베이스 싱크 또는 Azure SQL 데이터 웨어하우스 싱크에**, 다음 단계 hello지 않습니다:

* Windows 방화벽 및 회사 방화벽 둘 다에 대해 포트 **1433**에서 아웃바운드 **TCP** 통신을 허용합니다.
* Azure SQL server tooadd hello IP 주소 허용 된 IP 주소의 hello 게이트웨이 컴퓨터 toohello 목록 중 hello 방화벽 설정을 구성 합니다.

> [!NOTE]
> 방화벽이 아웃바운드 포트 1433을 허용하지 않으면 게이트웨이는 Azure SQL에 직접 액세스할 수 없습니다. 이 경우 사용할 수 있습니다 [준비 복사](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure 데이터베이스 / SQL Azure DW 합니다. 이 시나리오에서는 hello 데이터 이동에 대 한 HTTPS (포트 443)을만 필요할 것입니다.
>
>


### <a name="proxy-server-considerations"></a>프록시 서버 고려 사항
회사 네트워크 환경에는 프록시를 사용 하는 경우 서버 tooaccess hello 인터넷, 데이터 관리 게이트웨이 toouse 적절 한 프록시 설정을 구성 합니다. Hello 초기 등록 단계 동안 hello 프록시를 설정할 수 있습니다.

![등록 중에 프록시 설정](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

게이트웨이는 hello 프록시 서버 tooconnect toohello 클라우드 서비스를 사용합니다. 초기 설치 중에 **변경** 링크를 클릭합니다. Hello 참조 **프록시 설정을** 대화 상자.

![구성 관리자를 사용하여 프록시 설정](media/data-factory-data-management-gateway/SetProxySettings.png)

이 대화 상자에는 세 가지 구성 옵션이 있습니다.

* **프록시를 사용 하지 마십시오**: 게이트웨이 모든 프록시 tooconnect toocloud 서비스를 명시적으로 사용 하지 않습니다.
* **시스템 프록시를 사용 하 여**: 게이트웨이 설정에 구성 된 diahost.exe.config 및 diawp.exe.config hello 프록시를 사용 합니다.  프록시가 diahost.exe.config 및 diawp.exe.config에서 구성 되 면 게이트웨이 프록시를 통과 하지 않고 직접 toocloud 서비스를 연결 합니다.
* **사용자 지정 프록시를 사용 하 여**: diahost.exe.config diawp.exe.config 구성을 사용 하는 대신 게이트웨이에 대 한 프록시 설정 toouse hello HTTP 구성입니다.  이 경우 주소 및 포트를 지정해야 합니다.  사용자 이름 및 암호는 프록시 인증 설정에 따라 입력할 수 있습니다.  모든 설정은 hello 게이트웨이의 hello 자격 증명 인증서로 암호화 되며 hello 게이트웨이 호스트 컴퓨터에 로컬로 저장 됩니다.

hello 데이터 관리 게이트웨이 호스트 서비스 다시 자동으로 업데이트 하는 hello 프록시 설정을 저장 한 후 시작 합니다.

게이트웨이 등록 된 후 성공적으로, tooview 원하는 또는 프록시 설정을 업데이트 하는 경우, 데이터 관리 게이트웨이 구성 관리자를 사용 합니다.

1. **데이터 관리 게이트웨이 구성 관리자**를 시작합니다.
2. Toohello 전환 **설정을** 탭 합니다.
3. 클릭 **변경** 링크를 **HTTP 프록시** 섹션 toolaunch hello **HTTP 프록시 설정** 대화 상자.  
4. Hello를 클릭 한 후 **다음** 권한 toosave hello 프록시 설정 및 다시 시작 hello 게이트웨이 호스트 서비스에 대해 묻는 경고 대화 상자가 표시 단추를 합니다.

구성 관리자 도구를 사용하여 HTTP 프록시를 확인하고 업데이트할 수 있습니다.

![구성 관리자를 사용하여 프록시 설정](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> NTLM 인증을 사용 하 여 프록시 서버를 설정한 경우 게이트웨이 호스트 서비스가 hello 도메인 계정으로 실행 됩니다. 나중에 도메인 계정 hello에 대 한 hello 암호를 변경 하면 hello 서비스에 대 한 구성 설정을 tooupdate를 기억 하 고 그에 따라 다시 시작 합니다. Toothis 요구 사항, 인해 암호를 요구 하지 있습니다 tooupdate hello 자주 하는 전용된 도메인 계정을 tooaccess hello 프록시 서버를 사용 하는 것이 좋습니다.
>
>

### <a name="configure-proxy-server-settings"></a>프록시 서버 설정 구성
선택 하는 경우 **시스템 프록시를 사용 하 여** diahost.exe.config 및 diawp.exe.config에서 설정 하는 hello 프록시를 사용 하 여 게이트웨이 hello HTTP 프록시를 설정 합니다.  프록시가 diahost.exe.config 및 diawp.exe.config에 지정 된 경우 게이트웨이 toocloud 서비스 프록시를 통과 하지 않고 직접 연결 합니다. hello 다음 절차에서는 설명 hello diahost.exe.config 파일을 업데이트 합니다.  

1. 파일 탐색기에서 C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\Shared\diahost.exe.config tooback의 복사본을 안전 하 게 보호 hello 원본 파일을 구성 합니다.
2. 관리자 권한으로 Notepad.exe 실행을 시작하고 텍스트 파일 "C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config"를 엽니다. Hello 코드 다음에 표시 된 대로 system.net에 대 한 hello 기본 태그를 찾을:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   그런 다음 hello 다음 예제에에서 나와 있는 것 처럼 프록시 서버 세부 정보를 추가할 수 있습니다.

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   추가 속성 scriptLocation 같은 hello 프록시 태그 toospecify 필요한 hello 설정 내에서 허용 됩니다. 너무 참조[프록시 요소 (네트워크 설정)](https://msdn.microsoft.com/library/sa91de1e.aspx) 구문에 있습니다.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Hello 원래 위치로 hello 구성 파일을 저장 한 다음 hello hello 변경 내용을 선택 하는 데이터 관리 게이트웨이 호스트 서비스를 다시 시작 합니다. toorestart hello 서비스: hello 또는 hello 제어판에서 서비스 애플릿을 사용 하 여 **데이터 관리 게이트웨이 구성 관리자** > hello 클릭 **서비스 중지** 단추를 클릭 hello **서비스 시작**합니다. Hello 서비스가 시작 되지 않는 경우 가능성이 편집 된 hello 응용 프로그램 구성 파일에 잘못 된 XML 태그 구문을 추가 된 것입니다.

> [!IMPORTANT]
> Tooupdate를 잊지 마십시오 **둘 다** diahost.exe.config 및 diawp.exe.config 합니다.  


또한 toothese 지점 있어야 toomake 귀사의 허용 목록에 Microsoft Azure 인지 합니다. 유효한 Microsoft Azure IP 주소의 hello 목록을 hello에서 다운로드할 수 있습니다 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=41653)합니다.

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>방화벽 및 프록시 서버 관련 문제 발생 시 나타날 수 있는 증상
스토리를 다음 오류와 비슷한 toohello 발생 하는 경우 자체 연결 tooData 팩터리 tooauthenticate에서 게이트웨이 차단 하는 hello 방화벽 또는 프록시 서버 구성을 tooimproper 인해 될 합니다. 방화벽 및 프록시 서버에 제대로 구성 되어 tooprevious 섹션 tooensure를 참조 하십시오.

1. Hello 다음 오류가 수신 tooregister hello 게이트웨이 나타난다: "Failed tooregister hello 게이트웨이 키입니다. Tooregister hello 게이트웨이 키를 다시 시도 하기 전에 연결 된 상태에서 데이터 관리 게이트웨이 hello 및 데이터 관리 게이트웨이 호스트 서비스가 hello 시작됨인지 확인 합니다. "
2. 구성 관리자를 열 때 상태가 "연결 끊김" 또는 "연결 중"으로 표시됩니다. "이벤트 뷰어" 아래에서 Windows 이벤트 로그를 볼 때 > "응용 프로그램 및 서비스 로그" > 다음 오류가 hello와 같은 오류 메시지가 나타나면 "데이터 관리 게이트웨이":`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>자격 증명 암호화용 8050 포트 열기
hello **자격 증명 설정** 응용 프로그램에서는 hello 인바운드 포트 **8050** toorelay 자격 증명 toohello 게이트웨이 온-프레미스를 설정할 때 서비스 hello Azure 포털에에서 연결 합니다. 게이트웨이 설치 하는 동안 기본적으로 hello 게이트웨이 설치가 열립니다 hello 게이트웨이 컴퓨터에서.

타사 방화벽을 사용 하는 경우 hello 포트 8050 수동으로 열 수 있습니다. 게이트웨이 설치 하는 동안 방화벽 문제를 실행 하면 hello 방화벽을 구성 하지 않고 명령 tooinstall hello 게이트웨이 따르는 hello를 사용 하 여 시도할 수 있습니다.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Hello 포트 8050 hello 게이트웨이 컴퓨터에서 tooopen 하지 않으려는 경우 hello를 사용 하는 메커니즘을 사용 합니다. **자격 증명 설정** tooconfigure 데이터 응용 프로그램 자격 증명을 저장 합니다. 예를 들어 [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet을 사용할 수 있습니다. 데이터 저장소 자격 증명을 설정할 수 있는 방법은 [자격 증명 및 보안 설정](#set-credentials-and-securityy) 섹션을 참조하세요.

## <a name="update"></a>업데이트
기본적으로 최신 버전의 hello 게이트웨이 사용할 수 있는 데이터 관리 게이트웨이가 자동으로 업데이트 됩니다. hello 게이트웨이 모든 hello 예약 된 작업은 완료 될 때까지 업데이트 되지 않습니다. Hello 업데이트 작업이 완료 될 때까지 hello 게이트웨이에서 더 이상 작업이 처리 됩니다. Hello 업데이트가 실패 하면 게이트웨이 롤백됩니다 toohello 이전 버전입니다.

예약 된 hello 업데이트 시간 hello 위치 뒤에 표시 됩니다.

* hello Azure 포털의에서 hello 게이트웨이 속성 페이지.
* Hello 데이터 관리 게이트웨이 구성 관리자의 홈 페이지
* 시스템 트레이 알림 메시지

hello 데이터 관리 게이트웨이 구성 관리자의 홈 탭 hello 일정을 업데이트 하는 hello를 표시 하 고 hello 마지막 시간 hello 게이트웨이 설치/업데이트 되었습니다.

![업데이트를 예약](media/data-factory-data-management-gateway/UpdateSection.png)

Hello 업데이트 즉시 설치 또는 hello 게이트웨이 toobe hello 예약 된 시간에 자동으로 업데이트할 때까지 대기 합니다. 다음 이미지에서는 알림 메시지에에서 표시 된 hello 업데이트 단추를 클릭할 수 있는 tooinstall 함께 hello 게이트웨이 구성 관리자 것 바로 hello hello 예를 들어

![DMG 구성 관리자에서 업데이트](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

다음 이미지는 hello와 같이 hello 시스템 트레이에서 hello 알림 메시지 형태가 됩니다.

![시스템 트레이 메시지](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

업데이트 작업 (수동 또는 자동) hello 시스템 트레이에서 hello 상태가 표시 됩니다. 너무 링크와 함께 업데이트 되었습니다 그 hello 게이트웨이가 알림 hello에 대 한 메시지 참조 다음에 게이트웨이 구성 관리자를 시작할 때[새 주제 이란](data-factory-gateway-release-notes.md)합니다.

### <a name="toodisableenable-auto-update-feature"></a>자동 업데이트 기능을 toodisable/사용
있습니다 수 사용/사용 안함 hello 자동 업데이트 기능은 hello 다음 단계를 수행 하 여:

[단일 노드 게이트웨이의 경우]
1. Hello 게이트웨이 컴퓨터에서 Windows PowerShell을 시작 합니다.
2. Toohello C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\PowerShellScript 폴더를 전환 합니다.
3. 다음 명령은 tooturn hello 자동 업데이트 실행된 hello (해제) 해제 기능입니다.   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. 다시 tooturn:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[다중 노드 고가용성 및 확장 가능 게이트웨이(미리 보기)의 경우](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Hello 게이트웨이 컴퓨터에서 Windows PowerShell을 시작 합니다.
2. Toohello C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\PowerShellScript 폴더를 전환 합니다.
3. 다음 명령은 tooturn hello 자동 업데이트 실행된 hello (해제) 해제 기능입니다.   

    고가용성 기능(미리 보기)이 있는 게이트웨이의 경우 추가 AuthKey 매개 변수가 필요합니다.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. 다시 tooturn:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Hello 게이트웨이 컴퓨터와에서 다른 컴퓨터에서 hello 포털에 액세스 하는 경우 자격 증명 관리자 응용 프로그램 hello toohello 게이트웨이 컴퓨터에 연결할 수 있는지 확인 해야 합니다. Hello 응용 프로그램 hello 게이트웨이 컴퓨터에 연결할 수 없으면, 수 없습니다 하면 hello 데이터 원본과 tootest 연결 toohello 데이터 원본에 대 한 tooset 자격 증명입니다.  

Hello를 사용 하는 경우 **자격 증명 설정** 응용 프로그램을 hello 포털 hello 자격 증명 hello에 지정 된 hello 인증서로 암호화 **인증서** hello 탭 **게이트웨이 Configuration Manager** hello 게이트웨이 컴퓨터에 있습니다.

Hello 자격 증명을 암호화 하기 위한 API 기반 방법을 찾고 hello를 사용할 수 있습니다 [새로 AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt 자격 증명입니다. hello cmdlet hello 인증서 해당 게이트웨이 구성 된 toouse tooencrypt hello 자격 증명을 사용 합니다. 암호화 된 자격 증명 toohello 추가 **EncryptedCredential** hello의 요소 **connectionString** hello JSON에에서 있습니다. JSON hello를 사용 하 여 hello로 [새로 AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet 또는 hello 데이터 팩터리 편집기입니다.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

데이터 팩터리 편집기를 사용하여 자격 증명을 설정할 수 있는 방법이 한 가지 더 있습니다. 연결 된 SQL 서버를 만든 경우 hello 편집기를 사용 하 여 서비스 자격 증명을 일반 텍스트로 입력, hello 자격 증명 hello 데이터 팩터리 서비스를 소유 하는 인증서를 사용 하 여 암호화 됩니다. 해당 게이트웨이 구성 된 toouse hello 인증서를 사용 하지 않습니다. 경우에 따라 이 방법은 약간 빠를 수 있는 반면에 안전성이 떨어집니다. 따라서 개발/테스트 목적에 대해서만이 방법을 수행하는 것이 좋습니다.

## <a name="powershell-cmdlets"></a>PowerShell cmdlet
이 섹션에서는 설명 방법을 toocreate 및 Azure PowerShell cmdlet을 사용 하 여 게이트웨이 등록 합니다.

1. **Azure PowerShell**을 관리자 모드로 시작합니다.
2. 실행 하 여 Azure 계정 tooyour 로그인 hello 명령 하 고 Azure 자격 증명을 입력 합니다.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. 사용 하 여 hello **새로 AzureRmDataFactoryGateway** cmdlet toocreate 다음과 같이 논리적 게이트웨이:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **예제 명령 및 출력**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. Azure PowerShell에서 전환 toohello 폴더: **C:\Program Files\Microsoft 데이터 관리 Gateway\2.0\PowerShellScript\**합니다. 실행 **RegisterGateway.ps1** hello 지역 변수 연관 **$Key** 다음 명령을 hello와 같이 합니다. 이 스크립트는 이전에 만들 hello 논리 게이트웨이가 설치 된 컴퓨터에 설치 된 hello 클라이언트 에이전트를 등록 합니다.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Hello IsRegisterOnRemoteMachine 매개 변수를 사용 하 여 원격 컴퓨터에서 hello 게이트웨이 등록할 수 있습니다. 예제:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Hello를 사용할 수 있습니다 **Get AzureRmDataFactoryGateway** data factory에는 게이트웨이 cmdlet tooget hello 목록입니다. Hello 때 **상태** 표시 **온라인**, 게이트웨이가 준비 toouse 합니다.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Hello를 사용 하 여 게이트웨이 제거할 수 있습니다 **제거 AzureRmDataFactoryGateway** hello를 사용 하 여 게이트웨이에 대 한 cmdlet 및 업데이트 설명 **집합 AzureRmDataFactoryGateway** cmdlet. 이러한 cmdlet에 대한 구문 및 기타 세부 정보는 데이터 팩터리 Cmdlet 참조를 참조하세요.  

### <a name="list-gateways-using-powershell"></a>PowerShell을 사용하여 게이트웨이 나열

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>PowerShell을 사용하여 게이트웨이 제거

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>다음 단계
* [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요. Hello 연습 hello 게이트웨이 toomove 데이터는 온-프레미스 SQL Server 데이터베이스 tooan Azure blob에서 사용 하는 파이프라인을 만듭니다.  
