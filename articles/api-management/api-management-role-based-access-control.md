---
title: "Azure API 관리에서 역할 기반 액세스 제어 aaaHow tooUse | Microsoft Docs"
description: "방법을 배웁니다 toouse 기본 제공 역할 hello Azure API 관리에서 사용자 지정 역할 만들기"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>TooUse 역할 기반 액세스 제어 방법 Azure API 관리에서
Azure API 관리 신속히 알아봅니다 액세스 제어 (RBAC) tooenable 세부화 된 액세스 관리 API 관리 서비스 및 엔터티 (예:: Api, 정책)에 의존합니다. 이 문서에서는 API 관리에서 hello 기본 및 사용자 지정 역할에 대해 간략하게를 제공 합니다. Hello Azure 포털에서에서 액세스 관리에 대 한 자세한 내용은 참조 [hello Azure 포털에에서 대 한 액세스 관리 시작](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>기본 제공 역할
현재 API 관리 3 기본 제공 역할이 제공 하 고 hello 가까운 미래에에서 2 이상의 역할을 추가 합니다. 이러한 역할은 구독, 리소스 그룹 및 개별 API Management 인스턴스를 포함하여 서로 다른 범위에서 할당될 수 있습니다. 예를 들어, hello "Azure API 관리 서비스 읽기" 역할 tooan 사용자 hello 리소스 그룹 수준에서 할당 되 면 면 hello 사용자는는 hello 리소스 그룹의 내부 tooall API 관리 인스턴스를 읽기 액세스 합니다. 

hello 다음 표에서 간략 한 설명의 hello 기본 제공 역할입니다. Hello Azure 포털 또는 Azure를 포함 하 여 다른 도구를 사용 하 여 이러한 역할을 할당할 수 있습니다 [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell)Azure, [명령줄 인터페이스](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), 및 [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest)합니다. 자세한 내용은 방법에 대 한 tooassign 기본 제공 역할 참조 [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)합니다.

| 역할          | 읽기 액세스<sup>[1]</sup> | 쓰기 액세스<sup>[2]</sup> | 서비스 만들기, 삭제, 크기 조정, VPN 및 사용자 지정 도메인 구성 | Toolegacy Publsiher 포털 액세스 | 설명
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| API Management 서비스 참가자 | ✓ | ✓ | ✓ | ✓ | 슈퍼 사용자. 전체 CRUD 액세스 tooAPI 관리 서비스 및 엔터티 (예: Api, 정책)에 있습니다. 액세스 toohello 레거시 게시자 포털을 있습니다. |
| Azure API Management 서비스 독자 | ✓ | | || 읽기 전용 액세스 tooAPI 관리 서비스 및 엔터티에 있습니다. |
| Azure API Management 서비스 연산자 | ✓ | | ✓ | | 엔터티가 아닌 API Management 서비스를 관리할 수 있습니다.|
| Azure API Management 서비스 편집기<sup>*</sup> | ✓ | ✓ | |  | API Management 엔터티는 관리할 수 있지만 서비스는 관리할 수 없습니다.|
| Azure API Management 콘텐츠 관리자<sup>*</sup> | ✓ | | | ✓ | 개발자 포털을 관리할 수 있습니다. 읽기 전용 액세스 tooservices 및 엔터티입니다.|

<sup>[1] 읽기 권한을 tooAPI 관리 서비스 및 엔터티 (예:: Api, 정책)</sup>

<sup>[2] 쓰기 액세스 tooAPI 관리 서비스 및 엔터티를 제외 하 고 다음 opeartions: 1) 인스턴스 만들기, 삭제 및 배율 2) VPN 구성 3) 사용자 지정 도메인 이름 설정</sup>

<sup>\*hello 기존 게시자 포털 toohello Azure 포털에서에서 모든 관리 UI를 마이그레이션 했습니다 후 hello 서비스 편집기 역할을 사용할 수 있습니다. hello 내용 관리자 역할에 사용할 수 있습니다 tooonly 포함 기능 관련된 toomanaging hello 개발자 포털 후 hello 게시자 포털 리팩터링 되었습니다.</sup>  


## <a name="custom-roles"></a>사용자 지정 역할
특정 요구를 충족 hello 기본 제공 역할이 사용자 정의 역할을 만들 수 있는지 tooprovide 보다 세부적인 액세스 API 관리 엔터티에 대 한 관리 합니다. 예를 들어 읽기 전용 액세스 tooan API 관리 서비스에는 없지만 쓰기 액세스 tooone 특정 API는 사용자 지정 역할을 만들 수 있습니다. toolearn 사용자 지정 역할에 대 한 자세한 내용은 참조 [사용자 정의 역할에서 Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)합니다. 

사용자 지정 역할을 만들 때 보다 쉽게 toostart hello 기본 제공 역할 중 하나를 사용 합니다. 편집 hello 특성 tooadd hello 동작, NotActions, 또는 AssignableScopes, 한 다음 새 역할로 hello 변경 내용을 저장 합니다. hello 다음 예제에서는 "Azure API 관리 서비스 읽기" 역할 hello로 시작 하 고 "계산기 API 편집기" 라는 사용자 지정 역할을 만듭니다. 특정 API만 요금이 따라서 tooa 액세스 toothat API만 hello 사용자 지정 역할을 할당할 수 있습니다. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>비디오 개요 보기

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>다음 단계

* Azure의 역할 기반 액세스 제어에 대한 자세한 정보
  * [Hello Azure 포털에에서 대 한 액세스 관리 시작](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [역할 할당 toomanage tooyour Azure 구독의 리소스에 액세스를 사용 하 여](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Azure RBAC에서 사용자 지정 역할](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
