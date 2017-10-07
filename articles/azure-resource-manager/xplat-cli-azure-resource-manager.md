---
title: "hello Azure CLI를 사용 하 여 aaaManage 리소스 | Microsoft Docs"
description: "Hello Azure 명령줄 인터페이스 (CLI) toomanage Azure를 사용 하 여 리소스 및 그룹"
editor: 
manager: timlt
documentationcenter: 
author: tfitzmac
services: azure-resource-manager
ms.assetid: bb0af466-4f65-4559-ac3a-43985fa096ff
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: tomfitz
ms.openlocfilehash: 3df70e123d14d3bbf2648c71970bac1db4afc025
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cli-toomanage-azure-resources-and-resource-groups"></a>Hello Azure CLI toomanage Azure를 사용 하 여 리소스 및 리소스 그룹
> [!div class="op_single_selector"]
> * [포털](resource-group-portal.md) 
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
> 
> 

hello Azure CLI (명령줄 인터페이스 Azure)는 하나는 여러 도구 중 toodeploy를 사용 하 여 고 리소스 관리자와 리소스를 관리할 수 있습니다. 이 문서에서는 일반적인 방법으로 toomanage Azure 소개 리소스 및 리소스 그룹을 사용 하 여 리소스 관리자 모드에서 Azure CLI hello 합니다. Hello CLI toodeploy 리소스를 사용 하는 방법에 대 한 정보를 참조 하십시오. [리소스 관리자 템플릿 및 Azure CLI를 사용 하 여 리소스를 배포](resource-group-template-deploy-cli.md)합니다. Azure 리소스 및 리소스 관리자에 대 한 배경 방문 hello [Azure 리소스 관리자 개요](resource-group-overview.md)합니다.

> [!NOTE]
> toomanage Azure hello Azure CLI를 사용 하 여 리소스를 필요한 너무[hello Azure CLI 설치](../cli-install-nodejs.md), 및 [tooAzure 로그인](../xplat-cli-connect.md) hello를 사용 하 여 `azure login` 명령입니다. CLI는 리소스 관리자 모드에서 확인 되었는지 hello (실행 `azure config mode arm`). 다음과 같은이 작업을 수행 하는 경우 준비 toogo 합니다.
> 
> 

## <a name="get-resource-groups-and-resources"></a>리소스 그룹 및 리소스 가져오기
### <a name="resource-groups"></a>리소스 그룹
tooget 구독 및 해당 위치에 있는 모든 리소스 그룹의 목록에는이 명령을 실행 합니다.

    azure group list


### <a name="resources"></a>리소스
 toolist와 같은 그룹의 모든 리소스 이름을 *testRG*, hello 다음 명령을 사용 하 여:

    azure resource list testRG

명명 된 VM과 같은 hello 그룹 내에서 개별 리소스 tooview *MyUbuntuVM*를 hello 다음과 같은 명령을 사용 하 여:

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

공지 hello **Microsoft.Compute/virtualMachines** 매개 변수입니다. 이 매개 변수에서 정보를 요청 하는 hello 리소스의 hello 유형을 나타냅니다.

> [!NOTE]
> Hello를 사용 하는 경우 **azure 리소스** hello 이외의 명령을 **목록** hello hello 리소스의 hello API 버전 지정 해야 합니다. 명령을 **-o** 매개 변수입니다. Hello API 버전에 대 한 잘 모를 경우 hello 템플릿 파일을 참조 하 고 hello 리소스에 대 한 hello apiVersion 필드를 찾습니다. Resource Manager의 API 버전에 대한 자세한 내용은 [리소스 공급자 및 형식](resource-manager-supported-services.md)을 참조하세요.
> 
> 

경우 리소스에 대해 세부 정보를 보는 것이 유용한 toouse hello `--json` 매개 변수입니다. 이 매개 변수 되므로 일부 값은 중첩 된 구조 또는 컬렉션 보다 읽기 쉬운 hello 출력을 수 있습니다. hello 다음 예제에서는 hello의 hello 결과 반환 **표시** JSON 문서 명령입니다.

    azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json

