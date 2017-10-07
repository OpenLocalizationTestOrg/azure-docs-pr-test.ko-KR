---
ms.assetid: 
title: "주요 자격 증명 모음 보안 권역 aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="01d10-102">Azure Key Vault 보안 권역 및 지리적 경계</span><span class="sxs-lookup"><span data-stu-id="01d10-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="01d10-103">Azure Key Vault는 다중 테넌트 서비스이며, 각 Azure 위치의 HSM(하드웨어 보안 모듈) 풀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="01d10-104">모든 Hsm hello의 Azure 위치에 동일한 지리적 지역 공유 hello 동일한 암호화 경계 (Thales 보안 권역).</span><span class="sxs-lookup"><span data-stu-id="01d10-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="01d10-105">예를 들어 미국 동부 및 공유 미국 서 부 hello 동일한 보안 권역 toohello 미국 지리적 위치에 속하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="01d10-106">마찬가지로, 일본 공유의 모든 Azure 위치 오스트레일리아, 인도의 모든 Azure 위치와 동일한 보안 권역 hello 등에입니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="01d10-107">백업 및 복원 동작</span><span class="sxs-lookup"><span data-stu-id="01d10-107">Backup and restore behavior</span></span>

<span data-ttu-id="01d10-108">이러한 조건에 모두으로 다른 Azure 위치에 tooa에 키 자격 증명 모음. 복원 하는 Azure 위치 일 수 있습니다 하나에 키 자격 증명 모음에서 키의 백업:</span><span class="sxs-lookup"><span data-stu-id="01d10-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="01d10-109">모두 hello Azure 위치 toohello 속한 동일한 지리적 위치</span><span class="sxs-lookup"><span data-stu-id="01d10-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="01d10-110">Toohello 속한 hello 키 자격 증명 모음을 모두 동일한 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="01d10-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="01d10-111">예를 들어, 서인도에서 주요 자격 증명 모음에 있는 키의 지정 된 구독에 의해 발생 한 백업만 수 hello에 복원 된 tooanother에 키 자격 증명 모음. 동일한 구독과 지리적 위치입니다. 인도 서 부, 중앙 인도 또는 남 인도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="01d10-112">지역 및 제품</span><span class="sxs-lookup"><span data-stu-id="01d10-112">Regions and products</span></span>

- [<span data-ttu-id="01d10-113">Azure 지역</span><span class="sxs-lookup"><span data-stu-id="01d10-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="01d10-114">지역별 Microsoft 제품</span><span class="sxs-lookup"><span data-stu-id="01d10-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="01d10-115">지역에 매핑된 toosecurity 세계, 주요 hello 테이블 제목으로 표시 되는</span><span class="sxs-lookup"><span data-stu-id="01d10-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="01d10-116">예를 들어 hello 지역 문서에서 제품 hello에서는 **Americas** 탭 영역이 EAST US, 미국 중남부, 미국 서 부 모든 매핑 toohello Americas 합니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="01d10-117">예외로, 미국 국방부 동부 및 미국 국방부 중부에는 자체 보안 권역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="01d10-118">마찬가지로 hello에서 **유럽** 탭, 유럽 북부 및 서 부 유럽 모두 매핑할 toohello Europe 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="01d10-119">hello도 마찬가지입니다 hello에 **아시아 태평양** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="01d10-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



