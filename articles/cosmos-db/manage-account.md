---
title: "hello Azure 포털을 통해 Azure Cosmos DB 계정 aaaManage | Microsoft Docs"
description: "어떻게 toomanage Azure Cosmos DB는 hello Azure 포털을 통해을 계정에 대해 알아봅니다. Azure 포털 tooview hello, 복사, 삭제 및 액세스 계정 사용에 대 한 지침을 찾습니다."
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
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="7d8af-105">어떻게 toomanage Azure Cosmos DB 계정</span><span class="sxs-lookup"><span data-stu-id="7d8af-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="7d8af-106">자세한 내용은 tooset 전역 일관성을, 키를 사용 하 고 hello Azure 포털에서에서 Azure Cosmos DB 계정을 삭제 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="7d8af-107"><a id="consistency"></a>Azure Cosmos DB 일관성 설정 관리</span><span class="sxs-lookup"><span data-stu-id="7d8af-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="7d8af-108">Hello 오른쪽 일관성 수준을 선택 하는 응용 프로그램의 hello 의미 체계에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="7d8af-109">잘 이해 해야 Azure Cosmos DB에 hello 사용할 수 있는 일관성 수준으로 읽어 [toomaximize 가용성 및 Azure Cosmos DB의 성능 수준 일관성을 사용 하 여][consistency]합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="7d8af-110">Azure Cosmos DB는 데이터베이스 계정에서 사용할 수 있는 모든 일관성 수준에서 일관성, 가용성 및 성능을 보증합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="7d8af-111">강력한 일관성 수준이 데이터베이스 계정을 구성 하려면 데이터를 단일 Azure 지역 예외일된 tooa 및 전체적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="7d8af-112">반면 hello, bounded 부실, 세션 또는 최종 사용 상대적으로 느 일관성 수준-hello 있습니다 tooassociate 개수에 관계 없이 데이터베이스 계정 사용 하 여 Azure 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="7d8af-113">간단한 단계를 수행 하는 hello tooselect 기본 일관성 수준이 데이터베이스 계정에 대 한 hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="7d8af-114">Cosmos DB Azure 계정에 대 한 toospecify hello 기본 일관성</span><span class="sxs-lookup"><span data-stu-id="7d8af-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="7d8af-115">Hello에 [Azure 포털](https://portal.azure.com/), Azure Cosmos DB 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7d8af-116">Hello 계정 블레이드에서 클릭 **일관성 기본**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="7d8af-117">Hello에 **기본 일관성** 블레이드, 새 일관성 수준 선택 hello 및 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="7d8af-118">![기본 일관성 세션][5]</span><span class="sxs-lookup"><span data-stu-id="7d8af-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="7d8af-119"><a id="keys"></a>선택키 보기, 복사 및 다시 생성</span><span class="sxs-lookup"><span data-stu-id="7d8af-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="7d8af-120">Azure Cosmos DB 계정을 만들 때 hello 서비스는 hello Azure Cosmos DB 계정에 액세스할 때 인증에 사용할 수 있는 두 개의 마스터 액세스 키를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="7d8af-121">두 개의 액세스 키를 제공 함으로써 Azure Cosmos DB 하면 없는 중단 tooyour Azure Cosmos DB 계정 사용 하 여 tooregenerate hello 키.</span><span class="sxs-lookup"><span data-stu-id="7d8af-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="7d8af-122">Hello에 [Azure 포털](https://portal.azure.com/), 액세스 hello **키** hello hello 메뉴 리소스에서에서 블레이드 **Azure Cosmos DB 계정** 블레이드 tooview / 복사 / 재생성 hello 액세스 키를 사용 되는 tooaccess Azure Cosmos DB 계정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Azure 포털 스크린샷, 키 블레이드](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="7d8af-124">hello **키** 블레이드도 포함 되어 기본 및 hello에서 계정을 사용 하는 tooconnect tooyour 일 수 있는 보조 연결 문자열 [데이터 마이그레이션 도구](import-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="7d8af-125">읽기 전용 키도 이 블레이드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="7d8af-126">읽기 및 쿼리는 읽기 전용 작업이며 만들기, 삭제 및 바꾸기는 읽기 전용 작업이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="7d8af-127">Hello Azure 포털의에서 선택 키 복사</span><span class="sxs-lookup"><span data-stu-id="7d8af-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="7d8af-128">Hello에 **키** 블레이드에서 hello 클릭 **복사** toocopy 원하는 단추 toohello hello 키의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![표시 및 선택 키 hello 키 블레이드에서 Azure 포털에서 복사](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="7d8af-130">액세스 키 다시 생성</span><span class="sxs-lookup"><span data-stu-id="7d8af-130">Regenerate access keys</span></span>
<span data-ttu-id="7d8af-131">Hello 액세스 키 tooyour Azure Cosmos DB 계정을 변경 해야 주기적으로 toohelp 유지 되며 연결 더 안전 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="7d8af-132">두 개의 액세스 키 tooenable 할당 하면 toomaintain 연결 toohello 다시 생성 하는 동안에 한 선택 키를 사용 하 여 Azure Cosmos DB 계정을 hello 다른 선택 키입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="7d8af-133">액세스 키 다시 생성 하는 hello 현재 키에 의존 하는 모든 응용 프로그램을 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="7d8af-134">Hello 액세스 키 tooaccess hello Azure Cosmos DB 계정을 사용 하는 모든 클라이언트에 업데이트 된 toouse hello에 대 한 새 키 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="7d8af-135">응용 프로그램 또는 Azure Cosmos DB 계정 hello를 사용 하 여 클라우드 서비스를 설정한 경우 손실 됩니다 hello 연결 키를 다시 생성 하는 경우 키 롤 하지 않는 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="7d8af-136">hello 다음 단계에 간략하게 설명 키 롤링에 관련 된 hello 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="7d8af-137">응용 프로그램 코드 tooreference hello 보조 액세스 키의 hello Azure Cosmos DB 계정에 대 한 hello 액세스 키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7d8af-138">Cosmos DB Azure 계정에 대 한 hello 기본 액세스 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="7d8af-139">Hello에 [Azure 포털](https://portal.azure.com/), Azure Cosmos DB 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="7d8af-140">Hello에 **Azure Cosmos DB 계정** 블레이드에서 클릭 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="7d8af-141">Hello에 **키** 블레이드에서 hello 다시 생성 단추를 클릭 한 다음 클릭 **확인** tooconfirm 원하는 toogenerate 새 키입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="7d8af-142">![액세스 키 다시 생성](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="7d8af-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="7d8af-143">해당 hello 새 키를 사용 하기 위해 사용할 수를 확인 한 후 (약 5 분 후 다시 생성), 응용 프로그램 코드 tooreference hello 새 기본 액세스 키에 대 한 hello 액세스 키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="7d8af-144">Hello 보조 액세스 키 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-144">Regenerate hello secondary access key.</span></span>
   
    ![액세스 키 다시 생성](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="7d8af-146">Azure Cosmos DB 계정을 새로 생성 된 키를 사용 하는 tooaccess 수 전에 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="7d8af-147">Hello 구성 된 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="7d8af-147">Get hello  connection string</span></span>
<span data-ttu-id="7d8af-148">tooretrieve 연결 문자열, 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="7d8af-149">Hello에 [Azure 포털](https://portal.azure.com), Azure Cosmos DB 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="7d8af-150">Hello 리소스 메뉴에서 클릭 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="7d8af-151">Hello 클릭 **복사** 단추 다음 toohello **기본 연결 문자열** 또는 **보조 연결 문자열** 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="7d8af-152">Hello에서 연결 문자열 hello를 사용 하는 경우 [Azure Cosmos DB 데이터베이스 마이그레이션 도구](import-data.md), hello 데이터베이스 이름 toohello hello 연결 문자열의 끝에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="7d8af-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`</span><span class="sxs-lookup"><span data-stu-id="7d8af-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="7d8af-154"><a id="delete"></a> Azure Cosmos DB 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="7d8af-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="7d8af-155">tooremove Azure Cosmos DB 계정에서 hello Azure 포털 더 이상 사용 하는 hello 계정 이름 마우스 오른쪽 단추로 클릭 하 고 클릭 **계정 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![에 Azure Cosmos DB toodelete 계정을 방법 hello Azure 포털](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="7d8af-157">Hello에 [Azure 포털](https://portal.azure.com/), toodelete 원하는 hello Azure Cosmos DB 계정에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="7d8af-158">Hello에 **Azure Cosmos DB 계정** 블레이드에서 hello 계정을 마우스 오른쪽 단추로 클릭 하 고 **계정 삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="7d8af-159">결과 확인 블레이드에서 hello hello Azure Cosmos DB 계정 이름 tooconfirm toodelete hello 계정 한다는 것을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="7d8af-160">Hello 클릭 **삭제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-160">Click hello **Delete** button.</span></span>

![에 Azure Cosmos DB toodelete 계정을 방법 hello Azure 포털](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="7d8af-162"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="7d8af-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="7d8af-163">너무 방법에 대해 알아봅니다[Azure Cosmos DB 계정 시작](http://go.microsoft.com/fwlink/p/?LinkId=402364)합니다.</span><span class="sxs-lookup"><span data-stu-id="7d8af-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
