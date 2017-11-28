---
title: "PowerShell 스크립트 샘플-aaaAzure cert tooa 클러스터 응용 프로그램 추가 | Microsoft Docs"
description: "Azure PowerShell 스크립트 예제-는 응용 프로그램 인증서 tooa 서비스 패브릭 클러스터를 추가 합니다."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="1f148-103">응용 프로그램 인증서 tooa 서비스 패브릭 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="1f148-104">이 샘플 스크립트 hello 지정 된 Azure 키 자격 증명 모음에 자체 서명 된 인증서를 만들고 tooall 노드의 hello 서비스 패브릭 클러스터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="1f148-105">또한 hello 인증서 tooa 로컬 폴더를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="1f148-106">hello 다운로드 한 인증서의 hello 이름 hello 주요 자격 증명 모음에 hello 인증서의 hello 이름과 달라 서 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="1f148-107">필요에 따라 hello 매개 변수를 사용자 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="1f148-108">필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview) 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="1f148-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="1f148-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="1f148-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="1f148-110">Script explanation</span></span>

<span data-ttu-id="1f148-111">이 스크립트 명령 뒤 hello 사용: hello 테이블의 각 명령이 toocommand 특정 문서에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1f148-112">명령</span><span class="sxs-lookup"><span data-stu-id="1f148-112">Command</span></span> | <span data-ttu-id="1f148-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1f148-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1f148-114">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="1f148-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="1f148-115">새 응용 프로그램 인증서 toohello 가상 컴퓨터 크기 집합 hello 클러스터를 구성 하는 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="1f148-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1f148-116">Next steps</span></span>

<span data-ttu-id="1f148-117">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1f148-118">Azure Service Fabric에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1f148-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
