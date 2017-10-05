---
ms.assetid: 
title: "Azure Key Vault 보안 권역 | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 921bbd109c9ea98d8b5c286a7512bed026412d26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="8d9a5-102">Azure Key Vault 보안 권역 및 지리적 경계</span><span class="sxs-lookup"><span data-stu-id="8d9a5-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="8d9a5-103">Azure Key Vault는 다중 테넌트 서비스이며, 각 Azure 위치의 HSM(하드웨어 보안 모듈) 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="8d9a5-104">동일한 지역의 Azure 위치에 있는 모든 HSM은 동일한 암호화 경계(Thales 보안 권역)를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-104">All HSMs at Azure locations in the same geographic region share the same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="8d9a5-105">예를 들어 미국 동부 및 미국 서부는 미국 지리적 위치에 속하기 때문에 동일한 보안 권역을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-105">For example, East US and West US share the same security world because they belong to the US geo location.</span></span> <span data-ttu-id="8d9a5-106">일본의 모든 Azure 위치는 동일한 보안 권역을 공유하고 오스트레일리아, 인도 등의 모든 Azure 위치도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-106">Similarly, all Azure locations in Japan share the same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="8d9a5-107">백업 및 복원 동작</span><span class="sxs-lookup"><span data-stu-id="8d9a5-107">Backup and restore behavior</span></span>

<span data-ttu-id="8d9a5-108">다음 조건이 둘 다 true이기만 하면 특정 Azure 위치의 주요 자격 증명 모음에서 생성한 키 백업을 다른 Azure 위치의 주요 자격 증명 모음으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-108">A backup taken of a key from a key vault in one Azure location can be restored to a key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="8d9a5-109">두 Azure 위치는 동일한 지리적 위치에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-109">Both of the Azure locations belong to the same geographical location</span></span>
- <span data-ttu-id="8d9a5-110">두 주요 자격 증명 모음이 동일한 Azure 구독에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-110">Both of the key vaults belong to the same Azure subscription</span></span>

<span data-ttu-id="8d9a5-111">예를 들어 인도 서부에 있는 주요 자격 증명 모음의 키에 대해 지정된 구독이 생성한 백업은 동일한 구독 및 지리적 위치(인도 서부, 인도 중부 또는 인도 남부)에 있는 다른 주요 자격 증명 모음으로만 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored to another key vault in the same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="8d9a5-112">지역 및 제품</span><span class="sxs-lookup"><span data-stu-id="8d9a5-112">Regions and products</span></span>

- [<span data-ttu-id="8d9a5-113">Azure 지역</span><span class="sxs-lookup"><span data-stu-id="8d9a5-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="8d9a5-114">지역별 Microsoft 제품</span><span class="sxs-lookup"><span data-stu-id="8d9a5-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="8d9a5-115">지역은 표에서 주요 제목으로 표시된 보안 권역에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-115">Regions are mapped to security worlds, shown as major headings in the tables:</span></span>

<span data-ttu-id="8d9a5-116">예를 들어 지역별 제품 문서에서 **아메리카** 탭에는 미국 동부, 미국 중부, 미국 서부가 모두 아메리카 지역에 매핑되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-116">In the products by region article, for example, the **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping to the Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="8d9a5-117">예외로, 미국 국방부 동부 및 미국 국방부 중부에는 자체 보안 권역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="8d9a5-118">마찬가지로, **유럽** 탭에는 북유럽 및 서유럽이 둘 다 유럽 지역에 매핑되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-118">Similarly, on the **Europe** tab, NORTH EUROPE and WEST EUROPE both map to the Europe region.</span></span> <span data-ttu-id="8d9a5-119">**아시아 태평양** 탭에서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="8d9a5-119">The same is also true on the **Asia Pacific** tab.</span></span>



