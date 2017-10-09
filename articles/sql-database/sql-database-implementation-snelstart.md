---
title: "SQL 데이터베이스 Azure 사례 연구-aaaAzure Snelstart | Microsoft Docs"
description: "SnelStart 사용 하 여 SQL 데이터베이스 toorapidly 매달 1, 000 새 Azure SQL 데이터베이스의 속도로 비즈니스 서비스를 확장 하는 방법에 대해 알아보기"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: fab506b2-439d-4f1a-bdc5-d1d25c80d267
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 69572393f41a9baf44f41b4f5f4ebbef347de851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="with-azure-snelstart-has-rapidly-expanded-its-business-services-at-a-rate-of-1000-new-azure-sql-databases-per-month"></a>Azure를 사용하여 SnelStart는 매월 1,000개의 새 Azure SQL 데이터베이스 규모로 비즈니스 서비스를 빠르게 확장했습니다.
![SnelStart 로고](./media/sql-database-implementation-snelstart/snelstartlogo.png)

SnelStart는 hello 네덜란드에 인기 있는 재무 및 비즈니스-관리 소프트웨어가 소규모 및 중간 규모의 기업 (Smb)을 만듭니다. 이 회사의 55,000여 고객은 IT 직원 35명을 포함하여 110명의 직원에게 서비스를 받습니다. SnelStart 데스크톱 소프트웨어 tooa 소프트웨어-as a service (SaaS) 제품 기반으로 Azure를 이동 하 여 가장 hello을 만든 C#에서는 친숙 한 환경을 사용 하 고 모두 over-성능 및 확장성을 최적화 하는 관리를 자동화 하는 기본 제공 서비스 또는 탄력적 풀을 사용 하 여 미달 프로비저닝은 기업입니다. Azure를 사용 하 여 고객 온-프레미스 및 hello 간 이동의 SnelStart hello 가변 제공 클라우드입니다.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-SnelStart/player]
> 
> 

## <a name="why-snelstart-extended-services-from-hello-desktop-toohello-cloud"></a>SnelStart는 hello 데스크톱 toohello 클라우드에서 서비스를 확장 하는 이유
> "Azure 사용한 작업 म 소프트웨어를 더 빠르게 제공, 신속 하 게 반응 toocustomer 요구 하 여 수요 증가 하는 경우 솔루션을 확장 의미 합니다."
> 
> - 소프트웨어 설계자 Henry Been
> 
> 

SnelStart는 전통적인 개발 모델인 코드, 패키지, 배송 및 반복을 사용하여 수년 동안 소프트웨어 비즈니스를 성공적으로 실행했습니다. 시간이 지남에 따라 변경의 속도 hello 더 빠르게 증가 하 고 더 빠르게 합니다. 규정은 자주 변경 하 고 고객 보다 쉽게 방법으로 tooprocess 재무 레코드 필요한 변경 내용이 반영 된를 저장 및 정부 tookeep 항목과 함께 공동 작업 합니다.

"소프트웨어 toocustomers 전달 했습니다. 비용이 많이 들고 제한" tooHenry에 따라 소프트웨어 설계자를 되었습니다. 프로덕션, 패키지 및 배송 비용 때문에 우리가 소프트웨어를 출시하는 빈도에도 제한이 적용되었습니다. 정기적으로 배송에 대 한 toopackage 업데이트 했습니다. 하지만 하드 toomeet 수행 하는 고객의 요구 사항을 변경 합니다. म 되지 했음을 확인할 수 있습니다를 고객 toohello hello 제품의 최신 버전을 업그레이드 합니다. 따라서 했습니다. toosupport 여러 버전을 만드는 작업이 매우 어려운 toodo 잘 지원 hello. "

되었습니다를 추가 하면 "방식으로 싶었기 tooprogram 및 릴리스 업데이트에는 가속화 된 속도, 하므로 더 빠르게 혁신 하도록 하 고 고객에 대 한 새 서비스를 만들 수 없습니다. 했습니다 방식으로 tooautomate 더 처리 순서 toosimplify에 고객의 비즈니스 관리자 요구 사항을. "

