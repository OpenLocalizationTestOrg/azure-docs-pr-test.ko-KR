---
title: "aaaMulti 테 넌 트 웹 응용 프로그램 패턴 | Microsoft Docs"
description: "아키텍처 개요 및 tooimplement 다중 테 넌 트 웹 응용 프로그램을 Azure에서 하는 방법을 설명 하는 디자인 패턴을 찾습니다."
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Azure의 다중 테넌트 응용 프로그램
다중 테 넌 트 응용 프로그램은 수 있도록 하는 별도 사용자 또는 "테 넌 트," tooview hello 인 것 처럼 자신의 공유 리소스입니다. 자체 tooa 다중 테 넌 트 응용 프로그램을 제공 하는 일반적인 시나리오는 하나 이상의의 hello는 모든 사용자가 응용 프로그램 toocustomize hello 사용자 경험을 할 수 있습니다 하지만 그렇지 않으면 동일한 기본 비즈니스 요구 사항을 hello 합니다. 대규모 다중 테넌트 응용 프로그램의 예로는 Office 365, Outlook.com 및 visualstudio.com이 있습니다.

응용 프로그램 공급자의 관점에서 다중 테 넌 트의 hello 이점을 대부분 toooperational 및 관련 비용 효율성을 이용 합니다. 응용 프로그램의 한 버전 많은 테 넌 트/고객, 시스템의 통합 관리 작업 모니터링, 성능 조정, 소프트웨어 유지 관리 및 데이터 백업 같은 수의 hello 요구를 충족할 수 있습니다.

hello 다음 hello 가장 중요 한 목표와 요구 사항을 공급자의 관점에서의 목록이 표시 됩니다.

* **프로 비전**: hello 응용 프로그램에 대 한 새 테 넌 tooprovision 수 있어야 합니다.  많은 테 넌 트의 다중 테 넌 트 응용 프로그램의 경우는 일반적으로 필요한 tooautomate이이 프로세스에서 셀프 서비스 프로 비전을 사용 하도록 설정 합니다.
* **유지 관리 용이성**: 수 tooupgrade hello 응용 프로그램 이어야 하며, 여러 테 넌 트 사용 하는 동안 다른 유지 관리 작업을 수행 합니다.
* **모니터링**: 있습니다 모든 문제와 tootroubleshoot 수 toomonitor hello 응용 프로그램에 항상 tooidentify 있어야 해당 합니다. 여기에 각 테 넌 트 hello 응용 프로그램에서 사용 하는 방법을 모니터링 합니다.

제대로 구현 된 다중 테 넌 트 응용 프로그램 hello 다음 toousers 혜택을 제공 합니다.

* **격리**: hello 활동의 개별 테 넌 트가 다른 테 넌 트에서 hello 응용 프로그램의 hello 사용 영향을 주지 않습니다. 테넌트는 서로의 데이터에 액세스할 수 없습니다. Toohello 테 넌 트 표시 하는 것으로 hello 응용 프로그램을 단독으로 사용 됩니다.
* **가용성**: 개별 테 넌 트가 지속적으로 사용할 수 있는 hello 응용 프로그램 toobe 아마도 보장 SLA에 정의 되어 있습니다. 다시, 다른 테 넌 트의 hello 활동에서는 hello hello 응용 프로그램의 가용성에 영향을 주지 않습니다.
* **확장성**: hello 응용 프로그램의 개별 테 넌 트의 toomeet hello 요구가 확장성. hello 존재 여부와 다른 테 넌 트의 작업은 성능 영향을 주지 hello hello 응용 프로그램의 합니다.
* **비용**: 다중 테 넌 트 hello 리소스를 공유할 수 있도록 하기 때문에 전용, 단일 테 넌 트 응용 프로그램을 실행 하는 보다 낮은 비용 됩니다.
* **사용자 지정 가능**: hello 기능 toocustomize hello 응용 프로그램 추가 또는 제거 하는 기능, 색 및 로고, 변경 또는 자신의 코드 또는 스크립트를 추가 하는 등 다양 한 방법으로 개별 테 넌 트에 대 한 합니다.

