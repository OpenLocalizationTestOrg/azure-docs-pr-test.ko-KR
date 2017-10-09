---
title: "B2B-Azure 논리 앱에 대 한 통합 aaaEnterprise | Microsoft Docs"
description: "B2B 워크플로 작성 하 고 엔터프라이즈 통합 팩 hello 사용 하 여 논리 앱에 대 한 엔터프라이즈 통합 시나리오를 지원 합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>개요: B2B 시나리오 및 엔터프라이즈 통합 팩 hello와의 통신

기업 (B2B) 워크플로 및 Azure 논리 앱와 원활 하 게 통신에 대 한 Microsoft의 클라우드 기반 솔루션에서는 엔터프라이즈 통합 팩 hello 엔터프라이즈 통합 시나리오를 사용할 수 있습니다. 조직에서는 다른 프로토콜 및 형식을 사용하더라도 전자 방식으로 메시지를 교환할 수 있습니다. 다양 한 형식 시스템의 조직에서 해석 하 고 처리할 수 있는 한 형식으로 변환 하는 hello 팩. 조직은 [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) 및 [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md)를 비롯한 업계 표준 프로토콜을 통해 메시지를 교환할 수 있습니다. 암호화 및 디지털 서명 둘 다를 사용하여 메시지를 보호할 수 있습니다.

BizTalk Server 또는 Microsoft Azure BizTalk 서비스에 잘 알고 있다면 hello 엔터프라이즈 통합 기능은 쉽게 toouse 대부분 개념 유사 하기 때문에 있습니다. 한 가지 주요 차이점은 엔터프라이즈 통합 통합 계정 toosimplify hello 저장소 및 관리의 B2B 통신에 사용 되는 아티팩트를 사용 하도록 합니다. 

아키텍처 측면에서 엔터프라이즈 통합 팩 hello "통합 계정"은 기반으로 합니다. 이러한 계정은 스키마, 파트너, 인증서, 맵 및 규약 등의 모든 사용자 아티팩트를 저장하는 클라우드 기반 컨테이너입니다. 이러한 아티팩트 toodesign 사용 지정, 배포 및 B2B 응용 프로그램 및 또한 논리 앱에 대 한 toobuild B2B 워크플로 유지 합니다. 하지만 통합 계정 tooyour 논리 앱 전에 이러한 아티팩트를 사용 하려면 먼저 연결 해야 합니다. 그런 후에 논리 앱에서 통합 계정의 아티팩트에 액세스할 수 있습니다.

## <a name="why-should-you-use-enterprise-integration"></a>엔터프라이즈 통합을 사용하는 이유

* 엔터프라이즈 통합을 사용하면 통합 계정에 모든 아티팩트를 저장할 수 있습니다.
* B2B 워크플로 작성 하 고 hello Azure 논리 앱 엔진 및 모든 커넥터를 사용 하 여 제 3 자 소프트웨어 as service (SaaS) 앱, 온-프레미스 응용 프로그램, 사용자 지정 앱와 통합할 수 있습니다.
* Azure Functions를 사용하여 Logic Apps에 대한 사용자 지정 코드를 만들 수 있습니다.

## <a name="how-tooget-started-with-enterprise-integration"></a>Tooget를 어떻게 시작 엔터프라이즈 통합?

빌드하고 hello에 hello 논리가 응용 프로그램 디자이너를 통해 엔터프라이즈 통합 팩 hello 사용 하 여 B2B 앱을 관리할 수 있습니다 **Azure 포털**합니다. [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic Apps PowerShell 항목")을 사용하여 Logic Apps를 관리할 수도 있습니다.

Hello Azure 포털에서에서 앱을 만들기 전에 수행 해야 하는 hello 상위 수준 단계는 다음과 같습니다.

![개요 이미지](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>몇 가지 일반적인 시나리오는 무엇인가요?

엔터프라이즈 통합은 이러한 업계 표준을 지원합니다.

* EDI - 전자 데이터 교환
* EAI - 엔터프라이즈 응용 프로그램 통합

## <a name="heres-what-you-need-tooget-started"></a>여기에 시작 tooget

* 통합 계정을 사용하는 Azure 구독
* Visual Studio 2015 toocreate 맵과 스키마
* [Visual Studio용 Microsoft Azure Logic Apps 엔터프라이즈 통합 도구 2015 2.0](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>지금 평가판 사용

[배포 완벽 하 게 작동 샘플 AS2 송신 및 수신 논리 앱](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) Azure 논리 앱에 대 한 hello B2B 기능을 사용 하는 합니다.

## <a name="learn-more"></a>자세한 정보
* [규약](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")
* [비즈니스 tooBusiness (B2B) 시나리오](../logic-apps/logic-apps-enterprise-integration-b2b.md "학습 방법을 B2B 기능을 사용 하 여 toocreate 논리 앱")  
* [인증서](logic-apps-enterprise-integration-certificates.md "엔터프라이즈 통합 인증서에 대해 알아보기")
* [플랫 파일 인코딩/디코딩](logic-apps-enterprise-integration-flatfile.md "학습 방법을 tooencode 및 플랫 파일 내용을 디코딩")  
* [Integration accounts](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about 통합 계정")
* [맵](../logic-apps/logic-apps-enterprise-integration-maps.md "엔터프라이즈 통합 맵에 대해 알아보기")
* [파트너](logic-apps-enterprise-integration-partners.md "엔터프라이즈 통합 파트너에 대해 알아보기")
* [스키마](logic-apps-enterprise-integration-schemas.md "엔터프라이즈 통합 스키마에 대해 알아보기")
* [XML 메시지 유효성 검사](logic-apps-enterprise-integration-xml.md "논리 앱 toovalidate XML 메시지 하는 방법을 알아봅니다")
* [XML 변환](logic-apps-enterprise-integration-transform.md "엔터프라이즈 통합 맵에 대해 알아보기")
* [엔터프라이즈 통합 커넥터](../connectors/apis-list.md "엔터프라이즈 통합 팩 커넥터에 대해 알아보기")
* [통합 계정 메타데이터](../logic-apps/logic-apps-enterprise-integration-metadata.md "통합 계정 메타데이터에 대해 알아보기")
* [B2B 메시지 모니터링](logic-apps-monitor-b2b-message.md "B2B 메시지를 모니터링하는 방법에 대해 알아보기")
* [OMS 포털에서 B2B 메시지 추적](logic-apps-track-b2b-messages-omsportal.md "OMS 포털에서 B2B 메시지를 추적하는 방법에 대해 알아보기")

