---
title: "Azure 앱 서비스의 aaaWebJobs"
description: "WebJobs toorun 배경 toobuild 테스트 하는 방법에 대해 알아봅니다, 그리고 저장소 및 서비스 버스와 같은 서비스와 상호 작용 및 예약 된 작업을 만듭니다."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a>Azure 앱 서비스에서 WebJobs 사용
이 문서 연결 방법에 대 한 리소스 toodocumentation toouse Azure WebJobs Azure WebJobs SDK hello 및 합니다. Azure WebJobs 쉽게 toorun 스크립트를 제공 하거나으로 프로그램에서 프로세스를 백그라운드 [앱 서비스 웹 앱](http://go.microsoft.com/fwlink/?LinkId=529714)합니다. cmd, bat, exe(.NET), ps1, sh, php, py, js 및 jar와 같은 실행 파일을 업로드하고 실행할 수 있습니다. 이러한 프로그램은 일정에 따라(cron) 또는 지속적으로 WebJob으로 실행됩니다.

WebJobs SDK hello Azure 저장소 보다 쉽게 toouse가 있습니다. hello WebJobs SDK는 한 바인딩 및 서비스 버스 큐 뿐만 아니라 Microsoft Azure 저장소 Blob, 큐 및 테이블을 사용 하는 트리거 시스템에 있습니다.

Visual Studio의 통합 도구를 사용하면 WebJob을 원활하게 만들고, 배포하고, 관리할 수 있습니다. 템플릿에서 WebJob을 만들고, 게시하고 관리(실행/중지/모니터링/디버깅)할 수 있습니다.

hello Azure 포털에서에서 WebJobs 대시보드 hello hello hello 기능 tooinvoke WebJobs 내에서 개별 기능을 포함 하 여 WebJobs 실행에 대 한 모든 권한을 제공 하는 강력한 관리 기능을 제공 합니다. hello 대시보드 함수 런타임 및 로깅 출력에도 표시 됩니다.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

