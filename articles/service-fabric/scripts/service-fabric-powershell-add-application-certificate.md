---
title: "Azure PowerShell 스크립트 샘플 - 클러스터에 응용 프로그램 인증서 추가 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 클러스터에 응용 프로그램 인증서 추가"
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
ms.openlocfilehash: 9ccd6bb0458bc03e52103fa70cad26bd6bf98bd5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a><span data-ttu-id="75bbc-103">Service Fabric 클러스터에 응용 프로그램 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="75bbc-103">Add an application certificate to a Service Fabric cluster</span></span>

<span data-ttu-id="75bbc-104">이 샘플 스크립트는 지정된 Azure Key Vault에서 자체 서명된 인증서를 만들고 Service Fabric 클러스터의 모든 노드에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-104">This sample script creates a self-signed certificate in the specified Azure key vault and installs it to all nodes of the Service Fabric cluster.</span></span> <span data-ttu-id="75bbc-105">또한 인증서는 로컬 폴더로도 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-105">The certificate also downloads to a local folder.</span></span> <span data-ttu-id="75bbc-106">다운로드한 인증서의 이름은 Key Vault의 인증서 이름과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-106">The name of the downloaded certificate is the same as the name of the certificate in the key vault.</span></span> <span data-ttu-id="75bbc-107">필요에 따라 매개 변수를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-107">Customize the parameters as needed.</span></span>

<span data-ttu-id="75bbc-108">필요한 경우 [Azure PowerShell 가이드](/powershell/azure/overview)에 있는 지침을 사용하여 Azure PowerShell을 설치한 다음, `Login-AzureRmAccount`를 실행하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="75bbc-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="75bbc-109">Sample script</span></span>

<span data-ttu-id="75bbc-110">[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "클러스터에 응용 프로그램 인증서 추가")]</span><span class="sxs-lookup"><span data-stu-id="75bbc-110">[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate to a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="75bbc-111">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="75bbc-111">Script explanation</span></span>

<span data-ttu-id="75bbc-112">이 스크립트는 다음 명령을 사용합니다. 표의 각 명령은 명령 관련 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-112">This script uses the following commands: Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="75bbc-113">명령</span><span class="sxs-lookup"><span data-stu-id="75bbc-113">Command</span></span> | <span data-ttu-id="75bbc-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="75bbc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="75bbc-115">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="75bbc-115">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="75bbc-116">클러스터를 구성하는 가상 컴퓨터 확장 집합에 새 응용 프로그램 인증서를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-116">Add a new application certificate to the virtual machine scale set that make up the cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="75bbc-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="75bbc-117">Next steps</span></span>

<span data-ttu-id="75bbc-118">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75bbc-118">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="75bbc-119">Azure Service Fabric에 대한 추가 Azure PowerShell 샘플은 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75bbc-119">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
