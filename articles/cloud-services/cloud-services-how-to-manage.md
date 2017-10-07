---
title: "aaaCommon 클라우드 서비스 관리 작업 (클래식) | Microsoft Docs"
description: "Hello Azure 클래식 포털에서에서 toomanage 클라우드 서비스 하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>TooManage 클라우드 서비스 하는 방법
> [!div class="op_single_selector"]
> * [Azure 포털](cloud-services-how-to-manage-portal.md)
> * [Azure 클래식 포털](cloud-services-how-to-manage.md)
>
>

Hello에 **클라우드 서비스** 부문의 문제 hello Azure 클래식 포털에서 있습니다 수 서비스 역할 또는 배포 업데이트, 준비 된 배포 tooproduction 승격, hello 리소스를 볼 수 있도록 리소스 tooyour 클라우드 서비스에 연결 종속성 및 배율에는 리소스를 함께 hello 및 클라우드 서비스 또는 배포를 삭제 합니다.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>방법: 클라우드 서비스 역할 또는 배포 업데이트
클라우드 서비스에 대 한 tooupdate hello 응용 프로그램 코드를 필요 사용 **업데이트** hello 대시보드에서 **클라우드 서비스** 페이지 또는 **인스턴스** 페이지. 단일 역할이나 모든 역할을 업데이트할 수 있습니다. Tooupload 새 서비스 패키지 및 서비스 구성 파일이 필요 합니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), hello 대시보드에서 **클라우드 서비스** 페이지 또는 **인스턴스** 페이지 **업데이트**합니다.

    ![배포 업데이트](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. **배포 레이블**, 이름 tooidentify hello 배포 (예를 들어 mycloudservice4)을 입력 합니다. 배포 레이블 hello 있습니다 **퀵 스타트** hello 대시보드에서.
3. **패키지**를 사용 하 여 **찾아보기** tooupload hello 서비스 패키지 파일 (.cspkg).
4. **구성**를 사용 하 여 **찾아보기** tooupload hello 서비스 구성 파일 (.cscfg).
5. **역할**선택, **모든** hello에 있는 모든 역할이 클라우드 서비스 tooupgrade 하려는 경우. tooperform 단일 역할 업데이트 tooupdate 선택 hello 역할입니다. 특정 역할 tooupdate 선택 하는 경우에 hello 업데이트 hello 서비스 구성 파일에는 적용 된 tooall 역할입니다.
6. Hello 업데이트 변경 내용을 모든 역할의 hello 크기나 역할 수가 hello, hello 선택 **역할 크기나 역할 수가 변경 되 면 업데이트의 허용** 확인란 tooenable hello 업데이트 tooproceed 합니다.

    업그레이드할 역할 (즉, 역할 인스턴스를 호스팅하는 가상 컴퓨터의 hello 크기)의 hello 크기를 변경 하거나 역할 수가 hello 경우 각 역할 인스턴스 (가상 컴퓨터)은 이미지로 다시 설치 된 있어야 합니다. 모든 로컬 데이터가 손실 됩니다.

7. 모든 서비스 역할이 역할 인스턴스가 하나만 있는 경우 선택 hello **하나 이상의 역할에는 단일 인스턴스 확인란이 포함 하는 경우에 업데이트** tooenable hello 업그레이드 tooproceed 합니다.

    Azure는 각 역할에 둘 이상의 역할 인스턴스(가상 컴퓨터)가 있는 경우에만 클라우드 서비스 업데이트 중 99.95%의 서비스 가용성을 보장할 수 있습니다. 수 있도록 하나 가상 컴퓨터 tooprocess 클라이언트 요청 다른 hello를 업데이트 하는 동안 합니다.

8. 클릭 **확인** (확인 표시) toobegin hello 서비스를 업데이트 합니다.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>방법: 준비 된 배포 tooproduction 배포 toopromote 교체
사용 하 여 **교체** toopromote 클라우드 서비스 tooproduction의 스테이징 배포 합니다. Toodeploy 클라우드 서비스의 새 릴리스를 결정할 때 단계 하 고 고객이 프로덕션 환경에서 현재 릴리스 hello를 사용 하는 동안 클라우드 서비스가 스테이징 환경에 새 릴리스를 테스트할 수 있습니다. 준비가 끝나면 toopromote 새 릴리스 tooproduction hello를 사용할 수 있습니다 **교체** tooswitch hello Url는 hello 하 여 두 배포의 주소로 지정 합니다.

Hello에서 배포를 스왑할 수 **클라우드 서비스** 페이지나 hello 대시보드 합니다.

1. Hello에 [Azure 클래식 포털](https://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다.
2. 클라우드 서비스의 hello 목록에서 클릭 hello 클라우드 서비스 tooselect 것입니다.
3. **교환**을 클릭합니다.

    hello 다음과 같은 확인 프롬프트가 열립니다.

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Hello 배포 정보를 확인 한 후 클릭 **예** tooswap hello 배포 합니다.

    hello 배포 스왑 발생 신속 하 게 변경 하는 hello 유일한 항목은 hello 가상 IP 주소 (Vip) hello 배포에 대 한 합니다.

    toosave 계산 비용이 hello hello 새 프로덕션 배포 예상 대로 작동 확인 되 면 스테이징 환경에에서 hello 배포를 삭제할 수 있습니다.

### <a name="common-questions-about-swapping-deployments"></a>배포 교환에 대한 일반적인 질문

**Hello 필수 구성 요소 배포를 교환 하는 무엇입니까?**

성공적인 배포 교환을 위한 2가지 핵심 필수 조건은 다음과 같습니다.

- 프로덕션 슬롯에 대 한 고정 IP 주소를 toouse 하려는 경우에 프로그램 스테이징 슬롯에 대 한를 예약 해야 합니다. 그렇지 않으면 hello 스왑 실패 합니다.

- Hello 교체를 수행 하기 전에 역할의 모든 인스턴스를 실행 되어야 합니다. Hello Azure 클래식 포털에서에서 또는 사용 하 여 인스턴스의 hello 상태를 확인할 수 [Get-azurerole 명령을 Windows PowerShell의 hello](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0)합니다.

게스트 OS 업데이트 및 서비스 작업을 복구 배포 발생할 수 있습니다 참고 toofail을 바꿉니다. 자세한 내용은 [클라우드 서비스 배포 문제 해결](cloud-services-troubleshoot-deployment-problems.md)을 참조하세요.

**교체 시 응용 프로그램 가동 중지가 발생할 수 있습니까? 어떻게 처리해야 합니까?**

Hello 마지막 섹션에서 설명한 배포 스왑 일반적으로 매우 빠릅니다 hello Azure 부하 분산 장치에 구성 변경에 있기 때문입니다. 그러나 경우에 따라 10초 이상 걸리며 일시적인 연결 오류가 발생할 수 있습니다. toolimit 영향 tooyour 고객 구현을 고려할 [클라이언트 다시 시도 논리](../best-practices-retry-general.md)합니다.

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>방법: 리소스 tooa 클라우드 서비스를 연결 합니다.
tooshow 클라우드 서비스의 종속성 다른 리소스에 저장소 계정 toohello 클라우드 서비스 또는 Azure SQL 데이터베이스 인스턴스에 연결할 수 있습니다. 에 연결 하 고 hello에 리소스 연결을 해제 **연결 된 리소스** 페이지를 선택한 다음의 사용 현황을 hello 클라우드 서비스 대시보드에서 모니터링 합니다. 연결 된 저장소 계정에 설정 되어 모니터링 하는 경우에 hello 클라우드 서비스 대시보드에서 총 요청 수를 모니터링할 수 있습니다.

사용 하 여 **링크** toolink 기존 또는 새 SQL 데이터베이스 인스턴스나 저장소 계정 tooyour 클라우드 서비스입니다. hello를 사용 하는 hello 클라우드 서비스 역할과 함께 hello 데이터베이스를 확장할 수 있습니다 **배율** 페이지. (저장소 계정은 사용량이 늘어나면 자동으로 확장됩니다.) 자세한 내용은 참조 [어떻게 tooScale 클라우드 서비스와 연결 된 리소스](cloud-services-how-to-scale.md)합니다.

모니터링, 관리 하 고 수도 있습니다 hello로 hello 데이터베이스 크기를 조정 **데이터베이스** hello Azure 클래식 포털의 노드.

이런이 의미에서 리소스를 "연결" 응용 프로그램 toohello 리소스를 연결 되지는 않습니다. 사용 하 여 새 데이터베이스를 만드는 경우 **링크**, tooadd hello 연결 문자열 tooyour 응용 프로그램 코드와 다음 업그레이드 hello 클라우드 서비스가 필요 합니다. 응용 프로그램 연결 된 저장소 계정에 리소스를 사용 하는 경우에 tooadd 연결 문자열 해야 합니다.

절차를 수행 하는 hello toolink 새 SQL 데이터베이스 인스턴스를 배포 방법 새 SQL 데이터베이스 서버, tooa 클라우드 서비스에 설명 합니다.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink SQL 데이터베이스 인스턴스 tooa 클라우드 서비스
1. Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다. Hello 클라우드 서비스 tooopen hello 대시보드의 hello 이름을 클릭 합니다.
2. **연결된 리소스**를 클릭합니다.

    hello **연결 된 리소스** 페이지가 열립니다.

    ![연결된 리소스 페이지](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. **연결된 리소스** 또는 **연결**을 클릭합니다.

    hello **링크 리소스** 마법사가 시작 합니다.

    ![연결 페이지1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. **새 리소스 만들기** 또는 **기존 리소스에 연결**을 클릭합니다.
5. 리소스 toolink hello 형식을 선택 합니다. Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **SQL 데이터베이스**합니다. (Hello Azure 클래식 포털 지원 저장소 계정 tooa 클라우드 서비스를 연결 합니다.)
6. toocomplete hello 데이터베이스 구성이 hello에 대 한 도움말의 지침에 따라 **SQL 데이터베이스** hello Azure 클래식 포털의 영역입니다.

    Hello 연결 hello 메시지 영역에는 작업의 hello 진행률을 따를 수 있습니다.

    연결 완료 되 면 hello 클라우드 서비스 대시보드에서 hello 연결 된 리소스의 hello 상태를 모니터링할 수 있습니다. 연결 된 SQL 데이터베이스 확장에 대 한 정보를 참조 하십시오. [어떻게 tooScale 클라우드 서비스와 연결 된 리소스](cloud-services-how-to-scale.md)합니다.

### <a name="toounlink-a-linked-resource"></a>toounlink 링크 된 리소스
1. Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다. Hello 클라우드 서비스 tooopen hello 대시보드의 hello 이름을 클릭 합니다.
2. 클릭 **연결 된 리소스**, 한 다음 hello 리소스를 선택 합니다.
3. **연결 해제**를 클릭합니다. 클릭 **예** hello 명령 프롬프트에 있습니다.

    SQL 데이터베이스 연결을 해제 해도 hello 데이터베이스나 hello 응용 프로그램의 연결 toohello 데이터베이스에는 영향이 없습니다. Hello에 hello 데이터베이스를 계속 관리할 수 있습니다 **SQL 데이터베이스** hello Azure 클래식 포털의 영역입니다.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>방법: 배포 및 클라우드 서비스 삭제
클라우드 서비스를 삭제하려면 먼저 각각의 기존 배포를 삭제해야 합니다.

toosave 계산 비용이 프로덕션 배포 예상 대로 작동 하는지 확인 한 후 스테이징 배포를 삭제할 수 있습니다. 클라우드 서비스가 실행되고 있지 않은 경우에도 역할 인스턴스의 계산 비용이 청구됩니다.

배포 또는 클라우드 서비스 프로시저 toodelete 다음 hello를 사용 합니다.

1. Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**합니다.
2. Hello 클라우드 서비스를 선택한 다음 클릭 **삭제**합니다. (tooselect hello 대시보드를 열지 않고 클라우드 서비스는 아무 곳 이나 클릭 hello 클라우드 서비스 항목에서 hello 이름을 제외 하 고 있습니다.)

    스테이징 또는 프로덕션에 배포를 설정한 경우 비슷한 toohello hello hello 창 맨 아래에 하나를 선택 항목의 메뉴가 표시 됩니다. Hello 클라우드 서비스를 삭제 하기 전에 모든 기존 배포를 삭제 해야 합니다.

    ![삭제 메뉴](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete 해당 배포를 클릭 하 여 **프로덕션 배포 삭제** 또는 **스테이징 배포 삭제**합니다. Hello 명령 프롬프트에서 클릭 **예**합니다.
4. Toodelete hello 클라우드 서비스를 계획 하는 경우 필요에 따라 toodelete 다른 배포 3 단계를 반복 합니다.
5. toodelete hello 클라우드 서비스를 클릭 하 여 **삭제 클라우드 서비스**합니다. Hello 명령 프롬프트에서 클릭 **예**합니다.

> [!NOTE]
> 자세한 정보 표시 모니터링을 구성 된 경우 클라우드 서비스에 대 한 Azure hello hello 클라우드 서비스를 삭제 하면 모니터링 저장소 계정에서 데이터를 삭제 하지 않습니다. 수동으로 toodelete hello 데이터가 필요 합니다. 여기서 toofind hello 메트릭 테이블에 대 한 정보를 참조 하십시오. "하는 방법: hello Azure 클래식 포털 외부 자세한 정보 표시 모니터링 데이터에 액세스"에서 [tooMonitor 클라우드 서비스 방법](cloud-services-how-to-monitor.md)합니다.
>
>

## <a name="next-steps"></a>다음 단계
* [클라우드 서비스의 일반 구성](cloud-services-how-to-configure.md)
* 너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy.md)합니다.
* [사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)구성
* [SSL 인증서](cloud-services-configure-ssl-certificate.md)구성
