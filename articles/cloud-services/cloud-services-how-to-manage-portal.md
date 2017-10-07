---
title: "aaaCommon 클라우드 서비스 관리 작업 | Microsoft Docs"
description: "Hello Azure 포털에서에서 toomanage 클라우드 서비스 하는 방법에 대해 알아봅니다. 이러한 예제는 hello Azure 포털을 사용합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
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

Hello에 **클라우드 서비스 (클래식)** 부문의 문제 hello Azure 포털에서 있습니다 수 서비스 역할 또는 배포 업데이트, 준비 된 배포 tooproduction 승격, hello 리소스를 볼 수 있도록 리소스 tooyour 클라우드 서비스에 연결 종속성 및 배율에는 리소스를 함께 hello 및 클라우드 서비스 또는 배포를 삭제 합니다.

어떻게 tooscale 클라우드 서비스를 사용할 수에 대 한 자세한 내용은 [여기](cloud-services-how-to-scale-portal.md)합니다.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>방법: 클라우드 서비스 역할 또는 배포 업데이트
클라우드 서비스에 대 한 tooupdate hello 응용 프로그램 코드를 필요 사용 **업데이트** hello 클라우드 서비스 블레이드에서 합니다. 단일 역할이나 모든 역할을 업데이트할 수 있습니다. tooupdate, 서비스 구성 파일 또는 새 서비스 패키지를 업로드할 수 있습니다.

1. Hello에 [Azure 포털][Azure portal], tooupdate 원하는 hello 클라우드 서비스를 선택 합니다. 이 단계는 hello 클라우드 서비스 인스턴스 블레이드를 엽니다.
2. Hello 블레이드에서 hello 클릭 **업데이트** 단추입니다.

    ![업데이트 단추](./media/cloud-services-how-to-manage-portal/update-button.png)