SnelStart에 대 한 솔루션을 hello tooextend 해당 서비스는 클라우드 기반 SaaS 공급자 되 면 되었습니다. hello Azure SQL 데이터베이스 플랫폼 인프라-as a service (IaaS) 솔루션 요구 하는 hello 주요 IT 오버 헤드 없이 ु म ी SnelStart 작업 수 있습니다.

또한 hello 클라우드 모델 SnelStart toofix 버그를 사용 하도록 설정 하 고 고객 toodownload 및 소프트웨어 업그레이드 필요 없이 신속 하 게, 새로운 기능을 제공 합니다. 에 따라 tooBeen, "를 사용 하 여 Azure 클라우드 서비스 수 요구 사항을 변경 하는 제 3 자에서 tooquickly 적용할 수 있습니다. 대신 tooship 고객의 새 버전 toothousands, 우리를 조정 하 여 제 3 자가 필요한 우리의 데스크톱 응용 프로그램 toonew 형식에서 전송 되는 정보입니다. "

## <a name="a-modern-company-with-traditional-roots"></a>전형적인 기반의 현재 기업
SnelStart는 hello 창립자 음악 계측 부분의 제조업체도 hello 회사 시작 될 때 too1964, 데이트 미 천 한 루트와 최신, agile, 첨단 기술 비즈니스입니다. hello SnelStart 소프트웨어 비즈니스의 hello 핵심 실제로 hello 개인용 컴퓨터의 hello 급증 하는 동안 1980 hello에 비트 시작 되었습니다. hello 회사 문제를 자체 손에 걸리는 hello 시 사용할 수는 더 나은 대체 toohello 회계 소프트웨어 데 필요 합니다. 1982, hello 회사 SnelStart 회계 소프트웨어 결국은 어떤의 hello 기반을 만들었습니다. Hello 시작부터 hello 소프트웨어를 간단 하 고 속도 대 한 admired-많은 양의 hello 회사 결국 포커스를 변경 하 고 자체 소프트웨어 회사를 클라우드에 있도록 합니다.

1995년에 SnelStart는 최초의 Windows용 부기 응용 프로그램을 출시했습니다. Microsoft Visual Basic 1.0 및 Microsoft Access 데이터베이스를 기반으로 hello 응용 프로그램, 작업 5, 000 사용자 보다 hello 고객 기본 toomore 증가할 수 있습니다.

오늘날, SnelStart는 네덜란드의 중소기업 및 자영 사업가를 대상으로 하는 LOB(기간 업무) 및 비즈니스 관리 응용 프로그램의 주요 공급자입니다. Carlo Kuip, IT 설계자, 라고 표시 하는 대로 "목표는 고객에 대 한 비즈니스 관리 서비스의 100% 자동화 tooprovide."

## <a name="optimizing-performance-and-cost-with-elastic-pools"></a>탄력적 풀을 통해 성능 및 비용 최적화
SnelStart는 탄력적 풀을 대규모로 일찌감치 활용했습니다. 탄력적 풀 hello 회사 제한 비용 하 고 성능 요구를 보다 효율적으로 관리 합니다. "탄력적 풀을 사용 하 여 최적화할 수 있는 과도 하 게 프로 비전 하지의 고객에 hello 요구 사항에 따라 성능 tooBeen에 따라. 최대 부하에 따라 tooprovision, 있을 경우 상당한 비용이 많이 드는 것입니다. 대신, 옵션 tooshare 리소스 hello 여러 간에 낮은 사용 데이터베이스를 통해 toocreate 잘 수행 하는 비용 효율적인 솔루션입니다. "

