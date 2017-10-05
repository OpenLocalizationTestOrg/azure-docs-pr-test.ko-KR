---
title: "Azure Data Catalog에 대한 액세스를 보호하는 방법 | Microsoft Docs"
description: "이 문서에서는 데이터 카탈로그 및 해당 데이터 자산을 보호하는 방법을 설명합니다."
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
ms.openlocfilehash: 9664a7bc8493b08c8e0797ac6f1b212079829833
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-secure-access-to-data-catalog-and-data-assets"></a><span data-ttu-id="d3ea7-103">데이터 카탈로그 및 데이터 자산에 대한 액세스를 보호하는 방법</span><span class="sxs-lookup"><span data-stu-id="d3ea7-103">How to secure access to data catalog and data assets</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d3ea7-104">이 기능은 Azure Data Catalog 표준 버전에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-104">This feature is available only in the standard edition of Azure Data Catalog.</span></span>

<span data-ttu-id="d3ea7-105">Azure Data Catalog에서 데이터 카탈로그에 액세스할 수 있는 사용자 및 이 사용자가 카탈로그의 메타데이터에 대해 수행할 수 있는 작업(등록, 주석 달기, 소유권 가져오기)을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-105">Azure Data Catalog allows you to specify who can access the data catalog and what operations (register, annotate, take ownership) they can perform on metadata in the catalog.</span></span> 

## <a name="catalog-users-and-permissions"></a><span data-ttu-id="d3ea7-106">카탈로그 사용자 및 사용 권한</span><span class="sxs-lookup"><span data-stu-id="d3ea7-106">Catalog users and permissions</span></span>
<span data-ttu-id="d3ea7-107">사용자나 그룹에 데이터 카탈로그에 대한 액세스 권한을 제공하고 사용 권한을 설정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-107">To give a user or a group the access to a data catalog and set permissions:</span></span>