3. 새 서비스 패키지 파일 (.cspkg) 및 서비스 구성 파일 (.cscfg) 사용 하 여 hello 배포를 업데이트 합니다.

    ![배포 업데이트](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **필요에 따라** hello 배포 레이블 및 hello 저장소 계정을 업데이트 합니다.
5. 모든 역할 역할 인스턴스를 하나만 있는 경우 선택 hello **하나 이상의 역할 단일 인스턴스가 포함 된 경우에 배포** tooenable hello 업그레이드 tooproceed 합니다.

    Azure는 각 역할에 둘 이상의 역할 인스턴스(가상 컴퓨터)가 있는 경우에만 클라우드 서비스 업데이트 중 99.95%의 서비스 가용성을 보장할 수 있습니다. 두 개의 역할 인스턴스와 하나의 가상 컴퓨터 hello 다른 업데이트에 클라이언트 요청을 처리 합니다.

6. 확인 **배포 시작** toohave hello 업데이트 hello 패키지의 hello 업로드가 완료 된 후에 적용 합니다.
7. 클릭 **확인** toobegin hello 서비스를 업데이트 합니다.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>방법: 준비 된 배포 tooproduction 배포 toopromote 교체
단계는 클라우드 서비스의 새로운 릴리스가 toodeploy 결정 및 클라우드 서비스 스테이징 환경에서 새 릴리스를 테스트 합니다. 사용 하 여 **교체** tooswitch hello Url는 hello 하 여 두 개의 배포 사항은 및 새 릴리스 tooproduction 승격 합니다.

Hello에서 배포를 스왑할 수 **클라우드 서비스** 페이지나 hello 대시보드 합니다.

1. Hello에 [Azure 포털][Azure portal], tooupdate 원하는 hello 클라우드 서비스를 선택 합니다. 이 단계는 hello 클라우드 서비스 인스턴스 블레이드를 엽니다.
2. Hello 블레이드에서 hello 클릭 **교체** 단추입니다.

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. hello 다음과 같은 확인 프롬프트가 열립니다.

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Hello 배포 정보를 확인 한 후 클릭 **확인** tooswap hello 배포 합니다.

    hello 배포 스왑 발생 신속 하 게 변경 하는 hello 유일한 항목은 hello 가상 IP 주소 (Vip) hello 배포에 대 한 합니다.

    toosave 계산 비용이 hello 프로덕션 배포 예상 대로 작동 하는지 확인 한 후에 스테이징 배포를 삭제할 수 있습니다.

### <a name="common-questions-about-swapping-deployments"></a>배포 교환에 대한 일반적인 질문

**Hello 필수 구성 요소 배포를 교환 하는 무엇입니까?**

성공적인 배포 교환을 위한 2가지 핵심 필수 조건은 다음과 같습니다.

- 프로덕션 슬롯에 대 한 고정 IP 주소를 toouse 하려는 경우에 프로그램 스테이징 슬롯에 대 한를 예약 해야 합니다. 그렇지 않으면 hello 스왑 실패합니다.

- Hello 교체를 수행 하기 전에 역할의 모든 인스턴스를 실행 되어야 합니다. Hello Azure 포털의 hello 개요 블레이드에에서 인스턴스의 hello 상태를 확인할 수 있습니다. Hello 또는 사용할 수 있습니다 [Get-azurerole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) Windows PowerShell에서 명령을 합니다.

게스트 OS 업데이트 및 서비스 작업을 복구 배포에도 발생할 수 있습니다 toofail을 바꿉니다. 자세한 내용은 [클라우드 서비스 배포 문제 해결](cloud-services-troubleshoot-deployment-problems.md)을 참조하세요.

**교체 시 응용 프로그램 가동 중지가 발생할 수 있습니까? 어떻게 처리해야 합니까?**

Hello 마지막 섹션에서 설명한 배포 스왑은 hello Azure 부하 분산 장치에 구성 변경에 있기 때문에 일반적으로 속도가 빠릅니다. 그러나 경우에 따라 10초 이상 걸리며 일시적인 연결 오류가 발생할 수 있습니다. toolimit 영향 tooyour 고객 구현을 고려할 [클라이언트 다시 시도 논리](../best-practices-retry-general.md)합니다.

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>방법: 리소스 tooa 클라우드 서비스를 연결 합니다.
Azure 포털 hello hello 현재 Azure 클래식 포털 같이 함께 리소스를 연결 되지 않습니다. 대신, 추가 리소스 toohello 배포 hello 클라우드 서비스에서 사용 중인 동일한 리소스 그룹입니다.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>방법: 배포 및 클라우드 서비스 삭제
클라우드 서비스를 삭제하려면 먼저 각각의 기존 배포를 삭제해야 합니다.

toosave 계산 비용이 hello 프로덕션 배포 예상 대로 작동 하는지 확인 한 후에 스테이징 배포를 삭제할 수 있습니다. 중지된 배포된 역할 인스턴스의 계산 비용이 청구됩니다.

배포 또는 클라우드 서비스 프로시저 toodelete 다음 hello를 사용 합니다.

1. Hello에 [Azure 포털][Azure portal], toodelete 원하는 hello 클라우드 서비스를 선택 합니다. 이 단계는 hello 클라우드 서비스 인스턴스 블레이드를 엽니다.
2. Hello 블레이드에서 hello 클릭 **삭제** 단추입니다.

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. 확인 하 여 hello 전체 클라우드 서비스를 삭제 하려면 **클라우드 서비스 및 해당 배포** hello 중 하나를 선택 하거나 **프로덕션 배포** 또는 hello **스테이징 배포**합니다.

    ![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Hello 클릭 **삭제** hello 아래쪽 단추입니다.
5. toodelete hello 클라우드 서비스를 클릭 하 여 **삭제 클라우드 서비스**합니다. Hello 명령 프롬프트에서 클릭 **예**합니다.

> [!NOTE]
> 클라우드 서비스가 삭제 되 고 구성 되는 자세한 정보 표시 모니터링 하는 경우 저장소 계정에서 hello 데이터를 수동으로 삭제 해야 있습니다. 여기서 toofind hello 메트릭 테이블에 대 한 정보를 참조 하십시오. [이](cloud-services-how-to-monitor.md) 문서.


## <a name="how-to-find-more-information-about-failed-deployments"></a>방법: 실패한 배포에 대한 자세한 정보 보기
hello **개요** 블레이드 상태 표시줄이 hello 위쪽에 있습니다. Hello 막대를 클릭 하면는 새 블레이드가 열리고 모든 오류 정보를 표시 합니다. Hello 배포에 포함 된 오류가 hello 정보 블레이드에서 비어 있습니다.

![클라우드 서비스 교환](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>다음 단계
* [클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)
* 너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy-portal.md)합니다.
* [사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)구성
* [SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성
