---
title: "데이터 카탈로그 aaaHow toosecure 액세스 tooAzure | Microsoft Docs"
description: "이 문서에 설명 어떻게 toosecure 데이터 카탈로그 및 해당 데이터의 자산입니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d7c35fd57d8add1cdc152b75f111879288e1548f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-access-toodata-catalog-and-data-assets"></a><span data-ttu-id="f5ce1-103">Toosecure는 toodata 카탈로그 및 데이터 자산을 액세스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="f5ce1-103">How toosecure access toodata catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f5ce1-104">이 기능은 Azure Data Catalog hello standard edition 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-104">This feature is available only in hello standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="f5ce1-105">Azure Data Catalog 있습니다 toospecify hello 데이터 카탈로그 및 기능에 액세스할 수 있는 작업 (등록, 주석 달기, 소유권) hello 카탈로그에 대 한 메타 데이터에 대해 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-105">Azure Data Catalog allows you toospecify who can access hello data catalog and what operations (register, annotate, take ownership) they can perform on metadata in hello catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="f5ce1-106">카탈로그 사용자 및 사용 권한</span><span class="sxs-lookup"><span data-stu-id="f5ce1-106">Catalog users and permissions</span></span>
<span data-ttu-id="f5ce1-107">toogive 사용자 또는 그룹 hello tooa 데이터 카탈로그 액세스 및 사용 권한을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-107">toogive a user or a group hello access tooa data catalog and set permissions:</span></span>

1. <span data-ttu-id="f5ce1-108">Hello에 [데이터 카탈로그의 홈 페이지](http://www.azuredatacatalog.com), 클릭 **설정을** hello 도구 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-108">On hello [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on hello toolbar.</span></span>

    ![데이터 카탈로그 - 설정](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="f5ce1-110">Hello 설정 페이지에서 확장 hello **카탈로그 사용자** 섹션.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-110">In hello settings page, expand hello **Catalog Users** section.</span></span>
    <span data-ttu-id="f5ce1-111">![카탈로그 사용자 - 추가](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="f5ce1-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="f5ce1-112">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-112">Click **Add**.</span></span>
4. <span data-ttu-id="f5ce1-113">정규화 된 hello 입력 **사용자 이름** hello의 또는 이름을 **보안 그룹** hello hello 카탈로그와 연결 된 Azure Active Directory (AAD)에서.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-113">Enter hello fully qualified **user name** or name of hello **security group** in hello Azure Active Directory (AAD) associated with hello catalog.</span></span> <span data-ttu-id="f5ce1-114">사용자나 그룹을 둘 이상 추가하는 경우 쉼표(\`,’)를 구분 기호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="f5ce1-115">![카탈로그 사용자 - 사용자 또는 그룹](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="f5ce1-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="f5ce1-116">키를 눌러 **ENTER** 또는 **탭** hello 텍스트 상자를 벗어났습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-116">Press **ENTER** or **TAB** out of hello text box.</span></span> 
6.  <span data-ttu-id="f5ce1-117">확인 하는 모든 사용 권한을 (**주석 달기**, **등록**, 및 **Take Ownership**) toothese 사용자 또는 그룹 기본적으로 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned toothese users or groups by default.</span></span> <span data-ttu-id="f5ce1-118">Hello 사용자 또는 그룹의 수, 즉 [데이터 자산을 등록]( data-catalog-how-to-register.md), [데이터 자산에 주석 달기]( data-catalog-how-to-annotate.md), 및 [데이터 자산의 소유권]( data-catalog-how-to-manage.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-118">That is, hello user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="f5ce1-119">![카탈로그 사용자 - 기본 사용 권한](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="f5ce1-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="f5ce1-120">사용자 또는 그룹 toogive hello 읽기 액세스 toohello 카탈로그의 선택을 취소 hello **주석 달기** 해당 사용자나 그룹에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-120">toogive a user or group only hello read access toohello catalog, clear hello **annotate** option for that user or group.</span></span> <span data-ttu-id="f5ce1-121">이렇게 하면 hello 사용자 또는 그룹에 데이터 자산 hello 카탈로그에 주석을 달 수 없습니다 하지만 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-121">When you do so, hello user or group cannot annotate data assets in hello catalog but they can view them.</span></span> 
8.  <span data-ttu-id="f5ce1-122">toodeny 사용자 또는 그룹의 데이터 자산을 등록 취소 hello **등록** 해당 사용자나 그룹에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-122">toodeny a user or group from registering data assets, clear hello **register** option for that user or group.</span></span>
9.  <span data-ttu-id="f5ce1-123">toodeny 지우기 hello 데이터 자산의 소유권 사용자 **소유권** 해당 사용자나 그룹에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-123">toodeny a user from taking ownership of a data asset, clear hello **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="f5ce1-124">카탈로그 사용자에 게에서 사용자/그룹 toodelete 클릭 **x** hello hello 목록 맨 아래에 hello 사용자/그룹에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-124">toodelete a user/group from catalog users, click **x** for hello user/group at hello bottom of hello list.</span></span> 
    <span data-ttu-id="f5ce1-125">![카탈로그 사용자 - 사용자 삭제](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="f5ce1-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f5ce1-126">추가 사용자가 아닌 보안 그룹 toocatalog 사용자가 직접 추가 사용 권한을 할당 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-126">We recommend that you add security groups toocatalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="f5ce1-127">그런 다음 해당 역할 및 해당 필요한 액세스 toohello 카탈로그와 일치 하는 사용자 toohello 보안 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-127">Then, add users toohello security groups that match their roles and their required access toohello catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="f5ce1-128">특별 고려 사항</span><span class="sxs-lookup"><span data-stu-id="f5ce1-128">Special considerations</span></span>

- <span data-ttu-id="f5ce1-129">hello 사용 권한을 할당 toosecurity 그룹 누적 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-129">hello permissions assigned toosecurity groups are additive.</span></span> <span data-ttu-id="f5ce1-130">예를 들어 사용자가 두 그룹에 속한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-130">Say, a user is in two groups.</span></span> <span data-ttu-id="f5ce1-131">한 그룹에는 주석을 다는 권한이 있고 다른 그룹에는 이 권한이 없다면,</span><span class="sxs-lookup"><span data-stu-id="f5ce1-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="f5ce1-132">사용자는 주석을 달 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="f5ce1-133">hello 사용 권한을 할당 된 사용 권한을 toogroups toowhich hello 사용자가 속한 tooa 사용자 재정의 hello 명시적으로 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-133">hello permissions assigned explicitly tooa user override hello permissions assigned toogroups toowhich hello user belongs.</span></span> <span data-ttu-id="f5ce1-134">Hello 이전 예제에서는 예를 들어, hello 사용자 toocatalog 사용자가 명시적으로 추가 하 고 할당 하지 않으면 권한 주석을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-134">In hello previous example, say, you explicitly added hello user toocatalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="f5ce1-135">hello 사용자 hello 사용자가 없는 그룹의 구성원 권한이 주석을 추가 하는 경우에 데이터 자산에 주석을 달 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f5ce1-135">hello user cannot annotate data assets even though hello user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5ce1-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f5ce1-136">Next steps</span></span>
- [<span data-ttu-id="f5ce1-137">Azure Azure Data Catalog 시작</span><span class="sxs-lookup"><span data-stu-id="f5ce1-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

