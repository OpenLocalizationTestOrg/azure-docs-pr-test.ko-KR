---
title: "aaaAzure 팀 데이터 과학 프로세스 개요 | Microsoft Docs"
description: "데이터 과학 방법론 toodeliver 예측 분석 솔루션을 제공 지능형 응용 프로그램 및입니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Team Data Science Process 개요

hello 팀 데이터 과학 프로세스 (TDSP)는는 agile 반복 데이터 과학 방법론 toodeliver 예측 분석 솔루션 및 지능형 응용 프로그램 효율적으로 합니다. TDSP는 팀 공동 작업 및 학습을 향상하도록 돕습니다. Hello에 대 한 유용한 정보 및 구조에서 Microsoft 및 기타 hello 업계의 hello 데이터 과학 이니셔티브의 성공적인 구현을 용이 하 게 하는 추출할을 포함 됩니다. hello ´ ֲ toohelp 회사에는 완벽 하 게 해당 분석 프로그램의 hello 장점을 실제 이용 합니다.

이 문서에서는 TDSP 및 주요 구성 요소의 개요를 제공합니다. 다양 한 도구와 구현 될 수 있는 hello 프로세스 여기의 일반적인 설명을 제공 합니다. Hello 프로젝트 작업 및 hello 프로세스의 수명 주기 hello에에서 관련 된 역할의 더 자세한 설명은 추가 연결 된 항목에 제공 됩니다. Tooimplement hello Microsoft 도구 및 인프라 tooimplement hello TDSP을 사용 하 여 팀에서의 특정 집합을 사용 하 여 TDSP도 제공 방법에 대 한 지침입니다.

## <a name="key-components-of-hello-tdsp"></a>Hello TDSP의 주요 구성 요소

TDSP hello 다음과 같은 주요 구성 요소가 구성 됩니다.

- **데이터 과학 수명 주기** 정의
- **표준화된 프로젝트 구조**
- 데이터 과학 프로젝트에 대한 **인프라 및 리소스**
- 프로젝트 실행에 대한 **도구 및 유틸리티**


## <a name="data-science-lifecycle"></a>데이터 과학 수명 주기

hello 팀 데이터 과학 프로세스 (TDSP) 데이터 과학 프로젝트의 수명 주기 toostructure hello 개발을 제공합니다. hello 수명 주기에서 다음에 나오는 프로젝트 일반적으로 실행 될 때 시작 toofinish hello 단계를 간략하게 설명 합니다.