즉,에 수행 해야 하는 고려 많이 하는 동안 계정 tooprovide 확장성이 높은 서비스 hello 목표와는 일반적인 toomany 다중 테 넌 트 응용 프로그램 요구 사항 수 있습니다. 일부 하지 못할 특정 시나리오 및 개별 목표의 hello 중요성에 관련 및 요구 사항은 각 시나리오에서 달라 집니다. Hello 다중 테 넌 트 응용 프로그램의 공급자로 수 제공 됩니다 목표 및 요구와 같은 hello 테 넌 트의 목표 및 요구 사항, 수익성, 청구, 여러 서비스 수준, 프로 비전, 유지 관리, 모니터링 및 자동화를 달성 합니다.

다중 테넌트 응용 프로그램 설계와 관련된 추가 고려 사항에 대한 자세한 내용은 [Azure에서 다중 테넌트 응용 프로그램 호스트][Hosting a Multi-Tenant Application on Azure]를 참조하세요. 다중 테넌트 SaaS(software-as-a-service) 데이터베이스 응용 프로그램의 일반적인 데이터 아키텍처 패턴에 대한 정보는 [Azure SQL 데이터베이스를 사용한 다중 테넌트 SaaS 응용 프로그램의 설계 패턴](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md)을 참조하세요. 

Azure 다중 테 넌 트 시스템을 설계할 때 발생 하는 주요 문제를 hello tooaddress 사용할 수 있는 많은 기능을 제공 합니다.

**격리**

* 호스트 헤더로 웹 사이트 테넌트 분할(SSL 통신을 사용하거나 사용하지 않음)
* 쿼리 매개 변수로 웹 사이트 테넌트 분할
* 작업자 역할의 웹 서비스
  * 작업자 역할. 일반적으로는 hello 백 엔드 응용 프로그램의 데이터를 처리 합니다.
  * 일반적으로 응용 프로그램에 대 한 hello 프런트엔드 변수로 작동 하는 웹 역할입니다.

**저장소**

데이터 관리 hello와 같은 Azure SQL 데이터베이스 또는 Azure 저장소 서비스와 같은 테이블 대량의 구조화 되지 않은 데이터를 저장 하기 위한 서비스를 제공 하는 서비스 및 서비스 toostore 대량의 구조화 되지 않은 텍스트를 제공 하는 Blob 서비스 hello 또는 비디오, 오디오 및 이미지 등 이진 데이터입니다.

* SQL 데이터베이스의 다중 테넌트 데이터 보호 - 테넌트별 SQL Server 로그인에 적합합니다.
* Azure 테이블을 사용 하 여 응용 프로그램 리소스를 지정 하 여 컨테이너 수준 액세스 정책에 대 한, tooissue 새 URL의 공유 액세스 서명을 사용 하 여 보호 하는 hello 리소스에 대 한 필요 없이 기능 tooadjust 사용 권한을 hello 수 있습니다.
* 응용 프로그램 리소스 Azure 큐에 대 한 azure 큐는 테 넌 트를 대신 처리 하는 자주 사용 되는 toodrive 있지만 해야 할 수도 사용된 toodistribute 작업 프로 비전 또는 관리 합니다.
* 서비스 버스 큐를 꺼내는 작업 tooa 응용 프로그램 리소스에 대 한 공유 서비스, 사용 권한 (ACS에서 발행 한 클레임에서 파생 됨) 처럼 toopush toothat 큐 hello 서비스에서 유일한 hello 수신기 하는 동안에 각 테 넌 트 발신자만에 단일 큐에서 사용할 수 있습니다. 다중 테 넌 트에서 들어오는 hello 큐 hello 데이터에서 권한을 toopull이 있어야 합니다.

**연결 및 보안 서비스**

