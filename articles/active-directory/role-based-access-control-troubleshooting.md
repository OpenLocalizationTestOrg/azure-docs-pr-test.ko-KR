---
title: Azure RBAC aaaTroubleshoot | Microsoft Docs
description: "역할 기반 액세스 제어 리소스에 대해 발생하는 문제 또는 질문 사항에 대한 도움말을 봅니다."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>역할 기반 액세스 제어 문제 해결

이 문서 문서를 사용 하 여 hello hello Azure 포털에서에서 역할 및 액세스 문제 해결 하는 경우 어떤 tooexpect를 알 수 있도록는 역할이 부여 된 hello 특정 액세스 권한에 대 한 일반적인 질문에 대답 합니다. 이러한 세 가지 역할이 모든 리소스 유형에 적용됩니다.

* 소유자  
* 참여자  
* 읽기 권한자  

소유자 및 기여자를 경험 하는 전체 액세스 toohello 관리 들에 게 참가자 액세스 tooother 사용자 또는 그룹에 부여할 수는 없습니다. 작업 시간을 할애해 합니다 म 하므로 hello 판독기 역할로 좀 더 흥미로운를 가져옵니다. Hello 참조 [역할 기반 액세스 제어 started 문서](role-based-access-control-configure.md) toogrant 액세스 하는 방법에 대 한 세부 정보에 대 한 합니다.

## <a name="app-service-workloads"></a>앱 서비스 워크로드
### <a name="write-access-capabilities"></a>쓰기 액세스 기능
사용자 읽기 전용 액세스 tooa 단일 웹 응용 프로그램에 부여 하면 예상치 못한는 일부 기능은 사용할 수 없습니다. 필요한 관리 기능을 수행 하는 hello **쓰기** (참가자 또는 소유자), tooa 웹 앱에 액세스 한 모든 읽기 전용 시나리오에서 사용할 수 없습니다.

* 시작, 중지 등의 명령
* 일반 구성, 규모 설정, 백업 설정, 모니터링 설정 등의 설정 변경
* 게시 자격 증명과 앱 설정, 연결 문자열 등의 기타 암호 액세스
* 스트리밍 로그
* 진단 로그 구성
* 콘솔(명령 프롬프트)
* 활성 및 최근 배포(로컬 Git 연속 배포의 경우)
* 예상 소요 시간
* 웹 테스트
* 가상 네트워크 (만 표시 tooa 판독기 가상 네트워크 쓰기 액세스 권한이 있는 사용자가 이전에 구성 된 경우).

이러한 타일 중 하나에 액세스할 수 없는 경우 필요한 tooask 관리자 참가자 액세스 toohello 웹 앱에 대 한 합니다.

### <a name="dealing-with-related-resources"></a>관련 리소스 사용
웹 앱은 상호 작용 하는 몇 가지 다른 리소스의 hello 존재 복잡 합니다. 아래에는 웹 사이트 몇 개가 포함된 일반적인 리소스 그룹이 나와 있습니다.

![웹앱 리소스 그룹](./media/role-based-access-control-troubleshooting/website-resource-model.png)

결과적으로, 다른 사람이 액세스 toojust hello 웹 앱에 부여 hello Azure 포털에서에서 웹 사이트 블레이드에서 hello hello 기능 많이 사용 되지 않습니다.

이러한 항목의 해야 **쓰기** toohello 액세스 **앱 서비스 계획** tooyour 웹 사이트에 해당:  

* 보기 hello 웹 응용 프로그램의 가격 책정 계층 (무료 또는 표준)  
* 크기 조정 구성(인스턴스 수, 가상 컴퓨터 크기, 자동 크기 조정 설정)  
* 할당량(저장소, 대역폭, CPU)  

이러한 항목의 해야 **쓰기** 전체 액세스 toohello **리소스 그룹** 웹 사이트를 포함 하는:  

* SSL 인증서 및 바인딩 (hello 내의 사이트 간에 SSL 인증서를 공유할 수 같은 리소스 그룹 및 지리적 위치)  
* 경고 규칙  
* 자동 크기 조정 설정  
* Application Insights 구성 요소  
* 웹 테스트  

## <a name="virtual-machine-workloads"></a>가상 컴퓨터 작업
훨씬와 마찬가지로 웹 앱과 hello 가상 컴퓨터 블레이드의 일부 기능을 필요 쓰기 액세스 toohello 가상 컴퓨터 또는 hello 리소스 그룹의 tooother 리소스입니다.

가상 컴퓨터가 관련된 tooDomain 이름, 가상 네트워크, 저장소 계정 및 경고 규칙에 있습니다.

이러한 항목의 해야 **쓰기** toohello 액세스 **가상 컴퓨터**:

* 끝점  
* IP 주소  
* 디스크  
* 확장  

여기에 필요 **쓰기** 액세스 tooboth hello **가상 컴퓨터**, 및 hello **리소스 그룹** 한다는 중인 (함께 hello 도메인 이름):  

* 가용성 집합  
* 부하 분산된 집합  
* 경고 규칙  

이러한 타일 중 하나에 액세스할 수 없는 참가자 액세스 toohello 리소스 그룹에 대 한 관리자에 게 문의 합니다.

## <a name="see-more"></a>자세히 보기
* [역할 기반 액세스 제어](role-based-access-control-configure.md): RBAC hello Azure 포털을에서 시작 합니다.
* [기본 제공 역할](role-based-access-built-in-roles.md): RBAC에 기본적으로 제공 하는 hello 역할에 대 한 세부 정보를 가져옵니다.
* [사용자 정의 역할에서 Azure RBAC](role-based-access-control-custom-roles.md): 사용자의 액세스 요구 하는 사용자 지정 역할 toofit toocreate 방법을 알아봅니다.
* [액세스 변경 기록 보고서 만들기](role-based-access-control-access-change-history-report.md): RBAC에서 역할 할당 변경을 추적합니다.

