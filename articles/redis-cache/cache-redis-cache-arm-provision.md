---
title: "Azure 리소스 관리자를 사용 하 여 Redis Cache aaaProvision | Microsoft Docs"
description: "Azure 리소스 관리자 템플릿 toodeploy Azure Redis Cache를 사용 합니다."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>템플릿을 사용하여 Redis Cache 만들기
이 항목에서는 설명 Azure Redis Cache toocreate Azure 리소스 관리자 템플릿을 배포 하는 방법입니다. 기존 저장소 계정 tookeep 진단 데이터와 hello 캐시를 사용할 수 있습니다. 또한 학습 방법을 toodefine 리소스 배포 되 고 toodefine 매개 변수를 hello 배포를 실행 하는 경우 지정 된 합니다. 배포를 위한이 서식 파일을 사용 하거나 toomeet 사용자 지정할 수 있습니다 프로그램 요구 사항입니다.

Hello에서 모든 캐시에 대 한 진단 설정을 공유 되는 현재 구독에 대 한 동일한 영역입니다. Hello 지역에서 하나의 캐시를 업데이트 hello 지역에서 다른 모든 캐시를 영향을 줍니다.

템플릿을 만드는 더 자세한 내용은 [Azure 리소스 관리자 템플릿 작성하기](../azure-resource-manager/resource-group-authoring-templates.md)를 참조하십시오.

Hello 전체 서식 파일을 참조 하십시오. [Redis Cache 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json)합니다.

> [!NOTE]
> 새 hello에 대 한 리소스 관리자 템플릿을 [Premium 계층](cache-premium-tier-intro.md) 사용할 수 있습니다. 
> 
> * [클러스터링을 사용하여 프리미엄 Redis 캐시 만들기](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [지속성 데이터를 사용하여 프리미엄 Redis 캐시 만들기](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [VNet과 선택적 클러스터링을 사용하여 프리미엄 Redis 캐시 만들기](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> hello 최신 템플릿용으로 toocheck 참조 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 검색 한 `Redis Cache`합니다.
> 
> 

## <a name="what-you-will-deploy"></a>배포할 내용
이 템플릿에서 진단 데이터에 기존 저장소 계정을 사용하는 Azure Redis Cache를 배포합니다.

toorun 배포를 자동으로 hello, hello 다음 단추를 클릭 합니다.

[![TooAzure 배포](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>매개 변수
Azure 리소스 관리자와 정의한 매개 변수 값에 대 한 원하는 toospecify hello 서식 파일을 배포할 때. hello 템플릿은 모든 hello 매개 변수 값이 포함 된 매개 변수 라는 섹션을 포함 합니다.
에 배포 하는 hello 환경에 따라 또는 배포 하는 hello 프로젝트에 따라 달라 지는 해당 값에 대 한 매개 변수를 정의 해야 합니다. 동일한 값을 항상 유지 hello에 대 한 매개 변수를 정의 하지 않습니다. 각 매개 변수 값은 배포 된 hello 템플릿 toodefine hello 리소스에 사용 됩니다. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
hello Redis Cache의 hello 위치입니다. 최상의 성능을 위해 사용 하 여 동일한 hello hello 캐시 사용 응용 프로그램 toobe hello 위치입니다.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
진단에 대 한 기존 저장소 계정 toouse hello의 hello 이름입니다. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>enableNonSslPort
나타내는 부울 값을 tooallow 비 SSL 포트를 통해 액세스할 지 여부를 합니다.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
진단을 사용하도록 설정할지 여부를 나타내는 값입니다. ON 또는 OFF를 사용합니다.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>리소스 toodeploy
### <a name="redis-cache"></a>Redis 캐시
Azure Redis Cache hello를 만듭니다.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>명령 toorun 배포
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Azure CLI
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