* Azure 서비스 버스, 향상 된 확장 및 복원에 대 한 느슨하게 결합 된 방식 tooexchange 메시지를 허용 하는 응용 프로그램 사이 있는 메시징 인프라입니다.

**네트워킹 서비스**

Azure에서는 몇 가지 네트워킹 서비스를 통해 인증을 지원하고 호스트된 응용 프로그램의 관리 효율성을 향상합니다. 이러한 서비스는 hello 다음과를 같습니다.

* Azure 가상 네트워크를 사용하여 Azure에서 VPN(가상 사설망)을 프로비전하고 관리하며 온-프레미스 IT 인프라와 안전하게 연결할 수 있습니다.
* 가상 네트워크 트래픽 관리자 hello에서 실행 하는 서비스에 여러 호스팅된 Azure 전체에서 들어오는 트래픽을 tooload 균형을 사용 하면 동일한 데이터 센터 또는 hello 전 세계의 여러 데이터 센터입니다.
* Azure AD(Azure Active Directory)는 클라우드 응용 프로그램과 관련하여 ID를 관리하고 액세스를 제어할 수 있게 하는 최신 REST 기반 서비스입니다. Azure AD 응용 프로그램 리소스 tooprovides 쉽게 인증 하 고 사용자가 toogain 액세스 tooyour 웹 응용 프로그램 및 서비스의 팩터링 하는 인증 및 권한 부여 toobe의 hello 기능을 허용 하는 동안 권한 부여에 대 한 Azure AD를 사용 하 여 코드입니다.
* Azure 서비스 버스는 분산 및 하이브리드 응용 프로그램에 대해 복잡한 방화벽 및 보안 인프라 없이도 Azure 호스트된 응용 프로그램과 온-프레미스 응용 프로그램 및 서비스 사이의 통신과 같은 보안 메시징 및 데이터 흐름 기능을 제공합니다. 서비스 버스 릴레이 사용 하 여 응용 프로그램 리소스 toohello에 대 한 서비스 끝점 toohello 속할 수으로 노출 되는 테 넌 트 (예: 온-프레미스 같은 hello 시스템 외부에서 호스팅된), 또는 테 넌 트 (hello에 대 한 구체적으로 사용자를 프로 비전 하는 서비스 일 수 있습니다. 중요 한, 테 넌 트 별 데이터 간에 이동) 때문에.

**리소스 프로비전**

Azure는 hello 응용 프로그램에 대 한 다양 한 방법으로 프로 비전 새로운 테 넌 트를 제공합니다. 많은 테 넌 트의 다중 테 넌 트 응용 프로그램의 경우는 일반적으로 필요한 tooautomate이이 프로세스에서 셀프 서비스 프로 비전을 사용 하도록 설정 합니다.

* 작업자 역할 tooprovision 및 테 넌 트 리소스 (예: 때 새 테 넌 트가 등록 하거나 취소) 당 디 프로 비전을 사용 하면, 계량을 사용 하 고 특정 일정에 따라 크기 조정 관리 또는 키의 임계값 toohello 초과 응답 메트릭 수집 성과 지표입니다. 이 동일한 역할이 업데이트 및 업그레이드 toohello 솔루션 사용된 toopush 수도 있습니다.
* Azure Blob 컨테이너 수준 액세스 정책을 tooprotect hello 계산 서비스 패키지, VHD 이미지 및 기타 리소스를 제공 하는 동안 사용 되는 tooprovision compute 나 새 테 넌 트에 대 한 미리 초기화 된 저장소 리소스를 수 있습니다.
* 테넌트용으로 SQL 데이터베이스 리소스를 프로비전하는 옵션에는 다음이 포함됩니다.
  
  * DDL을 스크립트에 사용하거나 어셈블리 내 리소스로 포함
  * SQL Server 2008 R2 DAC 패키지를 프로그래밍 방식으로 배포
  * 마스터 참조 데이터베이스에서 복사
  * 파일에서 데이터베이스 가져오기 및 내보내기 tooprovision 새 데이터베이스를 사용합니다.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
