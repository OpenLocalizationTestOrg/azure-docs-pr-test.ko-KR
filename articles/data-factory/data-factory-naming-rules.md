---
title: "Azure Data Factory 엔터티 이름을 지정 하는 것에 대 한 aaaRules | Microsoft Docs"
description: "데이터 팩터리 엔터티에 대한 이름 지정 규칙을 설명합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="593d1-103">Azure Data Factory - 이름 지정 규칙</span><span class="sxs-lookup"><span data-stu-id="593d1-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="593d1-104">다음 표에서 hello 데이터 팩터리 아티팩트의 명명 규칙을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-104">hello following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="593d1-105">이름</span><span class="sxs-lookup"><span data-stu-id="593d1-105">Name</span></span> | <span data-ttu-id="593d1-106">이름 고유성</span><span class="sxs-lookup"><span data-stu-id="593d1-106">Name Uniqueness</span></span> | <span data-ttu-id="593d1-107">유효성 검사</span><span class="sxs-lookup"><span data-stu-id="593d1-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="593d1-108">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="593d1-108">Data Factory</span></span> |<span data-ttu-id="593d1-109">Microsoft Azure에서 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="593d1-110">이름은 대/소문자, 즉, `MyDF` 및 `mydf` toohello 참조 같은 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer toohello same data factory.</span></span> |<ul><li><span data-ttu-id="593d1-111">각 데이터 팩터리는 동 점된 tooexactly 단일 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="593d1-111">Each data factory is tied tooexactly one Azure subscription.</span></span></li><li><span data-ttu-id="593d1-112">개체 이름은 문자 또는 숫자로 시작 해야 하며 문자, 숫자 및 hello 대시 (-) 문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-112">Object names must start with a letter or a number, and can contain only letters, numbers, and hello dash (-) character.</span></span></li><li><span data-ttu-id="593d1-113">모든 대시(-) 문자는 앞뒤에 문자 또는 숫자가 와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="593d1-114">컨테이너 이름에서 연속 대시는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="593d1-115">이름은 3-63자까지 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="593d1-116">연결된 서비스/테이블/파이프라인</span><span class="sxs-lookup"><span data-stu-id="593d1-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="593d1-117">데이터 팩터리에서 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-117">Unique with in a data factory.</span></span> <span data-ttu-id="593d1-118">이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="593d1-119">테이블 이름에서 최대 문자 수는 260개입니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="593d1-120">개체 이름은 문자, 숫자 또는 밑줄(_)로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-120">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="593d1-121">사용할 수 없는 문자: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="593d1-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="593d1-122">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="593d1-122">Resource Group</span></span> |<span data-ttu-id="593d1-123">Microsoft Azure에서 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="593d1-124">이름은 대/소문자를 구분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="593d1-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="593d1-125">최대 문자 수: 1,000개</span><span class="sxs-lookup"><span data-stu-id="593d1-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="593d1-126">이름은 문자, 숫자 및 hello 문자를 포함할 수 있습니다: "-", "_",","및"."</span><span class="sxs-lookup"><span data-stu-id="593d1-126">Name can contain letters, digits, and hello following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

