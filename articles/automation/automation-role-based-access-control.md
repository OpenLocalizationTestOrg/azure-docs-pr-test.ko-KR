---
title: "Azure 자동화에서 aaaRole 기반 액세스 제어 | Microsoft Docs"
description: "RBAC(역할 기반 액세스 제어)를 통해 Azure 리소스에 대한 액세스 관리가 가능합니다. 이 문서에서는 설명 어떻게 tooset Azure 자동화에서 RBAC 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "자동화 rbac, 역할 기반 액세스 제어, azure rbac"
ms.assetid: 04b5625e-0ee8-4b5b-85cd-7734c1b3d4a3
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;sngun
ms.openlocfilehash: 051438e44d0c5c514d6dbaac5a312344ee311cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-in-azure-automation"></a>Azure 자동화의 역할 기반 액세스 제어
## <a name="role-based-access-control"></a>역할 기반 액세스 제어
RBAC(역할 기반 액세스 제어)를 통해 Azure 리소스에 대한 액세스 관리가 가능합니다. 사용 하 여 [RBAC](../active-directory/role-based-access-control-configure.md), 팀 내에서 업무의 네트워크를 격리할 수 있습니다 및 권한 부여에만 액세스 toousers, 그룹 및 필요 하다는 tooperform 업무 응용 프로그램의 양을 hello 합니다. Toousers hello Azure 포털, Azure 명령줄 도구 또는 Azure 관리 Api를 사용 하 여 역할 기반 액세스를 부여할 수 있습니다.

## <a name="rbac-in-automation-accounts"></a>자동화 계정의 RBAC
Azure 자동화에서 적절 한 RBAC 역할 toousers hello, 그룹 및 응용 프로그램에 hello 자동화 계정 범위를 할당 하 여 액세스가 허용 됩니다. 다음은 자동화 계정에서 지 원하는 기본 제공 역할 hello 됩니다.  

| **역할** | **설명** |
|:--- |:--- |
| 소유자 |hello 소유자 역할 tooall 리소스에 액세스 및 액세스 tooother 사용자, 그룹 및 응용 프로그램 toomanage hello 자동화 계정을 제공 하는 자동화 계정 내에서 작업을 허용 합니다. |
| 참여자 |hello 참가자 역할 toomanage 수 있습니다. 다른 사용자의 수정 제외한 모든 사용 권한을 tooan 자동화 계정에 액세스 합니다. |
| 읽기 권한자 |hello 읽기 역할이 있습니다 tooview를 자동화의 모든 hello 리소스 계정 수 있지만 변경할 수 없습니다. |
| 자동화 운영자 |hello 자동화 운영자 역할 있습니다 tooperform 운영 작업 시작 등, 중지, 일시 중단, 다시 시작 및 작업을 예약 합니다. 이 역할은 원하는 tooprotect runbook에서 자격 증명 자산 등 자동화 계정 리소스 표시 하거나 수정할 경우에 유용 하지만 조직 tooexecute의 구성원을 계속 이러한 runbook 사용할 수 있습니다. |
| 사용자 액세스 관리자 |hello 사용자 액세스 관리자 역할 toomanage 사용자 액세스 tooAzure 자동화 계정이 있습니다. |

> [!NOTE]
> 액세스 권한 tooa 특정 runbook 또는 runbook, toohello 자원과 hello 자동화 계정 내에서 동작을 부여할 수 없습니다.  
> 
> 

이 문서에서 우리는 방법을 안내 하 tooset Azure 자동화에서 RBAC 구성 합니다. 그러나 먼저 더 자세히 살펴보고 hello 개별 사용 권한 부여한 toohello 참가자, Reader, 자동화 연산자 및 사용자 액세스 관리자에 게 모든 사용자 권한을 부여 하기 전에 이해 이점도 take 권한의 toohello 자동화 계정 보겠습니다.  그렇지 않으면 의도하지 않거나 원하지 않은 결과가 발생할 수 있습니다.     

## <a name="contributor-role-permissions"></a>참가자 역할 권한
hello 다음 표에 표시 자동화의 hello 참가자 역할에서 수행할 수 있는 hello 동작 합니다.

| **리소스 종류** | **읽기** | **쓰기** | **삭제** | **다른 작업** |
|:--- |:--- |:--- |:--- |:--- |
| Azure 자동화 계정 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 인증서 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 연결 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 연결 형식 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 자격 증명 자산  |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 일정 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 변수 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 필요한 상태 구성 | | | |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |
| Hybrid Runbook Worker 리소스 종류 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure 자동화 작업 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |
| 자동화 작업 스트림 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 작업 일정 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| 자동화 모듈 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |
| Azure 자동화 Runbook |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |
| 자동화 Runbook 초안 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |
| 자동화 Runbook 초안 테스트 작업 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |
| 자동화 Webhook |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |

