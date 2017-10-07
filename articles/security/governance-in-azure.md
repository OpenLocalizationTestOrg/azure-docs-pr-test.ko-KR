---
title: "Azure에서 aaaGovernance | Microsoft Docs"
description: "다양 한 종류의 계산 인스턴스를 포함 하는 클라우드 기반 컴퓨팅 서비스 및 응용 프로그램 또는 엔터프라이즈의 hello 요구 자동으로 toomeet 위쪽 및 아래쪽으로 확장 될 수 있는 서비스에 알아봅니다."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: TomSh
ms.openlocfilehash: 956e82e92f4232c24069bdb79fed5315f1d6486f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="governance-in-azure"></a>Azure에서 거버넌스

회원님의 보안은 hello 클라우드에서 작업 하나 고 Azure 보안에 대 한 정확 하 고 시기 적절 한 정보를 찾을 얼마나 중요 한지 됩니다. Hello 최상의 이유 toouse Azure 응용 프로그램 및 서비스에 대 한 중 하나 tootake 활용 하는 다양 한 보안 도구 및 기능입니다. 이러한 도구와 기능 hello 보안 Azure 플랫폼에서 가능한 toocreate 보안 솔루션을 확인할 수 있습니다.

toohelp 두 hello 고객의 Microsoft Azure 내에서 거 버 넌 스 컨트롤의 hello 배열 구현 및 hello에 대 한 포괄적인 개요를 제공 하는 Microsoft operations 큐브 뷰,이 문서에서는 "거 버 넌 스의 Azure" 쓰여집니다 더 잘 이해 Microsoft Azure와 함께 사용할 수 있는 거 버 넌 스 기능입니다.

## <a name="azure-platform"></a>Azure 플랫폼

Azure는 다양한 운영 체제, 프로그래밍 언어, 프레임워크, 도구, 데이터베이스 및 장치를 지원하는 공용 클라우드 서비스 플랫폼입니다. Docker 통합으로 Linux 컨테이너를 실행할 수 있습니다. JavaScript, Python, .NET, PHP, Java 및 Node.js를 사용하여 앱을 빌드할 수 있습니다. iOS, Android 및 Windows 장치용 백 엔드를 빌드할 수 있습니다. Azure 공용 클라우드 서비스는 hello 동일한 기술을 수백만 명의 개발자 및 IT 전문가가 이미에 의존 하 고 신뢰를 지원 합니다.

를, 작성 하거나 IT 자산을 마이그레이션할 때 해당 조직의 능력 tooprotect 응용 프로그램 및 데이터 hello 서비스 및 hello 컨트롤을 사용 하는 공용 클라우드 서비스 공급자 제공 toomanage hello 보안의 클라우드 기반 자산에 합니다.

동시에 수백만 개의 고객을 호스팅하기 위한 hello 시설 tooapplications에서 azure의 인프라를 디자인 하 고는 기업의 보안 요구 사항을 충족할 수 있는 신뢰할 수 있는 기초를 제공 합니다. 또한 Azure는 다양 한 보안 옵션 및 hello 기능 toocontrol 보안 toomeet hello 조직의 배포의 고유한 요구를 사용자 지정할 수 있도록 합니다.

이 문서는 Azure 거버넌스 기능이 이러한 요구 사항을 충족하는 방법을 이해하는 데 도움이 됩니다.

## <a name="abstract"></a>요약

Microsoft Azure 클라우드 거 버 넌 스는 통합된 감사 및 검토 하 고 확인 하 라는 hello Azure 플랫폼의 용도에 조직에 대 한 컨설팅 접근 방식을 제공 합니다. Microsoft Azure 클라우드 거 버 넌 스 말합니다 toohello 의사 결정 프로세스, 조건 및 관련 된 정책 hello 계획, 아키텍처, 취득, 배포, 운영 및 관리 하는 클라우드 컴퓨팅입니다.

Microsoft Azure 클라우드 거 버 넌 스에 대 한 계획 toocreate 해야 tootake hello 사람, 프로세스 및 위치에 현재 기술에 심층적 만들고 IT tooconsistently 쉽게 하는 빌드 프레임 워크 지원 끝을 제공 하면서 비즈니스 요구 사항 hello 유연성 toouse hello 강력한 기능으로 Microsoft Azure의 사용자입니다.

이 문서에서는 Microsoft Azure에서 IT 리소스의 상승된 거버넌스 수준을 얻을 수 있는 방법에 대해 설명합니다. 이 문서 tooMicrosoft Azure에에서 기본 제공 hello 보안 및 거 버 넌 스 기능을 이해 수 있습니다.

이 문서에서 설명 하는 주요 hello 거 버 넌 스 문제 hello 다음과가 같습니다.

- 조직 목표에 따른 정책, 프로세스 및 프로시저의 구현

- 보안 및 지속적인 조직 표준 규정 준수

- 경고 및 모니터링

## <a name="implementation-of-policies-processes-and-procedures"></a>정책, 프로세스 및 프로시저의 구현 

관리는 Azure 전체에서 역할 및 책임 toooversee hello 정보 보안 정책 및 구현 작업 연속성을 설정 했습니다. Microsoft Azure 관리는 각 팀(타사 포함) 내에 보안 및 연속성 사례를 감독하고 보안 정책, 프로세스 및 표준 규정 준수를 용이하게 해야 합니다.

다음은 발전 하 고 hello 요소입니다.

- 계정 프로비전

- 구독 제어

- 역할 기반 액세스 제어

- 리소스 관리

- 리소스 추적

- 중요한 리소스 제어

- API 액세스 tooBilling 정보

- 네트워킹 제어

## <a name="account-provisioning"></a>계정 프로비전

계정 계층은 주요 단계 toouse 및 구조는 회사 내에서 Azure 서비스 이며 hello 핵심 거 버 넌 스 구조를 정의 합니다. Hello 기업 계약을 사용 하는 고객의 경우 고객 hello 부서, 계정 및 구독을 마지막으로 환경을 다시 세분화할 수 있습니다.

![계정 프로비전](./media/governance-in-azure/security-governance-in-azure-fig1.png)