## <a name="azure-sql-databases-help-containerize-data-for-isolation-and-security"></a>Azure SQL 데이터베이스는 격리 및 보안을 위해 데이터를 컨테이너에 보관하도록 지원합니다.
Azure SQL 데이터베이스 SnelStart tooeasily 있으며 특정 고객의 온-프레미스 비즈니스 관리 데이터 tooAzure 투명 하 게 이동 합니다. hello Azure SQL 데이터베이스는 인증, 권한 부여 및 쉽게 백업 및 복원 기능에 대 한 격리, 경계를 제공 하는 편리한 컨테이너입니다. 데이터베이스는 비즈니스 관리에 적합한 개념적 모델을 제공합니다. 에 따라 tooCarlo Kuip, IT 설계자, "이 컨테이너 경계 내에서 항목 중요 tooa 비즈니스 효율적으로 보호 하는 격리 된 데이터베이스에서에서 이러한 항목이 저장 되는 중요 한 데이터를 포함 하는 데 사용 됩니다. म 관리 hello 데이터베이스 수준에서 권한 부여 하 고 수 담당자에 대 한 데이터베이스 관리자 (Dba)를 요구 하지 않고 hello 관리 및 이러한 데이터베이스의 확장을 자동화할 수도 있습니다. "

또한 azure SQL 데이터 웨어하우스 hello SnelStart 보안 및 관리 스토리에서 역할 hello 회사 침입 감지, 사용자 작업 로깅 및 연결 등의 원격 분석 데이터를 수집할 수 있도록 지원 하 여을 담당 합니다.

## <a name="azure-removes-overhead-so-that-developers-can-spend-more-time-delivering-value"></a>Azure는 오버헤드를 제거하여 개발자가 가치를 전달하는 데 더 많은 시간을 투입할 수 있게 합니다.
hello Azure 플랫폼 모델 인프라 오버 헤드를 제거 하 고 C# 관리 라이브러리를 사용 하 여 SnelStart tooautomate 배포를 사용 하도록 설정 합니다. Kuip 상태 대로 "있었습니다. 수 toogrow 우리의 현재 작업과 동시에 증가 확장성, 속도 및 재해 복구 하는 동안 매우 작은 담당자가이 클라이언트에 대 한 옵션입니다. hello shift tooservices 개발 해제 리소스를 새로운 서비스와 기능을 바로 새 규정 또는 세금 코드와 함께 기존 코드 tookeep를 업데이트 하는 대신 toofocus. " "관리를 자동화 하 고 hello SaaS 제품을 사용 하 여, 있습니다 수 toodeliver 운영 담당자의 toomake 대규모 투자 하지 않고도 클라이언트에 대 한 값 더.", 추가 예를 들어 Azure 및 탄력적인 풀을 사용 하 여 SnelStart가 수 tooadd 다양 한 새로운 기능을 은행이와 보다 강력한 고객 데이터 통합을 포함 하 여 새 서비스, 백그라운드 소기업 검사 및 전자 메일 서비스의 대금 청구 합니다.

> "정당한 hello 2016 년의 처음 몇 개월 동안에서는 확장 되었고, 12, 000, 보다 약 5,500 toomore에서 우리의 Azure SQL 데이터베이스 배포 및 현재 월 당 약 1, 000 데이터베이스를 추가 하는 것입니다."
> 
> - 소프트웨어 설계자 Henry Been
> 
> 

데이터베이스 관리 hello 탄력적 작업 기능을 사용 하 여 자동 추가 됩니다. Kuip 상태 처럼 "매우에 감사 드립니다 hello SQL DB의 [서버] 인스턴스에서 데이터베이스의 자동 검색 합니다." 따라서 SnelStart tooexecute 관리 작업에서 동적으로 증가 하 고 고객의 추가 오버 헤드 없이 기본 있습니다.

또한 SnelStart는 고객 데이터와 타사 소프트웨어 파트너에서 제작한 앱 간에 브로커 역할을 하는 API를 개발하고 있습니다. Kuip 상태로 "이이 API는 사용 등의 다른 공급 업체 tooadd 기능 tooour 소프트웨어, 송장 및 기타 문서에 대 한 데이터 항목을 제거 합니다." 고객은 소기업 프로그램;에 toomanually 형식 송장 들이 더 이상 hello SnelStart 소프트웨어 hello 필요한 정보를 직접 교환 됩니다. 이렇게 하면 고객이 hello 업계의 디지털 변환에서 요구 하는 정보의 hello 에코 시스템이 포함 toojoin 자신의 비즈니스 관리 작업입니다.  

