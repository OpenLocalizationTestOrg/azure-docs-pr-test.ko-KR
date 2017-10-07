---
title: "Azure 웹 앱에 대 한 리소스 관리자 기반 크로스 플랫폼 명령줄 도구 aaaAzure | Microsoft Docs"
description: "어떻게 toouse hello 새 Azure 리소스 관리자 기반 크로스 플랫폼 명령줄 도구 toomanage Azure 웹 앱에 알아봅니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Azure App Service용 Azure Resource Manager 기반 XPlat CLI 사용
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Microsoft Azure 크로스 플랫폼 명령줄 도구 버전 0.10.5 hello 릴리스마다 새로운 명령이 추가 되었습니다. 이 명령은 hello 사용자 hello 기능 toouse Azure 리소스 관리자 기반 PowerShell 명령을 toomanage 앱 서비스를 제공합니다.

리소스 그룹을 관리 하는 방법에 대 한 toolearn 참조 [hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹](../azure-resource-manager/xplat-cli-azure-resource-manager.md)합니다. 

> [!NOTE] 
> 또한 사용해 [Azure CLI 2.0](https://github.com/Azure/azure-cli), 차세대 CLI hello 리소스 관리 배포 모델에 대 한 Python으로 작성 합니다.
>
>

## <a name="managing-app-service-plans"></a>앱 서비스 계획 관리
### <a name="create-an-app-service-plan"></a>앱 서비스 계획 만들기
앱 서비스 계획을 toocreate hello를 사용 하 여 **azure appserviceplan 만들** 명령입니다.

다음은 hello 다른 매개 변수:

* **-리소스 그룹**: 새로 만든 hello 앱 서비스 계획을 포함 하는 리소스 그룹입니다.
* **-이름**: hello 앱 서비스 계획의 이름입니다.
* **--location**: App Service 계획 위치
* **-sku**: hello 필요한 가격 책정 sku (hello 옵션은: F1 (Free). D1(공유) B1(Basic Small), B2(Basic Medium), B3(Basic Large) S1(Standard Small), S2(Standard Medium), S3(Standard Large) P1(Premium Small), P2(Premium Medium), P3(Premium Large)
* **-인스턴스**: (기본값은 1) hello 앱 서비스 계획의 작업자 수가 hello 합니다.

예제 toouse이이 cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Linux App Service 계획 만들기

동일한 hello를 사용 하 여 **azure appserviceplan 만들** hello로 명령을 추가 매개 변수 **-islinux true**합니다. Hello 제한 사항 및 지역에 설명 된 유의 [소개 tooApp linux 서비스](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>기존 앱 서비스 계획 나열
toolist hello 기존 앱 서비스 계획을 사용 하 여 **azure appserviceplan 목록** 명령입니다.

toolist 특정 리소스 그룹 아래의 모든 앱 서비스 계획을 사용 합니다.

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

tooget 특정 앱 서비스 계획을 사용 하 여 **azure appserviceplan 표시** 명령:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>기존 앱 서비스 계획 구성
기존 앱 서비스 계획에 대 한 toochange hello 설정을 사용 하 여 hello **azure appserviceplan config** 명령입니다. Hello sku 및 hello 작업자 수를 변경할 수 있습니다. 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>앱 서비스 계획 크기 조정
tooscale는 기존 앱 서비스 계획을 사용 합니다.

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>앱 서비스 계획의 SKU hello 변경
기존 앱 서비스 계획을 사용 하 여의 toochange hello sku:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>기존 앱 서비스 계획 삭제
기존 앱 서비스 계획 toodelete 모두 할당 됨 앱 필요 toobe 이동 하거나 먼저 삭제 합니다. 그런 다음 hello를 사용 하 여 **azure webapp 삭제** 명령 hello 앱 서비스 계획을 삭제할 수 있습니다.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>App Service 앱 관리
### <a name="create-a-web-app"></a>웹앱 만들기
toocreate 웹 응용 프로그램에서 사용 하 여 hello **azure webapp 만들** 명령입니다.

다음은 hello 다른 매개 변수:

* **-이름**: hello 웹 앱에 대 한 이름입니다.
* **-계획**: toohost hello 웹 응용 프로그램을 사용 하는 hello 서비스 계획에 대 한 이름을 지정 합니다.
* **-리소스 그룹**: hello 앱 서비스 계획을 호스팅하는 리소스 그룹입니다.
* **-위치**: 웹 앱 위치의 hello 합니다.

예제 toouse이이 cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>기존 앱 삭제
기존 앱 toodelete hello를 사용할 수 있습니다 **azure webapp 삭제** 명령입니다. Hello 앱 toospecify hello 이름과 hello 리소스 그룹 이름은 해야합니다.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>기존 앱 목록
toolist hello 기존 응용 프로그램을 사용 하 여 hello **azure webapp 목록** 명령입니다.

toolist 특정 리소스 그룹에서 모든 앱을 사용 합니다.

    azure webapp list --resource-group ContosoAzureResourceGroup

특정 앱 tooget hello를 사용 하 여 **azure webapp 표시** 명령입니다.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>기존 앱 구성
toochange hello 설정 및 기존 응용 프로그램에 대 한 구성을 사용 하 여 hello **azure webapp 구성 집합** 명령입니다.

응용 프로그램의 hello php 버전을 변경 하는 예 (1): 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

예 (2): 앱 설정 추가 또는 변경

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

tooknow 다른 구성을 변경할 수 있습니다를 사용 하 여 hello **azure webapp 구성 집합-h** 명령입니다.

### <a name="change-hello-state-of-an-existing-app"></a>기존 앱의 hello 상태 변경
#### <a name="restart-an-app"></a>앱 다시 시작
응용 프로그램 toorestart, hello 응용 프로그램의 hello 이름과 리소스 그룹을 지정 해야 합니다.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>앱 중지
응용 프로그램 toostop, hello 응용 프로그램의 hello 이름과 리소스 그룹을 지정 해야 합니다.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>앱 시작
응용 프로그램 toostart, hello 응용 프로그램의 hello 이름과 리소스 그룹을 지정 해야 합니다.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>앱의 게시 프로필 관리
각 응용 프로그램 코드를 사용 하는 toopublish 일 수 있는 게시 프로필에 있습니다.

#### <a name="get-publishing-profile"></a>게시 프로필 가져오기
tooget hello를 사용 하 여 응용 프로그램에 대 한 프로필 게시:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

이 명령은 hello 게시 프로필 사용자 이름 및 암호 toohello 명령줄에 표시 합니다.

### <a name="manage-app-hostnames"></a>앱 호스트 관리
응용 프로그램에 대 한 호스트 이름 바인딩을 toomanage hello를 사용 하 여 **azure webapp config hostnames** 명령  

#### <a name="list-hostname-bindings"></a>호스트 이름 바인딩 나열
응용 프로그램에 대 한 tooget hello 현재 호스트 이름 바인딩을 사용 합니다.

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>호스트 이름 바인딩 추가
tooadd 호스트 이름 바인딩 tooan 앱을 사용 하 여:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>호스트 이름 바인딩 삭제
toodelete 호스트 이름 바인딩을 사용 합니다.

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자 CLI 지원에 대 한 toolearn 참조 [hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹입니다.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* PowerShell을 사용 하는 응용 프로그램 서비스를 관리 하는 방법에 대 한 toolearn 참조 [Using Azure Resource Manager-Based PowerShell tooManage Azure 웹 앱입니다.](app-service-web-app-azure-resource-manager-powershell.md)
* linux에서 Azure 앱 서비스에 대 한 toolearn 참조 [소개 tooApp linux 서비스](app-service-linux-intro.md)