## <a name="reader-role-permissions"></a>읽기 역할 권한
hello 다음 표에 표시 자동화에서 hello 읽기 역할에서 수행할 수 있는 hello 동작 합니다.

| **리소스 종류** | **읽기** | **쓰기** | **삭제** | **다른 작업** |
|:--- |:--- |:--- |:--- |:--- |
| 클래식 구독 관리자 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 관리 잠금 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 사용 권한 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 공급자 작업 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 역할 할당 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 역할 정의 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="automation-operator-role-permissions"></a>자동화 운영자 역할 권한
hello 다음 표에 표시 hello 자동화 Operator 역할에 자동화가 수행할 수 있는 hello 동작 합니다.

| **리소스 종류** | **읽기** | **쓰기** | **삭제** | **다른 작업** |
|:--- |:--- |:--- |:--- |:--- |
| Azure 자동화 계정 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 인증서 자산 | | | | |
| 자동화 연결 자산 | | | | |
| 자동화 연결 형식 자산 | | | | |
| 자동화 자격 증명 자산  | | | | |
| 자동화 일정 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | |
| 자동화 변수 자산 | | | | |
| 자동화 필요한 상태 구성 | | | | |
| Hybrid Runbook Worker 리소스 종류 | | | | |
| Azure 자동화 작업 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |
| 자동화 작업 스트림 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 작업 일정 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | |
| 자동화 모듈 | | | | |
| Azure 자동화 Runbook |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 Runbook 초안 | | | | |
| 자동화 Runbook 초안 테스트 작업 | | | | |
| 자동화 Webhook | | | | |

자세한 내용은 hello [자동화 운영자 작업](../active-directory/role-based-access-built-in-roles.md#automation-operator) 목록 hello hello 자동화 연산자 역할 hello 자동화 계정 및 해당 리소스에 지원 되는 작업입니다.

## <a name="user-access-administrator-role-permissions"></a>사용자 액세스 관리자 역할 권한
hello 다음 표에 표시 자동화의 hello 사용자 액세스 관리자 역할에서 수행할 수 있는 hello 동작 합니다.

| **리소스 종류** | **읽기** | **쓰기** | **삭제** | **다른 작업** |
|:--- |:--- |:--- |:--- |:--- |
| Azure 자동화 계정 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 인증서 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 연결 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 연결 형식 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 자격 증명 자산  |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 일정 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 변수 자산 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 필요한 상태 구성 | | | | |
| Hybrid Runbook Worker 리소스 종류 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure 자동화 작업 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 작업 스트림 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 작업 일정 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 모듈 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| Azure 자동화 Runbook |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 Runbook 초안 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 Runbook 초안 테스트 작업 |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |
| 자동화 Webhook |![녹색 상태](media/automation-role-based-access-control/green-checkmark.png) | | | |

## <a name="configure-rbac-for-your-automation-account-using-azure-portal"></a>Azure 포털을 사용하여 자동화 계정에 대한 RBAC 구성
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) 자동화 계정을 hello 자동화 계정을 블레이드에서 엽니다.  
2. Hello 클릭 **액세스** hello 상단 오른쪽 모서리에서 제어 합니다. Hello 열립니다 **사용자** 블레이드를 추가할 수 있는 새 사용자, 그룹 및 응용 프로그램 toomanage 자동화 계정 및 보기 기존 역할에 대해 구성할 수 있는 자동화 계정 hello 합니다.  
   
   ![액세스 단추](media/automation-role-based-access-control/automation-01-access-button.png)  

> [!NOTE]
> **구독 관리자** hello 기본 사용자로 이미 있습니다. hello 서비스 관리자 및 Azure 구독에 대 한 co-administrator(s) hello 구독 관리자 active directory 그룹에 포함 되어 있습니다. 서비스 admin 님 안녕하세요 Azure 구독 및 해당 리소스의 hello 소유자 하며 됩니다는 hello 소유자 역할 상속 hello 자동화 계정에 대 한 너무 합니다. 즉, hello를 **Inherited** 에 대 한 **서비스 관리자와 공동 관리자** 구독 및 해당의 **할당** 다른 사용자가 hello 모두에 대 한 합니다. 클릭 **구독 관리자** tooview 해당 사용 권한에 대 한 더 자세히 설명 합니다.  
> 
> 

### <a name="add-a-new-user-and-assign-a-role"></a>새 사용자 추가 및 역할 할당
1. Hello 사용자 블레이드에서 클릭 **추가** tooopen hello **추가 액세스 블레이드** 사용자, 그룹 또는 응용 프로그램을 추가 하 고 역할 toothem를 할당할 수 있습니다.  
   
   ![사용자 추가](media/automation-role-based-access-control/automation-02-add-user.png)  
