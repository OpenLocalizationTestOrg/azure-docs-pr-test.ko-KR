---
title: "IntelliJ에 대 한 Azure 탐색기 hello aaaManaging Redis 캐시를 사용 하 여 | Microsoft Docs"
description: "Toomanage 프로그램 Azure redis 캐시 하는 방식을 IntelliJ 용 hello Azure 탐색기를 사용 하 여에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: 76ba37a2a35c26d0045e17003181108992eb957d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-intellij"></a>Redis 캐시 IntelliJ 용 hello Azure 탐색기를 사용 하 여 관리

hello hello IntelliJ 용 Azure 도구 키트의 일부인 Java 개발자가 사용 하기 쉬운 솔루션 내에서 Azure 계정과에 캐시가 redis 관리에 대 한 hello IntelliJ IDE를 제공 하는 Azure 탐색기.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>IntelliJ를 사용하여 Redis Cache 만들기

단계를 수행 하는 hello 과정을 단계별로 hello 단계 toocreate hello Azure 탐색기를 사용 하 여 redis 캐시 합니다.

1. Tooyour hello hello 단계를 사용 하는 Azure 계정 로그인 [hello IntelliJ 용 Azure 도구 키트에 대 한 로그인에 지침] 문서.

1. Hello에 **Azure 탐색기** 도구 창, hello 확장 **Azure** 노드를 마우스 오른쪽 단추로 클릭 **Redis 캐시**, 클릭 하 고 **Create Redis Cache**합니다.

   ![Redis Cache 만들기 메뉴][CR01]

1. Hello 때 **새 Redis 캐시** hello 다음 옵션을 지정 대화 상자가 나타납니다.

   ![새 Redis Cache 만들기 대화 상자][CR02]

   a. **DNS 이름**: 너무 앞에 추가 됩니다 hello 새 redis 캐시에 대 한 hello DNS 하위 도메인을 지정 ". redis.cache.windows.net"; 예: *wingtiptoys.redis.cache.windows.net*합니다.

   b. **구독**: hello toouse hello 새 redis 캐시에 사용할 Azure 구독을 지정 합니다.

   c. **리소스 그룹**: redis 캐시에 대 한 hello 리소스 그룹을 지정 합니다. 즉 hello 다음 옵션 중 하나를 toochoose 필요:
      * **새로 만들기**: toocreate 새 리소스 그룹 한다고 지정 합니다.
      * **기존 그룹 사용**: Azure 계정과 연결된 리소스 그룹 목록에서 선택하도록 지정합니다.

   d. **위치**: redis 캐시를 만들 위치; hello 위치를 지정 예를 들어 *West US*합니다.

   e. **가격 책정 계층**: redis 캐시를 사용 하는 가격 책정 계층을 지정 5d;이 설정은 hello 클라이언트 연결 수를 결정 합니다. 자세한 내용은 [Redis Cache 가격]을 참조하세요.

   f. **비SSL 포트**: Redis Cache에서 비SSL 연결을 허용하는지 여부를 지정합니다. 기본적으로 SSL 연결만 허용됩니다.

1. 모든 Redis Cache 설정을 지정한 후 **확인**을 클릭합니다.

Redis 캐시를 만든 후 hello Azure 탐색기에에서 표시 됩니다.

   ![Azure 탐색기의 Redis Cache][CR03]

> [!NOTE]
>
> Redis cache 설정 Azure를 구성 하는 방법에 대 한 자세한 내용은 참조 하십시오. [어떻게 tooconfigure Azure Redis Cache]합니다.
>

## <a name="display-hello-properties-for-your-redis-cache-in-intellij"></a>IntelliJ에서 Redis 캐시에 대 한 hello 속성을 표시 합니다.

1. 에 Azure 탐색기 hello redis 캐시를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성 표시**합니다.

   ![Redis 캐시에 대 한 azure 탐색기 상황에 맞는 메뉴 toodisplay 속성][SP01]

1. hello Azure 탐색기 redis 캐시에 대 한 hello 속성을 표시합니다.

   ![Redis Cache 속성][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>IntelliJ를 사용하여 Redis Cache 삭제

1. 에 Azure 탐색기 hello redis 캐시를 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제**합니다.

   ![Azure 탐색기 상황에 맞는 메뉴 toodelete redis 캐시][DE01]

1. 클릭 **예** 때 toodelete redis 캐시 라는 메시지가 표시 됩니다.

   ![Redis Cache 삭제 프롬프트][DE02]

## <a name="next-steps"></a>다음 단계

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Azure redis 캐시, 구성 설정 및 가격에 대 한 자세한 내용은 hello 다음 링크 참조:

* [Azure Redis 캐시(영문)]
* [Redis Cache 설명서]
* [Redis Cache 가격]
* [어떻게 tooconfigure Azure Redis Cache]

<!-- URL List -->

[Redis Cache 가격]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis 캐시(영문)]: https://azure.microsoft.com/services/cache/
[Redis Cache 설명서]: ./redis-cache/index.md
[어떻게 tooconfigure Azure Redis Cache]: ./redis-cache/cache-configure.md
[hello IntelliJ 용 Azure 도구 키트에 대 한 로그인에 지침]: ./azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
