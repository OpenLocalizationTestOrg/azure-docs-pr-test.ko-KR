---
title: "Azure 포털 toodeploy aaaUse Azure 리소스 | Microsoft Docs"
description: "Azure 포털 및 Azure 리소스 관리 toodeploy 리소스를 사용 합니다."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>리소스 관리자 템플릿과 Azure 포털로 리소스 배포
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [포털](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

이 항목에서는 방법을 toouse hello [Azure 포털](https://portal.azure.com) 와 [Azure 리소스 관리자](resource-group-overview.md) toodeploy Azure 리소스입니다. 리소스를 관리 하는 방법에 대 한 toolearn 참조 [포털을 통해 관리 하는 Azure 리소스](resource-group-portal.md)합니다.

현재, 모든 서비스는 hello 포털 또는 리소스 관리자를 지원합니다. 이러한 서비스에 대해 필요한 toouse hello [클래식 포털](https://manage.windowsazure.com)합니다. 각 서비스의 상태를 hello에 대 한 참조 [Azure 포털 가용성 차트](https://azure.microsoft.com/features/azure-portal/availability/)합니다.

## <a name="create-resource-group"></a>리소스 그룹 만들기
1. toocreate 빈 리소스 그룹을 선택 **새로** > **관리** > **리소스 그룹**합니다.
   
    ![빈 소스 그룹 만들기](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. 이름과 위치를 지정하고 필요한 경우 구독을 선택합니다. 리소스 그룹 hello hello 리소스에 대 한 메타 데이터를 저장 하기 때문에 hello 리소스 그룹 위치 tooprovide가 필요 합니다. 규정 준수 상의 이유로 toospecify 메타 데이터를 저장할 수도 있습니다. 일반적으로 대부분의 리소스가 상주할 위치를 지정하는 것이 좋습니다. 동일한 hello를 사용 하 여 위치 서식 파일을 단순화할 수 있습니다.
   
    ![그룹 값 설정](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>마켓플레이스에서 리소스 배포
리소스 그룹을 만든 후에 리소스 tooit hello Marketplace에서에서 배포할 수 있습니다. hello 마켓플레이스는 일반적인 시나리오에 대 한 미리 정의 된 솔루션을 제공 합니다.

1. toostart 해당 배포를 선택 **새로** hello 유형 및 리소스의 toodeploy 원할 것입니다. 그런 다음 hello hello 리소스의 특정 버전에 대 한 toodeploy 원할 것입니다.
   
    ![리소스 배포](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Toodeploy 원하는 hello 특정 솔루션, 표시 되지 않으면 마켓플레이스 hello에 대 한 검색할 수 있습니다.
   
    ![마켓플레이스 검색](./media/resource-group-template-deploy-portal/search-resource.png)
3. 선택한 리소스의 hello 형식에 따라 컬렉션을 배포 하기 전에 관련 속성 tooset 해야합니다. 리소스 유형에 따라 달라지므로 해당 옵션은 여기에 표시되지 않습니다. 모든 유형에 대해 대상 리소스 그룹을 선택해야 합니다. hello 다음 그림에서는 어떻게 toocreate 웹 앱 및 만든 toohello 리소스 그룹을 배포 합니다.
   
    ![리소스 그룹 만들기](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    또는 리소스를 배포할 때 toocreate 리소스 그룹을 결정할 수 있습니다. 선택 **새로 만들기** hello 리소스 그룹 이름을 지정 합니다.
   
    ![새 리소스 그룹 만들기](./media/resource-group-template-deploy-portal/select-new-group.png)
4. 배포가 시작됩니다. hello 배포는 몇 분 정도 걸릴 수 있습니다. Hello 배포 완료 되 면 알림이 표시 됩니다.
   
    ![알림 보기](./media/resource-group-template-deploy-portal/view-notification.png)
5. 리소스를 배포한 후 hello를 사용 하 여 더 많은 리소스 toohello 리소스 그룹을 추가할 수 있습니다 **추가** hello 리소스 그룹 블레이드 명령을 합니다.
   
    ![리소스 추가](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>사용자 지정 템플릿에서 배포
Tooexecute 배포 하지만 hello Marketplace에에서 hello 템플릿 중 하나를 사용 하지, 솔루션에 대 한 hello 인프라를 정의 하는 사용자 지정된 템플릿을 만들 수 있습니다. 서식 파일 만들기에 대 한 toolearn 참조 [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.

1. toodeploy hello 포털을 통해 사용자 지정된 된 템플릿을 선택 **새로**, 검색을 시작 하 고 **템플릿 배포** hello 옵션 중에서 선택할 수 있을 때까지 합니다.
   
    ![템플릿 배포 찾기](./media/resource-group-template-deploy-portal/search-template.png)
2. 선택 **템플릿 배포** hello 사용 가능한 리소스에서 합니다.
   
    ![템플릿 배포 선택](./media/resource-group-template-deploy-portal/select-template.png)
3. Hello 템플릿 배포를 시작한 후 사용자 지정에 사용할 수 있는 hello 빈 서식 파일을 엽니다.
   
    ![템플릿 만들기](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    Hello 편집기에서 원하는 toodeploy hello 리소스를 정의 하는 hello JSON 구문을 추가 합니다. 완료되면 **저장** 을 선택합니다. Hello JSON 구문을 작성에 대 한 지침을 참조 하십시오. [리소스 관리자 템플릿 연습](resource-manager-template-walkthrough.md)합니다.
   
    ![템플릿 편집](./media/resource-group-template-deploy-portal/edit-template.png)
4. Hello에서 기존 서식 파일을 선택할 수 있습니다 또는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/)합니다. 이러한 템플릿은 hello 커뮤니티 기여 하 합니다. 여러 가지 일반적인 시나리오를 처리 하 고 누군가가 템플릿에 비슷한 toowhat toodeploy를 시도 하는 추가 수 있습니다. Hello 템플릿 toofind에 시나리오와 일치 하는 내용을 검색할 수 있습니다.
   
    ![빠른 시작 템플릿 선택](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    선택한 템플릿을 hello hello 편집기에서 볼 수 있습니다.
5. 입력 한 후 모든 hello 다른 값, 선택 **만들기** toodeploy hello 템플릿. 
   
    ![템플릿 배포](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Tooyour 계정을 서식 파일에서 리소스를 배포 합니다.
hello 포털 toosave 템플릿 tooyour Azure 계정이 있으며 나중에 다시 배포 합니다. 다음 템플릿, 저장 된 사용에 대 한 자세한 내용은 [hello Azure 포털에서 개인 템플릿을 시작](../marketplace-consumer/mytemplates-getstarted.md)합니다.

1. 저장 된 템플릿을 선택 toofind **찾아보기** > **템플릿**합니다.
   
    ![템플릿 찾아보기](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Hello tooyour 계정을 저장 하는 템플릿 목록에서 하나의 원하는 toowork에 hello를 선택 합니다.
   
    ![저장된 템플릿](./media/resource-group-template-deploy-portal/saved-templates.png)
3. 선택 **배포** tooredeploy이 템플릿을 저장 합니다.
   
    ![저장된 템플릿 배포](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>다음 단계
* tooview 감사 로그 참조 [리소스 관리자와 작업을 감사](resource-group-audit.md)합니다.
* tootroubleshoot 배포 오류 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.
* 배포 또는 리소스 그룹에서 템플릿을 tooretrieve 참조 [기존 리소스에서 내보내기 Azure 리소스 관리자 템플릿을](resource-manager-export-template.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

