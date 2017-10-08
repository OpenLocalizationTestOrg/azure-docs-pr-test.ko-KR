---
title: "Azure 서버가 없는의 aaaOverview | Microsoft Docs"
description: "Hello 클라우드에서 인프라에 대 한 toothink 필요 없이 강력한 솔루션을 만듭니다."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>함수 및 Logic Apps로 Azure 서버를 사용하지 않음 개요

서버를 사용하지 않는 응용 프로그램은 개발 속도 향상, 필요한 코드 감소 및 규모 간소화의 이점을 제공합니다.  이 문서는 서버가 없는 솔루션 및 Azure 서버가 없는 제품의 hello 서로 다른 특성으로 이동합니다.

## <a name="what-is-serverless"></a>서버를 사용하지 않음은 무엇입니까?

서버 없이 서버가 없는-할 hello 개발자는 서버에 대 한 tooworry 없는 것은 아닙니다.  기존 응용 프로그램 개발 중 많은 부분 크기 조정, 호스팅 및 모니터링 hello 응용 프로그램의 솔루션 toomeet hello 요구 질문에 대답 됩니다.  서버 없이와 이러한 질문은 자동으로 처리 hello 솔루션의 일부로 합니다.  또한 서버를 사용하지 않는 응용 프로그램은 사용량 기반 계획에 대해 요금이 청구됩니다.  Hello 응용 프로그램은 사용 되지 않거나, 충전 발생 되지 않습니다.  이러한 기능을 사용 하면 개발자가 toofocus hello 솔루션의 hello 비즈니스 논리에만 전적으로 합니다.

서버 없이 주위 Azure의 hello 핵심 서비스는 [Azure 함수](https://azure.microsoft.com/services/functions/) 및 [Azure 논리 앱](https://azure.microsoft.com/services/logic-apps/)합니다.  이러한 두 가지이 솔루션 위의 hello 원칙을 따르는 및 개발자가 최소한의 코드로 toobuild 강력한 클라우드 응용 프로그램을 허용 합니다.

## <a name="what-are-azure-functions"></a>Azure Functions란?

Azure 함수 hello 클라우드에서 쉽게 소량의 코드 또는 "기능"을 실행 하기 위한 솔루션을입니다. 전체 응용 프로그램이 나 hello 인프라 toorun에 대 한 걱정 없이, hello 문제에 대 한 필요한 hello 코드만 작성할 수 있습니다. Functions는 개발 생산성을 높일 수 있으며 C#, F#, Node.js, Python, PHP 등의 원하는 개발 언어를 사용할 수 있습니다. 코드를 실행 하는 hello 시간에 대해서만 비용을 지불 하 고 필요에 따라 Azure 확장입니다.

Toojump 오른쪽 사용할 Azure 함수 시작 하는 경우 시작 [사용자 첫 번째 Azure 함수를 만들어](../azure-functions/functions-create-first-azure-function.md)합니다. 함수에 대 한 자세한 기술 정보를 찾고 hello 참조 [개발자 참조](../azure-functions/functions-reference.md)합니다.

## <a name="what-are-azure-logic-apps"></a>Azure Logic Apps란?

Azure 논리 앱 방식으로 toosimplify 제공 하 고 hello 클라우드에서 확장 가능한 통합 및 워크플로 구현 합니다. 비주얼 디자이너 toomodel 제공 하며 일련의 워크플로 호출 하는 단계로 프로세스를 자동화 합니다.  [많은 커넥터](../connectors/apis-list.md) tooquickly 클라우드 및 온-프레미스 서비스에서 응용 프로그램 서버가 없는 tooother Api를 연결 합니다.  논리 앱 트리거 (like '계정을 tooDynamics CRM가 추가 하 고' 하는 경우)로 시작 후 여러 조합 작업, 변환 및 조건 논리 실행을 시작할 수 있습니다.  논리 앱이 hello 프로세스 외부 시스템 또는 API와의 상호 작용 해야 하는 경우에 특히-프로세스에서 다양 한 Azure 기능을 조정 하는 경우 최선의 선택 합니다.

논리 앱 tooget 시작, 시작 [첫 번째 논리 앱을 만드는](logic-apps-create-a-logic-app.md)합니다.  논리 앱에 대 한 자세한 기술 정보를 찾고 hello 참조 [개발자 참조](logic-apps-workflow-actions-triggers.md)합니다.

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>Azure에서 서버를 사용하지 않는 응용 프로그램을 빌드 및 배포하려면 어떻게 해야 합니까?

Azure는 서버를 사용하지 않는 앱의 개발, 배포 및 관리에 대한 풍부한 도구 집합을 제공합니다.  사용 하거나 hello Azure 포털에서 직접 앱을 빌드할 수 [Visual Studio에서 tooling](logic-apps-serverless-get-started-vs.md)합니다.  응용 프로그램이 개발되면 [즉시 배포](logic-apps-create-deploy-template.md)될 수 있습니다.  Azure는 또한 서버를 사용하지 않는 앱에 대한 모니터링을 제공합니다.  이 모니터링 하는 hello 또는 통합된 도구 tooOMS 및 Application Insights hello API 또는 Sdk를 통해 Azure 포털에서에서 액세스할 수 있습니다.

## <a name="next-steps"></a>다음 단계

* [Visual Studio에서 서버를 사용하지 않는 앱 빌드 시작](logic-apps-serverless-get-started-vs.md)
* [서버를 사용하지 않는 Customer Insights 대시보드 만들기](logic-apps-scenario-social-serverless.md)
* [논리 앱에 대한 배포 템플릿 빌드](logic-apps-create-deploy-template.md)