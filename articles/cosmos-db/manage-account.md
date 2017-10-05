---
title: "Azure Portal을 통해 Azure Cosmos DB 계정 관리 | Microsoft Docs"
description: "Azure Portal을 통해 Azure Cosmos DB 계정을 관리하는 방법을 알아봅니다. Azure 포털을 사용하여 계정을 보기, 복사, 삭제 및 액세스하는 방법에 대한 지침을 찾습니다."
keywords: "Azure 포털, Documentdb, Azure, Microsoft Azure"
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="a4843-105">Azure Cosmos DB 계정을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="a4843-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="a4843-106">Azure Portal에서 전역 일관성을 설정하고, 키로 작업하고, Azure Cosmos DB 계정을 삭제하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="a4843-107"><a id="consistency"></a>Azure Cosmos DB 일관성 설정 관리</span><span class="sxs-lookup"><span data-stu-id="a4843-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="a4843-108">올바른 일관성 수준을 선택하는 것은 응용 프로그램의 의미 체계에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="a4843-109">[일관성 수준을 사용하여 Azure Cosmos DB의 가용성 및 성능 최대화][consistency]의 내용을 확인하여 Azure Cosmos DB에서 사용 가능한 일관성 수준을 숙지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="a4843-110">Azure Cosmos DB는 데이터베이스 계정에서 사용할 수 있는 모든 일관성 수준에서 일관성, 가용성 및 성능을 보증합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="a4843-111">일관성 수준 '강력'으로 데이터베이스 계정을 구성하려면 데이터를 단일 Azure 지역에서만 사용할 수 있도록 제한하고 전 세계적으로 제공하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="a4843-112">반면, 관대한 일관성 수준(제한된 부실, 세션 또는 최종 일관성)은 데이터베이스 계정과 여러 Azure 지역을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="a4843-113">아래의 간단한 단계는 데이터베이스 계정에서 기본 일관성 수준을 선택하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="a4843-114">Azure Cosmos DB 계정의 기본 일관성을 지정하려면</span><span class="sxs-lookup"><span data-stu-id="a4843-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="a4843-115">[Azure Portal](https://portal.azure.com/)에서 Azure Cosmos DB 계정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="a4843-116">계정 블레이드에서 **기본 일관성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="a4843-117">**기본 일관성** 블레이드에서 새 일관성 수준을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="a4843-118">![기본 일관성 세션][5]</span><span class="sxs-lookup"><span data-stu-id="a4843-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="a4843-119"><a id="keys"></a>선택키 보기, 복사 및 다시 생성</span><span class="sxs-lookup"><span data-stu-id="a4843-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="a4843-120">Azure Cosmos DB 계정을 만들면 해당 서비스에서 Azure Cosmos DB 계정에 액세스할 때 인증에 사용할 수 있는 2개의 마스터 액세스 키가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="a4843-121">Azure Cosmos DB에서는 2개의 액세스 키를 제공해서 사용자가 Azure Cosmos DB 계정에 대한 중단 없이 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="a4843-122">[Azure Portal](https://portal.azure.com/)에서 **Azure Cosmos DB 계정** 블레이드의 리소스 메뉴에 있는 **키** 블레이드에 액세스하여 Azure Cosmos DB 계정에 액세스하는 데 사용되는 선택키를 표시, 복사 및 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Azure 포털 스크린샷, 키 블레이드](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="a4843-124">**키** 블레이드에는 [데이터 마이그레이션 도구](import-data.md)에서 계정에 연결하는 데 사용할 수 있는 기본 및 보조 연결 문자열도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="a4843-125">읽기 전용 키도 이 블레이드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="a4843-126">읽기 및 쿼리는 읽기 전용 작업이며 만들기, 삭제 및 바꾸기는 읽기 전용 작업이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="a4843-127">Azure 포털에서 선택키 복사</span><span class="sxs-lookup"><span data-stu-id="a4843-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="a4843-128">**키** 블레이드에서 복사할 키 오른쪽의 **복사** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Azure 포털에서 선택키 보기 및 복사, 키 블레이드](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="a4843-130">액세스 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="a4843-130">Regenerate access keys</span></span>
<span data-ttu-id="a4843-131">저장소 연결을 더욱 안전하게 유지할 수 있도록 정기적으로 Azure Cosmos DB 계정의 액세스 키를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="a4843-132">두 개의 액세스 키가 할당되므로 액세스 키 하나를 다시 생성하는 동안 다른 액세스 키를 사용하여 Azure Cosmos DB 계정에 대한 연결을 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="a4843-133">액세스 키를 다시 생성하면 현재 키에 종속된 모든 응용 프로그램에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="a4843-134">액세스 키를 사용하여 Azure Cosmos DB 계정에 액세스하는 모든 클라이언트가 새 키를 사용하도록 업데이트되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="a4843-135">Azure Cosmos DB 계정을 사용하는 웹 응용 프로그램이나 클라우드 서비스가 있는 경우 키를 롤링하지 않고 다시 생성하면 연결이 끊어집니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="a4843-136">다음 단계에서는 키 롤링에 관련된 프로세스를 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="a4843-137">Azure Cosmos DB 계정의 보조 액세스 키를 참조하도록 응용 프로그램 코드의 액세스 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="a4843-138">Azure Cosmos DB 계정의 기본 액세스 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="a4843-139">[Azure Portal](https://portal.azure.com/)에서 Azure Cosmos DB 계정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="a4843-140">**Azure Cosmos DB 계정** 블레이드에서 **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="a4843-141">**키** 블레이드에서 다시 생성 단추를 클릭한 다음 **확인**을 클릭하여 새 키를 생성할 것임을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="a4843-142">![액세스 키 다시 생성](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="a4843-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="a4843-143">키를 다시 생성하고 약 5분 후에 새 키를 사용할 수 있는지 확인한 후 응용 프로그램 코드에서 새 기본 액세스 키를 참조하도록 액세스 키를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="a4843-144">보조 액세스 키를 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-144">Regenerate the secondary access key.</span></span>
   
    ![액세스 키 다시 생성](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="a4843-146">새로 생성된 키를 사용하여 Azure Cosmos DB 계정에 액세스할 수 있을 때까지 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="a4843-147">연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="a4843-147">Get the  connection string</span></span>
<span data-ttu-id="a4843-148">연결 문자열을 검색하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="a4843-149">[Azure Portal](https://portal.azure.com)에서 Azure Cosmos DB 계정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="a4843-150">리소스 메뉴에서 **키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="a4843-151">**기본 연결 문자열** 또는 **보조 연결 문자열** 상자 옆의 **복사** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="a4843-152">[Azure Cosmos DB 데이터베이스 마이그레이션 도구](import-data.md)에서 연결 문자열을 사용하는 경우 연결 문자열 끝에 데이터베이스 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="a4843-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="a4843-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="a4843-154"><a id="delete"></a> Azure Cosmos DB 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="a4843-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="a4843-155">Azure Portal에서 더 이상 사용하지 않는 Azure Cosmos DB 계정을 제거하려면 계정 이름을 마우스 오른쪽 단추로 클릭하고 **계정 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Azure Portal에서 Azure Cosmos DB 계정을 삭제하는 방법](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="a4843-157">[Azure Portal](https://portal.azure.com/)에서 삭제할 Azure Cosmos DB 계정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="a4843-158">**Azure Cosmos DB 계정** 블레이드에서 계정을 마우스 오른쪽 단추로 클릭하고 **계정 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="a4843-159">그러면 표시되는 확인 블레이드에서 Azure Cosmos DB 계정 이름을 입력하여 계정을 삭제할 것임을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="a4843-160">**삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-160">Click the **Delete** button.</span></span>

![Azure Portal에서 Azure Cosmos DB 계정을 삭제하는 방법](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="a4843-162"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="a4843-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="a4843-163">[Azure Cosmos DB 계정을 사용하기 시작](http://go.microsoft.com/fwlink/p/?LinkId=402364)하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="a4843-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