## <a name="how-azure-services-enable-saas-for-snelstart"></a>Azure 서비스에서 SnelStart에서 SaaS를 사용하도록 설정하는 방법
Azure를 사용 하 여 SnelStart 고객 및 해당 회계 담당자 hello 클라우드에서 보다 원활 하 게 사용할 수 있습니다. 예를 들어 고객과 회계사가 Azure에 호스트된 SnelStart의 클라이언트 API에 직접 액세스하여 정보를 공유할 수 있습니다. Kuip 상태 "이러한 다시 사용할 수 있는 서비스는 사용할 수 있는 tooour 고객 지향 웹 응용 프로그램 이벤트 및 제공 공용 인프라 및 함수 고객 및 고객에서 사용 하는 toothird 타사 소프트웨어에 대 한 tooallow 액세스 toobusiness 관리 합니다. 예로 제품 구성 기능 제공, 방화벽 규칙 관리 및 백업과 같은 장기 실행 프로세스 관리를 들 수 있습니다.

> 목표는 고객에 대 한 비즈니스 관리 서비스의 tooprovide 100% 자동화 합니다. " 
> 
> - IT 설계자, Carlo Kuip
> 
> 

또한 SnelStart 웹 서비스를 통해 고객과 회계 담당자 tooeasily Azure SQL 데이터베이스 탄력적 풀의 데이터에 액세스 합니다. 데이터베이스 탄력성 및 Azure 리소스 관리자와 결합된 이 SaaS 모델은 모든 Azure 배포를 보완하는 확장성 기능을 SnelStart에 제공합니다. hello 구현 C# 관리 라이브러리를 사용 하 여 자동 완벽 하 게 됩니다.

![SnelStart 아키텍처](./media/sql-database-implementation-snelstart/figure1.png)

그림 1. 2016년 6월을 기준으로 SnelStart는 11,000개가 넘는 데이터베이스와 50개가 넘는 탄력적 풀을 보유하고 있습니다.

## <a name="simplicity-from-hello-cloud"></a>단순성 hello 클라우드에서
Tooan Azure의 클라우드 기반 솔루션을 이동, 이후 SnelStart 혁신적인 기능 및 서비스를 제공 하는 동안 수 toosupport 신속 하 게 고객 증가 했습니다. TooBeen에 따라 "Azure를 입힐 수 거의 연속적인 업데이트 자사 고객을 위해 운영 담당자가이 확장 하지 않고 합니다. 얻을 수 있는 모든 hello 가지 뛰어난 Azure 기능 및-확장성 및 재해 복구와 같은-제공 됩니다. "

> "때 있었습니다 실제로 통해 레드먼드에... 특정 문제에 대 한 내게 면담 hello 네덜란드에 다시 개발자 로부터 호출을 나타났습니다. 여기서 문제 수 tooget Microsoft toodeliver toosolve 48 시간 내에서 프로덕션 환경에서 변경 되었습니다. "
> 
> - 소프트웨어 설계자 Henry Been
> 
> 

SnelStart도 hello 강력한 파트너 관계 hello Microsoft Azure SQL DB 팀과 개발한 감사 한다는 메시지가 표시 됩니다. Kuip 상태로 "토론 기능에 있으며 이러한 시각화가 toouse 기술 양쪽 모두에 지 환영 하는 방법 및."
hello 즉시 SnelStart에 대 한 ´ ֲ tookeep 만족된 한 고객을 기본 증가 합니다. 된 대로 상태를 "hello 기술 및 ISV로 서 했습니다. 리소스 제한 없으면 없습니다 제한 toohow까지 증가할 수 있습니다."

## <a name="more-information"></a>자세한 정보
* Azure 탄력적 풀에 대해 자세히 toolearn 참조 [탄력적 풀](sql-database-elastic-pool.md)합니다.
* 웹 역할 및 작업자 역할에 대해 자세히 toolearn 참조 [작업자 역할](../fundamentals-introduction-to-azure.md#compute)합니다.    
* Azure SQL 데이터 웨어하우스에 대 한 자세한 정보는 toolearn 참조 [SQL 데이터 웨어하우스](https://azure.microsoft.com/documentation/services/sql-data-warehouse/)
* toolearn SnelStart에 대 한 자세한 참조 [SnelStart](http://www.snelstart.nl)합니다.

