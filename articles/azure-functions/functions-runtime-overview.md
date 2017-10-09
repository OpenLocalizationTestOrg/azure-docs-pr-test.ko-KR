---
title: "aaaAzure 함수 런타임 개요 | Microsoft Docs"
description: "Hello Azure 함수 런타임 미리 보기의 개요"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Azure Functions 런타임 개요

hello Azure 함수 런타임은 새로운 방법을 제공 하면 tootake hello 단순성 및 활용할 hello Azure 함수의 유연성에 대 한 모델 온-프레미스를 프로그래밍 합니다. Hello 기반 동일 열기 소스 루트 Azure 함수, Azure 함수 런타임은 온-프레미스 배포 tooprovide 거의 동일한 개발 환경을 hello 클라우드 서비스

![Azure Functions 런타임 미리 보기 포털][1]

hello Azure 함수 런타임 toohello 클라우드를 커밋하기 전에 tooexperience Azure 함수에 대 한 방식으로 제공 합니다. 이러한 방식으로 작성 하는 hello 코드 자산 다음 가져올 수 있습니다 toohello 클라우드로 마이그레이션하는 경우.  내 온-프레미스 컴퓨터 toorun 일괄 처리 프로세스의 hello 예비 계산 능력을 사용 하는 등,에 대 한 새 옵션을 hello 런타임도 열립니다. 조직 tooconditionally 송신 데이터 tooother 시스템을 온-프레미스 및 hello 클라우드에서 장치를 사용할 수도 있습니다.

hello Azure 함수 런타임 두 부분으로 구성 됩니다.
* Azure Functions 런타임 관리 역할
* Azure Functions 런타임 작업자 역할

## <a name="azure-functions-management-role"></a>Azure Functions 관리 역할

hello Azure 함수 관리 역할 기능 온-프레미스의 hello 관리에 대 한 호스트를 제공합니다. 이 역할 hello 다음 작업을 수행 합니다.

* Hello에 나와 있는 것 동일한 hello hello는 hello Azure 함수 관리 포털에서의 호스팅을 [Azure 포털](https://portal.azure.com)합니다. 함수를 개발이에서는 hello hello Azure 포털에서에서 사용 하는 방식으로 동일 합니다.
* 여러 함수 작업자 간에 함수 배포
* Microsoft Visual Studio에서 직접 함수를 게시할 수 있도록 게시 끝점 제공

## <a name="azure-functions-worker-role"></a>Azure Functions 작업자 역할

Windows 컨테이너에서 hello Azure 함수 작업자 역할을 배포 하 고이 함수 코드를 실행 합니다.  조직 전체에서 여러 작업자 역할을 배포할 수 있으며 고객이 예비 Compute 능력을 활용할 수 있는 핵심 방법에 해당합니다.

## <a name="minimum-requirements"></a>최소 요구 사항

사용 하는 컴퓨터가 있어야 Azure 함수 런타임 hello로 시작 tooget **Windows Server 2016 또는 Windows 10 작성자가 업데이트** 액세스 tooa와 **SQL Server** 인스턴스.

## <a name="next-steps"></a>다음 단계

Hello 설치 [함수 런타임 Azure 미리 보기](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
