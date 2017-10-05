---
title: "Data Lake Store의 액세스 제어 개요 | Microsoft Docs"
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
ms.openlocfilehash: 99fbad770290d280bdec490d988391ad276ce1ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="access-control-in-azure-data-lake-store"></a><span data-ttu-id="791d1-103">Azure Data Lake Store에서 액세스 제어</span><span class="sxs-lookup"><span data-stu-id="791d1-103">Access control in Azure Data Lake Store</span></span>

<span data-ttu-id="791d1-104">Azure Data Lake Store는 HDFS에서 파생된 액세스 제어 모델을 구현하고, 차례로 HDFS는 POSIX 액세스 제어 모델에서 파생됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-104">Azure Data Lake Store implements an access control model that derives from HDFS, which in turn derives from the POSIX access control model.</span></span> <span data-ttu-id="791d1-105">이 문서에서는 Data Lake Store에 대한 액세스 제어 모델의 기본 사항을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-105">This article summarizes the basics of the access control model for Data Lake Store.</span></span> <span data-ttu-id="791d1-106">HDFS 액세스 제어 모델에 대해 자세히 알아보려면 [HDFS 권한 가이드](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="791d1-106">To learn more about the HDFS access control model, see [HDFS Permissions Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).</span></span>

## <a name="access-control-lists-on-files-and-folders"></a><span data-ttu-id="791d1-107">파일 및 폴더에 대한 액세스 제어 목록</span><span class="sxs-lookup"><span data-stu-id="791d1-107">Access control lists on files and folders</span></span>

<span data-ttu-id="791d1-108">**액세스 ACL** 및 **기본 ACL**이라는 두 가지 ACL(액세스 제어 목록)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-108">There are two kinds of access control lists (ACLs), **Access ACLs** and **Default ACLs**.</span></span>

* <span data-ttu-id="791d1-109">**액세스 ACL** – 개체에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-109">**Access ACLs**: These control access to an object.</span></span> <span data-ttu-id="791d1-110">파일과 폴더에는 모두 액세스 ACL이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-110">Files and folders both have Access ACLs.</span></span>

* <span data-ttu-id="791d1-111">**기본 ACL** - 해당 폴더 아래에 만든 모든 자식 항목에 대한 액세스 ACL을 결정하는 폴더와 연결된 ACL의 "템플릿"입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-111">**Default ACLs**: A "template" of ACLs associated with a folder that determine the Access ACLs for any child items that are created under that folder.</span></span> <span data-ttu-id="791d1-112">파일에는 기본 ACL이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-112">Files do not have Default ACLs.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

<span data-ttu-id="791d1-114">액세스 ACL 및 기본 ACL은 모두 구조가 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-114">Both Access ACLs and Default ACLs have the same structure.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> <span data-ttu-id="791d1-116">부모 항목에서 기본 ACL을 변경하면 이미 존재하는 자식 항목의 액세스 ACL 또는 기본 ACL에 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-116">Changing the Default ACL on a parent does not affect the Access ACL or Default ACL of child items that already exist.</span></span>
>
>

## <a name="users-and-identities"></a><span data-ttu-id="791d1-117">사용자 및 ID</span><span class="sxs-lookup"><span data-stu-id="791d1-117">Users and identities</span></span>

<span data-ttu-id="791d1-118">모든 파일 및 폴더에는 이러한 ID에 대한 고유한 사용 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-118">Every file and folder has distinct permissions for these identities:</span></span>

* <span data-ttu-id="791d1-119">파일을 소유한 사용자</span><span class="sxs-lookup"><span data-stu-id="791d1-119">The owning user of the file</span></span>
* <span data-ttu-id="791d1-120">소유 그룹</span><span class="sxs-lookup"><span data-stu-id="791d1-120">The owning group</span></span>
* <span data-ttu-id="791d1-121">명명된 사용자</span><span class="sxs-lookup"><span data-stu-id="791d1-121">Named users</span></span>
* <span data-ttu-id="791d1-122">명명된 그룹</span><span class="sxs-lookup"><span data-stu-id="791d1-122">Named groups</span></span>
* <span data-ttu-id="791d1-123">기타 모든 사용자</span><span class="sxs-lookup"><span data-stu-id="791d1-123">All other users</span></span>

<span data-ttu-id="791d1-124">사용자 및 그룹의 ID는 Azure AD(Azure Active Directory) ID입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-124">The identities of users and groups are Azure Active Directory (Azure AD) identities.</span></span> <span data-ttu-id="791d1-125">달리 설명하지 않는 한 Data Lake Store의 컨텍스트에서 "사용자"는 Azure AD 사용자 또는 Azure AD 보안 그룹을 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-125">So unless otherwise noted, a "user," in the context of Data Lake Store, can either mean an Azure AD user or an Azure AD security group.</span></span>

## <a name="permissions"></a><span data-ttu-id="791d1-126">권한</span><span class="sxs-lookup"><span data-stu-id="791d1-126">Permissions</span></span>

<span data-ttu-id="791d1-127">파일 시스템 개체에 대한 권한은 **읽기**, **쓰기** 및 **실행**이며 아래 표에서 보여 주듯이 파일과 폴더에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-127">The permissions on a filesystem object are **Read**, **Write**, and **Execute**, and they can be used on files and folders as shown in the following table:</span></span>

|            |    <span data-ttu-id="791d1-128">파일</span><span class="sxs-lookup"><span data-stu-id="791d1-128">File</span></span>     |   <span data-ttu-id="791d1-129">폴더</span><span class="sxs-lookup"><span data-stu-id="791d1-129">Folder</span></span> |
|------------|-------------|----------|
| <span data-ttu-id="791d1-130">**읽기(R)**</span><span class="sxs-lookup"><span data-stu-id="791d1-130">**Read (R)**</span></span> | <span data-ttu-id="791d1-131">파일의 내용을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-131">Can read the contents of a file</span></span> | <span data-ttu-id="791d1-132">폴더의 내용을 나열하려면 **읽기** 및 **실행**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-132">Requires **Read** and **Execute** to list the contents of the folder</span></span>|
| <span data-ttu-id="791d1-133">**쓰기(W)**</span><span class="sxs-lookup"><span data-stu-id="791d1-133">**Write (W)**</span></span> | <span data-ttu-id="791d1-134">쓰거나 파일에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-134">Can write or append to a file</span></span> | <span data-ttu-id="791d1-135">폴더에 자식 항목을 만들려면 **쓰기** 및 **실행**이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-135">Requires **Write** and **Execute** to create child items in a folder</span></span> |
| <span data-ttu-id="791d1-136">**실행(X)**</span><span class="sxs-lookup"><span data-stu-id="791d1-136">**Execute (X)**</span></span> | <span data-ttu-id="791d1-137">Data Lake Store의 컨텍스트에서 모든 것을 의미하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-137">Does not mean anything in the context of Data Lake Store</span></span> | <span data-ttu-id="791d1-138">폴더의 자식 항목을 트래버스하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-138">Required to traverse the child items of a folder</span></span> |

### <a name="short-forms-for-permissions"></a><span data-ttu-id="791d1-139">사용 권한에 대한 짧은 형식</span><span class="sxs-lookup"><span data-stu-id="791d1-139">Short forms for permissions</span></span>

<span data-ttu-id="791d1-140">**RWX**는 **읽기 + 쓰기 + 실행**을 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-140">**RWX** is used to indicate **Read + Write + Execute**.</span></span> <span data-ttu-id="791d1-141">**읽기=4**, **쓰기=2** 및 **실행=1**의 압축된 숫자 형식이 있으며, 그 합계는 권한을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-141">A more condensed numeric form exists in which **Read=4**, **Write=2**, and **Execute=1**, the sum of which represents the permissions.</span></span> <span data-ttu-id="791d1-142">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-142">Following are some examples.</span></span>

| <span data-ttu-id="791d1-143">숫자 형식</span><span class="sxs-lookup"><span data-stu-id="791d1-143">Numeric form</span></span> | <span data-ttu-id="791d1-144">짧은 형식</span><span class="sxs-lookup"><span data-stu-id="791d1-144">Short form</span></span> |      <span data-ttu-id="791d1-145">의미</span><span class="sxs-lookup"><span data-stu-id="791d1-145">What it means</span></span>     |
|--------------|------------|------------------------|
| <span data-ttu-id="791d1-146">7</span><span class="sxs-lookup"><span data-stu-id="791d1-146">7</span></span>            | <span data-ttu-id="791d1-147">RWX</span><span class="sxs-lookup"><span data-stu-id="791d1-147">RWX</span></span>        | <span data-ttu-id="791d1-148">읽기 + 쓰기 + 실행</span><span class="sxs-lookup"><span data-stu-id="791d1-148">Read + Write + Execute</span></span> |
| <span data-ttu-id="791d1-149">5</span><span class="sxs-lookup"><span data-stu-id="791d1-149">5</span></span>            | <span data-ttu-id="791d1-150">R-X</span><span class="sxs-lookup"><span data-stu-id="791d1-150">R-X</span></span>        | <span data-ttu-id="791d1-151">읽기 + 실행</span><span class="sxs-lookup"><span data-stu-id="791d1-151">Read + Execute</span></span>         |
| <span data-ttu-id="791d1-152">4</span><span class="sxs-lookup"><span data-stu-id="791d1-152">4</span></span>            | <span data-ttu-id="791d1-153">R--</span><span class="sxs-lookup"><span data-stu-id="791d1-153">R--</span></span>        | <span data-ttu-id="791d1-154">읽기</span><span class="sxs-lookup"><span data-stu-id="791d1-154">Read</span></span>                   |
| <span data-ttu-id="791d1-155">0</span><span class="sxs-lookup"><span data-stu-id="791d1-155">0</span></span>            | ---        | <span data-ttu-id="791d1-156">사용 권한 없음</span><span class="sxs-lookup"><span data-stu-id="791d1-156">No permissions</span></span>         |


### <a name="permissions-do-not-inherit"></a><span data-ttu-id="791d1-157">사용 권한은 상속하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-157">Permissions do not inherit</span></span>

<span data-ttu-id="791d1-158">Data Lake Store에서 사용하는 POSIX 스타일 모델에서 항목에 대한 권한은 항목 자체에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-158">In the POSIX-style model that's used by Data Lake Store, permissions for an item are stored on the item itself.</span></span> <span data-ttu-id="791d1-159">즉, 항목에 대한 사용 권한은 부모 항목에서 상속될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-159">In other words, permissions for an item cannot be inherited from the parent items.</span></span>

## <a name="common-scenarios-related-to-permissions"></a><span data-ttu-id="791d1-160">사용 권한과 관련된 일반적인 시나리오</span><span class="sxs-lookup"><span data-stu-id="791d1-160">Common scenarios related to permissions</span></span>

<span data-ttu-id="791d1-161">Data Lake Store 계정에서 특정 작업을 수행하는 데 필요한 권한을 이해하는 데 도움이 되는 몇 가지 일반적인 시나리오는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-161">Following are some common scenarios to help you understand which permissions are needed to perform certain operations on a Data Lake Store account.</span></span>

### <a name="permissions-needed-to-read-a-file"></a><span data-ttu-id="791d1-162">파일을 읽는 데 필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="791d1-162">Permissions needed to read a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* <span data-ttu-id="791d1-164">읽을 파일의 경우 호출자에 **읽기** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-164">For the file to be read, the caller needs **Read** permissions.</span></span>
* <span data-ttu-id="791d1-165">파일을 포함하는 폴더 구조에 있는 모든 폴더의 경우 호출자에 **실행** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-165">For all the folders in the folder structure that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-append-to-a-file"></a><span data-ttu-id="791d1-166">파일에 추가하는 데 필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="791d1-166">Permissions needed to append to a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* <span data-ttu-id="791d1-168">추가할 파일의 경우 호출자에 **쓰기** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-168">For the file to be appended to, the caller needs **Write** permissions.</span></span>
* <span data-ttu-id="791d1-169">파일을 포함하는 모든 폴더의 경우 호출자에 **실행** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-169">For all the folders that contain the file, the caller needs **Execute** permissions.</span></span>

### <a name="permissions-needed-to-delete-a-file"></a><span data-ttu-id="791d1-170">파일을 삭제하는 데 필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="791d1-170">Permissions needed to delete a file</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* <span data-ttu-id="791d1-172">부모 폴더의 경우 호출자에 **쓰기 + 실행** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-172">For the parent folder, the caller needs **Write + Execute** permissions.</span></span>
* <span data-ttu-id="791d1-173">파일의 경로에 있는 다른 모든 폴더의 경우 호출자에 **실행** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-173">For all the other folders in the file’s path, the caller needs **Execute** permissions.</span></span>



> [!NOTE]
> <span data-ttu-id="791d1-174">위의 두 조건이 참(true)이면 파일에 대한 쓰기 권한은 파일을 삭제하는 데 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-174">Write permissions on the file are not required to delete it as long as the previous two conditions are true.</span></span>
>
>

### <a name="permissions-needed-to-enumerate-a-folder"></a><span data-ttu-id="791d1-175">폴더를 열거하는 데 필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="791d1-175">Permissions needed to enumerate a folder</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* <span data-ttu-id="791d1-177">열거할 폴더의 경우 호출자에 **읽기 + 실행** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-177">For the folder to enumerate, the caller needs **Read + Execute** permissions.</span></span>
* <span data-ttu-id="791d1-178">모든 상위 폴더의 경우 호출자에 **실행** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-178">For all the ancestor folders, the caller needs **Execute** permissions.</span></span>

## <a name="viewing-permissions-in-the-azure-portal"></a><span data-ttu-id="791d1-179">Azure Portal에서 사용 권한 보기</span><span class="sxs-lookup"><span data-stu-id="791d1-179">Viewing permissions in the Azure portal</span></span>

<span data-ttu-id="791d1-180">Data Lake Store 계정의 **데이터 탐색기** 블레이드에서 **액세스**를 클릭하여 파일이나 폴더에 대한 ACL을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-180">From the **Data Explorer** blade of the Data Lake Store account, click **Access** to see the ACLs for a file or a folder.</span></span> <span data-ttu-id="791d1-181">**액세스**를 클릭하여 **mydatastore** 계정 아래의 **catalog** 폴더에 대한 ACL을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-181">Click **Access** to see the ACLs for the **catalog** folder under the **mydatastore** account.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

<span data-ttu-id="791d1-183">이 블레이드 위쪽의 섹션에는 보유하고 있는 권한에 대한 개요가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-183">On this blade, the top section shows an overview of the permissions that you have.</span></span> <span data-ttu-id="791d1-184">스크린샷에서 사용자는 Bob이며, 뒤를 이어 액세스 권한이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-184">(In the screenshot, the user is Bob.) Following that, the access permissions are shown.</span></span> <span data-ttu-id="791d1-185">그런 다음 **액세스** 블레이드에서 **단순 보기**를 클릭하여 단순 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-185">After that, from the **Access** blade, click **Simple View** to see the simpler view.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

<span data-ttu-id="791d1-187">**고급 보기**를 클릭하여 기본 ACL, 마스크 및 슈퍼 사용자의 개념을 보여 주는 자세한 고급 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-187">Click **Advanced View** to see the more advanced view, where the concepts of Default ACLs, mask, and super-user are shown.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="the-super-user"></a><span data-ttu-id="791d1-189">슈퍼 사용자</span><span class="sxs-lookup"><span data-stu-id="791d1-189">The super-user</span></span>

<span data-ttu-id="791d1-190">슈퍼 사용자는 Data Lake Store의 모든 사용자 중 가장 많은 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-190">A super-user has the most rights of all the users in the Data Lake Store.</span></span> <span data-ttu-id="791d1-191">슈퍼 사용자의 권한은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-191">A super-user:</span></span>

* <span data-ttu-id="791d1-192">**모든** 파일과 폴더에 대한 RWX 권한을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-192">Has RWX Permissions to **all** files and folders.</span></span>
* <span data-ttu-id="791d1-193">모든 파일이나 폴더에 대한 권한을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-193">Can change the permissions on any file or folder.</span></span>
* <span data-ttu-id="791d1-194">모든 파일이나 폴더의 소유 사용자 또는 소유 그룹을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-194">Can change the owning user or owning group of any file or folder.</span></span>

<span data-ttu-id="791d1-195">Azure에서 Data Lake Store 계정에는 다음을 포함하여 몇 가지 Azure 역할이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-195">In Azure, a Data Lake Store account has several Azure roles, including:</span></span>

* <span data-ttu-id="791d1-196">소유자</span><span class="sxs-lookup"><span data-stu-id="791d1-196">Owners</span></span>
* <span data-ttu-id="791d1-197">참가자</span><span class="sxs-lookup"><span data-stu-id="791d1-197">Contributors</span></span>
* <span data-ttu-id="791d1-198">읽기 권한자</span><span class="sxs-lookup"><span data-stu-id="791d1-198">Readers</span></span>

<span data-ttu-id="791d1-199">Data Lake Store 계정에 대한 **소유자** 역할을 지닌 모든 사용자는 자동으로 해당 계정에 대한 슈퍼 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-199">Everyone in the **Owners** role for a Data Lake Store account is automatically a super-user for that account.</span></span> <span data-ttu-id="791d1-200">자세한 내용은 [역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="791d1-200">To learn more, see [Role-based access control](../active-directory/role-based-access-control-configure.md).</span></span>
<span data-ttu-id="791d1-201">슈퍼 사용자 권한이 있는 사용자 지정 RBAC(역할 기반 액세스 제어) 역할을 만들려면 다음 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-201">If you want to create a custom role-based-access control (RBAC) role that has super-user permissions, it needs to have the following permissions:</span></span>
- <span data-ttu-id="791d1-202">Microsoft.DataLakeStore/accounts/Superuser/action</span><span class="sxs-lookup"><span data-stu-id="791d1-202">Microsoft.DataLakeStore/accounts/Superuser/action</span></span>
- <span data-ttu-id="791d1-203">Microsoft.Authorization/roleAssignments/write</span><span class="sxs-lookup"><span data-stu-id="791d1-203">Microsoft.Authorization/roleAssignments/write</span></span>


## <a name="the-owning-user"></a><span data-ttu-id="791d1-204">소유 그룹</span><span class="sxs-lookup"><span data-stu-id="791d1-204">The owning user</span></span>

<span data-ttu-id="791d1-205">항목을 만든 사용자는 자동으로 항목의 소유 사용자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-205">The user who created the item is automatically the owning user of the item.</span></span> <span data-ttu-id="791d1-206">소유 사용자는 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-206">An owning user can:</span></span>

* <span data-ttu-id="791d1-207">소유한 파일의 권한을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-207">Change the permissions of a file that is owned.</span></span>
* <span data-ttu-id="791d1-208">소유 사용자가 대상 그룹의 멤버이면 소유한 파일의 소유 그룹을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-208">Change the owning group of a file that is owned, as long as the owning user is also a member of the target group.</span></span>

> [!NOTE]
> <span data-ttu-id="791d1-209">소유 사용자는 소유한 다른 파일의 소유 사용자를 *변경할 수 없습니다*.</span><span class="sxs-lookup"><span data-stu-id="791d1-209">The owning user *cannot* change the owning user of another owned file.</span></span> <span data-ttu-id="791d1-210">슈퍼 사용자만이 파일이나 폴더의 소유 사용자를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-210">Only super-users can change the owning user of a file or folder.</span></span>
>
>

## <a name="the-owning-group"></a><span data-ttu-id="791d1-211">소유 그룹</span><span class="sxs-lookup"><span data-stu-id="791d1-211">The owning group</span></span>

<span data-ttu-id="791d1-212">POSIX ACL에서 모든 사용자는 "주 그룹"과 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-212">In the POSIX ACLs, every user is associated with a "primary group."</span></span> <span data-ttu-id="791d1-213">예를 들어 "alice" 사용자는 "finance" 그룹에 속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-213">For example, user "alice" might belong to the "finance" group.</span></span> <span data-ttu-id="791d1-214">또한 Alice는 여러 그룹에 속할 수 있지만 항상 한 그룹을 주 그룹으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-214">Alice might also belong to multiple groups, but one group is always designated as her primary group.</span></span> <span data-ttu-id="791d1-215">POSIX에서 Alice가 파일을 만들 때는 해당 파일의 소유 그룹이 자신의 주 그룹(여기서는 "finance"임)으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-215">In POSIX, when Alice creates a file, the owning group of that file is set to her primary group, which in this case is "finance."</span></span>

<span data-ttu-id="791d1-216">새 파일 시스템 항목을 만들면 Data Lake Store는 소유 그룹에 값을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-216">When a new filesystem item is created, Data Lake Store assigns a value to the owning group.</span></span>

* <span data-ttu-id="791d1-217">**사례 1** - "/" 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-217">**Case 1**: The root folder "/".</span></span> <span data-ttu-id="791d1-218">이 폴더는 Data Lake Store 계정이 만들어질 때 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-218">This folder is created when a Data Lake Store account is created.</span></span> <span data-ttu-id="791d1-219">이 경우 소유 그룹은 계정을 만든 사용자로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-219">In this case, the owning group is set to the user who created the account.</span></span>
* <span data-ttu-id="791d1-220">**사례 2**(기타 모든 경우) - 새 항목을 만들 때 소유 그룹이 부모 폴더에서 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-220">**Case 2** (Every other case): When a new item is created, the owning group is copied from the parent folder.</span></span>

<span data-ttu-id="791d1-221">소유 그룹은 다음에 의해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-221">The owning group can be changed by:</span></span>
* <span data-ttu-id="791d1-222">모든 슈퍼 사용자</span><span class="sxs-lookup"><span data-stu-id="791d1-222">Any super-users.</span></span>
* <span data-ttu-id="791d1-223">소유 사용자가 대상 그룹의 구성원이기도 한 경우 소유 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-223">The owning user, if the owning user is also a member of the target group.</span></span>

## <a name="access-check-algorithm"></a><span data-ttu-id="791d1-224">액세스 검사 알고리즘</span><span class="sxs-lookup"><span data-stu-id="791d1-224">Access check algorithm</span></span>

<span data-ttu-id="791d1-225">다음 그림은 Data Lake Store 계정에 대한 액세스 검사 알고리즘을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-225">The following illustration represents the access check algorithm for Data Lake Store accounts.</span></span>

![Data Lake Store ACL 알고리즘](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="the-mask-and-effective-permissions"></a><span data-ttu-id="791d1-227">마스크 및 "유효 사용 권한"</span><span class="sxs-lookup"><span data-stu-id="791d1-227">The mask and "effective permissions"</span></span>

<span data-ttu-id="791d1-228">**마스크**는 액세스 검사 알고리즘을 수행할 때 **명명된 사용자**, **소유 그룹** 및 **명명된 그룹**에 대한 액세스를 제한하는 데 사용되는 RWX 값입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-228">The **mask** is an RWX value that is used to limit access for **named users**, the **owning group**, and **named groups** when you're performing the access check algorithm.</span></span> <span data-ttu-id="791d1-229">마스크에 대한 핵심 개념은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-229">Here are the key concepts for the mask.</span></span>

* <span data-ttu-id="791d1-230">마스크는 "유효 권한"을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-230">The mask creates "effective permissions."</span></span> <span data-ttu-id="791d1-231">즉 액세스 검사 시 권한을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-231">That is, it modifies the permissions at the time of access check.</span></span>
* <span data-ttu-id="791d1-232">파일 소유자와 모든 슈퍼 사용자가 마스크를 직접 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-232">The mask can be directly edited by the file owner and any super-users.</span></span>
* <span data-ttu-id="791d1-233">마스크는 권한을 제거하여 유효 권한을 만들 수 있지만,</span><span class="sxs-lookup"><span data-stu-id="791d1-233">The mask can remove permissions to create the effective permission.</span></span> <span data-ttu-id="791d1-234">유효 권한에 권한을 *추가할 수는 없습니다* .</span><span class="sxs-lookup"><span data-stu-id="791d1-234">The mask *cannot* add permissions to the effective permission.</span></span>

<span data-ttu-id="791d1-235">몇 가지 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-235">Let's look at some examples.</span></span> <span data-ttu-id="791d1-236">다음 예에서 마스크는 **RWX**로 설정되어 있습니다. 즉 마스크에서 어떤 권한도 제거하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-236">In the following example, the mask is set to **RWX**, which means that the mask does not remove any permissions.</span></span> <span data-ttu-id="791d1-237">명명된 사용자, 소유 그룹 및 명명된 그룹에 대한 유효 권한은 액세스 검사 중에 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-237">The effective permissions for the named user, owning group, and named group are not altered during the access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

<span data-ttu-id="791d1-239">다음 예에서 마스크는 **R-X**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-239">In the following example, the mask is set to **R-X**.</span></span> <span data-ttu-id="791d1-240">이는 액세스 검사 시 **명명된 사용자**, **소유 그룹** 및 **명명된 그룹**에 대한 **쓰기 권한을 해제함**을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-240">This means that it **turns off the Write permissions** for **named user**, **owning group**, and **named group** at the time of access check.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

<span data-ttu-id="791d1-242">참조를 위해 Azure Portal에서 파일이나 폴더에 대한 마스크를 표시하는 위치는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-242">For reference, here is where the mask for a file or folder appears in the Azure portal.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> <span data-ttu-id="791d1-244">새 Data Lake Store 계정의 경우 루트 폴더("/")의 액세스 ACL 및 기본 ACL에 대한 마스크는 기본적으로 RWX를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-244">For a new Data Lake Store account, the mask for the Access ACL and Default ACL of the root folder ("/") defaults to RWX.</span></span>
>
>

## <a name="permissions-on-new-files-and-folders"></a><span data-ttu-id="791d1-245">새 파일 및 폴더에 대한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="791d1-245">Permissions on new files and folders</span></span>

<span data-ttu-id="791d1-246">기존 폴더에서 새 파일이나 폴더를 만들 때 부모 폴더에 대한 기본 ACL은 다음 항목을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-246">When a new file or folder is created under an existing folder, the Default ACL on the parent folder determines:</span></span>

- <span data-ttu-id="791d1-247">자식 폴더의 기본 ACL 및 액세스 ACL</span><span class="sxs-lookup"><span data-stu-id="791d1-247">A child folder’s Default ACL and Access ACL.</span></span>
- <span data-ttu-id="791d1-248">자식 파일의 액세스 ACL(파일에 기본 ACL이 없는 경우)</span><span class="sxs-lookup"><span data-stu-id="791d1-248">A child file's Access ACL (files do not have a Default ACL).</span></span>

### <a name="the-access-acl-of-a-child-file-or-folder"></a><span data-ttu-id="791d1-249">자식 파일이나 폴더의 액세스 ACL</span><span class="sxs-lookup"><span data-stu-id="791d1-249">The Access ACL of a child file or folder</span></span>

<span data-ttu-id="791d1-250">자식 파일이나 폴더를 만들 때 부모의 기본 ACL이 자식 파일이나 폴더의 액세스 ACL로 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-250">When a child file or folder is created, the parent's Default ACL is copied as the Access ACL of the child file or folder.</span></span> <span data-ttu-id="791d1-251">또한 **다른** 사용자가 부모의 기본 ACL에서 RWX 권한을 가지고 있으면 자식 항목의 액세스 ACL에서 RWX 권한이 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-251">Also, if **other** user has RWX permissions in the parent's default ACL, it is removed from the child item's Access ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

<span data-ttu-id="791d1-253">대부분의 시나리오에서 자식 항목의 액세스 ACL을 결정하는 방법에 대해 알아야 할 것은 모두 위의 내용과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-253">In most scenarios, the previous information is all you need to know about how a child item’s Access ACL is determined.</span></span> <span data-ttu-id="791d1-254">하지만 POSIX 시스템에 잘 알고 있으며 이 변환이 수행되는 방법을 자세히 이해하려면 이 문서의 뒷부분에서 [새 파일 및 폴더에 대한 액세스 ACL을 만드는 Umask의 역할](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="791d1-254">However, if you are familiar with POSIX systems and want to understand in-depth how this transformation is achieved, see the section [Umask’s role in creating the Access ACL for new files and folders](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) later in this article.</span></span>


### <a name="a-child-folders-default-acl"></a><span data-ttu-id="791d1-255">자식 폴더의 기본 ACL</span><span class="sxs-lookup"><span data-stu-id="791d1-255">A child folder's Default ACL</span></span>

<span data-ttu-id="791d1-256">부모 폴더 아래에 자식 폴더를 만들 때 부모 폴더의 기본 ACL이 있는 그대로 자식 폴더의 기본 ACL에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-256">When a child folder is created under a parent folder, the parent folder's Default ACL is copied over as is to the child folder's Default ACL.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a><span data-ttu-id="791d1-258">Data Lake Store에서 ACL을 이해하기 위한 고급 항목</span><span class="sxs-lookup"><span data-stu-id="791d1-258">Advanced topics for understanding ACLs in Data Lake Store</span></span>

<span data-ttu-id="791d1-259">Data Lake Store 파일이나 폴더에 대한 ACL을 결정하는 방법을 이해하는 데 도움이 되는 몇 가지 고급 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-259">Following are some advanced topics to help you understand how ACLs are determined for Data Lake Store files or folders.</span></span>

### <a name="umasks-role-in-creating-the-access-acl-for-new-files-and-folders"></a><span data-ttu-id="791d1-260">새 파일 및 폴더에 대한 액세스 ACL을 만드는 Umask의 역할</span><span class="sxs-lookup"><span data-stu-id="791d1-260">Umask’s role in creating the Access ACL for new files and folders</span></span>

<span data-ttu-id="791d1-261">POSIX 호환 시스템에서 일반적인 개념은 umask가 새 자식 파일이나 폴더의 액세스 ACL에서 **소유 사용자**, **소유 그룹** 및 **기타**에 대한 권한을 변환하는 데 사용되는 부모 폴더의 9비트 값이라는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-261">In a POSIX-compliant system, the general concept is that umask is a 9-bit value on the parent folder that's used to transform the permission for **owning user**, **owning group**, and **other** on the Access ACL of a new child file or folder.</span></span> <span data-ttu-id="791d1-262">umask의 비트는 자식 항목의 액세스 ACL에서 해제되는 비트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-262">The bits of a umask identify which bits to turn off in the child item’s Access ACL.</span></span> <span data-ttu-id="791d1-263">따라서 **소유 사용자**, **소유 그룹** 및 **기타**에 대한 권한이 전파되지 않도록 선택적으로 방지하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-263">Thus it is used to selectively prevent the propagation of permissions for **owning user**, **owning group**, and **other**.</span></span>

<span data-ttu-id="791d1-264">HDFS 시스템에서 umask는 일반적으로 관리자가 제어하는 사이트 전체 구성 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-264">In an HDFS system, the umask is typically a sitewide configuration option that is controlled by administrators.</span></span> <span data-ttu-id="791d1-265">Data Lake Store는 변경할 수 없는 **계정 전체 umask** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-265">Data Lake Store uses an **account-wide umask** that cannot be changed.</span></span> <span data-ttu-id="791d1-266">다음 표에서는 Data Lake Store의 마스크 해제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-266">The following table shows the unmask for Data Lake Store.</span></span>

| <span data-ttu-id="791d1-267">사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="791d1-267">User group</span></span>  | <span data-ttu-id="791d1-268">설정</span><span class="sxs-lookup"><span data-stu-id="791d1-268">Setting</span></span> | <span data-ttu-id="791d1-269">새 자식 항목의 액세스 ACL에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="791d1-269">Effect on new child item's Access ACL</span></span> |
|------------ |---------|---------------------------------------|
| <span data-ttu-id="791d1-270">소유 사용자</span><span class="sxs-lookup"><span data-stu-id="791d1-270">Owning user</span></span> | ---     | <span data-ttu-id="791d1-271">영향 없음</span><span class="sxs-lookup"><span data-stu-id="791d1-271">No effect</span></span>                             |
| <span data-ttu-id="791d1-272">소유 그룹</span><span class="sxs-lookup"><span data-stu-id="791d1-272">Owning group</span></span>| ---     | <span data-ttu-id="791d1-273">영향 없음</span><span class="sxs-lookup"><span data-stu-id="791d1-273">No effect</span></span>                             |
| <span data-ttu-id="791d1-274">다른</span><span class="sxs-lookup"><span data-stu-id="791d1-274">Other</span></span>       | <span data-ttu-id="791d1-275">RWX</span><span class="sxs-lookup"><span data-stu-id="791d1-275">RWX</span></span>     | <span data-ttu-id="791d1-276">읽기 + 쓰기 + 실행 제거</span><span class="sxs-lookup"><span data-stu-id="791d1-276">Remove Read + Write + Execute</span></span>         |

<span data-ttu-id="791d1-277">다음 그림에서는 이 umask가 작동하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-277">The following illustration shows this umask in action.</span></span> <span data-ttu-id="791d1-278">순수 영향은 **다른** 사용자에 대한 **읽기 + 쓰기 + 실행**을 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-278">The net effect is to remove **Read + Write + Execute** for **other** user.</span></span> <span data-ttu-id="791d1-279">umask가 **소유 사용자** 및 **소유 그룹**에 대한 비트를 지정하지 않았기 때문에 이러한 권한은 변환되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-279">Because the umask did not specify bits for **owning user** and **owning group**, those permissions are not transformed.</span></span>

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="the-sticky-bit"></a><span data-ttu-id="791d1-281">고정 비트</span><span class="sxs-lookup"><span data-stu-id="791d1-281">The sticky bit</span></span>

<span data-ttu-id="791d1-282">고정 비트는 POSIX 파일 시스템의 고급 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-282">The sticky bit is a more advanced feature of a POSIX filesystem.</span></span> <span data-ttu-id="791d1-283">Data Lake Store의 컨텍스트에서 고정 비트가 필요할 가능성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-283">In the context of Data Lake Store, it is unlikely that the sticky bit will be needed.</span></span>

<span data-ttu-id="791d1-284">아래 표에서는 Data Lake Store에서 고정 비트가 작동하는 방식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-284">The following table shows how the sticky bit works in Data Lake Store.</span></span>

| <span data-ttu-id="791d1-285">사용자 그룹</span><span class="sxs-lookup"><span data-stu-id="791d1-285">User group</span></span>         | <span data-ttu-id="791d1-286">파일</span><span class="sxs-lookup"><span data-stu-id="791d1-286">File</span></span>    | <span data-ttu-id="791d1-287">폴더</span><span class="sxs-lookup"><span data-stu-id="791d1-287">Folder</span></span> |
|--------------------|---------|-------------------------|
| <span data-ttu-id="791d1-288">고정 비트 **끄기**</span><span class="sxs-lookup"><span data-stu-id="791d1-288">Sticky bit **OFF**</span></span> | <span data-ttu-id="791d1-289">영향 없음</span><span class="sxs-lookup"><span data-stu-id="791d1-289">No effect</span></span>   | <span data-ttu-id="791d1-290">영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-290">No effect.</span></span>           |
| <span data-ttu-id="791d1-291">고정 비트 **켜기**</span><span class="sxs-lookup"><span data-stu-id="791d1-291">Sticky bit **ON**</span></span>  | <span data-ttu-id="791d1-292">영향 없음</span><span class="sxs-lookup"><span data-stu-id="791d1-292">No effect</span></span>   | <span data-ttu-id="791d1-293">자식 항목의 **슈퍼 사용자** 및 **소유 사용자**를 제외하고 누구도 해당 자식 항목의 이름을 삭제하거나 바꾸지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-293">Prevents anyone except **super-users** and the **owning user** of a child item from deleting or renaming that child item.</span></span>               |

<span data-ttu-id="791d1-294">고정 비트는 Azure Portal에서 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-294">The sticky bit is not shown in the Azure portal.</span></span>

## <a name="common-questions-about-acls-in-data-lake-store"></a><span data-ttu-id="791d1-295">Data Lake Store의 ACL에 대한 일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="791d1-295">Common questions about ACLs in Data Lake Store</span></span>

<span data-ttu-id="791d1-296">Data Lake Store의 ACL에 대해 자주 제기하는 몇 가지 질문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-296">Here are some questions that come up often about ACLs in Data Lake Store.</span></span>

### <a name="do-i-have-to-enable-support-for-acls"></a><span data-ttu-id="791d1-297">ACL에 대한 지원을 사용하도록 설정해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="791d1-297">Do I have to enable support for ACLs?</span></span>

<span data-ttu-id="791d1-298">아니요.</span><span class="sxs-lookup"><span data-stu-id="791d1-298">No.</span></span> <span data-ttu-id="791d1-299">ACL을 통한 액세스 제어는 항상 Data Lake Store 계정에 대하여 켜져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-299">Access control via ACLs is always on for a Data Lake Store account.</span></span>

### <a name="which-permissions-are-required-to-recursively-delete-a-folder-and-its-contents"></a><span data-ttu-id="791d1-300">폴더 및 해당 내용을 재귀적으로 삭제하는 데 필요한 권한은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="791d1-300">Which permissions are required to recursively delete a folder and its contents?</span></span>

* <span data-ttu-id="791d1-301">부모 폴더에는 **쓰기 + 실행** 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-301">The parent folder must have **Write + Execute** permissions.</span></span>
* <span data-ttu-id="791d1-302">삭제할 폴더와 그 안의 모든 폴더에는 **읽기 + 쓰기 + 실행** 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-302">The folder to be deleted, and every folder within it, requires **Read + Write + Execute** permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="791d1-303">폴더의 파일을 삭제하는 데에는 쓰기 권한이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-303">You do not need Write permissions to delete files in folders.</span></span> <span data-ttu-id="791d1-304">또한 "/" 루트 폴더는 **절대로** 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-304">Also, the root folder "/" can **never** be deleted.</span></span>
>
>

### <a name="who-is-the-owner-of-a-file-or-folder"></a><span data-ttu-id="791d1-305">파일이나 폴더의 소유자는 누구인가요?</span><span class="sxs-lookup"><span data-stu-id="791d1-305">Who is the owner of a file or folder?</span></span>

<span data-ttu-id="791d1-306">파일 또는 폴더의 작성자는 소유자가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-306">The creator of a file or folder becomes the owner.</span></span>

### <a name="which-group-is-set-as-the-owning-group-of-a-file-or-folder-at-creation"></a><span data-ttu-id="791d1-307">파일이나 폴더를 만들 때 소유 그룹으로 설정되는 그룹은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="791d1-307">Which group is set as the owning group of a file or folder at creation?</span></span>

<span data-ttu-id="791d1-308">소유 그룹은 새 파일이나 폴더가 만들어지는 부모 폴더의 소유 그룹에서 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-308">The owning group is copied from the owning group of the parent folder under which the new file or folder is created.</span></span>

### <a name="i-am-the-owning-user-of-a-file-but-i-dont-have-the-rwx-permissions-i-need-what-do-i-do"></a><span data-ttu-id="791d1-309">파일의 소유 사용자이지만 필요한 RWX 사용 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-309">I am the owning user of a file but I don’t have the RWX permissions I need.</span></span> <span data-ttu-id="791d1-310">어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="791d1-310">What do I do?</span></span>

<span data-ttu-id="791d1-311">소유 사용자는 파일의 권한을 변경하여 필요한 RWX 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-311">The owning user can change the permissions of the file to give themselves any RWX permissions they need.</span></span>

### <a name="when-i-look-at-acls-in-the-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a><span data-ttu-id="791d1-312">Azure Portal에서 ACL을 확인할 때는 사용자 이름이 표시되지만 API를 통해 확인할 때는 GUID가 표시되는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="791d1-312">When I look at ACLs in the Azure portal I see user names but through APIs, I see GUIDs, why is that?</span></span>

<span data-ttu-id="791d1-313">ACL의 항목은 Azure AD의 사용자에 해당하는 GUID로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-313">Entries in the ACLs are stored as GUIDs that correspond to users in Azure AD.</span></span> <span data-ttu-id="791d1-314">API는 GUID를 있는 그대로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-314">The APIs return the GUIDs as is.</span></span> <span data-ttu-id="791d1-315">Azure Portal은 가능한 경우 GUID를 친숙한 이름으로 변환하여 ACL을 보다 쉽게 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-315">The Azure portal tries to make ACLs easier to use by translating the GUIDs into friendly names when possible.</span></span>

### <a name="why-do-i-sometimes-see-guids-in-the-acls-when-im-using-the-azure-portal"></a><span data-ttu-id="791d1-316">Azure Portal을 사용할 때 때때로 ACL에 GUID가 표시되는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="791d1-316">Why do I sometimes see GUIDs in the ACLs when I'm using the Azure portal?</span></span>

<span data-ttu-id="791d1-317">사용자가 Azure AD에 더 이상 존재하지 않으면 GUID가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-317">A GUID is shown when the user doesn't exist in Azure AD anymore.</span></span> <span data-ttu-id="791d1-318">일반적으로 사용자가 퇴사하거나 Azure AD에서 해당 계정이 삭제될 때 이러한 현상이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-318">Usually this happens when the user has left the company or if their account has been deleted in Azure AD.</span></span>

### <a name="does-data-lake-store-support-inheritance-of-acls"></a><span data-ttu-id="791d1-319">Data Lake Store는 ACL의 상속을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="791d1-319">Does Data Lake Store support inheritance of ACLs?</span></span>

<span data-ttu-id="791d1-320">아니요.</span><span class="sxs-lookup"><span data-stu-id="791d1-320">No.</span></span>

### <a name="what-is-the-difference-between-mask-and-umask"></a><span data-ttu-id="791d1-321">마스크와 umask 간의 차이는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="791d1-321">What is the difference between mask and umask?</span></span>

| <span data-ttu-id="791d1-322">마스크</span><span class="sxs-lookup"><span data-stu-id="791d1-322">mask</span></span> | <span data-ttu-id="791d1-323">umask</span><span class="sxs-lookup"><span data-stu-id="791d1-323">umask</span></span>|
|------|------|
| <span data-ttu-id="791d1-324">**마스크** 속성은 모든 파일 및 폴더에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-324">The **mask** property is available on every file and folder.</span></span> | <span data-ttu-id="791d1-325">**umask** 는 Data Lake Store 계정의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-325">The **umask** is a property of the Data Lake Store account.</span></span> <span data-ttu-id="791d1-326">따라서 Data Lake Store에는 단 하나의 umask만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-326">So there is only a single umask in the Data Lake Store.</span></span>    |
| <span data-ttu-id="791d1-327">파일의 소유 사용자 또는 소유 그룹이나 슈퍼 사용자는 파일 또는 폴더에 대한 마스크 속성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-327">The mask property on a file or folder can be altered by the owning user or owning group of a file or a super-user.</span></span> | <span data-ttu-id="791d1-328">슈퍼 사용자를 포함한 모든 사용자는 umask 속성을 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-328">The umask property cannot be modified by any user, even a super-user.</span></span> <span data-ttu-id="791d1-329">변경할 수 없는 상수 값입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-329">It is an unchangeable, constant value.</span></span>|
| <span data-ttu-id="791d1-330">mask 속성은 런타임 시 액세스 검사 알고리즘에서 사용되어 사용자가 파일이나 폴더의 작업에서 수행할 수 있는 권한을 가지고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-330">The mask property is used during the access check algorithm at runtime to determine whether a user has the right to perform on operation on a file or folder.</span></span> <span data-ttu-id="791d1-331">마스크의 역할은 액세스 확인 시 "유효 사용 권한"을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-331">The role of the mask is to create "effective permissions" at the time of access check.</span></span> | <span data-ttu-id="791d1-332">umask는 액세스 검사 중에 전혀 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-332">The umask is not used during access check at all.</span></span> <span data-ttu-id="791d1-333">umask는 폴더의 새 자식 항목에서 액세스 ACL을 결정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-333">The umask is used to determine the Access ACL of new child items of a folder.</span></span> |
| <span data-ttu-id="791d1-334">마스크는 액세스 확인 시 명명된 사용자, 명명된 그룹 및 소유 사용자에 적용되는 3비트 RWX 값입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-334">The mask is a 3-bit RWX value that applies to named user, named group, and owning user at the time of access check.</span></span>| <span data-ttu-id="791d1-335">umask는 새로운 자식의 소유 사용자, 소유 그룹 및 **기타**에 적용되는 9비트 값입니다.</span><span class="sxs-lookup"><span data-stu-id="791d1-335">The umask is a 9-bit value that applies to the owning user, owning group, and **other** of a new child.</span></span>|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a><span data-ttu-id="791d1-336">POSIX 액세스 제어 모델에 대한 어디서 자세히 알아볼 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="791d1-336">Where can I learn more about POSIX access control model?</span></span>

* <span data-ttu-id="791d1-337">[Linux의 POSIX 액세스 제어 목록](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="791d1-337">[POSIX Access Control Lists on Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)</span></span>

* <span data-ttu-id="791d1-338">[HDFS 권한 가이드](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)(영문)</span><span class="sxs-lookup"><span data-stu-id="791d1-338">[HDFS permission guide](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)</span></span>

* [<span data-ttu-id="791d1-339">POSIX FAQ</span><span class="sxs-lookup"><span data-stu-id="791d1-339">POSIX FAQ</span></span>](http://www.opengroup.org/austin/papers/posix_faq.html)

* [<span data-ttu-id="791d1-340">POSIX 1003.1 2008</span><span class="sxs-lookup"><span data-stu-id="791d1-340">POSIX 1003.1 2008</span></span>](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [<span data-ttu-id="791d1-341">POSIX 1003.1 2013</span><span class="sxs-lookup"><span data-stu-id="791d1-341">POSIX 1003.1 2013</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [<span data-ttu-id="791d1-342">POSIX 1003.1 2016</span><span class="sxs-lookup"><span data-stu-id="791d1-342">POSIX 1003.1 2016</span></span>](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [<span data-ttu-id="791d1-343">Ubuntu의 POSIX ACL</span><span class="sxs-lookup"><span data-stu-id="791d1-343">POSIX ACL on Ubuntu</span></span>](https://help.ubuntu.com/community/FilePermissionsACLs)

* <span data-ttu-id="791d1-344">[ACL: Linux의 액세스 제어 목록 사용](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)(영문)</span><span class="sxs-lookup"><span data-stu-id="791d1-344">[ACL using access control lists on Linux](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)</span></span>

## <a name="see-also"></a><span data-ttu-id="791d1-345">참고 항목</span><span class="sxs-lookup"><span data-stu-id="791d1-345">See also</span></span>

* [<span data-ttu-id="791d1-346">Azure 데이터 레이크 저장소 개요</span><span class="sxs-lookup"><span data-stu-id="791d1-346">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
