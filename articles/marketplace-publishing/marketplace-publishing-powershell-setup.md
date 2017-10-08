---
title: "PowerShell toocreate 마켓플레이스 hello에 대 한 VM aaaSet | Microsoft Docs"
description: "Azure PowerShell을 설정 하 고 사용 하 여 선택적 되는 프로세스에 대 한 지침, toocreate VM 이미지 toodeploy 흐름 및에서 판매할 hello Azure 마켓플레이스"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="5e28a-103">Azure PowerShell toocreate hello Azure Marketplace에 대 한 제안을 설정합니다</span><span class="sxs-lookup"><span data-stu-id="5e28a-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="5e28a-104">방법에 대 한 자세한 내용은 tooset Azure에서 PowerShell 참조 하세요. [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="5e28a-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5e28a-105">간단한 방법은 toouse hello 인증서 메서드를 다운로드 하 고 인증에 필요한 인증서를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="5e28a-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="5e28a-106">tooobtain hello 필요한 인증서, hello를 사용 하 여 **Get-azurepublishsettingsfile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5e28a-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="5e28a-107">메시지가 나타나면 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e28a-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="5e28a-108">PowerShell 세션을 사용 하 여 hello에 tooimport hello 인증서 **Import-azurepublishsettingsfile** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5e28a-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="5e28a-109">tooconfigure 및 스토어 hello 일반적인 Microsoft Azure 구독 설정 hello PowerShell 세션에 대 한 hello를 사용 하 여 **집합 AzureSubscription** 및 **Select-azuresubscription** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5e28a-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="5e28a-110">hello 첫 번째 명령은 기본 저장소 계정 (일부 VM 프로 비전 작업에 필요) hello 구독에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e28a-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="5e28a-111">두 번째 hello (다른 cmdlet에서 인식 됨)는 현재 하나 hello hello 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e28a-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="5e28a-112">참고 항목</span><span class="sxs-lookup"><span data-stu-id="5e28a-112">See also</span></span>
* [<span data-ttu-id="5e28a-113">시작 하기: 어떻게 toopublish 제안 toohello Azure 마켓플레이스</span><span class="sxs-lookup"><span data-stu-id="5e28a-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="5e28a-114">마켓플레이스 hello에 대 한 가상 컴퓨터 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="5e28a-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