> [!NOTE]
> 원하는 경우 hello를 사용 하 여 JSON 데이터 toofile hello 저장 &gt; 문자 toodirect hello 출력 tooa 파일입니다. 예:
> 
> `azure resource show testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15" --json > myfile.json`
> 
> 

### <a name="tags"></a>태그
[!INCLUDE [resource-manager-tag-resources-cli](../../includes/resource-manager-tag-resources-cli.md)]

## <a name="manage-resources"></a>리소스 관리
저장소 계정 tooa 리소스 그룹을 같은 리소스 tooadd 비슷한 명령을 실행 합니다.

    azure resource create testRG MyStorageAccount "Microsoft.Storage/storageAccounts" "westus" -o "2015-06-15" -p "{\"accountType\": \"Standard_LRS\"}"

또한이 toospecifying hello 리소스의 API 버전을 hello로 hello **-o** 매개 변수를 사용 하 여 hello **-p** 와 모든 필수 매개 변수 toopass JSON 형식 문자열 또는 추가 속성입니다.

가상 컴퓨터 리소스와 같은 기존 리소스 toodelete hello 다음과 같은 명령을 사용 합니다.

    azure resource delete testRG MyUbuntuVM Microsoft.Compute/virtualMachines -o "2015-06-15"

toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 **azure 리소스 이동** 명령입니다. hello 방법을 예제와 다음 toomove Redis Cache tooa 새 리소스 그룹입니다. Hello에 **-i** 매개 변수를 toomove hello 리소스 id의 쉼표로 구분 된 목록을 제공 합니다.

    azure resource move -i "/subscriptions/{guid}/resourceGroups/OldRG/providers/Microsoft.Cache/Redis/examplecache" -d "NewRG"

## <a name="control-access-tooresources"></a>컨트롤 액세스 tooresources
Azure CLI toocreate hello를 사용 하 고 정책 toocontrol tooAzure 리소스 액세스를 관리할 수 있습니다. 정책 정 및 할당 정책 tooresources 대 한 배경 정보를 참조 하십시오. [정책 toomanage 리소스를 사용 하 고 액세스 제어](resource-manager-policy.md)합니다.

예를 들어 hello 정책 toodeny 다음 여기서 위치는 하지 West US 또는 북 중미 모든 요청을 정의 하 고 toohello 정책 정의 파일 policy.json 저장:

    {
    "if" : {
        "not" : {
        "field" : "location",
        "in" : ["westus" ,  "northcentralus"]
        }
    },
    "then" : {
        "effect" : "deny"
    }
    }

그러고 나 서 hello **정책 정의 만들기** 명령:

    azure policy definition create MyPolicy -p c:\temp\policy.json

이 명령은 유사한 toohello 다음을 출력을 보여 줍니다.

    + Creating policy definition MyPolicy data:    PolicyName:             MyPolicy data:    PolicyDefinitionId:     /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy

    data:    PolicyType:             Custom data:    DisplayName:            undefined data:    Description:            undefined data:    PolicyRule:             field=location, in=[westus, northcentralus], effect=deny

 정책 범위의 hello 사용 하 여 hello tooassign **PolicyDefinitionId** hello 이전 명령에서 반환 합니다. 다음 예제는 hello,이 범위 hello 구독 하지만 tooresource 그룹이 나 개별 리소스 범위를 지정할 수 있습니다.

    azure policy assignment create MyPolicyAssignment -p /subscriptions/########-####-####-####-############/providers/Microsoft.Authorization/policyDefinitions/MyPolicy -s /subscriptions/########-####-####-####-############/

가져오기, 변경 또는 hello를 사용 하 여 정책 정의 제거 **정책 정의 표시**, **정책 정의 집합**, 및 **정책 정의 삭제** 명령입니다.

마찬가지로, 또는 얻을 수 있습니다, 변경, 정책 할당 hello를 사용 하 여 제거 **정책 할당 표시**, **정책 할당 집합**, 및 **정책 할당을 삭제** 명령 .

