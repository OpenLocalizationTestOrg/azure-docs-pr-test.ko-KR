---
title: "aaaHow toomigrate 논리 앱 tooschema 버전 2015-08-01-미리 보기 | Microsoft Docs"
description: "논리 앱 toohello 최신 스키마 버전을 쉽게 마이그레이션할 수 있습니다. 다음 단계를 수행합니다."
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="d190d-104">어떻게 toomigrate 논리 앱 tooschema 버전 2015-08-01-미리 보기</span><span class="sxs-lookup"><span data-stu-id="d190d-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="d190d-105">toomove 기존 논리 앱 toohello 새 스키마를 따르는 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d190d-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="d190d-106">Hello Azure 포털에서에서 논리 앱을 열으십시오</span><span class="sxs-lookup"><span data-stu-id="d190d-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="d190d-107">스키마 업데이트를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d190d-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="d190d-108">![API 아이콘][step1] </span><span class="sxs-lookup"><span data-stu-id="d190d-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="d190d-109">hello 스키마 업데이트 페이지에 표시 되며 hello 새 스키마에 hello 향상 된 기능에 세부 정보를 제공 하는 링크 tooa 문서를: ![API 아이콘][step2]</span><span class="sxs-lookup"><span data-stu-id="d190d-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="d190d-110">선택 하는 경우 **스키마 업데이트**,에서는 자동으로 hello 마이그레이션 단계를 실행 하 고 hello 코드 출력을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d190d-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="d190d-111">그러나이 tooupdate 정의 사용, hello에 설명 된 같은 좋은 코딩 방법에 따라 수 **모범 사례** 아래 섹션.</span><span class="sxs-lookup"><span data-stu-id="d190d-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="d190d-112">논리 앱 toohello 최신 스키마 버전을 마이그레이션할 때 모범 사례:</span><span class="sxs-lookup"><span data-stu-id="d190d-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="d190d-113">복사 hello 마이그레이션 스크립트 tooa 새로운 논리 앱-hello 이전 테스트 및 확인 된 hello 마이그레이션된 응용 프로그램을 완료 한이 예상 대로 작동을 덮어쓰지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d190d-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="d190d-114">프로덕션에 배치하기 **전에** 논리 앱을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d190d-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="d190d-115">마이그레이션을 완료 한 후 업데이트 하 여 논리 앱 toouse hello 시작 [관리 되는 Api](apis-list.md) 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="d190d-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="d190d-116">예를 들어 DropBox v1을 사용하는 경우 Dropbox v2를 사용하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d190d-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="d190d-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d190d-117">What's next</span></span>
* [<span data-ttu-id="d190d-118">Toomanually 논리 앱을 마이그레이션 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="d190d-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






