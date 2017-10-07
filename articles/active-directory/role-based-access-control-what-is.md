---
title: "aaaManage 액세스 및 RBAC-Azure RBAC를 사용한 사용 권한 | Microsoft Docs"
description: "시작 액세스 관리에서 hello Azure 포털의에서 Azure 역할 기반 액세스 제어 합니다. 역할 할당 tooassign 권한을 사용 하 여 디렉터리에 있습니다."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8f8aadeb-45c9-4d0e-af87-f1f79373e039
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 1c133b2b57b49d85f0e12a318c7997478e095fb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-role-based-access-control-in-hello-azure-portal"></a>Hello Azure 포털에서에서 역할 기반 액세스 제어를 시작.
보안 지향적인 회사 직원에 게 필요한 hello 정확 하 게 사용 권한이 부여에 초점을 맞추어야 합니다. 너무 많은 권한을 계정 tooattackers를 노출할 수 있습니다. 권한이 너무 적으면 직원이 업무를 효율적으로 수행할 수 없습니다. Azure RBAC(역할 기반 액세스 제어)는 Azure에 대한 세밀한 액세스 관리를 제공하여 이 문제를 해결하도록 도와줍니다.

RBAC를 사용 하 여 팀 내에서 업무를 구분할 수 있으며 필요 하다는 tooperform 업무 hello 양의 데이터만 toousers 액세스 권한을 부여 수도 있습니다. Azure 구독 또는 리소스에서 모든 사람에게 무제한 권한을 제공하는 대신 특정 작업만 허용할 수 있습니다. 예를 들어 구독에서 가상 컴퓨터를 관리 하는 사용 하 여 RBAC toolet 직원이 한 명, 다른를 관리할 수 있는 반면 SQL 데이터베이스 hello 내에서 동일한 구독 합니다.

## <a name="basics-of-access-management-in-azure"></a>Azure에서 액세스 관리의 기본 사항
각각의 Azure 구독은 하나의 Azure AD(Active Directory) 디렉터리와 연결됩니다. 사용자, 그룹 및 해당 디렉터리에서 응용 프로그램 hello Azure 구독에서에서 리소스를 관리할 수 있습니다. Hello Azure 포털, Azure 명령줄 도구 및 Azure 관리 Api를 사용 하 여 이러한 액세스 권한을 할당 합니다.

적절 한 RBAC 역할 toousers hello, 그룹 및 특정 범위의 응용 프로그램을 할당 하 여 액세스를 부여 합니다. 역할 할당의 hello 범위는 구독, 리소스 그룹 또는 단일 리소스 될 수 있습니다. 부모 범위에서 지정 된 역할이 부여 액세스 toohello 자식에 포함 합니다. 예를 들어 액세스 tooa 리소스 그룹에 있는 사용자에 포함 된 웹 사이트, 가상 컴퓨터 및 서브넷와 같은 모든 hello 리소스를 관리할 수 있습니다.

![Azure Active Directory 요소 간 관계 - 다이어그램](./media/role-based-access-control-what-is/rbac_aad.png)

hello RBAC 역할 할당 하는 어떤 리소스 hello 사용자, 그룹 또는 응용 프로그램은 해당 범위 내에서 관리할 수를 지정 합니다.

## <a name="built-in-roles"></a>기본 제공 역할
Azure RBAC tooall 리소스 유형에 적용 되는 세 가지 기본 역할에 있습니다.

* **소유자** 에 대 한 모든 권한을 tooall 리소스가 hello 오른쪽 toodelegate 액세스 tooothers를 포함 합니다.
* **참가자** 수 만들고 모든 유형의 Azure 리소스를 관리할 수 있지만 tooothers 액세스 권한을 부여할 수 없습니다.
* **읽기 권한자** 는 기존 Azure 리소스를 볼 수 있습니다.