## <a name="export-a-resource-group-as-a-template"></a>리소스 그룹을 템플릿으로 내보내기
기존 리소스 그룹에 대 한 hello 리소스 그룹에 대 한 hello 리소스 관리자 템플릿을 볼 수 있습니다. 내보내는 hello 서식 파일에는 두 가지 이점을 제공합니다.

1. 모든 hello 인프라 hello 서식 파일에 정의 되어 있기 때문에 쉽게 hello 솔루션의 향후 배포를 자동화할 수 있습니다.
2. 템플릿 구문에 잘 알고 hello 솔루션을 나타내는 JSON 보고 될 수 있습니다.

Hello Azure CLI를 사용 하 여 hello 리소스 그룹의 현재 상태를 나타내는 템플릿 내보내기 하거나 특정 배포에 사용 된 hello 템플릿을 다운로드 합니다.

* **리소스 그룹에 대 한 hello 템플릿 내보내기** -이 변경 내용 tooa 리소스 그룹에서 항목과 필요한 tooretrieve hello 현재 상태로의 JSON 표현을 때 유용 합니다. 그러나 생성 된 템플릿 hello 최소한 매개 변수 및 변수를 포함합니다. 대부분의 hello 값 hello 템플릿에 하드 코드 됩니다. Hello 생성 된 서식 파일을 배포 하기 전에 수도 있습니다 tooconvert hello 값 중 매개 변수를 다양 한 환경에 대 한 hello 배포를 사용자 지정할 수 있습니다.
  
    리소스 그룹 tooa 로컬 디렉터리를 hello 실행에 대 한 tooexport hello 템플릿을 `azure group export` hello 다음 예제와 같이 명령입니다. (운영 체제 환경에 맞게 적합한 로컬 디렉터리로 대체)
  
        azure group export testRG ~/azure/templates/
* **특정 배포에 대 한 hello 템플릿을 다운로드** -tooview hello 실제 서식 파일을 사용 하는 toodeploy 리소스 했습니다 할 때 유용 합니다. 모든 매개 변수 및 변수 hello 원래 배포에 대해 정의 된 hello 서식 파일에 포함 되어 있습니다. 그러나 시도 하면 조직의 누군가가 hello 정의 외부에서 변경 내용 toohello 리소스 그룹 hello 서식 파일에서이 템플릿을 hello hello 리소스 그룹의 현재 상태를 나타내지 않습니다.
  
    특정 배포 tooa 로컬 디렉터리 hello 실행에 사용 되는 toodownload hello 템플릿입니다 `azure group deployment template download` 명령입니다. 예:
  
        azure group deployment template download TestRG testRGDeploy ~/azure/templates/downloads/

> [!NOTE]
> 템플릿 내보내기는 미리 보기 버전이며, 템플릿 내보내기를 지원하지 않는 리소스 유형도 있습니다. Tooexport 서식 파일을 시도할 때 일부 리소스를 내보내지 못했습니다 되었다는 오류가 표시 될 수 있습니다. 필요한 경우 템플릿을 다운로드한 후 템플릿에서 이러한 리소스를 수동으로 정의합니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* 배포 작업의 세부 정보 tooget hello Azure CLI를 사용 하 여 배포 오류 문제를 해결 하 고, 참조 [배포 작업을 보려면](resource-manager-deployment-operations.md)합니다.
* 응용 프로그램 또는 스크립트 tooaccess 리소스를 toouse hello CLI tooset 참조 [서비스 주체를 사용 하 여 Azure CLI toocreate tooaccess 리소스](resource-group-authenticate-service-principal-cli.md)합니다.
* 기업에서는 리소스 관리자 tooeffectively 사용 방법에 대 한 지침에 대 한 구독을 관리, 참조 [Azure enterprise 스 캐 폴드-규범적인 구독 거 버 넌 스](resource-manager-subscription-governance.md)합니다.