다른 데이터 과학 수명 주기를와 같은 사용 중인 경우 [CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining), [KDD](https://wikipedia.org/wiki/Data_mining#Process) 회사의 사용자 지정 프로세스를 계속 사용할 수 있습니다 또는 해당 개발의 hello 컨텍스트에서 작업 기반 TDSP hello 주기 합니다. 상위 수준에서 이러한 다양한 방법에는 많은 공통점이 있습니다. 

이 수명 주기는 지능형 응용 프로그램의 일부로 제공되는 데이터 과학 프로젝트를 위해 설계되었습니다. 이러한 응용 프로그램은 예측 분석을 위해 기계 학습 또는 인공 지능 모델을 배포합니다. 예비 데이터 과학 프로젝트 또는 임시 분석 프로젝트에서 이 프로세스를 사용하여 활용할 수도 있습니다. 하지만 이러한 경우에 설명 된 hello 단계 중 일부는 필요 하지 않습니다.    

hello TDSP 수명 주기는 반복적으로 실행 되는 5 개의 주요 단계로 구성 됩니다.

* **비즈니스 이해**
* **데이터 취득 및 이해**
* **모델링**
* **배포웹사이트를**
* **고객 승인**

여기 hello의 시각적 표현인 **팀 데이터 과학 프로세스 수명 주기**합니다. 

![TDSP 수명 주기](./media/data-science-process-overview/tdsp-lifecycle.png) 

hello 목표, 작업 및 TDSP에 hello 주기의 각 단계에 대 한 설명서 아티팩트에에서 설명 된 hello [팀 데이터 과학 프로세스 수명 주기](data-science-process-lifecycle.md) 항목입니다. 이러한 작업 및 아티팩트는 프로젝트 역할과 관련이 있습니다.

- 솔루션 설계자
- 프로젝트 관리자
- 데이터 과학자
- 프로젝트 책임자 

hello 다음 다이어그램에서는 hello (파란색) 작업과 hello 세로 축) (에 이러한 역할에 대 한 hello 가로 축) (에 hello 주기의 각 단계와 관련 된 (녹색)으로 아티팩트의 표 뷰. 

![TDSP 역할 및 작업](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>표준화된 프로젝트 구조

모든 프로젝트 디렉터리 구조를 공유 하 고 프로젝트의 문서에 대 한 서식 파일을 사용 하면 해당 프로젝트에 대 한 hello 팀 구성원 toofind 정보를 쉽게 있습니다. 모든 코드 및 문서 Git, TFS 또는 Subversion tooenable 팀 공동 작업와 같은 버전 제어 시스템 (VC)에 저장 됩니다. 작업 및 Jira와 같은 시스템을 추적 하는 agile 프로젝트의 기능을 추적, Rally, Visual Studio Team Services 추적할 수 있게 가깝게 개별 기능에 대 한 hello 코드입니다. 이러한 추적에는 팀 tooobtain을 더 비용을 추산 수 있습니다. TDSP 버전 관리, 정보 보안 및 공동 작업에 대 한 hello VCS에 각 프로젝트에 대 한 별도 저장소를 만드는 것을 권장 합니다. hello는 hello 조직 전체에서 모든 프로젝트는 데 도움이 됩니다 빌드 조직의 지식에 대 한 구조를 표준화 합니다.

Hello 폴더 구조 및 기본 위치에 필요한 문서에 대 한 템플릿을 제공합니다. 이 폴더 구조는 hello 파일 데이터 탐색 및 기능 추출에 대 한 코드를 포함 하 고 해당 모델 반복 레코드를 구성 합니다. 이러한 템플릿을 사용 하면 다른 사용자가 수행 하는 팀 멤버 toounderstand 작업에 대 한 보다 쉽게 새 멤버 tooteams tooadd 하 고 있습니다. 것이 쉬운 tooview 및 업데이트 문서 템플릿 마크 다운 형태로 표시 합니다. 각 프로젝트 tooinsure hello 문제는 잘 정의 된 및 해당 결과물 hello 품질 예상을 충족에 대 한 주요 질문으로 tooprovide 검사 목록 서식 파일을 사용 합니다. 예를 들면 다음과 같습니다.

- 프로젝트 기본 문서 toodocument hello 비즈니스 문제 및 hello 프로젝트의 범위
- 데이터는 toodocument hello 구조와 hello 원시 데이터의 통계를 보고합니다.
- 모델 보고서 toodocument hello 파생 기능
- ROC 곡선 또는 MSE와 같은 모델 성능 메트릭


![TDSP 디렉터리](./media/data-science-process-overview/tdsp-dir-structure.png)

hello 디렉터리 구조에서 복제할 수 있는 [Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate)합니다.

## <a name="infrastructure-and-resources-for-data-science-projects"></a>데이터 과학 프로젝트에 대한 인프라 및 리소스

TDSP는 다음과 같은 공유 분석 및 저장소 인프라를 관리하기 위한 권장 사항을 제공합니다.

- 데이터 집합을 저장하기 위한 클라우드 파일 시스템, 
- 데이터베이스
- 빅 데이터(Hadoop 또는 Spark) 클러스터 
- 기계 학습 서비스 

hello 분석 및 저장소 인프라 hello 클라우드 또는 온-프레미스 될 수 있습니다. 이는 원시 및 처리된 데이터 집합이 저장되는 위치입니다. 이 인프라는 재현 가능한 분석을 활성화합니다. 또한 불필요 한 인프라 비용 및 tooinconsistencies 될 수 있는 중복을 방지할 수 있습니다. 도구는 tooprovision hello 공유 리소스, 추적 하 고 각 팀 멤버 tooconnect toothose 리소스를 안전 하 게 허용 제공. 프로젝트 멤버가 일관성 있는 계산 환경을 만들도록 하는 것도 좋은 연습입니다. 그러면 다른 팀 멤버는 실험을 복제하고 유효성을 검사할 수 있습니다.

여러 프로젝트에서 작업하고 다양한 클라우드 분석 인프라 구성 요소를 공유하는 팀의 예는 다음과 같습니다.

![TDSP 인프라](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>프로젝트 실행에 대한 도구 및 유틸리티

대부분의 조직에서 프로세스를 소개하는 것은 어렵습니다. 도구는 tooimplement hello 데이터 과학 프로세스 및 수명 주기 hello 일관성의 도입을 증가 시킬 낮은 hello 장벽을 tooand 도움말을 제공 합니다. TDSP 팀 내에서 toojump 시작 단기간 TDSP 초기 집합이 도구 및 스크립트를 제공합니다. 또한 hello hello 데이터 과학 수명 주기 데이터 탐색 및 초기 계획 모델링 등의 일반적인 작업 중 일부를 자동화할 수 있습니다. 개인에 대 한 toocontribute 공유 도구와 유틸리티는 팀의 코드를 공유 저장소로 제공에 잘 정의 된 구조입니다. 이러한 리소스는 다음 hello 팀 또는 hello 조직 내 다른 프로젝트에서 활용할 수 있습니다. 또한 TDSP 도구 및 유틸리티 toohello 전체 커뮤니티의 tooenable hello 기여를 계획합니다. hello TDSP 유틸리티에서 복제할 수 있는 [Github](https://github.com/Azure/Azure-TDSP-Utilities)합니다.


## <a name="next-steps"></a>다음 단계

[데이터 과학 프로세스 팀: 역할 및 작업](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md) hello 핵심 인력 역할 및이 프로세스를 표준화 하는 데이터 과학 팀에 대 한 관련된 작업에 간략하게 설명 합니다. 
