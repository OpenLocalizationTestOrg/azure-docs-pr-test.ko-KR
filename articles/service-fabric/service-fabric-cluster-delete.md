---
title: "Azure aaaDelete 클러스터와 해당 리소스 | Microsoft Docs"
description: "방법 toocompletely 삭제 서비스 패브릭 클러스터 hello 클러스터를 포함 하 되 중 하나가 삭제 hello 리소스 그룹 또는 리소스를 선택적으로 삭제 하 여에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a>Azure 및 hello 리소스를 사용 하 여 서비스 패브릭 클러스터를 삭제 합니다.
서비스 패브릭 클러스터 구성 된 다양 한 Azure 리소스 뿐만 아니라 자체 toohello 클러스터 리소스입니다. Toocompletely 서비스 패브릭 클러스터를 삭제 하므로 toodelete 모든 hello 리소스 구성 되어 있어야 합니다.
두 가지 옵션이 있습니다:에 클러스터 hello 중 하나가 삭제 hello 리소스 그룹이 (삭제 하 hello 클러스터 리소스 및 hello 리소스 그룹의 다른 리소스) 또는 특히 hello 클러스터 리소스를 삭제 하 고 리소스에 연결 (다른 하지 않음 에서 리소스 hello 리소스 그룹)입니다.

> [!NOTE]
> Hello 클러스터 리소스를 삭제 **없는** 서비스 패브릭 클러스터는 구성 하는 다른 리소스를 hello 모두 삭제 합니다.
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a>서비스 패브릭 클러스터에는 hello hello 전체 리소스 그룹 (RG)를 삭제 합니다.
이 hello hello 리소스 그룹을 포함 하 여 클러스터와 연결 된 모든 hello 리소스를 삭제 하는 가장 쉬운 방법은 tooensure입니다. PowerShell을 사용 하 여 hello 리소스 그룹을 삭제할 수 있습니다 또는 hello Azure 포털을 통해. 리소스 그룹 관련된 tooService 패브릭 클러스터 되지 않은 리소스가 있는 경우, 특정 리소스를 삭제할 수 있습니다.

### <a name="delete-hello-resource-group-using-azure-powershell"></a>Azure PowerShell을 사용 하 여 hello 리소스 그룹 삭제
Hello 다음 Azure PowerShell cmdlet을 실행 하 여 hello 리소스 그룹을 삭제할 수도 있습니다. 컴퓨터에 Azure PowerShell 1.0 이상이 설치되어 있는지 확인합니다. 이전 수행 하지 않은 경우에 설명 된 hello 단계에 따라 [어떻게 tooinstall 및 Azure PowerShell을 구성 합니다.](/powershell/azure/overview)

PowerShell 창을 열고 hello 다음 PS cmdlet을 실행 합니다.

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

Hello를 사용 하지 않은 경우 프롬프트 tooconfirm hello 삭제 받아볼 수 *-Force* 옵션입니다. Hello RG에서 확인 하 고 포함 된 모든 hello 리소스 삭제 됩니다.

### <a name="delete-a-resource-group-in-hello-azure-portal"></a>Hello Azure 포털에에서 있는 리소스 그룹 삭제
1. 로그인 toohello [Azure 포털](https://portal.azure.com)합니다.
2. 원하는 toodelete toohello 서비스 패브릭 클러스터를 이동 합니다.
3. Hello hello 클러스터 essentials 페이지에서 리소스 그룹 이름을 클릭 합니다.
4. 그러면 hello **리소스 그룹 Essentials** 페이지.
5. **삭제**를 클릭합니다.
6. Hello 리소스 그룹의 해당 페이지 toocomplete hello 삭제 시 hello 지침을 따릅니다.

![리소스 그룹 삭제][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a>삭제 hello 클러스터 리소스 및를 사용 하는 hello 리소스 있지만 hello 리소스 그룹의 다른 리소스에 없습니다
리소스 그룹에 리소스를 관련된 toohello 서비스 패브릭 클러스터 toodelete, 원하는 경우 보다 쉽게 toodelete hello 전체 리소스 그룹. 리소스 그룹의 tooselectively delete hello 리소스 여 하나씩을 하려는 경우에 다음이 단계를 수행 합니다.

Hello 서비스 패브릭 리소스 관리자 템플릿 중 하나를 사용 하 여 hello 템플릿 갤러리에서 또는 hello 포털을 사용 하 여 클러스터를 배포한 경우 다음 모든 hello 리소스 클러스터 사용 하 여 hello를 태그로 지정 됩니다 hello 두 태그입니다. 원하는 어떤 리소스 toodecide 사용할 수 toodelete 합니다.

***태그 #1:*** 키 = clusterName, 값 = 'hello 클러스터의 이름'

***Tag#2:*** 키 = resourceName, 값 = ServiceFabric

### <a name="delete-specific-resources-in-hello-azure-portal"></a>Hello Azure 포털의에서 특정 리소스를 삭제 합니다.
1. 로그인 toohello [Azure 포털](https://portal.azure.com)합니다.
2. 원하는 toodelete toohello 서비스 패브릭 클러스터를 이동 합니다.
3. 너무 이동**모든 설정을** hello essentials 블레이드에서 합니다.
4. 클릭 **태그** 아래 **리소스 관리** hello 설정 블레이드에서 합니다.
5. Hello 중 하나를 클릭 **태그** hello 태그 블레이드 tooget 태그가 있는 모든 hello 리소스 목록에에서 있습니다.
   
    ![리소스 태그][ResourceTags]
6. 태그가 지정 된 리소스 목록이 hello를 만든 후 각 hello 리소스 클릭 하 고 삭제 합니다.
   
    ![태그가 지정된 리소스][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a>Azure PowerShell을 사용 하 여 hello 리소스 삭제
Hello 리소스 여 하나씩 hello 다음 Azure PowerShell cmdlet을 실행 하 여 삭제할 수 있습니다. 컴퓨터에 Azure PowerShell 1.0 이상이 설치되어 있는지 확인합니다. 이전 수행 하지 않은 경우에 설명 된 hello 단계에 따라 [어떻게 tooinstall 및 Azure PowerShell을 구성 합니다.](/powershell/azure/overview)

PowerShell 창을 열고 hello 다음 PS cmdlet을 실행 합니다.

```powershell
Login-AzureRmAccount
```
각 hello 리소스에 대 한 원하는 toodelete를 hello 다음 실행:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

toodelete hello 클러스터 리소스를 hello 다음 실행:

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a>다음 단계
클러스터 업그레이드 및 서비스를 분할 하는 방법에 대 한 자세한 내용은 tooalso 다음 읽기 hello:

* [클러스터 업그레이드 알아보기](service-fabric-cluster-upgrade.md)
* [최대 크기를 위해 상태 저장 서비스를 분할하는 방법 알아보기](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