2. Hello 사용 가능한 역할 목록에서 역할을 선택 합니다. 에서는 hello를 선택 합니다 **판독기** hello 사용 가능한 기본 제공 역할을 지 원하는 자동화 계정 중 하나 또는 사용자 지정 역할 정의 될 수 있습니다 하지만 역할을 선택할 수 있습니다.  
   
   ![역할 선택](media/automation-role-based-access-control/automation-03-select-role.png)  
3. 클릭 **사용자 추가** tooopen hello **사용자 추가** 블레이드입니다. 모든 사용자, 그룹 또는 응용 프로그램 toomanage를 추가한 경우에 구독 한 다음 해당 사용자가 나열 되 고 tooadd 액세스를 선택할 수 있습니다. 사용자가 나열 하거나 hello 사용자 추가에 관심이 나열 되지 않은 경우 클릭 하지 않은 경우 **초대** tooopen hello **게스트 초대** 올바른 Microsoft 계정으로 사용자를 초대할 수 있는 블레이드 예: Outlook.com, OneDrive, Xbox Live Id 전자 메일 주소입니다. 클릭 하 여 hello 사용자의 hello 전자 메일 주소를 입력 하 고 나면 **선택** tooadd 사용자 hello 및 클릭 **확인**합니다. 
   
   ![사용자 추가](media/automation-role-based-access-control/automation-04-add-users.png)  
   
   이제 추가한 hello 사용자를 표시 해야 toohello **사용자** hello로 블레이드 **판독기** 할당 된 역할입니다.  
   
   ![사용자 나열](media/automation-role-based-access-control/automation-05-list-users.png)  
   
   Hello에서 역할 toohello 사용자를 할당할 수도 있습니다 **역할** 블레이드입니다. 
4. 클릭 **역할** hello 사용자 블레이드 tooopen hello에서 **역할 블레이드**합니다. 이 블레이드에서 hello 역할, 사용자 및 그룹 toothat 역할 할당의 hello 수가의 hello 이름을 볼 수 있습니다.
   
    ![사용자 블레이드에서 역할 할당](media/automation-role-based-access-control/automation-06-assign-role-from-users-blade.png)  
   
   > [!NOTE]
   > 역할 기반 액세스 제어 hello 자동화 계정 수준에서 설정할 수 있습니다 및 hello 자동화 계정 아래의 모든 리소스에 없습니다.
   > 
   > 
   
    둘 이상의 역할 tooa 사용자, 그룹 또는 응용 프로그램을 할당할 수 있습니다. 예를 들어 hello 추가 **자동화 연산자** hello 함께 역할 **읽기 역할** toohello 사용자 다음 있습니다 수 모든 hello 자동화 리소스 보기으로 hello runbook 작업을 실행 합니다. Hello 드롭다운 tooview toohello 사용자 지정 된 역할의 목록을 확장할 수 있습니다.  
   
    ![여러 역할 보기](media/automation-role-based-access-control/automation-07-view-multiple-roles.png)  

### <a name="remove-a-user"></a>사용자 제거
자동화 계정을 hello를 관리 하지 않습니다 또는 hello 조직에 게 더 이상 작동 하는 사용자에 대 한 hello 액세스 권한을 제거할 수 없습니다. 다음 사용자 단계 tooremove hello 됩니다. 

1. Hello에서 **사용자** 블레이드, tooremove 원하는 선택 hello 역할 할당 합니다.
2. Hello 클릭 **제거** hello 할당 세부 정보 블레이드에서 단추입니다.
3. 클릭 **예** tooconfirm 제거 합니다. 
   
   ![사용자 제거](media/automation-role-based-access-control/automation-08-remove-users.png)  

## <a name="role-assigned-user"></a>역할이 할당된 사용자
Hello 목록에 나열 된 hello 소유자의 계정 사용자만 할당 tooa 역할 tootheir 자동화 계정에 로그인 할 때 이제 볼 수 **기본 디렉터리**합니다. 자동화 계정에 추가 하는 순서 tooview hello에 hello 기본 디렉터리 toohello 소유자 기본 디렉터리를 전환 해야 합니다.  

![기본 디렉터리](media/automation-role-based-access-control/automation-09-default-directory-in-role-assigned-user.png)  

### <a name="user-experience-for-automation-operator-role"></a>자동화 운영자 역할에 대한 사용자 환경
인 사용자를 할당 하면 toohello 자동화 연산자 역할 뷰 hello 자동화 계정에 할당 된, runbook만 보기 hello 목록을 수, runbook 작업 및 일정 hello 자동화 계정 만들었지만 해당 정의 볼 수 없습니다. 있습니다 수 시작, 중지, 일시 중단, 다시 시작 또는 hello runbook 작업을 예약 합니다. hello 사용자 hybrid worker 그룹 또는 DSC 노드 구성 같은 tooother 자동화 리소스 액세스 없을 것입니다.  

