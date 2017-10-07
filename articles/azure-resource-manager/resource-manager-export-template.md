---
title: "Azure 리소스 관리자 템플릿 aaaExport | Microsoft Docs"
description: "Azure 리소스 관리 tooexport 기존 리소스 그룹에서 서식 파일을 사용 합니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a>기존 리소스에서 Azure Resource Manager 템플릿 내보내기
이 문서에서는 설명 어떻게 tooexport 구독에 기존 리소스에서 리소스 관리자 템플릿 합니다. 해당 생성 된 템플릿 toogain 템플릿 구문에 사용할 수 있습니다.

서식 파일은 두 가지 방법으로 tooexport:

* Hello를 내보낼 수 **배포에 사용 되는 실제 템플릿**합니다. hello 내보낸된 템플릿에 hello 원본 서식 파일에 표시 된 그대로 hello 매개 변수 및 변수를 모두 포함 됩니다. 이 방법은 hello 포털을 통해 리소스를 배포할 때 유용 하 고 toosee hello 템플릿 toocreate 이러한 리소스입니다. 이 템플릿은 곧 사용할 수 있습니다. 
* 내보낼 수는 **hello hello 리소스 그룹의 현재 상태를 나타내는 템플릿을 생성**합니다. hello에서 내보낸된 템플릿 배포에 사용 된 파일 따르지 않습니다. 대신, 템플릿에 hello 리소스 그룹의 스냅숏을 만듭니다. hello에서 내보낸된 템플릿에 하드 코드 된 값이 많은 및 일반적으로 정의할 때와 하지 못할 수의 매개 변수입니다. 이 방법은 배포 후 hello 리소스 그룹을 수정한 경우에 유용 합니다. 일반적으로 이 템플릿을 사용하기 전에 수정해야 합니다.

이 항목에서는 hello 포털을 통해 두 가지 방법을 모두 보여 줍니다.

## <a name="deploy-resources"></a>리소스 배포
서식 파일로 내보내는 데 사용할 수 있는 리소스 tooAzure를 배포 하 여 시작 하겠습니다. Tooexport tooa 템플릿을 하려는 구독에 리소스 그룹이 이미 있는 경우에이 섹션을 건너뛸 수 있습니다. 이 문서의 나머지 부분에서는 hello hello web app 및이 섹션에 표시 된 SQL 데이터베이스 솔루션을 배포한 가정 합니다. 다른 솔루션을 사용 하 여 환경을 약간 다를 수 있습니다 있지만 tooexport 서식 파일은 hello 단계 hello 동일 합니다. 