Azure의 hello RBAC 역할 hello 나머지 특정 Azure 리소스 관리를 허용 합니다. 예를 들어 hello 가상 컴퓨터 참가자 역할 hello 사용자 toocreate 허용 하 고 가상 컴퓨터를 관리 합니다. 제공 되지 않습니다 해당 액세스 toohello 가상 네트워크 또는 가상 컴퓨터를 hello hello 서브넷에 연결 합니다. 

[기본 제공 역할 RBAC](role-based-access-built-in-roles.md) 목록 hello Azure에서 사용할 수 있는 역할입니다. Hello 작업과 toousers 각 기본 제공 역할에 부여 하는 범위를 지정 합니다. 찾고 있는 경우 toodefine 더 많은 컨트롤에 대 한 사용자 역할, 참조 방법을 toobuild [사용자 지정 역할에서 Azure RBAC](role-based-access-control-custom-roles.md)합니다.

## <a name="resource-hierarchy-and-access-inheritance"></a>리소스 계층 구조 및 액세스 상속
* 각 **구독** Azure 속한 tooonly 한 디렉터리입니다. 그러나 각 디렉터리는 하나 이상의 구독을 가질 수 있습니다.
* 각 **리소스 그룹** tooonly 구독 하나에 속합니다.
* 각 **리소스** tooonly 한 리소스 그룹에 속해 있습니다.

부모 범위에서 부여되는 액세스 권한은 자식 범위에서 상속됩니다. 예:

* Hello 구독 범위에서 hello 판독기 역할 tooan Azure AD 그룹에 할당할 합니다. 해당 그룹의 hello 멤버 hello 구독에서 모든 리소스 그룹 및 리소스를 볼 수 있습니다.
* Hello 참가자 역할 tooan 응용 프로그램 hello 리소스 그룹 범위에 할당 합니다. 해당 리소스 그룹에 있지만 hello 구독에서 다른 리소스 그룹 하지에 있는 모든 형식의 리소스를 관리할 수 있습니다.

## <a name="azure-rbac-vs-classic-subscription-administrators"></a>Azure RBAC와 클래식 구독 관리자 비교
클래식 구독 관리자 및 공동 관리자에 대 한 모든 권한을 toohello Azure 구독 포함 됩니다. Hello를 사용 하 여 리소스를 관리할 수 있는 [Azure 포털](https://portal.azure.com) Azure 리소스 관리자 Api 또는 hello [Azure 클래식 포털](https://manage.windowsazure.com) 및 Azure 클래식 배포 모델입니다. Hello RBAC 모델 클래식 관리자 hello 소유자 역할 hello 구독 범위에서 할당 됩니다.

Azure 포털 hello 및 새로운 Azure 리소스 관리자 Api 지원 Azure RBAC를 hello만 합니다. 사용자와 응용 프로그램 RBAC 역할에 할당 된 hello 클래식 관리 포털 및 hello Azure 클래식 배포 모델을 사용할 수 없습니다.

## <a name="authorization-for-management-vs-data-operations"></a>관리를 위한 권한 부여와 데이터 작업 비교
Azure RBAC만의 관리 작업을 지원 합니다. hello에 Azure 리소스가 hello Azure 포털 및 Azure 리소스 관리자 Api입니다. Azure 리소스의 모든 데이터 수준 작업에 대한 권한을 부여할 수 있는 것은 아닙니다. 다른 사용자를 인증할 수는 예를 들어 되지만 저장소 계정 내의 테이블 및 blob이 아닌 toohello toomanage, 저장소 계정입니다. 마찬가지로, SQL 데이터베이스 관리할 수는 있지만 그 안에 테이블을 hello 하지 합니다.

## <a name="next-steps"></a>다음 단계
* 시작 [hello Azure 포털의에서 역할 기반 액세스 제어](role-based-access-control-configure.md)합니다.
* Hello 참조 [RBAC 기본 제공 역할](role-based-access-built-in-roles.md)
* [Azure RBAC에서 사용자 지정 역할](role-based-access-control-custom-roles.md)