1. <span data-ttu-id="d3ea7-108">[데이터 카탈로그 홈페이지](http://www.azuredatacatalog.com)에서 도구 모음의 **설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-108">On the [home page of your data catalog](http://www.azuredatacatalog.com),  click **Settings** on the toolbar.</span></span>

    ![데이터 카탈로그 - 설정](media/data-catalog-how-to-secure-catalog/data-catalog-settings.png)
2. <span data-ttu-id="d3ea7-110">[설정] 페이지에서 **카탈로그 사용자** 섹션을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-110">In the settings page, expand the **Catalog Users** section.</span></span>
    <span data-ttu-id="d3ea7-111">![카탈로그 사용자 - 추가](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span><span class="sxs-lookup"><span data-stu-id="d3ea7-111">![Catalog Users - Add](media/data-catalog-how-to-secure-catalog/data-catalog-add-button.png)</span></span>
3. <span data-ttu-id="d3ea7-112">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-112">Click **Add**.</span></span>
4. <span data-ttu-id="d3ea7-113">정규화된 **사용자 이름**이나 카탈로그와 연결된 AAD(Azure Active Directory)의 **보안 그룹** 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-113">Enter the fully qualified **user name** or name of the **security group** in the Azure Active Directory (AAD) associated with the catalog.</span></span> <span data-ttu-id="d3ea7-114">사용자나 그룹을 둘 이상 추가하는 경우 쉼표(\`,’)를 구분 기호로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-114">Use comma (\`,’) as a separator if you are adding more than one user or group.</span></span>
    <span data-ttu-id="d3ea7-115">![카탈로그 사용자 - 사용자 또는 그룹](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span><span class="sxs-lookup"><span data-stu-id="d3ea7-115">![Catalog Users - users or groups](media/data-catalog-how-to-secure-catalog/data-catalog-users-groups.png)</span></span>
5. <span data-ttu-id="d3ea7-116">**Enter** 키나 **Tab** 키를 눌러 텍스트 상자 밖으로 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-116">Press **ENTER** or **TAB** out of the text box.</span></span> 
6.  <span data-ttu-id="d3ea7-117">모든 사용 권한(**주석 달기**, **등록** 및 **소유권 가져오기**)이 이러한 사용자나 그룹에 기본적으로 할당되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-117">Confirm that all permissions (**Annotate**, **Register**, and **Take Ownership**) are assigned to these users or groups by default.</span></span> <span data-ttu-id="d3ea7-118">즉, 사용자나 그룹이 [데이터 자산을 등록]( data-catalog-how-to-register.md)하고, [데이터 자산에 주석을 달고]( data-catalog-how-to-annotate.md), [데이터 자산에 대한 소유권을 가져올]( data-catalog-how-to-manage.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-118">That is, the user or group can [register data assets]( data-catalog-how-to-register.md), [annotate data assets]( data-catalog-how-to-annotate.md), and [take ownership of data assets]( data-catalog-how-to-manage.md).</span></span> 
    <span data-ttu-id="d3ea7-119">![카탈로그 사용자 - 기본 사용 권한](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="d3ea7-119">![Catalog Users - default permissions](media/data-catalog-how-to-secure-catalog/data-catalog-default-permissions.png)</span></span>
7.  <span data-ttu-id="d3ea7-120">사용자 또는 그룹에 카탈로그에 대한 읽기 권한만 부여하려면 사용자나 그룹의 **주석 달기** 옵션을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-120">To give a user or group only the read access to the catalog, clear the **annotate** option for that user or group.</span></span> <span data-ttu-id="d3ea7-121">그러면 사용자나 그룹이 카탈로그의 데이터 자산에 주석을 달 수 없지만 볼 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-121">When you do so, the user or group cannot annotate data assets in the catalog but they can view them.</span></span> 
8.  <span data-ttu-id="d3ea7-122">사용자 또는 그룹이 데이터 자산을 등록하지 못하게 하려면 해당 사용자나 그룹의 **등록** 옵션을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-122">To deny a user or group from registering data assets, clear the **register** option for that user or group.</span></span>
9.  <span data-ttu-id="d3ea7-123">사용자가 데이터 자산의 소유권을 가져오지 못하게 하려면 해당 사용자나 그룹의 **소유권 가져오기** 옵션을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-123">To deny a user from taking ownership of a data asset, clear the **take ownership** option for that user or group.</span></span> 
10. <span data-ttu-id="d3ea7-124">카탈로그 사용자에서 사용자/그룹을 삭제하려면 목록 아래쪽에서 사용자/그룹에 대해 **x**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-124">To delete a user/group from catalog users, click **x** for the user/group at the bottom of the list.</span></span> 
    <span data-ttu-id="d3ea7-125">![카탈로그 사용자 - 사용자 삭제](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="d3ea7-125">![Catalog Users - delete user](media/data-catalog-how-to-secure-catalog/data-catalog-delete-user.png)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d3ea7-126">사용자를 직접 추가하고 사용 권한을 할당하기보다는 카탈로그 사용자에 보안 그룹을 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-126">We recommend that you add security groups to catalog users rather than adding users directly and assign permissions.</span></span> <span data-ttu-id="d3ea7-127">그런 다음, 사용자의 역할과 사용자에게 필요한 카탈로그에 대한 액세스 권한과 일치하는 보안 그룹에 사용자를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-127">Then, add users to the security groups that match their roles and their required access to the catalog.</span></span>

## <a name="special-considerations"></a><span data-ttu-id="d3ea7-128">특별 고려 사항</span><span class="sxs-lookup"><span data-stu-id="d3ea7-128">Special considerations</span></span>

- <span data-ttu-id="d3ea7-129">보안 그룹에 할당되는 권한은 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-129">The permissions assigned to security groups are additive.</span></span> <span data-ttu-id="d3ea7-130">예를 들어 사용자가 두 그룹에 속한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-130">Say, a user is in two groups.</span></span> <span data-ttu-id="d3ea7-131">한 그룹에는 주석을 다는 권한이 있고 다른 그룹에는 이 권한이 없다면,</span><span class="sxs-lookup"><span data-stu-id="d3ea7-131">One group has annotate permissions and other group does not have annotate permissions.</span></span> <span data-ttu-id="d3ea7-132">사용자는 주석을 달 수 있는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-132">Then, user has annotate permissions.</span></span> 
- <span data-ttu-id="d3ea7-133">사용자에게 명시적으로 할당된 사용 권한이 사용자가 속한 그룹에 할당된 사용 권한을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-133">The permissions assigned explicitly to a user override the permissions assigned to groups to which the user belongs.</span></span> <span data-ttu-id="d3ea7-134">앞의 예에서 사용자를 카탈로그 사용자에 명시적으로 추가했고 주석 달기 권한은 할당하지 않는다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-134">In the previous example, say, you explicitly added the user to catalog users and do not assign annotate permissions.</span></span> <span data-ttu-id="d3ea7-135">이 경우 사용자는 주석 달기 권한이 있는 그룹의 구성원이지만 데이터 자산에 주석을 달 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d3ea7-135">The user cannot annotate data assets even though the user is a member of a group that does have annotate permissions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3ea7-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3ea7-136">Next steps</span></span>
- [<span data-ttu-id="d3ea7-137">Azure Azure Data Catalog 시작</span><span class="sxs-lookup"><span data-stu-id="d3ea7-137">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)