기업 계약이 없는 경우를 사용해 [Azure 태그](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) 구독 수준 toodefine 계층 구조에서. Azure 구독 리소스를 모두 포함 된 hello 기본 단위입니다. 코어 수, 리소스 등 Azure 내에서 여러 가지 한도도 정의합니다. 구독에는 [리소스 그룹](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)이 포함될 수 있고 리소스 그룹에는 리소스가 포함할 수 있습니다. [RBAC](https://docs.microsoft.com/azure/api-management/api-management-role-based-access-control) 원칙이 이러한 세 가지 수준에 적용됩니다.

모든 기업의 다른 이며 보다 유연 하 게 hello 회사 내에서 Azure는 구성 하는 방법에 대 한 엔터프라이즈가 아닌 고객의 경우 Azure 태그를 사용 하 여 hello 계층 구조를 허용 합니다. Microsoft Azure의에서 리소스를 배포 하기 전에 모델 계층 하 고 대금 청구, 리소스 액세스와 복잡성에 대 한 hello 영향을 이해 해야 합니다.

## <a name="subscription-controls"></a>구독 제어

구독은 리소스 사용량의 보고 및 청구 방식을 제어합니다. 구독은 별도의 청구 및 지불을 설정할 수 있습니다. 앞에서 언급한 대로 하나의 Azure 계정에 여러 구독이 있을 수 있습니다. 구독에 회사의 여러 부서의 사용된 toodetermine hello Azure 리소스 사용 될 수 있습니다.

예를 들어 회사에 IT, HR 및 마케팅 부서가 있는 경우 이러한 부서는 서로 다른 프로젝트를 실행합니다. 각 부서에서 가상 컴퓨터와 같은 Azure 리소스의 hello 용도에 따라, 있습니다 청구할 수 있는 적절 하 게 합니다. 이 각 부서의 hello finances 제어할 수 있습니다.

Azure 구독은 세 개의 매개 변수를 설정합니다.

- 고유한 구독자 ID

- 청구 위치

- 사용 가능한 리소스 집합

하나의 Microsoft 계정 ID를 포함 하는 개인에 대 한 신용 카드 번호와 hello 전체 패키지를 Azure 서비스-있지만 Microsoft는 hello 구독 유형에 따라 소비 제한을 적용 합니다.

Azure 등록 계층은 기업계약 내에 서비스 구성 방법을 정의합니다. hello Enterprise Portal toodivide tooAzure 리소스를 액세스는 유연한 계층 사용자 지정 가능한 tooan 조직의 고유한 요구에 따라 기업 계약과 연결 된 고객 수 있습니다. hello 대금 청구 관련 및 리소스 액세스에 대 한 정확 하 게 고려 될 수 있도록 조직의 관리 및 지리적 구조 hello 계층 패턴 일치 해야 합니다.

hello 3 높은 수준의 패턴은 기능, 비즈니스 단위 및 지리적를 사용 하 여 부서에 대 한 관리는 구문으로 계정 그룹화 합니다. 각 부서 내에서 계정은 할당된 구독일 수 있으며 Azure에서 몇 가지 주요 제한(예: VM 수, 저장소 계정) 및 청구에 대한 사일로를 만듭니다.

![구독 제어](./media/governance-in-azure/security-governance-in-azure-fig2.png)


기업계약이 있는 조직의 경우 Azure 구독은 4-수준 계층 구조를 수행합니다.

- 기업 등록계약 관리자

- 부서 관리자

- 계정 소유자

- 서비스 관리자

이 계층 구조 hello 다음을 제어 합니다.

- 청구 관계

- 계정 관리

- 역할 기반 액세스 제어 (RBAC) tooartifacts

- 경계/제한

- 경계

  - 사용량 및 청구(제품 번호 기준 요금 카드)

  - 제한

  - 가상 네트워크

- Too1 AAD 연결 (1 AAD와 연결할 구독 수)

- 연결 된 tooan 엔터프라이즈 등록 계정

## <a name="role-based-access-controls"></a>역할 기반 액세스 제어

액세스 제어 tooa 구독 된 기본 Azure 처음 릴리스 되었을 때: 관리자 또는 공동 관리자입니다. Tooa 구독 hello 포털 hello 기본 사용 권한에 포함 된 모델 액세스 tooall hello 리소스에 액세스 합니다. 세분화 된 제어가이 처럼 Azure 등록에 대 한 구독 tooprovide 적절 한 액세스 제어의 수준 toohello 확산 led.

![역할 기반 액세스 제어](./media/governance-in-azure/security-governance-in-azure-fig3.png)

이제 더 이상 구독 수를 늘리지 않아도 됩니다. 역할 기반 액세스 제어를 사용한 toostandard 역할 (예: 일반적인 "reader" 및 "writer" 유형의 역할) 사용자에 게 할당할 수 있습니다. 사용자 지정 역할을 정의할 수도 있습니다.

[Azure RBAC(역할 기반 액세스 제어)](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles)를 통해 Azure에 대한 세밀한 액세스 관리가 가능합니다. RBAC를 사용 하 여 권한을 부여할 수 있습니다만 hello 제한 된 액세스 사용자를에 tooperform 업무를 필요 합니다. 보안 지향적인 회사 직원에 게 필요한 hello 정확 하 게 사용 권한이 부여에 초점을 맞추어야 합니다. 너무 많은 권한을 계정 tooattackers를 노출합니다. 권한이 너무 적으면 직원이 업무를 효율적으로 수행할 수 없습니다. Azure RBAC(역할 기반 액세스 제어)는 Azure에 대한 세밀한 액세스 관리를 제공하여 이 문제를 해결하도록 도와줍니다. RBAC를 사용 하면 팀 및 권한 부여만 hello 시간 내에 필요 하다는 tooperform 업무 액세스 toousers toosegregate 의무 수 있습니다. Azure 구독 또는 리소스에서 모든 사람에게 무제한 권한을 제공하는 대신 특정 작업만 허용할 수 있습니다.

예를 들어 구독에서 가상 컴퓨터를 관리 하는 사용 하 여 RBAC toolet 직원이 한 명, 다른를 관리할 수 있는 반면 SQL 데이터베이스 hello 내에서 동일한 구독 합니다.

Azure RBAC tooall 리소스 유형에 적용 되는 세 가지 기본 역할에 있습니다.

- **소유자** 에 대 한 모든 권한을 tooall 리소스가 hello 오른쪽 toodelegate 액세스 tooothers를 포함 합니다.

- **참가자** 수 만들고 모든 유형의 Azure 리소스를 관리할 수 있지만 tooothers 액세스 권한을 부여할 수 없습니다.

- **읽기 권한자** 는 기존 Azure 리소스를 볼 수 있습니다.

Azure의 hello RBAC 역할 hello 나머지 특정 Azure 리소스 관리를 허용 합니다. 예를 들어 hello 가상 컴퓨터 참가자 역할 hello 사용자 toocreate 허용 하 고 가상 컴퓨터를 관리 합니다. 제공 되지 않습니다 해당 액세스 toohello 가상 네트워크 또는 가상 컴퓨터를 hello hello 서브넷에 연결 합니다.

[기본 제공 역할 RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) 목록 hello Azure에서 사용할 수 있는 역할입니다. Hello 작업과 toousers 각 기본 제공 역할에 부여 하는 범위를 지정 합니다.

적절 한 RBAC 역할 toousers hello, 그룹 및 특정 범위의 응용 프로그램을 할당 하 여 액세스를 부여 합니다. 역할 할당의 hello 범위는 구독, 리소스 그룹 또는 단일 리소스 될 수 있습니다. 부모 범위에서 지정 된 역할이 부여 액세스 toohello 자식에 포함 합니다.

예를 들어 액세스 tooa 리소스 그룹에 있는 사용자에 포함 된 웹 사이트, 가상 컴퓨터 및 서브넷와 같은 모든 hello 리소스를 관리할 수 있습니다.

Azure RBAC만의 관리 작업을 지원 합니다. hello에 Azure 리소스가 hello Azure 포털 및 Azure 리소스 관리자 Api입니다. Azure 리소스의 모든 데이터 수준 작업에 대한 권한을 부여할 수 있는 것은 아닙니다. 예를 들어 toomanage 저장소 계정이 있지만 하지 toohello blob 또는 저장소 계정 내의 테이블 수 없습니다. 다른 사용자 권한을 부여할 수 있습니다. 마찬가지로, SQL 데이터베이스 관리할 수는 있지만 그 안에 테이블을 hello 하지 합니다.

RBAC를 사용하여 액세스를 관리하는 방법에 대한 자세한 정보를 원하는 경우 [역할 기반 액세스 제어란](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)을 참조하세요.

수도 있습니다 [사용자 지정 역할](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles) 신속히 알아봅니다 액세스 제어 (RBAC)에서 특정 액세스 맞는 구성이 없는 hello 기본 제공 역할의 경우 필요 합니다. 사용 하 여 사용자 지정 역할을 만들 수 [Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell), [Azure 명령줄 인터페이스 (CLI)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-azure-cli), 및 hello [REST API](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-rest)합니다. 기본 제공 역할 마찬가지로 toousers, 그룹 및 구독, 리소스 그룹 및 리소스 범위에서 응용 프로그램의 사용자 지정 역할을 할당할 수 있습니다.

각 구독 내에서 too2000 역할 할당을 부여할 수 있습니다.

## <a name="resource-management"></a>리소스 관리

Azure는 원래만 hello 클래식 배포 모델을 제공 합니다. 이 모델에서는 각 리소스 존재 하지 독립적으로; 방법이 함께 toogroup 관련 리소스입니다. 솔루션 또는 응용 프로그램을 구성 하는 리소스를 추적 하 고 기억 toomanage toomanually 사용 했던 대신는 조정 된 방식으로 해당 합니다.

솔루션 toodeploy tooeither hello 클래식 포털을 통해 개별적으로 각 리소스를 만들거나 hello 올바른 순서로 모든 hello 리소스를 배포 하는 스크립트를 만들 했습니다. 솔루션 toodelete 했습니다 toodelete 각 리소스 개별적으로. 관련 리소스에 대한 액세스 제어 정책을 쉽게 적용 및 업데이트할 수 없었습니다. 마지막으로 리소스를 모니터링 하 고 대금 청구를 관리 하는 데 도움이 되는 용어를 사용 하 여 태그 tooresources toolabel을 적용 하지 못했습니다.

2014 년 Azure 리소스 그룹의 hello 개념 추가 리소스 관리자를 도입 했습니다. 리소스 그룹은 공통 수명 주기를 공유하는 리소스의 컨테이너입니다. hello 리소스 관리자 배포 모델에는 여러 가지 이점을 제공합니다.

- 배포, 관리 하 고 이러한 서비스를 개별적으로 처리 하지 않고 그룹에서 솔루션에 대 한 모든 hello 서비스를 모니터링할 수 있습니다.

- 수명 주기 내내 솔루션을 반복적으로 배포하며 안심하고 일관된 상태로 리소스를 배포할 수 있습니다.

- 리소스 그룹에 대 한 액세스 제어 tooall 리소스를 적용할 수 있습니다 및 새 리소스를 추가 toohello 리소스 그룹에 자동으로 해당 정책이 적용 됩니다.

- 태그를 적용할 수 tooresources toologically 구독에서 모든 hello 리소스를 구성 합니다.

- 솔루션에 대 한 개체 JSON (JavaScript Notation) toodefine hello 인프라를 사용할 수 있습니다. hello JSON 파일 리소스 관리자 템플릿을 라고 합니다.

- Hello 올바른 순서로 배포 되므로 리소스 간의 종속성을 hello를 정의할 수 있습니다.

![리소스 관리](./media/governance-in-azure/security-governance-in-azure-fig4.png)

리소스 관리자에 사용할 수 있게 하면 tooput 리소스 관리, 청구, 또는 자연 선호도 대 한 의미 있는 그룹입니다. 앞서 설명했듯이, Azure에는 두 가지 배포 모델이 있습니다. 이전 hello에 [클래식 모델](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model), 관리의 기본 단위 hello hello 구독 했습니다. 많은 구독 toohello 만들기를 초래한 구독 내에서 리소스 아래로 어려운 toobreak 있었습니다. Hello 리소스 관리자, 모델로 hello 소개를 리소스 그룹에 대해 살펴보았습니다.

리소스 그룹은 Azure 솔루션에 관련된 리소스를 보유하는 컨테이너입니다. [리소스 그룹 hello](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) hello 솔루션에 대 한 모든 hello 리소스 또는 그룹으로 toomanage 되도록 하는 리소스에만 포함할 수 있습니다. 원하는 tooallocate 리소스를 결정 하는 요소 hello 조직에 가장 적합 한 기반으로 tooresource 그룹입니다.

템플릿에 대한 권장 사항은 [Azure Resource Manager 템플릿 생성 모범 사례](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)를 참조하세요.

Azure 리소스 관리자는 hello 올바른 순서로 tooensure 리소스가 생성 되는 종속성을 분석 합니다. 한 리소스가 다른 리소스(예: 디스크에 대한 저장소 계정을 필요로 하는 가상 컴퓨터)의 값에 의존하는 경우 종속성을 설정합니다.

>[!Note]
>자세한 정보는 [Azure 리소스 관리자 템플릿에서 종속성 정의](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-define-dependencies)를 참조하세요.

또한 업데이트 toohello 인프라에 대 한 hello 서식 파일을 사용할 수 있습니다. 예를 들어 리소스 tooyour 솔루션을 추가한 이미 배포 된 hello 리소스에 대 한 구성 규칙을 추가 합니다. Hello 템플릿 지정 리소스가 이미 존재 하지만 해당 리소스를 만드는 Azure 리소스 관리자 새 자산을 만드는 대신 한 업데이트를 수행 합니다. Azure 리소스 관리자 업데이트 hello 기존 자산 toohello 동일 하므로 상태 새 것입니다.

리소스 관리자는 hello 설치에 포함 되지 않은 소프트웨어를 설치 하는 등의 추가 작업을 할 때 시나리오에 대 한 확장을 제공 합니다.

## <a name="resource-tracking"></a>리소스 추적

조직의 사용자가 리소스 toohello 구독을 추가한 hello 적절 한 부서, 고객 및 환경을 사용 하 여 점점 더 중요 해 tooassociate 리소스 됩니다. 메타 데이터 tooresources 태그를 통해 연결할 수 있습니다. 사용 하면 [태그](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) hello 리소스 또는 hello 소유자에 대 한 tooprovide 정보입니다. 태그는 toonot만 집계 및 여러 가지 방법으로 리소스 그룹을 사용 하면 하지만 비용 정산의 hello 목적을 위해 해당 데이터를 사용 합니다.

태그를 사용 하 여 리소스 그룹 및 리소스의 복잡 한 컬렉션 하는 경우 대부분 의미 tooyou hello에 수행 하는 hello 방식으로 이러한 자산 toovisualize 필요 합니다. 조직에서 비슷한 역할을 제공 하거나 toohello 속해 있는 리소스 태그 수는 예를 들어 같은 동일 부서입니다.

태그를 조직의 사용자가 만들 수 없는 toolater 어려울 수 있는 여러 리소스를 식별 하 고 관리 합니다. 예를 들어 프로젝트에 대 한 모든 hello 리소스 toodelete를 지정할 수 있습니다. 이러한 리소스는 hello 프로젝트에 대 한 태그가 지정 되지를 하는 경우 수동으로 찾을 해야 있습니다. 태그를 지정 하면 구독에 tooreduce 불필요 한 비용에 대 한는 가장 좋은 방법은 수 있습니다.

리소스 hello에 tooreside 불필요 동일한 리소스 그룹 tooshare 태그입니다. 사용자 고유의 태그 분류 tooensure 조직의 모든 사용자가 대신 사용 하도록 일반 태그 약간 다른 태그 (예: "dept" 대신 "department")가 실수로 적용 하는 사용자가 만들 수 있습니다.

리소스 정책을 사용 하면 조직에 대 한 표준 규칙 toocreate 있습니다. 리소스 hello 적절 한 값으로 태그가 지정 되어 있는지 확인 하는 정책을 만들 수 있습니다.

> [!Note]
> 자세한 내용은 [태그에 대한 리소스 정책 적용](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags)을 참조하세요.

Hello Azure 포털을 통해 태그가 지정 된 리소스를 볼 수 있습니다.

hello [사용 현황 보고서](https://docs.microsoft.com/azure/billing/billing-understand-your-bill) 구독에 포함 되어 태그 이름 및 값을 나타냄 toobreak 비용으로 사용할 수 있는 대 한 합니다.

> [!Note]
> 태그에 대 한 자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)합니다.

다음과 같은 제한을 hello tootags를 적용 됩니다.

- 각 리소스 또는 리소스 그룹에는 최대 15개의 태그 키/값 쌍이 포함될 수 있습니다. 이 제한은 직접 적용 tootags toohello 리소스 그룹 또는 리소스에만 적용 됩니다. 리소스 그룹은 각각 15개의 태그 키/값 쌍이 있는 여러 리소스를 포함할 수 있습니다.

- hello 태그 이름에는 제한 된 too512 자입니다.

- hello 태그 값은 제한 된 too256 문자입니다.

- 적용 된 태그 toohello 리소스 그룹으로 해당 리소스 그룹에 리소스를 hello 상속 되지 않습니다.

리소스와 tooassociate 해야 하는 15 개 이상의 값이 있으면 hello 태그 값에 대 한 JSON 문자열을 사용 합니다. JSON 문자열 hello 적용된 tooa 단일 태그를 통해 많은 값을 포함할 수 있습니다.

### <a name="tags-and-billing"></a>태그 및 청구

태그는 청구 데이터에 toogroup 있습니다를 사용 합니다. 예를 들어 서로 다른 조직에 대 한 여러 Vm을 실행 하는 경우 hello 태그 toogroup 사용 비용 센터를 사용 합니다. 런타임 환경;에 의해 태그 toocategorize 비용을 사용할 수도 있습니다. 프로덕션 환경에서 실행 중인 Vm에 대 한 청구 사용량을 hello와 같은 합니다.

Hello 통해 태그에 대 한 정보를 검색할 수 [Azure 리소스 사용량 및 RateCard Api](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview) 또는 hello 사용 현황 쉼표로 구분 된 값 (CSV) 파일입니다. Hello에서 hello 사용량 파일을 다운로드 [Azure 계정 포털](https://account.windowsazure.com/) 또는 [EA 포털](https://ea.azure.com/)합니다.

>[!Note]
> 프로그래밍 방식 액세스 toobilling 정보에 대 한 자세한 내용은 참조 [Microsoft Azure 리소스 소비량에 대 한 이해력](https://docs.microsoft.com/azure/billing/billing-usage-rate-card-overview)합니다. REST API 작업에 대한 내용은 [Azure 청구 REST API 참조](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)를 참조하세요.

결제 태그를 지원 서비스에 대 한 hello 사용 CSV를 다운로드 하면 hello 태그 hello 태그 열에 나타납니다.

## <a name="critical-resource-controls"></a>중요한 리소스 제어

Core 서비스 toohello 구독에 추가 하는 조직에 이러한 서비스에 사용할 수 있는 tooavoid 비즈니스 중단도 점점 더 중요 해 tooensure 됩니다. [리소스 잠금을](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-lock-resources) 수정 하거나 삭제 응용 프로그램 또는 클라우드 인프라에 상당한 영향을 미칠 것 여기서 중요 리소스에 toorestrict 작업을 활성화 합니다. 잠금 tooa 구독, 리소스 그룹 또는 리소스를 적용할 수 있습니다. 일반적으로 가상 네트워크, 게이트웨이 및 저장소 계정 등의 잠금 toofoundational 리소스를 적용 합니다.

리소스 잠금은 현재 두 가지 값(CanNotDelete 및 ReadOnly)을 지원합니다. 로그인 한 사용자 (hello 적절 한) 할 수 있다는 CanNotDelete 읽을 또는 리소스 수정 있지만 삭제할 수 없습니다. ReadOnly는 권한이 있는 사용자가 리소스를 삭제 또는 수정할 수 없음을 의미합니다.

리소스 관리자 잠금을 적용 너무 전송 작업으로 구성 되는 hello 관리 평면에서 발생 하는 toooperations만<https://management.azure.com>. hello 잠금 리소스에서 자신의 기능을 수행 하는 방법을 제한 하지 않습니다. 리소스 변경은 제한되지만 리소스 작업은 제한되지 않습니다. 예를 들어 SQL 데이터베이스에 대 한 읽기 전용 잠금을 못하도록 삭제 하거나 수정 하지만 hello 데이터베이스 때도 만들기, 업데이트 또는 hello 데이터베이스의에서 데이터를 삭제할 수 있습니다.

적용 **ReadOnly** 처럼 보일 수도 있지만 일부 작업 읽기 작업에 추가 작업 필요 하기 때문에 toounexpected 결과가 발생할 수 있습니다. 예를 들어 배치는 **ReadOnly** 저장소 계정에 대 한 잠금을 나열 hello 키의 모든 사용자가 방지 합니다. 키 작업 hello 키에 사용할 수 있는 반환 했기 때문에 POST 요청을 통해 처리 hello 목록 쓰기 작업입니다.

![중요한 리소스 제어](./media/governance-in-azure/security-governance-in-azure-fig5.png)

또 다른 예에 대 한 상호 작용을 지 쓰기 권한이 필요 하기 때문에 hello 리소스에 대 한 파일을 표시에서 Visual Studio 서버 탐색기 방지 앱 서비스 리소스에 대 한 읽기 전용 잠금을 배치 합니다.

역할 기반 액세스 제어와 달리 모든 사용자 및 역할에서 관리 잠금 tooapply 제한을 사용합니다. 사용자 및 역할에 대 한 사용 권한을 설정 하는 방법에 대 한 toolearn 참조 [Azure 역할 기반 액세스 제어](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)합니다.

부모 범위에서 잠금을 적용 하면 해당 범위 내에서 모든 리소스 상속 hello 동일한 잠금. Hello 잠금 hello 부모에서 상속 하는 리소스도 나중에 추가 합니다. hello hello 상속에 가장 제한적인 잠금 우선 적용 됩니다.

관리 잠금 toocreate 또는 delete 있어야 액세스 tooMicrosoft.Authorization/ _또는 Microsoft.Authorization/locks/_ 동작 합니다. Hello 기본 제공 역할 중만 **소유자** 및 **사용자 액세스 관리자에 게** 이러한 작업을 부여 됩니다.

## <a name="api-access-toobilling-information"></a>API 액세스 toobilling 정보

Azure 청구 Api toopull 사용 및 리소스 데이터를 사용 하 여 기본 설정된 된 데이터 분석 도구입니다. hello Azure 리소스 사용량 및 RateCard Api 유용 정확 하 게 예상 하 고 비용을 관리 합니다. 리소스 공급자와 hello 제품군 hello Azure 리소스 관리자에 의해 노출 되는 Api의 일부 hello Api 구현 됩니다.

### <a name="azure-resource-usage-api-preview"></a>Azure 리소스 사용량 API(미리 보기)

사용 하 여 hello Azure [리소스 사용량 API](https://msdn.microsoft.com/library/azure/mt219003) tooget 예상된 Azure 사용량 데이터입니다. hello API에는 다음이 포함 됩니다.

- **Azure 역할 기반 액세스 제어** -액세스 구성 hello에 정책을 [Azure 포털](https://portal.azure.com/) 또는 [Azure PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/overview) toospecify 있는 사용자 또는 응용 프로그램 액세스 권한을 얻을 수 toohello 구독 사용 현황 데이터입니다. 호출자가 인증에 대한 표준 Azure Active Directory 토큰을 사용해야 합니다. Hello 호출자 tooeither hello 판독기 대금 청구, 판독기, 소유자 또는 참가자 역할 tooget 액세스 toohello 사용 현황 데이터는 특정 Azure 구독에 대 한 추가 합니다.

- **매시간 또는 매일 집계** -호출자는 Azure 사용 데이터를 매시간 버킷 또는 매일 버킷으로 할지 지정할 수 있습니다. hello 기본값은 매일입니다.

- **(리소스 태그가 포함)의 인스턴스 메타 데이터** – 정규화 된 리소스 uri hello와 같은 인스턴스 수준의 세부 사항을 가져옵니다 (/subscriptions/ {구독 id} /..), 리소스 그룹 정보 및 리소스 태그 hello 합니다. 이 메타 데이터를 사용 하면 명확 하 게 하 고 프로그래밍 방식으로 hello 태그로 간 충전 같은 사용 사례에 대 한 사용을 할당 합니다.

- **리소스 메타 데이터** -hello 미터 이름, 측정기 범주, 측정기 하위 범주, 단위, 지역 등 리소스 정보를 사용 된 작업의 hello 호출자에 게 제공 합니다. 또한 tooalign 리소스 메타 데이터 용어 hello Azure 포털, Azure 사용량 CSV, EA CSV, 청구 및 기타 공용 환경, 환경에서 데이터를 상관 성을 toolet 걸친 협력 합니다.

- **모든 사용 유형에 대한 사용** – 종량제, MSDN, 약정 금액, 금액 크레딧 및 EA와 같은 모든 사용 유형에 대한 사용 데이터가 제공됩니다.

**Azure 리소스 RateCard API(미리 보기)**

사용 하 여 hello Azure 리소스 RateCard API tooget hello 사용 가능한 Azure 리소스 목록 및 예상 가격 각각에 대 한 정보입니다. hello API에는 다음이 포함 됩니다.

- **Azure 역할 기반 액세스 제어** -hello Azure 포털에서 액세스 정책을 구성 하거나 사용자 또는 응용 프로그램이 액세스할 수 있는 Azure PowerShell cmdlet toospecify 통해 toohello RateCard 데이터에 액세스 합니다. 호출자가 인증에 대한 표준 Azure Active Directory 토큰을 사용해야 합니다. Hello 호출자 tooeither hello 판독기, 소유자 또는 참가자 역할 tooget 액세스 toohello 사용 현황 데이터는 특정 Azure 구독에 대 한 추가 합니다.

- **종량제, MSDN, 금액 약정 및 금액 크레딧 제공(EA은 지원되지 않음)** - 이 API는 Azure 제공 수준 환율 정보를 제공합니다. 이 API의 hello 호출자 hello 제공 tooget 리소스 세부 정보 및 속도 전달 해야 합니다. 여러분 EA 제안 등록 당 속도 사용자 지정한 때문에 현재 없습니다 tooprovide EA 세요. 다음은 몇 가지 가능한 hello 사용량 및 RateCard Api hello hello 조합 하 여 적용 된 hello 시나리오입니다.

- **Hello (월) 동안 azure 지출** -hello 사용량 및 RateCard Api tooget 통찰력에 클라우드로의 hello 조합을 사용 하 여 hello (월) 동안 소비 합니다. 일별 사용 현황 및 요금 청구 버킷 예상 및 매시간 hello를 분석할 수 있습니다.

- **경고를 설정** – hello 사용을 사용 하 고 hello RateCard Api tooget 클라우드 사용 및 요금, 예상 리소스 또는 통화 기반 경고를 설정 합니다.

- **청구서 예측** – Get 예상된 소비와 클라우드를 보내며 기계 학습 알고리즘 toopredict 어떤 hello bill 청구 주기 hello hello 끝에 있는 것을 적용 합니다.

- **사전 소비 비용 분석** – hello RateCard API toopredict 작업 tooAzure 이동할 때 예상 되는 용도 대 한 청구 금액이 것을 사용 합니다. 기존 작업에서 다른 클라우드 또는 사설 클라우드를 설정한 경우 Azure의 보다 정확한 예상치 지출 hello Azure 속도 tooget와 사용량을 매핑할 수도 있습니다. 이 예상 값을 제공 제안에는 기능 toopivot hello 종 량 제, 초과 hello 각 제안 유형에 간의 비교는 현금 약정 및 화폐 성 차변을 같은입니다. 또한 제공 hello API hello 기능 toosee 비용 차이 지역별 및 toodo 배포 결정을 내린 가상 비용 분석 toohelp 있습니다.

- **가상 분석** -다른 지역의 또는 hello Azure 리소스의 다른 구성에 더 많은 비용 효율적인 toorun 작업 인지를 확인할 수 있습니다. 사용 중인 Azure 지역 hello에 기반 azure 리소스 비용 다를 수 있습니다.

- 다른 Azure 제품 유형에서 Azure 리소스에 더 나은 속도를 제공하는지 결정할 수도 있습니다.

## <a name="networking-controls"></a>네트워킹 제어

내부 (내 hello 회사의 네트워크) 또는 외부 액세스 tooresources 될 수 있습니다 (을 통해 인터넷 hello). 사용자가 조직 tooinadvertently put 리소스 hello 잘못 된 위치에 사용 되며 잠재적 열지 toomalicious 액세스 합니다. 온-프레미스와 마찬가지로 / 장치, 기업에서는 Azure 사용자 hello 올바른 결정을 확인 하는 적절 한 컨트롤 tooensure를 추가 해야 합니다.

![네트워킹 제어](./media/governance-in-azure/security-governance-in-azure-fig6.png)

구독 관리를 위해 기본적인 액세스 제어를 제공하는 핵심 리소스를 식별합니다. hello 코어 리소스는 다음으로 구성 됩니다.

### <a name="network-connectivity"></a>네트워크 연결

[가상 네트워크](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)는 서브넷에 대한 컨테이너 개체입니다. 경우에 반드시 필요 하지 응용 프로그램 toointernal 회사 리소스에 연결할 때 주로 사용 됩니다. 안녕 toosecurely 하면 가상 네트워크 (Vnet)를 사용 하 여 다른 Azure 리소스 tooeach를 연결 하는 Azure 가상 네트워크 서비스 수 있습니다.

VNet은 hello 클라우드에서 사용자의 네트워크의 표현입니다. VNet의 hello Azure 클라우드 전용 tooyour 구독 논리적 격리입니다. 또한 Vnet tooyour 온-프레미스 네트워크를 연결할 수 있습니다.

다음은 Azure Virtual Networks의 기능입니다.

- **격리**: VNet은 서로 완전히 격리됩니다. 사용 하 여 hello 개발, 테스트 및 프로덕션에 대 한 별도 Vnet에 만들 수 같은 CIDR 주소 블록입니다. 반대로, 여러 CIDR 주소 블록을 사용하는 VNet을 만들어 네트워크를 서로 연결할 수도 있습니다. VNet은 여러 서브넷으로 분할할 수 있습니다. 클라우드 서비스 역할 인스턴스 tooa VNet 연결 및 azure Vm에 대 한 내부 이름 확인을 제공 합니다. 필요에 따라 VNet toouse Azure 내부 이름 확인을 사용 하는 대신 고유한 DNS 서버를 구성할 수 있습니다.

- **인터넷 연결**: 연결 된 VNet tooa 있어야 하는 모든 Azure 가상 컴퓨터 (VM) 및 클라우드 서비스 역할 인스턴스 기본적으로 toohello 인터넷에 액세스 합니다. 필요에 따라 toospecific 리소스에 인바운드 액세스를 설정할 수도 있습니다.

- **Azure 리소스 연결**: 클라우드 서비스 및 Vm와 같은 Azure 리소스에 연결 된 toohello 수 동일한 VNet입니다. hello 리소스 다른 tooeach 연결할 수 있는 개인 IP를 사용 하 여 주소, 서브넷이 서로 다른 경우에 합니다. Azure 없습니다 tooconfigure 하 고 경로 관리 하므로 기본 서브넷, Vnet 및 온-프레미스 네트워크 간의 라우팅을 제공 합니다.

- **VNet 연결**: Vnet에는 다른 연결 된 tooeach 수 있으며, tooany VNet toocommunicate 다른 VNet에 리소스와 연결 된 리소스를 사용 하도록 설정 합니다.

- **온-프레미스 연결**: Vnet hello 인터넷을 통해 네트워크와 Azure 간의 개인 네트워크 연결을 통해 또는 사이트 간 VPN 연결을 통해 네트워크에 연결 된 tooon 온-프레미스 네트워크를 수 있습니다.

- **트래픽 필터링**: VM 및 Cloud Services 역할 인스턴스 네트워크 트래픽을 원본 IP 주소 및 포트, 대상 IP 주소 및 포트 및 프로토콜별로 인바운드 및 아웃바운드에 따라 필터링할 수 있습니다.

- **라우팅**: 자체 경로를 구성하여 또는 네트워크 게이트웨이를 통해 BGP 경로를 사용하여 Azure의 기본 라우팅을 선택적으로 재정의할 수 있습니다.

## <a name="network-access-controls"></a>네트워크 액세스 컨트롤

[네트워크 보안 그룹](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) hello 네트워크를 통해 어떻게 리소스 수와 "통신"에 대 한 규칙을 제공 하는 방화벽 같은 합니다. 서브넷 (또는 가상 컴퓨터) toohello 인터넷 또는 다른 서브넷에 연결할 수 있는 경우 동일한 hello / 방법 보다 세부적으로 제어를 제공 합니다. 이러한 가상 네트워크입니다.

네트워크 보안 그룹 NSG ()를 허용 하거나 거부할 네트워크 트래픽 tooresources tooAzure 가상 네트워크 (VNet) 연결 하는 보안 규칙 목록이 포함 되어 있습니다. 개별 네트워크 인터페이스 (NIC) 연결 tooVMs (리소스 관리자) 또는 Nsg 연결된 toosubnets, 개별 Vm (클래식)를 수 있습니다.

NSG 연결된 tooa 서브넷 이면 tooall 리소스 연결 된 toohello 서브넷 hello 규칙에 적용 됩니다. 또한 VM 또는 NIC.는 NSG tooa를 연결 하 여 트래픽을 추가로 제한할 수

## <a name="security-and-continuous-compliance-with-organizational-standards"></a>보안 및 지속적인 조직 표준 준수

비즈니스마다 요구 사항이 다르며 모든 비즈니스는 클라우드 솔루션에서 차별화된 이점을 누립니다. 모든 종류의 고객에 아직 hello toohello 클라우드를 이동 하는 방법에 대 한 기본도 별 염려가 됩니다. 투명도 호환성을 유지 하면서 모든 보안 및 개인을 유지 하는 해당 데이터 toobe 원하는 및 데이터를 tooretain 제어 하려고 합니다.

고객이 클라우드 공급자에게 바라는 점은 다음과 같습니다.

- **데이터 보호** 데이터 보안 및 관리 제어의 증가 hello 클라우드 제공할 수 있는지를 승인, IT 리더 여전히 관련이 있는지 마이그레이션 toohello 클라우드는 그대로 현재의 보다 더 취약 toohackers 자체 솔루션입니다.

- **데이터 보관** 사설 클라우드 서비스는 비즈니스에 고유한 개인정보보호 문제를 발생시킵니다. 회사 toohello 클라우드 toosave 인프라 비용 표시 되 고의 유연성 향상을 손실 데이터가 저장 된, 사용자에 액세스 하는, 및 사용 되는 방법을 제어 하는 방법에 대 한도 중요 합니다.

- **컨트롤을 제공** 은 hello 클라우드 toodeploy 자세한 혁신적인 솔루션을 활용 하는 대로도 회사 매우에 대해 염려 제어 데이터의 손실입니다. 법률 및 3 차 법적 수단을 통해 고객 데이터에 액세스 하려는 정부 기관의 hello 최근 공개 확인 일부 Cio hello 클라우드에 데이터를 저장할 때는 주의 합니다.

- **투명도 수준 올리기** hello 기능 보안, 개인 정보 및 컨트롤은 중요 한 toobusiness 의사 결정자, 또한 합니다 tooindependently 어떻게 자신의 저장 되는 데이터를 액세스, 되며 보안을 확인 합니다.

- **규정 준수를 유지 관리** 회사의 클라우드 기술 용도 확장, 표준 및 규정의 hello 복잡성과 범위 tooevolve를 계속 합니다. 회사 규정 준수 표준을 충족 되 고 시간에 따라 규정 변경으로 해당 규정 준수 점점 발전 하 tooknow가 필요 합니다.

## <a name="security-configuration-monitoring-and-alerting"></a>보안 구성, 모니터링 및 경고

Azure 구독자는 관리 워크스테이션, 개발자 PC, 심지어 작업별 사용 권한을 가진 최종 사용자 장치 등 여러 장치에서 자신의 클라우드 환경을 관리할 수 있습니다. 경우에 따라 관리 기능 등 hello Azure 포털-웹 기반 콘솔을 통해 수행 됩니다. 다른 경우, 가상 사설망 (Vpn), 터미널 서비스, 클라이언트 응용 프로그램 프로토콜, 또는 (프로그래밍 방식) hello Azure 서비스 관리 API SMAPI ()를 통해 온-프레미스 시스템에서 직접 연결 tooAzure 수 있습니다. 또한 클라이언트 끝점은 태블릿이나 스마트폰 같이 조인 또는 격리되고 관리되지 않는 도메인이 될 수 있습니다.

액세스 및 관리 기능을 여러 다양 한 옵션을 제공 하지만이 가변성 상당한 위험 tooa 클라우드 배포를 추가할 수 있습니다. 것이 어려운 toomanage 추적 및 관리 작업을 감사 합니다. 이 가변성 클라우드 서비스 관리에 사용 되는 비조절형된 액세스 tooclient 끝점을 통해 보안 위협 사용할 수 있습니다. 인프라를 개발 및 관리하기 위한 일반 또는 개인 워크스테이션을 사용 하면 웹 검색(예: 워터링 홀 공격) 또는 전자 메일(예: 소셜 엔지니어링 및 피싱 공격)와 같이 예측할 수 없는 위협 벡터를 열게 됩니다.

모니터링, 로깅 및 감사 추적 및 관리 작업을 이해 하는 것에 대 한 기초를 제공 하지만에서 작업을 모두 완료 인해 생성 된 데이터 양 toohello 세부 불가능 tooaudit 항상 아닐 수 있습니다. 그러나 Hello 관리 정책의 hello 효율성을 감사는는 것이 좋습니다.

AD DS Gpo toocontrol에서 azure 보안 거 버 넌 스 모든 hello 관리자의 Windows 인터페이스를 파일 공유와 같은 합니다. 감사, 모니터링 및 로깅 프로세스에 관리 워크스테이션을 포함합니다. 모든 관리자 및 개발자 액세스 및 사용을 추적합니다.

### <a name="azure-security-center"></a>Azure Security Center

hello [Azure 보안 센터](https://docs.microsoft.com/azure/security-center/security-center-intro) 중앙 hello 구독에서 리소스의 hello 보안 상태 보기를 제공 하 고 손상 된 리소스를 방지 하는 데 도움이 되는 권장 사항을 제공 합니다. 보다 세부적인 정책 (예를 들어 적용 정책 toospecific 리소스 그룹을 실현 하 상태 toohello 위험 hello 엔터프라이즈 tootailor 허용)를 허용 합니다.

![Azure 보안 센터](./media/governance-in-azure/security-governance-in-azure-fig7.png)

Security Center는 Azure 구독을 통해 통합된 보안 모니터링 및 정책 관리를 제공하고, 달리 발견되지 않을 수도 있는 위협을 검색하는 데 도움이 되며, 보안 솔루션의 광범위한 에코시스템에서 작동합니다. 사용 하도록 설정한 후 [보안 정책](https://docs.microsoft.com/azure/security-center/security-center-policies) 구독의 리소스에 대 한 보안 센터를 hello 보안 리소스 tooidentify 잠재적인 취약점을 분석 합니다. 네트워크 구성 정보는 즉시 이용할 수 있지만,

Azure Security Center는 Azure 구독 내에 모든 리소스에 대한 모범 사례 분석 및 보안 정책 관리의 조합을 나타냅니다. 이 강력 하 고 쉽게 toouse 도구 보안 팀을 사용 하 고 위험 임원 tooprevent을 감지 하 고 자동으로 수집 하 고 Azure 리소스, hello 네트워크와 같은 파트너 솔루션의 보안 데이터를 분석 하 여 toosecurity 위협 응답 맬웨어 방지 프로그램, 방화벽 합니다.

또한 Azure 보안 센터 Microsoft 제품 및 서비스를 Microsoft Digital Crimes 단위 (DCU), hello hello Microsoft에서에서 전역 위협 인텔리전스를 활용 하면서 기계 학습 및 동작 분석을 포함 하는 고급 분석을 적용 보안 대응 센터 (MSRC) 및 외부 피드입니다. [보안 거 버 넌 스](https://www.credera.com/blog/credera-site/azure-governance-part-4-other-tools-in-the-toolbox/) toospecific, 세분화 된 요구 사항 적용 tooindividual 정책 정의 통해 리소스 축소 또는 hello 구독 수준에서 광범위 하 게 적용할 수 있습니다.

마지막으로, Azure 보안 센터 해당 정책에 따라 리소스 보안 상태를 분석 하 고이 tooprovide 통찰력 대시보드 및 시도 예: 맬웨어 검색 또는 악성 IP 연결 이벤트에 대 한 경고를 사용 합니다.

>[!Note]
> 방법에 대 한 자세한 내용은 tooapply 권장 사항, 읽을 [Azure 보안 센터에서 보안 권장 사항 구현](https://docs.microsoft.com/azure/security-center/security-center-recommendations)합니다.

보안 센터에서에서 데이터를 수집한 가상 컴퓨터 tooassess 자신의 보안 상태, 보안 권장 사항을 제공 하 고 있습니다 toothreats 경고 합니다. 보안 센터에 처음 액세스할 경우 구독의 모든 가상 컴퓨터에서 데이터 수집을 활성화합니다. 데이터 수집 권장 되지만 있습니다 수 옵트아웃 하 여 [데이터 수집을 사용 하지 않도록 설정](https://docs.microsoft.com/azure/security-center/security-center-faq) hello 정책 보안 센터에에서 있습니다.

마지막으로 Azure 보안 센터에는 Microsoft 파트너 및 해당 기능을 Azure 보안 센터 tooenhance에 연결 하는 독립 소프트웨어 공급 업체 toocreate 소프트웨어 수 있도록 하는 개방형 플랫폼입니다.

Azure 보안 센터 hello 다음 Azure 리소스를 모니터링 합니다.

- VM(가상 컴퓨터)(Cloud Services 포함)

- Azure 가상 네트워크

- Azure SQL 서비스

- VM 및 [App Service Environment](https://docs.microsoft.com/azure/app-service/app-service-app-service-environments-readme)에서 웹 응용 프로그램 방화벽 같이 Azure 구독과 통합된 파트너 솔루션

### <a name="operations-management-suite"></a>Operations Management Suite

OMS 소프트웨어 개발 hello 및 서비스 팀의 정보 보안 및 [거 버 넌 스 프로그램](https://github.com/Microsoft/azure-docs/blob/master/articles/log-analytics/log-analytics-security.md) 해당 비즈니스 요구 사항을 지원 하 고에 설명 된 대로 toolaws 및 규정 준수 [Microsoft Azure 보안 센터 ](https://azure.microsoft.com/support/trust-center/) 및 [Microsoft 보안 센터 준수](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)합니다. 여기에는 OMS가 보안 요구 사항을 정하고 보안 컨트롤을 식별하며 위험을 관리 및 모니터링하는 방식도 설명되어 있습니다. 정책, 표준, 절차, 지침을 매년 검토합니다.

각 OMS 개발 팀원은 공식적인 애플리케이션 보안 교육을 이수합니다. 내부적으로는 소프트웨어 개발에 대한 버전 관리 시스템을 사용합니다. 각 소프트웨어 프로젝트 hello 버전 제어 시스템으로 보호 됩니다.

Microsoft에는 Microsoft의 모든 서비스를 감독 및 평가하는 보안 및 규정 준수 팀이 있습니다. 정보 보안 책임자 hello 팀을 구성 하 고 연결 되지 않은 엔지니어링 부서는 OMS 개발 hello로 합니다. hello 보안 책임자 자신의 관리 체인 있고 제품 및 서비스 tooensure 보안 및 규정 준수에 대 한 독립적인 평가 수행 합니다.

Operations Management Suite (OMS)은 hello 처음부터 hello 클라우드에서으로 설계 된 관리 서비스의 컬렉션입니다. OMS 구성 요소는 온-프레미스 리소스를 배포하고 관리하는 대신 Azure에서 전적으로 호스트됩니다. 구성 작업이 최소화되어 문자 그대로 몇 분 안에 실행할 수 있습니다.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig8.png)

OMS 서비스에서 실행 해 서 온-프레미스 환경 효과적으로 관리할 수 없다고 hello 클라우드가 아닙니다.

모든 Windows 에이전트를 저장 하거나 데이터 센터의 Linux 컴퓨터는 다른 모든 데이터와 함께 분석 될 수 있습니다 분석 프레미스 서비스에서 또는 클라우드에서 수집한 데이터 tooLog 보냅니다. -프레미스 리소스에 대 한 백업 및 고가용성에 대 한 Azure 백업 및 Azure 사이트 복구 tooleverage hello 클라우드를 사용 합니다.

Runbook hello 클라우드에서 온-프레미스 리소스를 액세스할 일반적으로 수 없지만 하나 이상의 컴퓨터에 에이전트를 설치할 수 있습니다 너무를 호스팅할 데이터 센터에서 runbook입니다. Runbook을 시작 하면 지정 하면 추가할지 toorun hello 클라우드 또는 로컬 작업자에서 됩니다.

OMS의 핵심 기능 hello Azure에서 실행 되는 서비스 집합에서 제공 됩니다. 각 서비스는 특정 관리 기능을 제공 하 고 서비스 tooachieve 다른 관리 시나리오를 결합할 수 있습니다.

![Operations Manager Suite](./media/governance-in-azure/security-governance-in-azure-fig9.JPG)

Azure 작업 관리자는 관리 솔루션을 제공하여 해당 기능을 확장합니다. [관리 솔루션](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions)은 하나 이상의 OMS 서비스를 활용하여 관리 시나리오를 구현하는 미리 패키지된 논리 집합입니다.

![Azure 작업 관리](./media/governance-in-azure/security-governance-in-azure-fig10.png)

다른 솔루션은 oms에서 투자의 tooyour tooincrease hello 가치를 Azure 구독을 쉽게 추가할 수는 파트너 및 Microsoft에서 사용할 수 있습니다.

파트너 응용 프로그램 및 서비스 사용자 고유의 솔루션 toosupport를 만들 수 있으며 hello Azure 마켓플레이스 또는 빠른 시작 템플릿을 통해 toousers를 제공 하 고 키를 누릅니다.

## <a name="performance-alerting-and-monitoring"></a>성능 경고 및 모니터링

### <a name="alerting"></a>경고

경고는 Azure 리소스 메트릭, 이벤트 또는 로그를 모니터링하고 사용자가 지정한 조건에 부합하면 알림을 보내는 방법입니다.

**다른 Azure 서비스에서의 경고**

경고는 다음과 같은 다양한 서비스에서 사용할 수 있습니다.

- Application Insights: 웹 테스트 및 메트릭 경고가 가능합니다.

>[!Note]
> [Application Insights에서 경고 설정](https://docs.microsoft.com/azure/application-insights/app-insights-alerts) 및 [모든 웹 사이트의 가용성 및 응답성 모니터링](https://docs.microsoft.com/azure/application-insights/app-insights-monitor-web-app-availability)을 참조하세요.

- 로그 분석 (Operations Management Suite): hello 작업 및 진단 로그 tooLog 분석의 라우팅을 활성화 합니다. Operations Management Suite에서는 메트릭, 로그 및 기타 경고 유형을 지원합니다.

>[!Note]
> 자세한 내용은 [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-alerts)의 경고를 참조하세요.

- Azure Monitor: 메트릭 값과 활동 로그 이벤트 모두를 기반으로 한 경고가 가능합니다. Hello를 사용할 수 있습니다 [Azure 모니터 REST API](https://msdn.microsoft.com/library/dn931943.aspx) toomanage 경고 합니다.

>[!Note]
> 자세한 내용은 참조 [hello Azure 포털, PowerShell 또는 hello 명령줄 인터페이스 toocreate 경고를 사용 하 여](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-alerts-portal)합니다.

### <a name="monitoring"></a>모니터링

클라우드 앱의 성능 문제는 비즈니스에 영향을 미칠 수 있습니다. 상호 연결된 여러 구성 요소와 자주 제공되는 릴리스를 사용하면 언제든지 성능 저하가 발생할 수 있습니다. 앱을 개발하는 경우 사용자는 일반적으로 테스트에서 찾지 못한 문제를 발견합니다. 이러한 문제를 즉시 알아야 하 고 hello 문제 진단 및 해결에 대 한 도구를 설치 해야 합니다. Microsoft Azure에는 이러한 문제를 식별할 수 있는 다양한 도구가 있습니다.

**Azure 클라우드 앱을 모니터링하는 방법은?**

Azure 응용 프로그램과 서비스를 모니터링하기 위한 다양한 도구가 있습니다. 일부 기능은 겹칩니다. 기록 상의 용도로 부분적와 부분적으로 개발 및 응용 프로그램의 작업 간의 뜨 리고 toohello 때문입니다.

Hello 주 도구는 다음과 같습니다.

- **Azure Monitor** - Azure에서 실행되는 서비스를 모니터링하는 기본 도구입니다. 서비스와 환경 주변 hello hello 처리량에 대 한 인프라 수준의 데이터 제공 합니다. Azure에서 모든 앱을 관리 하는 경우 여부를 리소스를 위아래로 tooscale, 다음 Azure 모니터 제공 사용 하 여 결정 toostart 합니다.

- **Application Insights** - 개발을 위해 사용하거나 프로덕션 모니터링 솔루션으로 사용할 수 있습니다. 앱에 패키지를 설치하여 작동하므로 진행 상황에 대한 자세한 내부 보기를 제공합니다. 이 데이터에는 종속성, 예외 추적, 디버깅 스냅숏, 실행 프로필의 응답 시간이 포함됩니다. 앱과 함께 수행 하는 사용자가 이해 하는 toohelp 디버그 두 toohelp 강력한 스마트 도구가 모든 원격이 분석 분석을 위해 제공 합니다. 응답 시간이 급증 때문 인지를 알 수는 응용 프로그램 또는 일부 외부 resourcing 문제에서 toosomething 합니다. Visual Studio를 사용 하는 경우 잘못 hello 앱은 있습니다 수 수 가져오므로 오른쪽 toohello 문제 줄을 코드의 문제를 해결할 수 있습니다.

- **로그 분석** 은 프로덕션 환경에서 실행 중인 응용 프로그램에서 tootune 성능 및 계획 유지 관리 해야 합니다. 이는 Azure에 기반을 두고 있습니다. 수집 하 고 10 too15 분 간의 지연이 사항이 있는 여러 소스에서 데이터를 집계 합니다. Azure, 온-프레미스 및 타사 클라우드 기반 인프라(예: Amazon Web Services)에 대한 전체적인 IT 관리 솔루션을 제공합니다. 제공 다양 한 도구 tooanalyze 데이터 자세한 소스 간에, 모든 로그에서 복잡 한 쿼리를 허용 하 고 지정 된 조건에 적극적으로 경고할 수 있습니다. 사용자 지정 데이터를 해당되는 중앙의 리포지토리에 수집하여 쿼리하고 시각화할 수도 있습니다.

- **SCOM(System Center Operations Manager)** - 대규모 클라우드 설치를 관리하고 모니터링하기 위한 것입니다. 온-프레미스 Windows Sever 및 Hyper-V 기반 클라우드를 위한 관리 도구로 이미 친숙해 있을 수 있지만, Azure 앱과 통합하여 이러한 앱을 관리할 수도 있습니다. 무엇보다도 기존의 라이브 앱에 Application Insights를 설치할 수 있습니다. 앱 작동이 중단되면 수 초 안에 알려줍니다.


## <a name="next-steps"></a>다음 단계

- [Azure Resource Manager 템플릿 생성 모범 사례](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)

- [Azure 구독 거버넌스 구현 예제](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-subscription-examples)

- [Microsoft Azure Government](https://docs.microsoft.com/azure/azure-government/)
