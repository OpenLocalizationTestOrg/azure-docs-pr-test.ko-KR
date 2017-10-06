---
title: "데이터 레이크 저장소의 액세스 제어의 aaaOverview | Microsoft Docs"
description: "Azure Data Lake Store에서 액세스 제어가 작동하는 방식을 이해합니다."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="0b8f4-103">Azure Data Lake Store에서 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="0b8f4-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="0b8f4-104">Azure 데이터 레이크 저장소 hello POSIX 액세스 제어 모델에서 파생 HDFS에서 파생 되는 액세스 제어 모델을 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from hello POSIX access control model.</span></span> <span data-ttu-id="0b8f4-105">이 문서에 데이터 레이크 저장소에 대 한 hello 액세스 제어 모델의 기본 사항 hello 요약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-105">This article summarizes hello basics of hello access control model for Data Lake Store.</span></span> <span data-ttu-id="0b8f4-106">hello HDFS 액세스 제어 모델에 대해 자세히 toolearn 참조 [HDFS 권한을 가이드](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-106">toolearn more about hello HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="0b8f4-107">파일 및 폴더에 대한 액세스 제어 목록</span><span class="sxs-lookup"><span data-stu-id="0b8f4-107">Access control lists on files and folders</span></span>

<span data-ttu-id="0b8f4-108">**액세스 ACL** 및 **기본 ACL**이라는 두 가지 ACL(액세스 제어 목록)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="0b8f4-109">**Acl 액세스**: 이러한 컨트롤 액세스 tooan 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-109">**Access ACLs**: These control access tooan object.</span></span> <span data-ttu-id="0b8f4-110">파일과 폴더에는 모두 액세스 ACL이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="0b8f4-111">**기본 Acl**:는 "템플릿" Acl의 해당 폴더 아래에 만들어진 모든 자식 항목에 대 한 hello 액세스 Acl을 결정 하는 폴더와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine hello Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="0b8f4-112">파일에는 기본 ACL이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="0b8f4-114">액세스 Acl와 기본 Acl이 hello 있는 동일한 구조입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-114">Both Access ACLs and Default ACLs have hello same structure.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="0b8f4-116">부모의 기본 ACL 변경 hello hello ACL 액세스 또는 이미 존재 하는 자식 항목의 기본 ACL 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-116">Changing hello Default ACL on a parent does not affect hello Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="0b8f4-117">사용자 및 ID</span><span class="sxs-lookup"><span data-stu-id="0b8f4-117">Users and identities</span></span>

<span data-ttu-id="0b8f4-118">모든 파일 및 폴더에는 이러한 ID에 대한 고유한 사용 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="0b8f4-119">hello 파일의 사용자를 소유 하는 hello</span><span class="sxs-lookup"><span data-stu-id="0b8f4-119">hello owning user of hello file</span></span>
* <span data-ttu-id="0b8f4-120">hello 소유 그룹</span><span class="sxs-lookup"><span data-stu-id="0b8f4-120">hello owning group</span></span>
* <span data-ttu-id="0b8f4-121">명명된 사용자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-121">Named users</span></span>
* <span data-ttu-id="0b8f4-122">명명된 그룹</span><span class="sxs-lookup"><span data-stu-id="0b8f4-122">Named groups</span></span>
* <span data-ttu-id="0b8f4-123">기타 모든 사용자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-123">All other users</span></span>

<span data-ttu-id="0b8f4-124">사용자 및 그룹의 hello id에는 Azure Active Directory (Azure AD) id가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-124">hello identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="0b8f4-125">","의 사용자 데이터 레이크 저장소의 hello 컨텍스트 수, 하나는 Azure AD 사용자 또는 Azure AD 보안 그룹 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-125">So unless otherwise noted, a "user," in hello context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="0b8f4-126">권한</span><span class="sxs-lookup"><span data-stu-id="0b8f4-126">Permissions</span></span>

<span data-ttu-id="0b8f4-127">파일 시스템 개체에 hello 권한이 **읽기**, **쓰기**, 및 **Execute**, 다음 표에 hello와 같이 파일 및 폴더에 사용할 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="0b8f4-127">hello permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in hello following table:</span></span>

|            |    <span data-ttu-id="0b8f4-128">파일</span><span class="sxs-lookup"><span data-stu-id="0b8f4-128">File</span></span>     |   <span data-ttu-id="0b8f4-129">폴더</span><span class="sxs-lookup"><span data-stu-id="0b8f4-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="0b8f4-130">**읽기(R)**</span><span class="sxs-lookup"><span data-stu-id="0b8f4-130">**Read (R)**</span></span> | <span data-ttu-id="0b8f4-131">파일의 hello 내용을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-131">Can read hello contents of a file</span></span> | <span data-ttu-id="0b8f4-132">필요한 **읽기** 및 **Execute** toolist hello 내용의 hello 폴더</span><span class="sxs-lookup"><span data-stu-id="0b8f4-132">Requires **Read** and **Execute** toolist hello contents of hello folder</span></span>|
| <span data-ttu-id="0b8f4-133">**쓰기(W)**</span><span class="sxs-lookup"><span data-stu-id="0b8f4-133">**Write (W)**</span></span> | <span data-ttu-id="0b8f4-134">쓰거나 tooa 파일을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-134">Can write or append tooa file</span></span> | <span data-ttu-id="0b8f4-135">필요한 **쓰기** 및 **Execute** toocreate 자식 폴더에에서 있는 항목</span><span class="sxs-lookup"><span data-stu-id="0b8f4-135">Requires **Write** and **Execute** toocreate child items in a folder</span></span> |
| <span data-ttu-id="0b8f4-136">**실행(X)**</span><span class="sxs-lookup"><span data-stu-id="0b8f4-136">**Execute (X)**</span></span> | <span data-ttu-id="0b8f4-137">데이터 레이크 저장소의 hello 컨텍스트에서 모든 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-137">Does not mean anything in hello context of Data Lake Store</span></span> | <span data-ttu-id="0b8f4-138">폴더의 필요한 tootraverse hello 자식 항목</span><span class="sxs-lookup"><span data-stu-id="0b8f4-138">Required tootraverse hello child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="0b8f4-139">사용 권한에 대한 짧은 형식</span><span class="sxs-lookup"><span data-stu-id="0b8f4-139">Short forms for permissions</span></span>

<span data-ttu-id="0b8f4-140">**RWX** 가 사용 되는 tooindicate **읽기, 쓰기 + 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-140">**RWX** is used tooindicate **Read + Write + Execute**.</span></span> <span data-ttu-id="0b8f4-141">더 압축 된 숫자 형식에는 존재 **읽기 = 4**, **쓰기 = 2**, 및 **Execute = 1**, hello 합 hello 사용 권한을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, hello sum of which represents hello permissions.</span></span> <span data-ttu-id="0b8f4-142">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-142">Following are some examples.</span></span>

| <span data-ttu-id="0b8f4-143">숫자 형식</span><span class="sxs-lookup"><span data-stu-id="0b8f4-143">Numeric form</span></span> | <span data-ttu-id="0b8f4-144">짧은 형식</span><span class="sxs-lookup"><span data-stu-id="0b8f4-144">Short form</span></span> |      <span data-ttu-id="0b8f4-145">의미</span><span class="sxs-lookup"><span data-stu-id="0b8f4-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="0b8f4-146">7</span><span class="sxs-lookup"><span data-stu-id="0b8f4-146">7</span></span>            | <span data-ttu-id="0b8f4-147">RWX</span><span class="sxs-lookup"><span data-stu-id="0b8f4-147">RWX</span></span>        | <span data-ttu-id="0b8f4-148">읽기 + 쓰기 + 실행</span><span class="sxs-lookup"><span data-stu-id="0b8f4-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="0b8f4-149">5</span><span class="sxs-lookup"><span data-stu-id="0b8f4-149">5</span></span>            | <span data-ttu-id="0b8f4-150">R-X</span><span class="sxs-lookup"><span data-stu-id="0b8f4-150">R-X</span></span>        | <span data-ttu-id="0b8f4-151">읽기 + 실행</span><span class="sxs-lookup"><span data-stu-id="0b8f4-151">Read + Execute</span></span>         |
| <span data-ttu-id="0b8f4-152">4</span><span class="sxs-lookup"><span data-stu-id="0b8f4-152">4</span></span>            | <span data-ttu-id="0b8f4-153">R--</span><span class="sxs-lookup"><span data-stu-id="0b8f4-153">R--</span></span>        | <span data-ttu-id="0b8f4-154">읽기</span><span class="sxs-lookup"><span data-stu-id="0b8f4-154">Read</span></span>                   |
| <span data-ttu-id="0b8f4-155">0</span><span class="sxs-lookup"><span data-stu-id="0b8f4-155">0</span></span>            | ---        | <span data-ttu-id="0b8f4-156">사용 권한 없음</span><span class="sxs-lookup"><span data-stu-id="0b8f4-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="0b8f4-157">사용 권한은 상속하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-157">Permissions do not inherit</span></span>

<span data-ttu-id="0b8f4-158">데이터 레이크 저장소에서 사용 되는 hello POSIX 스타일 모델에서 항목에 대 한 권한은 hello 항목 자체에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-158">In hello POSIX-style model that's used by Data Lake Store, permissions for an item are stored on hello item itself.</span></span> <span data-ttu-id="0b8f4-159">즉, 항목에 대 한 권한은 hello 구성 항목은 부모에서 상속할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-159">In other words, permissions for an item cannot be inherited from hello parent items.</span></span>

## <a name="common-scenarios-related-toopermissions"></a><span data-ttu-id="0b8f4-160">일반적인 시나리오 관련된 toopermissions</span><span class="sxs-lookup"><span data-stu-id="0b8f4-160">Common scenarios related toopermissions</span></span>

<span data-ttu-id="0b8f4-161">다음은 사용 권한을 이해 몇 가지 일반적인 시나리오 toohelp tooperform 데이터 레이크 저장소 계정에 대해 특정 작업을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-161">Following are some common scenarios toohelp you understand which permissions are needed tooperform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-tooread-a-file"></a><span data-ttu-id="0b8f4-162">사용 권한 tooread 파일 필요</span><span class="sxs-lookup"><span data-stu-id="0b8f4-162">Permissions needed tooread a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="0b8f4-164">Hello 파일 toobe 읽기에 대 한 호출자에 게 요구 hello **읽기** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-164">For hello file toobe read, hello caller needs **Read** permissions.</span></span>
* <span data-ttu-id="0b8f4-165">모든 hello 폴더 구조의 폴더에에서 hello 파일을 포함 하는 hello에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-165">For all hello folders in hello folder structure that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-tooappend-tooa-file"></a><span data-ttu-id="0b8f4-166">사용 권한 tooappend tooa 파일 필요</span><span class="sxs-lookup"><span data-stu-id="0b8f4-166">Permissions needed tooappend tooa file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="0b8f4-168">Hello 파일 toobe에 추가에 대 한 hello 호출자에 게 요구 **쓰기** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-168">For hello file toobe appended to, hello caller needs **Write** permissions.</span></span>
* <span data-ttu-id="0b8f4-169">모든 hello hello 파일을 포함 하는 폴더에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-169">For all hello folders that contain hello file, hello caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-toodelete-a-file"></a><span data-ttu-id="0b8f4-170">사용 권한 toodelete 파일 필요</span><span class="sxs-lookup"><span data-stu-id="0b8f4-170">Permissions needed toodelete a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="0b8f4-172">Hello 상위 폴더에 대 한 호출자에 게 요구 hello **쓰기 / 실행** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-172">For hello parent folder, hello caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="0b8f4-173">Hello 파일의 경로 있는 다른 폴더를 hello 모두에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-173">For all hello other folders in hello file’s path, hello caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="0b8f4-174">사용할 수 없는 것으로 hello 두 이전 조건이 충족 되는 필수 toodelete hello 파일에 대 한 권한이 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-174">Write permissions on hello file are not required toodelete it as long as hello previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a><span data-ttu-id="0b8f4-175">사용 권한 필요 tooenumerate 폴더</span><span class="sxs-lookup"><span data-stu-id="0b8f4-175">Permissions needed tooenumerate a folder</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="0b8f4-177">Hello 폴더 tooenumerate에 대 한 호출자에 게 요구 hello **읽기 + Execute** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-177">For hello folder tooenumerate, hello caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="0b8f4-178">상위 폴더를 hello 모두에 대 한 hello 호출자에 게 요구 **Execute** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-178">For all hello ancestor folders, hello caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-hello-azure-portal"></a><span data-ttu-id="0b8f4-179">Hello Azure 포털에서에서 사용 권한 보기</span><span class="sxs-lookup"><span data-stu-id="0b8f4-179">Viewing permissions in hello Azure portal</span></span>

<span data-ttu-id="0b8f4-180">Hello에서 **데이터 탐색기** hello Data Lake 저장소 계정이의 블레이드에서 클릭 **액세스** toosee hello Acl 파일 또는 폴더에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-180">From hello **Data Explorer** blade of hello Data Lake Store account, click **Access** toosee hello ACLs for a file or a folder.</span></span> <span data-ttu-id="0b8f4-181">클릭 **액세스** hello에 대 한 Acl toosee hello **카탈로그** hello 아래에 폴더 **mydatastore** 계정.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-181">Click **Access** toosee hello ACLs for hello **catalog** folder under hello **mydatastore** account.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="0b8f4-183">이 블레이드를 hello 맨 위 섹션에 있는 hello 사용 권한 개요를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-183">On this blade, hello top section shows an overview of hello permissions that you have.</span></span> <span data-ttu-id="0b8f4-184">(Hello 스크린 샷 hello 사용자 Bob입니다.) 그런 다음, hello 액세스 권한은 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-184">(In hello screenshot, hello user is Bob.) Following that, hello access permissions are shown.</span></span> <span data-ttu-id="0b8f4-185">Hello에서 그 후 **액세스** 블레이드에서 클릭 **간단한 보기** toosee hello 간단한 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-185">After that, from hello **Access** blade, click **Simple View** toosee hello simpler view.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="0b8f4-187">클릭 **고급 보기** toosee hello 더 높은 수준의 보기 hello 개념의 기본 Acl, 마스크 및 상위 사용자 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-187">Click **Advanced View** toosee hello more advanced view, where hello concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a><span data-ttu-id="0b8f4-189">hello 상위 사용자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-189">hello super-user</span></span>

<span data-ttu-id="0b8f4-190">상위 권한을 사용자에 hello 대부분 모든 hello 사용자의 hello Data Lake 저장소에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-190">A super-user has hello most rights of all hello users in hello Data Lake Store.</span></span> <span data-ttu-id="0b8f4-191">슈퍼 사용자의 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-191">A super-user:</span></span>

* <span data-ttu-id="0b8f4-192">RWX 권한이 너무**모든** 파일 및 폴더.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-192">Has RWX Permissions too**all** files and folders.</span></span>
* <span data-ttu-id="0b8f4-193">파일이 나 폴더에 대 한 hello 권한을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-193">Can change hello permissions on any file or folder.</span></span>
* <span data-ttu-id="0b8f4-194">Hello 사용자 소유 또는 소유 파일이 나 폴더의 그룹을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-194">Can change hello owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="0b8f4-195">Azure에서 Data Lake Store 계정에는 다음을 포함하여 몇 가지 Azure 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="0b8f4-196">소유자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-196">Owners</span></span>
* <span data-ttu-id="0b8f4-197">참가자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-197">Contributors</span></span>
* <span data-ttu-id="0b8f4-198">읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-198">Readers</span></span>

<span data-ttu-id="0b8f4-199">Hello에 있는 모든 사용자 **소유자** 데이터 레이크 저장소 계정에 대 한 역할은 자동으로 해당 계정에 대 한 상위 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-199">Everyone in hello **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="0b8f4-200">toolearn 더 참조 [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-200">toolearn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="0b8f4-201">Toocreate 상위 사용자 권한이 있는 사용자 지정 역할 기반 액세스 제어 (RBAC) 역할을 사용 하도록 하려는 경우 다음 권한을 toohave hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-201">If you want toocreate a custom role-based-access control (RBAC) role that has super-user permissions, it needs toohave hello following permissions:</span></span>
- <span data-ttu-id="0b8f4-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="0b8f4-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="0b8f4-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="0b8f4-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="hello-owning-user"></a><span data-ttu-id="0b8f4-204">hello 소유 사용자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-204">hello owning user</span></span>

<span data-ttu-id="0b8f4-205">hello 항목을 만든 hello 사용자는 자동으로 hello 담당 hello 항목의 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-205">hello user who created hello item is automatically hello owning user of hello item.</span></span> <span data-ttu-id="0b8f4-206">소유 사용자는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-206">An owning user can:</span></span>

* <span data-ttu-id="0b8f4-207">소유 하 고 있는 파일의 hello 권한을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-207">Change hello permissions of a file that is owned.</span></span>
* <span data-ttu-id="0b8f4-208">Hello 소유 사용자 hello 대상 그룹의 멤버 이기도으로 그룹을 소유 하는 파일을 소유 하는 hello를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-208">Change hello owning group of a file that is owned, as long as hello owning user is also a member of hello target group.</span></span>

> [!NOTE]
> <span data-ttu-id="0b8f4-209">사용자 소유 hello *없습니다* hello 담당 소유한 다른 파일의 사용자를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-209">hello owning user *cannot* change hello owning user of another owned file.</span></span> <span data-ttu-id="0b8f4-210">상위 사용자만 파일 또는 폴더의 사용자를 소유 하는 hello를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-210">Only super-users can change hello owning user of a file or folder.</span></span>
>
>

## <a name="hello-owning-group"></a><span data-ttu-id="0b8f4-211">hello 소유 그룹</span><span class="sxs-lookup"><span data-stu-id="0b8f4-211">hello owning group</span></span>

<span data-ttu-id="0b8f4-212">Hello POSIX Acl, 모든 사용자가 그룹에 연결 된"주."</span><span class="sxs-lookup"><span data-stu-id="0b8f4-212">In hello POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="0b8f4-213">예를 들어 사용자 "alice" toohello "finance" 그룹을 속해 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-213">For example, user "alice" might belong toohello "finance" group.</span></span> <span data-ttu-id="0b8f4-214">Alice toomultiple 그룹에도 속해 수 있지만 한 그룹의 주 그룹으로 항상 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-214">Alice might also belong toomultiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="0b8f4-215">POSIX, Alice가 파일을 만들 때 해당 파일의 그룹을 소유 하는 hello 설정 됩니다 tooher 주 그룹, 즉이 경우 "finance"로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-215">In POSIX, when Alice creates a file, hello owning group of that file is set tooher primary group, which in this case is "finance."</span></span>

<span data-ttu-id="0b8f4-216">새 파일 시스템 항목을 만들면 데이터 레이크 저장소 그룹을 소유 하는 값 toohello를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-216">When a new filesystem item is created, Data Lake Store assigns a value toohello owning group.</span></span>

* <span data-ttu-id="0b8f4-217">**사례 1**: hello 루트 폴더 "/"입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-217">**Case 1**: hello root folder "/".</span></span> <span data-ttu-id="0b8f4-218">이 폴더는 Data Lake Store 계정이 만들어질 때 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="0b8f4-219">이 경우 hello 소유 그룹 hello 계정을 만든 toohello 사용자를 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-219">In this case, hello owning group is set toohello user who created hello account.</span></span>
* <span data-ttu-id="0b8f4-220">**사례 2** (다른 모든 경우): 새 항목이 생성 되 면 hello 소유 그룹 hello 부모 폴더에서 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-220">**Case 2** (Every other case): When a new item is created, hello owning group is copied from hello parent folder.</span></span>

<span data-ttu-id="0b8f4-221">hello 소유 그룹으로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-221">hello owning group can be changed by:</span></span>
* <span data-ttu-id="0b8f4-222">모든 슈퍼 사용자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-222">Any super-users.</span></span>
* <span data-ttu-id="0b8f4-223">hello hello 소유 사용자 hello 대상 그룹의 구성원 이기도 한 경우 사용자가 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-223">hello owning user, if hello owning user is also a member of hello target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="0b8f4-224">액세스 검사 알고리즘</span><span class="sxs-lookup"><span data-stu-id="0b8f4-224">Access check algorithm</span></span>

<span data-ttu-id="0b8f4-225">다음 그림 hello Data Lake 저장소 계정에 대 한 hello 액세스 검사 알고리즘을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-225">hello following illustration represents hello access check algorithm for Data Lake Store accounts.</span></span>

![Data Lake Store ACL 알고리즘](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a><span data-ttu-id="0b8f4-227">hello 마스크 및 "유효 사용 권한"</span><span class="sxs-lookup"><span data-stu-id="0b8f4-227">hello mask and "effective permissions"</span></span>

<span data-ttu-id="0b8f4-228">hello **마스크** 는 RWX은 값에 대 한 액세스를 사용 하는 toolimit **명명 된 사용자**, hello **소유 그룹**, 및 **명명 된 그룹** 라인인 경우 hello 액세스 검사 알고리즘을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-228">hello **mask** is an RWX value that is used toolimit access for **named users**, hello **owning group**, and **named groups** when you're performing hello access check algorithm.</span></span> <span data-ttu-id="0b8f4-229">다음은 hello hello 마스크에 대 한 주요 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-229">Here are hello key concepts for hello mask.</span></span>

* <span data-ttu-id="0b8f4-230">hello 마스크 "유효 사용 권한입니다."를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-230">hello mask creates "effective permissions."</span></span> <span data-ttu-id="0b8f4-231">즉, 액세스 권한 확인의 hello 시 hello 사용 권한을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-231">That is, it modifies hello permissions at hello time of access check.</span></span>
* <span data-ttu-id="0b8f4-232">hello 마스크 hello 파일 소유자 및 모든 상위 사용자가 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-232">hello mask can be directly edited by hello file owner and any super-users.</span></span>
* <span data-ttu-id="0b8f4-233">hello 마스크 권한을 toocreate hello 유효 사용 권한을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-233">hello mask can remove permissions toocreate hello effective permission.</span></span> <span data-ttu-id="0b8f4-234">hello 마스크 *없습니다* 권한을 toohello 유효 사용 권한을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-234">hello mask *cannot* add permissions toohello effective permission.</span></span>

<span data-ttu-id="0b8f4-235">몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-235">Let's look at some examples.</span></span> <span data-ttu-id="0b8f4-236">다음 예제는 hello에서 hello mask가 설정 되어 너무**RWX**, 해당 hello 엔터티를 의미 하는 모든 사용 권한을 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-236">In hello following example, hello mask is set too**RWX**, which means that hello mask does not remove any permissions.</span></span> <span data-ttu-id="0b8f4-237">명명 된 사용자, 그룹을 소유 하 고 명명 된 그룹 hello에 대 한 유효 사용 권한 hello hello 액세스 검사 하는 동안 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-237">hello effective permissions for hello named user, owning group, and named group are not altered during hello access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="0b8f4-239">다음 예제는 hello에서 hello mask가 설정 되어 너무**R-X**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-239">In hello following example, hello mask is set too**R-X**.</span></span> <span data-ttu-id="0b8f4-240">즉, 해당 it **hello 쓰기 권한이 해제** 에 대 한 **명명 된 사용자**, **소유 그룹**, 및 **그룹 이라는** 액세스 hello 시 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-240">This means that it **turns off hello Write permissions** for **named user**, **owning group**, and **named group** at hello time of access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="0b8f4-242">참조용으로 다음 파일 또는 폴더에 대 한 hello 마스크 hello Azure 포털에에서 나타나는입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-242">For reference, here is where hello mask for a file or folder appears in hello Azure portal.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="0b8f4-244">새 데이터 레이크 저장소 계정, ACL 액세스 hello에 대 한 hello 마스크 및 hello 루트의 ACL 기본에 대 한 폴더 ("/") tooRWX의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-244">For a new Data Lake Store account, hello mask for hello Access ACL and Default ACL of hello root folder ("/") defaults tooRWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="0b8f4-245">새 파일 및 폴더에 대한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="0b8f4-245">Permissions on new files and folders</span></span>

<span data-ttu-id="0b8f4-246">기존 폴더에 새 파일이 나 폴더를 만들면 hello 기본 ACL hello 상위 폴더에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-246">When a new file or folder is created under an existing folder, hello Default ACL on hello parent folder determines:</span></span>

- <span data-ttu-id="0b8f4-247">자식 폴더의 기본 ACL 및 액세스 ACL</span><span class="sxs-lookup"><span data-stu-id="0b8f4-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="0b8f4-248">자식 파일의 액세스 ACL(파일에 기본 ACL이 없는 경우)</span><span class="sxs-lookup"><span data-stu-id="0b8f4-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="hello-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="0b8f4-249">hello 자식 파일 또는 폴더의 ACL 액세스</span><span class="sxs-lookup"><span data-stu-id="0b8f4-249">hello Access ACL of a child file or folder</span></span>

<span data-ttu-id="0b8f4-250">자식 파일 또는 폴더를 만들 때 기본 ACL hello 부모 hello hello 자식 파일 또는 폴더의 ACL 액세스도 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-250">When a child file or folder is created, hello parent's Default ACL is copied as hello Access ACL of hello child file or folder.</span></span> <span data-ttu-id="0b8f4-251">또한 경우 **다른** hello 부모의 기본 ACL에서에서 사용자에 게 RWX 권한이, hello 자식 항목의 ACL 액세스에서에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-251">Also, if **other** user has RWX permissions in hello parent's default ACL, it is removed from hello child item's Access ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="0b8f4-253">대부분의 시나리오에서 hello 이전 정보는 ACL 자식 항목의 액세스를 결정 하는 방법에 대 한 tooknow 하기만 하면는입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-253">In most scenarios, hello previous information is all you need tooknow about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="0b8f4-254">하지만 POSIX 시스템 및 원하는 toounderstand 심층 분석이 변환을 구현 하는 방법에 대해 잘 알고 있다면 hello 섹션을 참조 [Umask의 역할을 새 파일 및 폴더에 대 한 ACL 액세스 hello 만드는](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) 이 문서의 뒷부분에 나오는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-254">However, if you are familiar with POSIX systems and want toounderstand in-depth how this transformation is achieved, see hello section [Umask’s role in creating hello Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="0b8f4-255">자식 폴더의 기본 ACL</span><span class="sxs-lookup"><span data-stu-id="0b8f4-255">A child folder's Default ACL</span></span>

<span data-ttu-id="0b8f4-256">부모 폴더 아래의 자식 폴더를 만들면 기본 ACL toohello 자식 폴더를 그대로 hello 부모 폴더의 기본 ACL은 통해 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-256">When a child folder is created under a parent folder, hello parent folder's Default ACL is copied over as is toohello child folder's Default ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="0b8f4-258">Data Lake Store에서 ACL을 이해하기 위한 고급 항목</span><span class="sxs-lookup"><span data-stu-id="0b8f4-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="0b8f4-259">다음은 몇 가지 고급 항목 toohelp 데이터 레이크 저장소 파일 또는 폴더에 대 한 Acl의 결정 방식을 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-259">Following are some advanced topics toohelp you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a><span data-ttu-id="0b8f4-260">새 파일 및 폴더에 대 한 ACL 액세스 hello 만드는 Umask의 역할</span><span class="sxs-lookup"><span data-stu-id="0b8f4-260">Umask’s role in creating hello Access ACL for new files and folders</span></span>

<span data-ttu-id="0b8f4-261">POSIX 규격 시스템에서 hello 일반 개념은 해당 umask 사용에 대 한 tootransform hello 권한을 hello 부모 폴더에는 9 비트 값은 **사용자 소유**, **소유 그룹**, 및  **다른** 새 자식 파일 또는 폴더의 ACL 액세스 hello에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-261">In a POSIX-compliant system, hello general concept is that umask is a 9-bit value on hello parent folder that's used tootransform hello permission for **owning user**, **owning group**, and **other** on hello Access ACL of a new child file or folder.</span></span> <span data-ttu-id="0b8f4-262">umask의 hello 비트 hello 자식 항목의 액세스 ACL에 해제는 비트 tooturn를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-262">hello bits of a umask identify which bits tooturn off in hello child item’s Access ACL.</span></span> <span data-ttu-id="0b8f4-263">따라서 사용 tooselectively 방지에 대 한 사용 권한 hello 전파 **사용자 소유**, **소유 그룹**, 및 **다른**합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-263">Thus it is used tooselectively prevent hello propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="0b8f4-264">일반적으로 HDFS 시스템 hello umask 관리자에 의해 제어 되는 사이트 전체 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-264">In an HDFS system, hello umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="0b8f4-265">Data Lake Store는 변경할 수 없는 **계정 전체 umask** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="0b8f4-266">데이터 레이크 저장소에 대 한 다음 테이블에서는 hello hello 마스크 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-266">hello following table shows hello unmask for Data Lake Store.</span></span>

| <span data-ttu-id="0b8f4-267">사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="0b8f4-267">User group</span></span>  | <span data-ttu-id="0b8f4-268">설정</span><span class="sxs-lookup"><span data-stu-id="0b8f4-268">Setting</span></span> | <span data-ttu-id="0b8f4-269">새 자식 항목의 액세스 ACL에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="0b8f4-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="0b8f4-270">소유 사용자</span><span class="sxs-lookup"><span data-stu-id="0b8f4-270">Owning user</span></span> | ---     | <span data-ttu-id="0b8f4-271">영향 없음</span><span class="sxs-lookup"><span data-stu-id="0b8f4-271">No effect</span></span>                             |
| <span data-ttu-id="0b8f4-272">소유 그룹</span><span class="sxs-lookup"><span data-stu-id="0b8f4-272">Owning group</span></span>| ---     | <span data-ttu-id="0b8f4-273">영향 없음</span><span class="sxs-lookup"><span data-stu-id="0b8f4-273">No effect</span></span>                             |
| <span data-ttu-id="0b8f4-274">다른</span><span class="sxs-lookup"><span data-stu-id="0b8f4-274">Other</span></span>       | <span data-ttu-id="0b8f4-275">RWX</span><span class="sxs-lookup"><span data-stu-id="0b8f4-275">RWX</span></span>     | <span data-ttu-id="0b8f4-276">읽기 + 쓰기 + 실행 제거</span><span class="sxs-lookup"><span data-stu-id="0b8f4-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="0b8f4-277">hello 다음 그림에서는 실행이이 umask 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-277">hello following illustration shows this umask in action.</span></span> <span data-ttu-id="0b8f4-278">hello 한 순수 효과 tooremove **읽기, 쓰기 + 실행** 에 대 한 **다른** 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-278">hello net effect is tooremove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="0b8f4-279">Umask hello에 대 한 비트를 지정 하지 않아 **사용자 소유** 및 **소유 그룹**, 이러한 사용 권한은 변환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-279">Because hello umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a><span data-ttu-id="0b8f4-281">hello 스티커 비트</span><span class="sxs-lookup"><span data-stu-id="0b8f4-281">hello sticky bit</span></span>

<span data-ttu-id="0b8f4-282">hello 스티커 비트 POSIX 파일 시스템의 고급 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-282">hello sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="0b8f4-283">데이터 레이크 저장소의 hello 컨텍스트에서 그럴 가능성은 해당 hello 스티커 비트를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-283">In hello context of Data Lake Store, it is unlikely that hello sticky bit will be needed.</span></span>

<span data-ttu-id="0b8f4-284">hello 다음 표에 hello 스티커 비트 데이터 레이크 저장소에서 작동 하는 방법을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-284">hello following table shows how hello sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="0b8f4-285">사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="0b8f4-285">User group</span></span>         | <span data-ttu-id="0b8f4-286">파일</span><span class="sxs-lookup"><span data-stu-id="0b8f4-286">File</span></span>    | <span data-ttu-id="0b8f4-287">폴더</span><span class="sxs-lookup"><span data-stu-id="0b8f4-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="0b8f4-288">고정 비트 **끄기**</span><span class="sxs-lookup"><span data-stu-id="0b8f4-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="0b8f4-289">영향 없음</span><span class="sxs-lookup"><span data-stu-id="0b8f4-289">No effect</span></span>   | <span data-ttu-id="0b8f4-290">영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-290">No effect.</span></span>           |
| <span data-ttu-id="0b8f4-291">고정 비트 **켜기**</span><span class="sxs-lookup"><span data-stu-id="0b8f4-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="0b8f4-292">영향 없음</span><span class="sxs-lookup"><span data-stu-id="0b8f4-292">No effect</span></span>   | <span data-ttu-id="0b8f4-293">제외 하 고 누구도 **상위 사용자** 및 hello **사용자 소유** 가 삭제 또는 해당 자식 항목의 이름을 바꾸면 자식 항목의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-293">Prevents anyone except **super-users** and hello **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="0b8f4-294">hello 스티커 비트 hello Azure 포털에에서 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-294">hello sticky bit is not shown in hello Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="0b8f4-295">Data Lake Store의 ACL에 대한 일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="0b8f4-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="0b8f4-296">Data Lake Store의 ACL에 대해 자주 제기하는 몇 가지 질문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-tooenable-support-for-acls"></a><span data-ttu-id="0b8f4-297">Acl에 대 한 지원을 tooenable 있습니까?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-297">Do I have tooenable support for ACLs?</span></span>

<span data-ttu-id="0b8f4-298">아니요.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-298">No.</span></span> <span data-ttu-id="0b8f4-299">ACL을 통한 액세스 제어는 항상 Data Lake Store 계정에 대하여 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="0b8f4-300">사용 권한을 필요한 toorecursively delete 폴더와 해당 내용?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-300">Which permissions are required toorecursively delete a folder and its contents?</span></span>

* <span data-ttu-id="0b8f4-301">hello 부모 폴더가 있어야 **쓰기 / 실행** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-301">hello parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="0b8f4-302">삭제 폴더 toobe hello와 그 안의 모든 폴더에 필요 하므로 **읽기, 쓰기 + 실행** 사용 권한.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-302">hello folder toobe deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="0b8f4-303">쓰기 권한이 toodelete 파일 폴더에 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-303">You do not need Write permissions toodelete files in folders.</span></span> <span data-ttu-id="0b8f4-304">또한 루트 폴더 hello "/" 수 **되지** 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-304">Also, hello root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a><span data-ttu-id="0b8f4-305">파일 또는 폴더의 hello 소유자가 누군지 않습니까?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-305">Who is hello owner of a file or folder?</span></span>

<span data-ttu-id="0b8f4-306">파일 또는 폴더의 hello 작성자 hello 소유자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-306">hello creator of a file or folder becomes hello owner.</span></span>

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="0b8f4-307">어떤 그룹의 파일이 나 폴더를 만들 때 그룹을 소유 하는 hello로 설정 되어 있습니까?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-307">Which group is set as hello owning group of a file or folder at creation?</span></span>

<span data-ttu-id="0b8f4-308">hello 소유 그룹 hello 부모 폴더는 hello 아래의 새 파일 또는 폴더가 생성 되는 그룹을 소유 하는 hello에서 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-308">hello owning group is copied from hello owning group of hello parent folder under which hello new file or folder is created.</span></span>

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="0b8f4-309">파일의 사용자를 소유 하는 hello 저는 없 hello RWX 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-309">I am hello owning user of a file but I don’t have hello RWX permissions I need.</span></span> <span data-ttu-id="0b8f4-310">어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-310">What do I do?</span></span>

<span data-ttu-id="0b8f4-311">hello 소유 권한을 변경할 수 있습니다 hello hello 파일 toogive의 자체 RWX 권한이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-311">hello owning user can change hello permissions of hello file toogive themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="0b8f4-312">Acl을 확인할 때 hello Azure 포털에서에서 사용자 이름 보이지만 Guid, Api를 통해 나타나는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-312">When I look at ACLs in hello Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="0b8f4-313">Hello Acl의 항목은 Azure AD에서 toousers에 해당 하는 Guid로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-313">Entries in hello ACLs are stored as GUIDs that correspond toousers in Azure AD.</span></span> <span data-ttu-id="0b8f4-314">hello Api 그대로 hello Guid를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-314">hello APIs return hello GUIDs as is.</span></span> <span data-ttu-id="0b8f4-315">가능 하면 친숙 한 이름으로 Guid hello를 변환 하 여 hello Azure 포털에 toomake Acl 보다 쉽게 toouse 하려고 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-315">hello Azure portal tries toomake ACLs easier toouse by translating hello GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a><span data-ttu-id="0b8f4-316">경우에 따라 보이지 이유 hello Acl에서 Guid hello Azure 포털을 사용 중일 때?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-316">Why do I sometimes see GUIDs in hello ACLs when I'm using hello Azure portal?</span></span>

<span data-ttu-id="0b8f4-317">GUID는 hello 사용자는 더 이상 Azure AD에 존재 하지 않는 경우에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-317">A GUID is shown when hello user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="0b8f4-318">일반적으로이 hello 사용자 hello 회사를 떠난 또는 Azure AD에서 자신의 계정을 삭제 된 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-318">Usually this happens when hello user has left hello company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="0b8f4-319">Data Lake Store는 ACL의 상속을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="0b8f4-320">아니요.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-320">No.</span></span>

### <a name="what-is-hello-difference-between-mask-and-umask"></a><span data-ttu-id="0b8f4-321">마스크와 umask hello 차이 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-321">What is hello difference between mask and umask?</span></span>

| <span data-ttu-id="0b8f4-322">마스크</span><span class="sxs-lookup"><span data-stu-id="0b8f4-322">mask</span></span> | <span data-ttu-id="0b8f4-323">umask</span><span class="sxs-lookup"><span data-stu-id="0b8f4-323">umask</span></span>|
|------|------|
| <span data-ttu-id="0b8f4-324">hello **마스크** 속성은 모든 파일 및 폴더에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-324">hello **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="0b8f4-325">hello **umask** hello Data Lake 저장소 계정이의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-325">hello **umask** is a property of hello Data Lake Store account.</span></span> <span data-ttu-id="0b8f4-326">따라서에 없는 경우 단일 umask만 hello 데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="0b8f4-326">So there is only a single umask in hello Data Lake Store.</span></span>    |
| <span data-ttu-id="0b8f4-327">hello 담당 사용자 또는 그룹은 파일 또는 상위 사용자의 소유 하 여 파일 또는 폴더에 hello 마스크 속성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-327">hello mask property on a file or folder can be altered by hello owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="0b8f4-328">모든 사용자는 슈퍼 사용자도가 hello umask 속성을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-328">hello umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="0b8f4-329">변경할 수 없는 상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="0b8f4-330">작업 파일이 나 폴더에 있는 사용자는 hello 오른쪽 tooperform 여부 런타임 toodetermine에 hello 액세스 검사 알고리즘 중 hello 마스크 속성이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-330">hello mask property is used during hello access check algorithm at runtime toodetermine whether a user has hello right tooperform on operation on a file or folder.</span></span> <span data-ttu-id="0b8f4-331">hello 마스크의 hello 역할은 액세스 권한 확인의 hello 시간에 toocreate "유효 사용 권한"입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-331">hello role of hello mask is toocreate "effective permissions" at hello time of access check.</span></span> | <span data-ttu-id="0b8f4-332">hello umask 액세스 검사 하는 동안 전혀 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-332">hello umask is not used during access check at all.</span></span> <span data-ttu-id="0b8f4-333">hello umask는 사용 되는 toodetermine hello 폴더의 새 자식 항목의 ACL 액세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-333">hello umask is used toodetermine hello Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="0b8f4-334">hello 마스크는 toonamed 사용자, 명명 된 그룹 및 소유 사용자 액세스 권한 확인의 hello 시 적용 되는 3 비트 RWX 값입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-334">hello mask is a 3-bit RWX value that applies toonamed user, named group, and owning user at hello time of access check.</span></span>| <span data-ttu-id="0b8f4-335">hello umask는 9 비트 값 그룹을 소유 하는 사용자, 소유 toohello 적용 되 고 **다른** 새 자식입니다.</span><span class="sxs-lookup"><span data-stu-id="0b8f4-335">hello umask is a 9-bit value that applies toohello owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="0b8f4-336">POSIX 액세스 제어 모델에 대한 어디서 자세히 알아볼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="0b8f4-336">Where can I learn more about POSIX access control model?</span></span>

* <span data-ttu-id="0b8f4-337">[Linux의 POSIX 액세스 제어 목록](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="0b8f4-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)</span></span>

* <span data-ttu-id="0b8f4-338">[HDFS 권한 가이드](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="0b8f4-338">[HDFS permission guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)</span></span>

* [<span data-ttu-id="0b8f4-339">POSIX FAQ</span><span class="sxs-lookup"><span data-stu-id="0b8f4-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="0b8f4-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="0b8f4-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="0b8f4-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="0b8f4-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="0b8f4-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="0b8f4-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="0b8f4-343">Ubuntu의 POSIX ACL</span><span class="sxs-lookup"><span data-stu-id="0b8f4-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* <span data-ttu-id="0b8f4-344">[ACL: Linux의 액세스 제어 목록 사용](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)(영문)</span><span class="sxs-lookup"><span data-stu-id="0b8f4-344">[ACL using access control lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)</span></span>

## <a name="see-also"></a><span data-ttu-id="0b8f4-345">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0b8f4-345">See also</span></span>

* [<span data-ttu-id="0b8f4-346">Azure 데이터 레이크 저장소 개요</span><span class="sxs-lookup"><span data-stu-id="0b8f4-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
