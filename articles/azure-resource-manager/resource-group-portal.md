---
title: "Azure 포털 toomanage aaaUse Azure 리소스 | Microsoft Docs"
description: "Azure 포털 및 Azure 리소스 관리 toomanage 리소스를 사용 합니다. 표시 방법을 toowork 대시보드 toomonitor 리소스입니다."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>포털을 통해 Azure 리소스 관리
> [!div class="op_single_selector"]
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [포털](resource-group-portal.md) 
> * [REST API](resource-manager-rest-api.md)
> 
> 

이 항목에서는 방법을 toouse hello [Azure 포털](https://portal.azure.com) 와 [Azure 리소스 관리자](resource-group-overview.md) toomanage Azure 리소스입니다. toolearn hello 포털을 통해 리소스를 배포 하는 방법에 대 한 참조 [리소스 관리자 템플릿 및 Azure 포털을 사용 하 여 리소스를 배포](resource-group-template-deploy-portal.md)합니다.

현재, 모든 서비스는 hello 포털 또는 리소스 관리자를 지원합니다. 이러한 서비스에 대해 필요한 toouse hello [클래식 포털](https://manage.windowsazure.com)합니다. 각 서비스의 상태를 hello에 대 한 참조 [Azure 포털 가용성 차트](https://azure.microsoft.com/features/azure-portal/availability/)합니다.

## <a name="manage-resource-groups"></a>리소스 그룹 관리

리소스 그룹은 Azure 솔루션에 관련된 리소스를 보유하는 컨테이너입니다. 리소스 그룹 hello hello 솔루션에 대 한 모든 hello 리소스 또는 그룹으로 toomanage 되도록 하는 리소스에만 포함할 수 있습니다. 원하는 tooallocate 리소스를 결정 하는 요소 hello 조직에 가장 적합 한 기반으로 tooresource 그룹입니다. 일반적으로 hello를 공유 하는 리소스를 추가 같은 수명 주기 toohello 동일한 리소스 그룹 수 있도록 쉽게 배포, 업데이트를 그룹으로 삭제 합니다. 

리소스 그룹 hello hello 리소스에 대 한 메타 데이터를 저장합니다. 따라서 hello 리소스 그룹에 대 한 위치를 지정 하면 지정 하는 메타 데이터가 저장 됩니다. 규정 준수 상의 이유로 tooensure 할 수 있습니다는 데이터가 저장 되는 특정 지역에 있습니다.

1. toosee 구독에서 모든 hello 리소스 그룹 선택 **리소스 그룹**합니다.
   
    ![리소스 그룹 찾아보기](./media/resource-group-portal/browse-groups.png)
2. toocreate 빈 리소스 그룹을 선택 **추가**합니다.
   
    ![리소스 그룹 추가](./media/resource-group-portal/add-resource-group.png)
3. 이름 및 hello 새 리소스 그룹에 대 한 위치를 제공 합니다. **만들기**를 선택합니다.
   
    ![리소스 그룹 만들기](./media/resource-group-portal/create-empty-group.png)
4. Tooselect 야 **새로 고침** toosee hello 최근에 만든 리소스 그룹입니다.
   
    ![리소스 그룹 새로 고침](./media/resource-group-portal/refresh-resource-groups.png)
5. 리소스 그룹에 대해 표시 되는 toocustomize hello 정보 선택 **열**합니다.
   
    ![열 사용자 지정](./media/resource-group-portal/select-columns.png)
6. Hello 열 tooadd를 선택한 다음 선택 **업데이트**합니다.
   
    ![열 추가](./media/resource-group-portal/add-columns.png)
7. toolearn 리소스 tooyour 새 리소스 그룹 배포에 대 한 참조 [리소스 관리자 템플릿 및 Azure 포털을 사용 하 여 리소스를 배포](resource-group-template-deploy-portal.md)합니다.
8. 빠른 액세스 tooa 리소스 그룹에 대 한 hello 블레이드 tooyour 대시보드에 고정할 수 있습니다.
   
    ![리소스 그룹 고정](./media/resource-group-portal/pin-group.png)
9. hello 대시보드 hello 리소스 그룹 및 해당 리소스를 표시합니다. Hello 리소스 그룹 또는 해당 리소스 toonavigate toohello 항목 중 하나를 선택할 수 있습니다.
   
    ![리소스 그룹 고정](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>리소스 태그 지정
태그 tooresource 그룹을 적용할 수 있으며 리소스 toologically 자산을 구성 합니다. 작업 태그에 대 한 정보를 참조 하십시오. [를 사용 하 여 Azure 리소스를 tooorganize 태그](resource-group-using-tags.md)합니다.

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>리소스 모니터링
리소스를 선택 하는 경우 기본 그래프와 해당 리소스 유형의 모니터링에 대 한 테이블 hello 리소스 블레이드를 표시 합니다.

1. 리소스와 통지 hello 선택 **모니터링** 섹션. 관련 toohello 리소스 종류는 그래프를 포함 합니다. hello 다음 이미지 표시 hello 기본 저장소 계정에 대 한 데이터를 모니터링 합니다.
   
    ![모니터링 표시](./media/resource-group-portal/show-monitoring.png)
2. Hello 섹션 위에 hello 줄임표 (...)를 선택 하 여 hello 블레이드 tooyour 대시보드의 섹션을 고정할 수 있습니다. Hello 블레이드에서 hello 크기 hello 섹션을 사용자 지정 하거나 완전히 제거할 수 있습니다. hello 다음 이미지 또는 방법을 보여 줍니다 toopin, 사용자 지정 hello CPU 및 메모리 섹션을 제거 합니다.
   
    ![선택 고정](./media/resource-group-portal/pin-cpu-section.png)
3. Hello 섹션 toohello 대시보드를 고정 한 후 요약 hello hello 대시보드에 표시 됩니다. 및 hello 데이터에 대 한 세부 정보 toomore 즉시 선택 하면 이동 합니다.
   
    ![대시보드 보기](./media/resource-group-portal/view-startboard.png)
4. toocompletely hello 포털을 통해 모니터링, tooyour 기본 대시보드를 탐색 및 선택 hello 데이터를 사용자 지정 **새 대시보드**합니다.
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. 새 대시보드의 이름을 지정 하 고 hello 대시보드 타일 끌어다 키를 누릅니다. hello 타일은 다양 한 옵션으로 필터링 됩니다.
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     대시보드를 사용 하는 방법에 대 한 toolearn 참조 [만들고 hello Azure 포털에서에서 대시보드 공유](../azure-portal/azure-portal-dashboards.md)합니다.

## <a name="manage-resources"></a>리소스 관리
리소스에 대 한 hello 블레이드에서 hello 리소스를 관리 하기 위한 hello 옵션 볼 수 있습니다. hello 포털 해당 특정 리소스 종류에 대 한 관리 옵션을 표시합니다. Hello의 위쪽 hello 리소스 블레이드 및 hello 왼쪽에 걸쳐 hello 관리 명령을 볼 수 있습니다.

![리소스 관리](./media/resource-group-portal/manage-resources.png)

이러한 옵션 중에서 시작 하 고 가상 컴퓨터를 중지 하거나 hello 가상 컴퓨터의 hello 속성을 다시 구성 하는 등의 작업을 수행할 수 있습니다.

## <a name="move-resources"></a>리소스 이동
Toomove 리소스 tooanother 리소스 그룹 또는 다른 구독, 필요한 경우 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](resource-group-move-resources.md)합니다.

## <a name="lock-resources"></a>리소스 잠금
잠글 수 있습니다 구독, 리소스 그룹 또는 리소스 tooprevent 다른 사용자가 조직의 실수로 삭제 하거나 중요 한 리소스를 수정 합니다. 자세한 내용은 [Azure 리소스 관리자를 사용하여 리소스 잠그기](resource-group-lock-resources.md)를 참조하세요.

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>구독 및 비용 보기
모든 리소스에 대 한 구독 및 hello 겹쳐서 비용에 대 한 정보를 볼 수 있습니다. 선택 **구독** 및 toosee hello 구독 합니다. 하나의 구독 tooselect만 있을 수 있습니다.

![subscription](./media/resource-group-portal/select-subscription.png)

Hello 구독 블레이드에서 이내 진행 속도 표시 합니다.

![진행 속도](./media/resource-group-portal/burn-rate.png)

그리고 리소스 유형별 비용 분석이 표시됩니다.

![리소스 비용](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>템플릿 내보내기
리소스 그룹을 설정한 후 hello 리소스 그룹에 대 한 tooview hello 리소스 관리자 템플릿을 할 수 있습니다. 내보내는 hello 서식 파일에는 두 가지 이점을 제공합니다.

1. Hello 템플릿에 모든 hello 전체 인프라를 포함 하기 때문에 hello 솔루션의 향후 배포를 쉽게 자동화할 수 있습니다.
2. 템플릿 구문에 잘 알고 hello 개체 JSON (JavaScript Notation) 솔루션을 나타내는 보고 될 수 있습니다.

단계별 지침은 [기존 리소스에서 Azure Resource Manager 템플릿 내보내기](resource-manager-export-template.md)를 참조하세요.

## <a name="delete-resource-group-or-resources"></a>리소스 그룹 또는 리소스 삭제
리소스 그룹을 삭제 하면 그 안에 포함 된 hello 리소스를 모두 삭제 합니다. 리소스 그룹 내부의 개별 리소스를 삭제할 수도 있습니다. 다른 리소스 그룹에 연결 된 tooit 있는 리소스 수 있으므로 리소스 그룹을 삭제 하면 원하는 tooexercise 주의 해야 합니다. 리소스 관리자는 연결 된 리소스를 삭제 하지 않습니다 하지만 올바르게 hello 예상 리소스 없이 작동 하지 않을 수 있습니다.

![그룹 삭제](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>다음 단계
* tooview 활동 로그 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.
* tooview 세부 정보는 배포에 대 한 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.
* hello 포털을 통해 toodeploy 리소스 참조 [리소스 관리자 템플릿 및 Azure 포털을 사용 하 여 리소스를 배포](resource-group-template-deploy-portal.md)합니다.
* toomanage 액세스 tooresources 참조 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](../active-directory/role-based-access-control-configure.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

