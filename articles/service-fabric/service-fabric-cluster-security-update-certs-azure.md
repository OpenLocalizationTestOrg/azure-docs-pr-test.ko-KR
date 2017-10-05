---
title: "Azure Service Fabric 클러스터에서 인증서 관리 | Microsoft Docs"
description: "Service Fabric 클러스터에서 새 인증서를 추가, 교체 및 제거하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: c433e8683755e454f9561f094269c3daccf78a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="c734b-103">Azure에서 서비스 패브릭 클러스터에 대한 인증서 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="c734b-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="c734b-104">Service Fabric이 X.509 인증서를 사용하는 방법을 숙지하고 [클러스터 보안 시나리오](service-fabric-cluster-security.md)를 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="c734b-105">다음 과정으로 진행하기 전에 클러스터 인증서가 무엇이며 어떤 용도로 사용되는지를 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="c734b-106">클러스터를 만드는 동안 클라이언트 인증서 외에도 인증서 보안을 구성할 때 Service Fabric을 사용하여 기본 인증서와 보조 인증서의 두 클러스터 인증서를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span></span> <span data-ttu-id="c734b-107">만드는 시점에서의 설정에 관한 자세한 내용은 [포털을 통해 Azure 클러스터 만들기](service-fabric-cluster-creation-via-portal.md) 또는 [Azure Resource Manager를 통해 Azure 클러스터 만들기](service-fabric-cluster-creation-via-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c734b-107">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="c734b-108">만드는 시점에 클러스터 인증서를 하나만 지정하는 경우 해당 인증서가 기본 인증서로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-108">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span></span> <span data-ttu-id="c734b-109">클러스터를 만든 후 새 인증서를 보조 인증서로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="c734b-110">보안 클러스터의 경우 항상 하나 이상의 유효한(취소되지 않거나 만료되지 않은) 클러스터 인증서(기본 또는 보조)를 배포해야 하며 그러지 않으면 클러스터가 작동을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span></span> <span data-ttu-id="c734b-111">모든 유효한 인증서가 만료되기 90일 전에 시스템은 해당 노드에 대해 경고 추적 및 경고 상태 이벤트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-111">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span></span> <span data-ttu-id="c734b-112">현재, 서비스 패브릭이 이 항목에 대해 전송하는 전자 메일 또는 기타 알림은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a><span data-ttu-id="c734b-113">포털을 사용하여 보조 클러스터 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="c734b-113">Add a secondary cluster certificate using the portal</span></span>

<span data-ttu-id="c734b-114">Azure Portal로는 보조 클러스터 인증서를 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-114">Secondary cluster certificate cannot be added through the Azure portal.</span></span> <span data-ttu-id="c734b-115">Azure Powershell을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-115">You have to use Azure powershell for that.</span></span> <span data-ttu-id="c734b-116">이 프로세스는 이 문서의 뒷부분에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-116">The process is outlined later in this document.</span></span>

## <a name="swap-the-cluster-certificates-using-the-portal"></a><span data-ttu-id="c734b-117">포털을 사용하여 클러스터 인증서 교환 </span><span class="sxs-lookup"><span data-stu-id="c734b-117">Swap the cluster certificates using the portal</span></span>

<span data-ttu-id="c734b-118">보조 클러스터 인증서를 배포한 후 기본 인증서와 보조 인증서를 교환하려면 보안 블레이드로 이동한 다음 상황별 메뉴에서 '기본과 스왑' 옵션을 선택하여 보조 인증서를 기본 인증서와 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-118">After you have successfully deployed a secondary cluster certificate, if you want to swap the primary and secondary, then navigate to the Security blade, and select the 'Swap with primary' option from the context menu to swap the secondary cert with the primary cert.</span></span>

![인증서 교환][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-the-portal"></a><span data-ttu-id="c734b-120">포털을 사용하여 클러스터 인증서 제거</span><span class="sxs-lookup"><span data-stu-id="c734b-120">Remove a cluster certificate using the portal</span></span>

<span data-ttu-id="c734b-121">보안 클러스터의 경우 항상 적어도 하나의 유효한(취소되지 않거나 만료되지 않은) 기본 또는 보조 인증서를 배포해야 하며 그러지 않으면 클러스터가 작동을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, the cluster stops functioning.</span></span>

<span data-ttu-id="c734b-122">클러스터 보안에서 사용되는 보조 인증서를 제거하려면 보안 블레이드로 이동하여 보조 인증서에 대한 상황별 메뉴에서 '삭제' 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-122">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the secondary certificate.</span></span>

<span data-ttu-id="c734b-123">기본으로 표시된 인증서를 제거하려는 경우 먼저 보조 인증서와 교환한 다음 업그레이드 완료 후 보조 인증서를 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-123">If your intent is to remove the certificate that is marked primary, then you will need to swap it with the secondary first, and then delete the secondary after the upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="c734b-124">Resource Manager Powershell을 사용하여 보조 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="c734b-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="c734b-125">이러한 단계에서는 Resource Manager의 작동 원리에 익숙하며, Resource Manager 템플릿을 사용하여 하나 이상의 Service Fabric 클러스터를 배포했고, 클러스터를 설정하는 데 사용한 템플릿이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span></span> <span data-ttu-id="c734b-126">또한 JSON을 잘 사용하여 작업할 수 있다고 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="c734b-127">시작 지점으로 사용하거나 필요할 때 사용할 수 있는 샘플 템플릿 및 매개 변수를 찾으려는 경우 이 [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-127">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="c734b-128">Resource Manager 템플릿 편집</span><span class="sxs-lookup"><span data-stu-id="c734b-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="c734b-129">편의를 위해 5-VM-1-NodeTypes-Secure_Step2.JSON 샘플에는 앞으로 수행할 모든 편집이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span></span> <span data-ttu-id="c734b-130">이 샘플은 [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-130">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="c734b-131">**모든 단계를 수행해야 합니다.**</span><span class="sxs-lookup"><span data-stu-id="c734b-131">**Make sure to follow all the steps**</span></span>

<span data-ttu-id="c734b-132">**1단계:** 클러스터를 배포하는 데 사용한 Resource Manager 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-132">**Step 1:** Open up the Resource Manager template you used to deploy you Cluster.</span></span> <span data-ttu-id="c734b-133">위의 리포지토리에서 샘플을 다운로드한 경우 5-VM-1-NodeTypes-Secure_Step1.JSON을 사용하여 보안 클러스터를 배포한 다음 해당 템플릿을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-133">(If you have downloaded the sample from the above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="c734b-134">**2단계:** **유형이 "string"인 두 매개 변수**  "secCertificateThumbprint"와 "secCertificateUrlValue"를 템플릿의 매개 변수 섹션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span></span> <span data-ttu-id="c734b-135">다음 코드 조각을 복사하여 템플릿에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-135">You can copy the following code snippet and add it to the template.</span></span> <span data-ttu-id="c734b-136">템플릿 원본에 따라 이미 이 항목을 정의했을 수 있습니다. 이 경우 다음 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-136">Depending on the source of your template, you may already have these defined, if so move to the next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="c734b-137">**3단계:** **Microsoft.ServiceFabric/clusters** 리소스를 변경합니다. 템플릿에서 "Microsoft.ServiceFabric/clusters" 리소스 정의를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-137">**Step 3:** Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="c734b-138">이 정의의 속성에서 "Certificate" JSON 태그를 찾을 수 있습니다. 이 태그는 다음 JSON 조각과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="c734b-139">새 태그 "ThumbprintSecondary"를 추가하고 "[parameters('secCertificateThumbprint')]" 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="c734b-140">이제 리소스 정의는 다음처럼 보일 것입니다(템플릿 원본에 따라, 아래 조각과 정확히 같지는 않을 수 있음).</span><span class="sxs-lookup"><span data-stu-id="c734b-140">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="c734b-141">**인증서를 교체**하려면 새 인증서를 기본으로 지정한 다음 현재 인증서를 보조로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-141">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="c734b-142">그러면 한 배포 단계에서 현재 기본 인증서가 새 인증서로 교체됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-142">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="c734b-143">**4단계:** **모든** **Microsoft.Compute/virtualMachineScaleSets** 리소스 정의 변경 - Microsoft.Compute/virtualMachineScaleSets 리소스 정의를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-143">**Step 4:** Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="c734b-144">"virtualMachineProfile" 아래 "publisher": "Microsoft.Azure.ServiceFabric"으로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-144">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="c734b-145">Service Fabric 게시자 설정이 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-145">In the service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="c734b-147">새 인증서 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-147">Add the new cert entries to it</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="c734b-148">이제 속성이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-148">The properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="c734b-150">**인증서를 교체**하려면 새 인증서를 기본으로 지정한 다음 현재 인증서를 보조로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-150">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="c734b-151">이를 통해 하나의 배포 단계에서 현재 인증서가 새 인증서로 롤오버됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-151">This results in the rollover of your current certificate to the new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="c734b-152">이제 속성이 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-152">The properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="c734b-154">**5단계:** **모든** **Microsoft.Compute/virtualMachineScaleSets** 리소스 정의를 변경합니다. Microsoft.Compute/virtualMachineScaleSets 리소스 정의를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-154">**Step 5:** Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="c734b-155">"OSProfile" 아래 "VaultCertificates"로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-155">Scroll to the "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="c734b-156">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="c734b-158">여기에 secCertificateUrlValue를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-158">Add the secCertificateUrlValue to it.</span></span> <span data-ttu-id="c734b-159">다음 조각을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-159">use the following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="c734b-160">이제 결과 JSON은 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-160">Now the resulting Json should look something like this.</span></span>
<span data-ttu-id="c734b-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="c734b-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="c734b-162">템플릿의 모든 Nodetypes/Microsoft.Compute/virtualMachineScaleSets 리소스 정의에 대해 4, 5단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-162">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="c734b-163">하나라도 누락되면 인증서가 VMSS에 설치되지 않으며 클러스터에서 클러스터 다운 등과 같은 예기치 않은 결과가 발생합니다(클러스터가 보안에 사용할 유효한 인증서가 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="c734b-163">If you miss one of them, the certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span></span> <span data-ttu-id="c734b-164">따라서 진행에 앞서 다시 한 번 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c734b-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a><span data-ttu-id="c734b-165">위에서 추가한 새 매개 변수를 반영하도록 템플릿 파일 편집</span><span class="sxs-lookup"><span data-stu-id="c734b-165">Edit your template file to reflect the new parameters you added above</span></span>
<span data-ttu-id="c734b-166">[git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)의 샘플을 따라 사용하는 경우 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 샘플을 변경하여 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-166">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="c734b-167">Resource Manager 템플릿 매개 변수 파일을 편집하고 secCertificateThumbprint 및 secCertificateUrlValue에 대한 새로운 두 매개 변수를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-167">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a><span data-ttu-id="c734b-168">Azure에 템플릿 배포</span><span class="sxs-lookup"><span data-stu-id="c734b-168">Deploy the template to Azure</span></span>

- <span data-ttu-id="c734b-169">이제 Azure에 템플릿을 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-169">You are now ready to deploy your template to Azure.</span></span> <span data-ttu-id="c734b-170">Azure PS 버전 1+ 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="c734b-171">Azure 계정에 로그인하고 특정 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-171">Log in to your Azure Account and select the specific azure subscription.</span></span> <span data-ttu-id="c734b-172">이 단게는 둘 이상의 Azure 구독에 대해 액세스 권한이 있는 사용자들을 위한 중요한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-172">This is an important step for folks who have access to more than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="c734b-173">템플릿을 배포하기 전에 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-173">Test the template prior to deploying it.</span></span> <span data-ttu-id="c734b-174">현재 클러스터가 배포된 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-174">Use the same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="c734b-175">리소스 그룹에 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-175">Deploy the template to your resource group.</span></span> <span data-ttu-id="c734b-176">현재 클러스터가 배포된 동일한 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-176">Use the same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="c734b-177">New-AzureRmResourceGroupDeployment 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-177">Run the New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="c734b-178">기본값은 **incremental**이므로 모드는 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-178">You do not need to specify the mode, since the default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="c734b-179">Mode를 Complete로 설정하면 템플릿에 없는 리소스를 실수로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-179">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="c734b-180">따라서 이러한 경우에는 사용하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="c734b-181">다음은 동일한 powershell의 작성된 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-181">Here is a filled out example of the same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="c734b-182">배포가 완료되면 새 인증서를 사용하여 클러스터에 연결하고 일부 쿼리를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-182">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span></span> <span data-ttu-id="c734b-183">가능한 경우</span><span class="sxs-lookup"><span data-stu-id="c734b-183">If you are able to do.</span></span> <span data-ttu-id="c734b-184">그런 다음 기존 인증서를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-184">Then you can delete the old certificate.</span></span> 

<span data-ttu-id="c734b-185">자체 서명된 인증서를 사용하는 경우 로컬 TrustedPeople 인증서 저장소로 인증서를 가져와야 하는 것을 잊지 마세요.</span><span class="sxs-lookup"><span data-stu-id="c734b-185">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="c734b-186">다음은 빠른 참조를 위해 제공되는 보안 클러스터 연결 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-186">For quick reference here is the command to connect to a secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="c734b-187">다음은 빠른 참조를 위해 제공되는 클러스터 상태 확인 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-187">For quick reference here is the command to get cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a><span data-ttu-id="c734b-188">클러스터에 응용 프로그램 인증서를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-188">Deploying Application certificates to the cluster.</span></span>

<span data-ttu-id="c734b-189">앞의 5단계에서 설명한 것과 같은 단계를 사용하여 Key Vault에서 인증서를 노드에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-189">You can use the same steps as outlined in Steps 5 above to have the certificates deployed from a keyvault to the Nodes.</span></span> <span data-ttu-id="c734b-190">다른 매개 변수를 정의하여 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="c734b-191">클라이언트 인증서 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="c734b-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="c734b-192">클러스터 인증서 외에, Service Fabric 클러스터에 대한 관리 작업을 수행하는 클라이언트 인증서를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-192">In addition to the cluster certificates, you can add client certificates to perform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="c734b-193">관리자 또는 읽기 전용 등, 두 종류의 클라이언트 인증서를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="c734b-194">그런 다음 이 인증서를 사용하여 클러스터에서의 관리자 작업과 쿼리 작업에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-194">These then can be used to control access to the admin operations and Query operations on the cluster.</span></span> <span data-ttu-id="c734b-195">기본적으로 클러스터 인증서는 허용된 관리자 인증서 목록에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-195">By default, the cluster certificates are added to the allowed Admin certificates list.</span></span>

<span data-ttu-id="c734b-196">클라이언트 수를 원하는 대로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="c734b-197">추가/삭제될 때마다 Service Fabric 클러스터에서 구성이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-197">Each addition/deletion results in a configuration update to the service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="c734b-198">포털을 통해 관리자 또는 읽기 전용 클라이언트 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="c734b-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="c734b-199">보안 블레이드로 이동하고 보안 블레이드 맨 위의 ‘+ 인증’ 버튼을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-199">Navigate to the Security blade, and select the '+ Authentication' button on top of the security blade.</span></span>
2. <span data-ttu-id="c734b-200">‘인증 추가' 블레이드에서 ‘인증 유형' - ‘읽기 전용 클라이언트' 또는 ‘관리자 클라이언트'를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-200">On the 'Add Authentication' blade, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="c734b-201">이제 인증 방법을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-201">Now choose the Authorization method.</span></span> <span data-ttu-id="c734b-202">주체 이름을 사용하거나 지문으로 이 인증서를 찾아야 하는 경우 서비스 패브릭에 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-202">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span></span> <span data-ttu-id="c734b-203">일반적으로 주체 이름을 인증 방법으로 사용하는 것은 보안상 좋지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-203">In general, it is not a good security practice to use the authorization method of subject name.</span></span> 

![클라이언트 인증서 추가][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a><span data-ttu-id="c734b-205">포털을 사용하여 관리자 또는 읽기 전용 클라이언트 인증서 삭제 </span><span class="sxs-lookup"><span data-stu-id="c734b-205">Deletion of Client Certificates - Admin or Read-Only using the portal</span></span>

<span data-ttu-id="c734b-206">클러스터 보안에서 사용되는 특정 인증서를 제거하려면 보안 블레이드로 이동하여 보조 인증서에 대한 상황별 메뉴에서 '삭제' 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c734b-206">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="c734b-207">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c734b-207">Next steps</span></span>
<span data-ttu-id="c734b-208">클러스터 관리에 대한 자세한 내용은 다음 문서를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="c734b-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="c734b-209">서비스 패브릭 클러스터 업그레이드 프로세스 및 사용자 기대 수준</span><span class="sxs-lookup"><span data-stu-id="c734b-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="c734b-210">클라이언트에 대한 역할 기반 액세스 설정</span><span class="sxs-lookup"><span data-stu-id="c734b-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