![액세스 tooresourcres 없음](media/automation-role-based-access-control/automation-10-no-access-to-resources.png)  

Hello 사용자 hello runbook을 클릭할 때 hello tooview 소스 hello 또는 hello runbook 편집 명령은 제공 되지 않습니다 hello 자동화 운영자 역할 toothem 액세스를 허용 하지 않습니다.  

![액세스 tooedit runbook 없음](media/automation-role-based-access-control/automation-11-no-access-to-edit-runbook.png)  

hello 사용자 액세스 tooview 및 toocreate 일정이 있지만 액세스 tooany 다른 자산 형식을 가지 지 않습니다.  

![액세스 tooassets 없음](media/automation-role-based-access-control/automation-12-no-access-to-assets.png)  

이 사용자도 없는 경우 runbook에 연결할 액세스 tooview hello webhook

![액세스 toowebhooks 없음](media/automation-role-based-access-control/automation-13-no-access-to-webhooks.png)  

## <a name="configure-rbac-for-your-automation-account-using-azure-powershell"></a>Azure PowerShell을 사용하여 자동화 계정에 대한 RBAC를 구성합니다.
역할 기반 액세스는 또한 구성 된 tooan 자동화 계정 수 hello 다음을 사용 하 여 [Azure PowerShell cmdlet](../active-directory/role-based-access-control-manage-access-powershell.md)합니다.

• [Get AzureRmRoleDefinition](https://msdn.microsoft.com/library/mt603792.aspx) 에는 Azure Active Directory에서 사용할 수 있는 모든 RBAC 역할이 나열됩니다. 이 명령은 hello와 함께 사용할 수 있습니다 **이름** 속성 toolist 모든 hello 특정 역할을 통해 수행할 수 있는 작업입니다.  
    **예제:**  
    ![역할 정의 가져오기](media/automation-role-based-access-control/automation-14-get-azurerm-role-definition.png)  

• [Get AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt619413.aspx) 목록 hello에서 Azure AD의 RBAC 역할 할당 범위를 지정 합니다. 이 명령은 모든 매개 변수 없이 hello 구독에서 만들어진 모든 hello 역할 할당을 반환 합니다. 사용 하 여 hello **ExpandPrincipalGroups** 가 멤버인을 hello 지정한 hello 그룹 뿐만 아니라 사용자 hello 사용자에 대 한 매개 변수 toolist 액세스 할당 합니다.  
    **예:** 모든 hello 사용자와 해당 역할은 자동화 계정 내에서 사용 하 여 hello 다음 명령은 toolist 합니다.

    Get-AzureRMRoleAssignment -scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>” 

![역할 할당 가져오기](media/automation-role-based-access-control/automation-15-get-azurerm-role-assignment.png)

• [새로 AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603580.aspx) tooassign 액세스 toousers, 그룹 및 응용 프로그램 tooa 특정 범위입니다.  
    **예:** 사용 하 여 hello 다음 명령은 사용자 hello 자동화 계정 범위에에서 대 한 tooassign hello "자동화 운영자" 역할.

    New-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish toogrant access> -RoleDefinitionName "Automation operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”  

![새 역할 할당](media/automation-role-based-access-control/automation-16-new-azurerm-role-assignment.png)

• 사용 [제거 AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt603781.aspx) 지정 된 사용자, 그룹 또는 특정 범위에서 응용 프로그램의 tooremove 액세스 합니다.  
    **예:** 사용 하 여 hello 다음 명령은 tooremove hello 사용자 hello "자동화 운영자" 역할 hello 자동화 계정 범위에에서가 있습니다.

    Remove-AzureRmRoleAssignment -SignInName <sign-in Id of a user you wish tooremove> -RoleDefinitionName "Automation Operator" -Scope “/subscriptions/<SubscriptionID>/resourcegroups/<Resource Group Name>/Providers/Microsoft.Automation/automationAccounts/<Automation Account Name>”

위의 예제는 hello, 바꿉니다 **Id 로그인**, **구독 Id**, **리소스 그룹 이름은** 및 **자동화 계정 이름** 와 사용자 계정 세부 정보입니다. 선택 **예** 때 tooconfirm tooremove 사용자 역할 할당을 계속 하기 전에 메시지가 표시 됩니다.   

## <a name="next-steps"></a>다음 단계
* 에 대 한 내용은 다양 한 방법 tooconfigure RBAC Azure 자동화에 대 한 참조 너무[Azure PowerShell을 사용한 RBAC 관리](../active-directory/role-based-access-control-manage-access-powershell.md)합니다.
* 다양 한 방법 toostart runbook에 대 한 세부 정보를 참조 하세요. [runbook 시작](automation-starting-a-runbook.md)
* 다른 runbook 형식에 대 한 정보에 대 한 참조 너무[Azure 자동화 runbook 형식](automation-runbook-types.md)