1. Hello에 [Azure 포털](https://portal.azure.com)선택, **새로**합니다.
   
      ![새로 만들기 선택](./media/resource-manager-export-template/new.png)
2. 검색할 **웹 응용 프로그램 + SQL** hello 사용 가능한 옵션에서 선택 합니다.
   
      ![웹앱 및 SQL 검색](./media/resource-manager-export-template/webapp-sql.png)

3. **만들기**를 선택합니다.

      ![만들기 선택](./media/resource-manager-export-template/create.png)

4. Hello web app 및 SQL 데이터베이스에 대 한 hello 필요한 값을 제공 합니다. **만들기**를 선택합니다.

      ![웹 및 SQL 값 제공](./media/resource-manager-export-template/provide-web-values.png)

hello 배포 1 분을 걸릴 수 있습니다. Hello 배포 완료 되 면 hello 솔루션 구독에 포함 되어 있습니다.

## <a name="view-template-from-deployment-history"></a>배포 기록의 템플릿 보기
1. 새 리소스 그룹에 대 한 toohello 리소스 그룹 블레이드로 이동 합니다. 해당 hello 블레이드 hello hello 마지막 배포 결과 보여 줍니다. 확인 합니다. 이 링크를 선택합니다.
   
      ![리소스 그룹 블레이드](./media/resource-manager-export-template/select-deployment.png)
2. Hello 그룹에 대 한 배포의 기록을 표시 합니다. 여기에서 hello 블레이드 아마도 하나의 배포를 나열합니다. 이 배포를 선택합니다.
   
     ![마지막 배포](./media/resource-manager-export-template/select-history.png)
3. hello 블레이드 hello 배포의 요약 정보를 표시합니다. hello 요약 hello 배포의 hello 상태 작업 및 매개 변수에 대해 제공 하는 hello 값을 포함 합니다. hello 배포에 사용한 toosee hello 템플릿을 **템플릿 보기**합니다.
   
     ![배포 요약 보기](./media/resource-manager-export-template/view-template.png)
4. 리소스 관리자를 다음 7 개의 파일이 hello를 검색 합니다.
   
   1. **템플릿** -솔루션에 대 한 hello 인프라를 정의 하는 hello 템플릿입니다. 리소스 관리자 템플릿 toodeploy 사용 hello 포털을 통해 hello 저장소 계정을 만들 때 해당 하 고 나중에 참조할 수에 대 한 해당 서식 파일을 저장 합니다.
   2. **매개 변수** -배포 중 toopass을 사용할 값의 수 있는 매개 변수 파일입니다. Hello 첫 번째 배포 중에 제공 하는 hello 값을 포함 합니다. Hello 서식 파일을 다시 배포할 때 다음이 값 중 하나를 변경할 수 있습니다.
   3. **CLI** -Azure command 명령줄 인터페이스 (CLI) 스크립트 파일 toodeploy hello 서식 파일을 사용할 수 있습니다.
   3. **CLI 2.0** -Azure command 명령줄 인터페이스 (CLI) 스크립트 파일 toodeploy hello 서식 파일을 사용할 수 있습니다.
   4. **PowerShell** -는 Azure PowerShell 스크립트 파일 toodeploy hello 서식 파일을 사용할 수 있습니다.
   5. **.NET** -A.NET 클래스 toodeploy hello 서식 파일을 사용할 수 있습니다.
   6. **Ruby** -A Ruby 클래스 toodeploy hello 서식 파일을 사용할 수 있습니다.
      
      hello 파일 hello 블레이드에서 링크를 통해 제공 됩니다. 기본적으로 hello 블레이드 hello 템플릿을 표시합니다.
      
       ![템플릿 보기](./media/resource-manager-export-template/see-template.png)
      
이 템플릿은 hello 실제 템플릿을 toocreate 사용 하는 경우 웹 앱 및 SQL 데이터베이스입니다. 배포 하는 동안 tooprovide 서로 다른 값을 사용 하는 매개 변수를 포함 하는 것을 확인 합니다. 참조는 템플릿의 hello 구조에 대해 자세히 toolearn [제작 Azure 리소스 관리자 템플릿을](resource-group-authoring-templates.md)합니다.

## <a name="export-hello-template-from-resource-group"></a>리소스 그룹에서 hello 템플릿 내보내기
리소스 변경 수동으로 했거나 여러 배포에서 리소스를 추가 하는 경우 hello 배포 기록에서 서식 파일을 검색 반영 하지 않습니다 hello hello 리소스 그룹의 현재 상태. 이 섹션에서는 tooexport 반영 하는 템플릿을 hello 리소스 그룹의 현재 상태를 hello 하는 방법을 보여 줍니다. 

> [!NOTE]
> 200개 이상의 리소스가 있는 리소스 그룹에 대한 템플릿을 내보낼 수 없습니다.
> 
> 

1. 리소스 그룹 선택에 대 한 tooview hello 템플릿을 **자동화 스크립트**합니다.
   
      ![리소스 그룹 내보내기](./media/resource-manager-export-template/select-automation.png)
   
     Hello 리소스 그룹의 hello 리소스를 평가 하 고 해당 리소스에 대 한 서식 파일을 생성 하는 리소스 관리자입니다. 일부 리소스 형식은 hello 내보내기 템플릿 함수를 지원합니다. Hello 내보내기에 문제가 있다는 것을 나타내는 오류가 표시 될 수 있습니다. 어떻게 toohandle 된 문제에 대해 알아봅니다 hello [내보내기 관련 문제를 해결할](#fix-export-issues) 섹션.
2. 다시 tooredeploy hello 솔루션을 사용할 수 있는 hello 6 개의 파일을 참조 하십시오. 그러나이 시간 hello 서식 파일은 약간 다릅니다. 생성 된 템플릿 hello 포함 매개 변수가 이전 섹션에서 hello 서식 파일 보다 적습니다. 또한 많은 hello 값 (예: 위치 및 SKU 값) 매개 변수 값을 허용 하는 대신이 서식 파일에 하드 코드 되어 있습니다. 이 서식 파일을 다시 사용 하기 전에 tooedit hello 템플릿 toomake를 효과적으로 사용할 매개 변수를 할 수 있습니다. 
   
3. 두 가지 toowork이이 템플릿 사용 하 여 계속 하기 위한 옵션이 해야 합니다. Hello 템플릿을 다운로드 고 로컬로 JSON 편집기에 사용할 수 있습니다. 또는 hello 템플릿 tooyour 라이브러리를 저장 하 고 hello 포털을 통해에 사용할 수 있습니다.
   
     에 익숙한 경우와 같은 JSON 편집기를 사용 하 여 [VS Code](https://code.visualstudio.com/) 또는 [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), hello 서식 파일을 로컬로 다운로드 하 고 해당 편집기를 사용 하 여 수도 있습니다. toowork 로컬로 선택 **다운로드**합니다.
   
      ![템플릿 다운로드](./media/resource-manager-export-template/download-template.png)
   
     JSON 편집기를 설정 하지, hello 포털을 통해 hello 템플릿을 편집 하는 것이 좋습니다. 이 항목의 나머지 부분에서는 hello hello 템플릿 tooyour 라이브러리 hello 포털에 저장 한 가정 합니다. 그러나 수행한 동일한 hello 구문 JSON 편집기로 또는 hello 포털을 통해 로컬로 작동 하는지 toohello 서식 파일을 변경 합니다. hello 포털을 통해 toowork 선택 **toolibrary 추가**합니다.
   
      ![toolibrary 추가](./media/resource-manager-export-template/add-to-library.png)
   
     템플릿 toohello 라이브러리에 추가할 때는 이름 및 설명을 hello 서식 파일을 지정 합니다. 그런 다음 **저장**을 선택합니다.
   
     ![템플릿 값 설정](./media/resource-manager-export-template/save-library-template.png)
4. tooview 라이브러리에 저장 된 템플릿을 선택 **더 많은 서비스**, 형식 **템플릿** toofilter 결과 **템플릿**합니다.
   
      ![템플릿 찾기](./media/resource-manager-export-template/find-templates.png)
5. 저장 하는 hello 이름의 hello 템플릿을 선택 합니다.
   
      ![템플릿 선택](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a>Hello 템플릿을 사용자 지정
내보낸 hello 템플릿 작동 동일한 웹 응용 프로그램 및 모든 배포에 대 한 SQL 데이터베이스 toocreate hello를 원하는 경우 세밀 하 게 합니다. 하지만 Resource Manager는 훨씬 더 유연하게 템플릿을 배포할 수 있도록 옵션을 제공합니다. 이 문서에서는 tooadd 매개 변수 hello에 대 한 데이터베이스 관리자 이름 및 암호를 보여 줍니다. Hello 서식 파일의 다른 값에 대 한이 동일한 접근 방식을 tooadd를 보다 융통성 있게를 사용할 수 있습니다.

1. 선택 toocustomize hello 템플릿을 **편집**합니다.
   
     ![템플릿 표시](./media/resource-manager-export-template/select-edit.png)
2. Hello 템플릿을 선택 합니다.
   
     ![템플릿 편집](./media/resource-manager-export-template/select-added-template.png)
3. toobe 수 toopass hello 값 toospecify 배포 하는 동안 선택 추가 다음 두 개의 매개 변수 toohello hello **매개 변수** hello 서식 파일의 섹션:

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. toouse hello 새 매개 변수를 대체 hello에 SQL server 정의 hello **리소스** 섹션. **administratorLogin** 및 **administratorLoginPassword**는 이제 매개 변수 값을 사용합니다.

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. 선택 **확인** 완료 한 경우 hello 서식 파일을 편집 합니다.
7. 선택 **저장** toosave hello 변경 toohello 템플릿.
   
     ![템플릿 저장](./media/resource-manager-export-template/save-template.png)
8. 선택 tooredeploy 업데이트 hello 템플릿을 **배포**합니다.
   
     ![템플릿 배포](./media/resource-manager-export-template/redeploy-template.png)
9. 매개 변수 값을 제공 하 고 한 리소스 그룹 toodeploy hello 리소스를 선택 합니다.


## <a name="fix-export-issues"></a>내보내기 문제 수정
일부 리소스 형식은 hello 내보내기 템플릿 함수를 지원합니다. 이 문제를 수동으로 tooresolve 서식 파일에 다시 hello 누락 리소스를 추가 합니다. hello 오류 메시지에 내보낼 수 없는 hello 리소스 종류를 포함 합니다. [템플릿 참조](/azure/templates/)에서 리소스 종류를 찾습니다. 예를 들어 가상 네트워크 게이트웨이 추가, 참조 toomanually [Microsoft.Network/virtualNetworkGateways 템플릿 참조](/azure/templates/microsoft.network/virtualnetworkgateways)합니다.

> [!NOTE]
> 배포 기록이 아닌 리소스 그룹에서 내보낸 경우 내보내기 문제가 발생합니다. 마지막 배포 hello hello 리소스 그룹의 현재 상태를 정확 하 게 나타내는 경우 hello 리소스 그룹 대신 hello 배포 기록에서 hello 서식 파일을 내보내야 합니다. 만 단일 서식 파일에 정의 되어 있지 않은 변경 내용 toohello 리소스 그룹을 변경한 경우 리소스 그룹에서 내보냅니다.
> 
> 

## <a name="next-steps"></a>다음 단계
배웠습니다 어떻게 tooexport hello 포털에서 만든 리소스에서 템플릿 합니다.

* [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md) 또는 [REST API](resource-group-template-deploy-rest.md)를 통해 템플릿을 배포할 수 있습니다.
* tooexport PowerShell 통해서만 템플릿을 참조 하는 방법을 toosee [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](powershell-azure-resource-manager.md)합니다.
* tooexport Azure CLI를 통해 템플릿을 참조 하는 방법을 toosee [사용 하 여 hello Mac, Linux 및 Windows Azure 리소스 관리자에 대 한 Azure CLI](xplat-cli-azure-resource-manager.md)합니다.

