---
title: "Azure Virtual Machine Scale Sets에 대한 FAQ | Microsoft Docs"
description: "Virtual Machine Scale Sets에 대한 FAQ(질문과 대답)에 대해 알아봅니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: f320dd5d1f8c99317792f4ae9e09bc5adaf79e25
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="cff84-103">Azure Virtual Machine Scale Sets에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="cff84-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="cff84-104">Azure의 Virtual Machine Scale Sets에 대한 FAQ(질문과 대답)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-104">Get answers to frequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="cff84-105">Autoscale</span><span class="sxs-lookup"><span data-stu-id="cff84-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="cff84-106">Azure 자동 크기 조정에 대한 모범 사례는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="cff84-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="cff84-107">자동 크기 조정에 대한 모범 사례는 [가상 컴퓨터 자동 크기 조정에 대한 모범 사례](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="cff84-108">호스트 기반 메트릭을 사용하는 자동 크기 조정에 대한 메트릭 이름은 어디에서 찾을 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="cff84-109">호스트 기반 메트릭을 사용하는 자동 크기 조정에 대한 메트릭 이름은 [Azure Monitor에서 지원되는 메트릭](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="cff84-110">Azure Service Bus 토픽과 큐 길이를 기준으로 하는 자동 크기 조정의 예가 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="cff84-111">예.</span><span class="sxs-lookup"><span data-stu-id="cff84-111">Yes.</span></span> <span data-ttu-id="cff84-112">Azure Service Bus 토픽과 큐 길이를 기준으로 하는 자동 크기 조정의 예는 [Azure Monitor 자동 크기 조정 공용 메트릭](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="cff84-113">Service Bus 큐를 모니터링하려면 다음 JSON을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-113">For a Service Bus queue, use the following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="cff84-114">저장소 큐의 경우 다음 JSON을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-114">For a storage queue, use the following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="cff84-115">예제 값을 리소스 URI(Uniform Resource Identifier)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="cff84-116">자동 크기 조정을 수행할 때 호스트 기반 메트릭과 진단 확장 중에서 어떤 방식을 사용하는 것이 바람직한가요?</span><span class="sxs-lookup"><span data-stu-id="cff84-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="cff84-117">VM에 자동 크기 조정 설정을 만들면 호스트 수준 메트릭 또는 게스트 OS 기반 메트릭을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-117">You can create an autoscale setting on a VM to use host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="cff84-118">지원되는 메트릭 목록에 대해서는 [Azure Monitor 자동 크기 조정 공용 메트릭](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="cff84-119">가상 컴퓨터 확장 집합의 전체 샘플을 보려면 [가상 컴퓨터 확장 집합에 대해 Resource Manager 템플릿을 사용하여 고급 자동 크기 조정 구성](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="cff84-120">샘플에서는 호스트 수준의 CPU 메트릭 및 메시지 개수 메트릭을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-120">The sample uses the host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="cff84-121">가상 컴퓨터 확장 집합에 대해 경고 규칙을 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="cff84-122">PowerShell 또는 Azure CLI를 통해 가상 컴퓨터 확장 집합의 메트릭에 대해 경고를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="cff84-123">자세한 내용은 [Azure Monitor PowerShell 빠른 시작 샘플](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) 및 [Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="cff84-124">가상 컴퓨터 확장 집합의 TargetResourceId는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-124">The TargetResourceId of the virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="cff84-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="cff84-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="cff84-126">경고를 설정할 메트릭으로 어떤 VM 성능 카운터도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-126">You can choose any VM performance counter as the metric to set an alert for.</span></span> <span data-ttu-id="cff84-127">자세한 내용은 [Azure Monitor 자동 크기 조정 공용 메트릭](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) 문서의 [Resource Manager 기반 Windows VM에 대한 게스트 OS 메트릭](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) 및 [Linux VM에 대한 게스트 OS 메트릭](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in the [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="cff84-128">PowerShell을 사용하여 가상 컴퓨터 확장 집합에 대해 자동 크기 조정을 설정하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="cff84-129">PowerShell을 사용하여 가상 컴퓨터 확장 집합에 대해 자동 크기 조정을 설정하려면 [Azure Virtual Machine Scale Set에 자동 크기 조정을 추가하는 방법](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/) 블로그 게시물을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-129">To set up autoscale on a virtual machine scale set by using PowerShell, see the blog post [How to add autoscale to an Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="cff84-130">인증서</span><span class="sxs-lookup"><span data-stu-id="cff84-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-to-the-vm-how-do-i-provision-a-virtual-machine-scale-set-to-run-a-website-where-the-ssl-for-the-website-is-shipped-securely-from-a-certificate-configuration-the-common-certificate-rotation-operation-would-be-almost-the-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-to-do-this"></a><span data-ttu-id="cff84-131">VM에 인증서를 안전하게 배달하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-131">How do I securely ship a certificate to the VM?</span></span> <span data-ttu-id="cff84-132">인증서 구성에서 가상 컴퓨터 확장 집합을 프로비전하여 웹 사이트의 SSL이 안전하게 배달되는 웹 사이트를 실행하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-132">How do I provision a virtual machine scale set to run a website where the SSL for the website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="cff84-133">(일반적인 인증서 순환 작업은 구성 업데이트 작업과 거의 동일합니다.) 이 작업을 수행하는 방법을 보여 주는 예제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-133">(The common certificate rotation operation would be almost the same as a configuration update operation.) Do you have an example of how to do this?</span></span> 

<span data-ttu-id="cff84-134">VM에 인증서를 안전하게 전달하기 위해 고객의 Key Vault에서 Windows 인증서 저장소로 직접 고객 인증서를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-134">To securely ship a certificate to the VM, you can install a customer certificate directly into a Windows certificate store from the customer's key vault.</span></span>

<span data-ttu-id="cff84-135">다음 JSON을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-135">Use the following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="cff84-136">코드는 Windows와 Linux를 모두 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-136">The code supports Windows and Linux.</span></span>

<span data-ttu-id="cff84-137">자세한 내용은 [가상 컴퓨터 확장 집합 만들기 또는 업데이트](https://msdn.microsoft.com/library/mt589035.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="cff84-138">자체 서명된 인증서 예제</span><span class="sxs-lookup"><span data-stu-id="cff84-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="cff84-139">Key Vault에서 자체 서명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="cff84-140">다음 PowerShell 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-140">Use the following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="cff84-141">이 명령은 Azure Resource Manager 템플릿에 대한 입력을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-141">This command gives you the input for the Azure Resource Manager template.</span></span>

    <span data-ttu-id="cff84-142">Key Vault에서 자체 서명된 인증서를 만드는 방법에 대한 예제를 보려면 [Service Fabric 클러스터 보안 시나리오](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-142">For an example of how to create a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="cff84-143">Resource Manager 템플릿을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-143">Change the Resource Manager template.</span></span>

    <span data-ttu-id="cff84-144">가상 컴퓨터 확장 집합 리소스의 일부로 **virtualMachineProfile**에 다음 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-144">Add this property to **virtualMachineProfile**, as part of the virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-to-use-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="cff84-145">Resource Manager 템플릿에서 Linux 가상 컴퓨터 확장 집합으로 SSH 인증에 사용하려는 SSH 키 쌍을 지정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-145">Can I specify an SSH key pair to use for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="cff84-146">예.</span><span class="sxs-lookup"><span data-stu-id="cff84-146">Yes.</span></span> <span data-ttu-id="cff84-147">**osProfile**에 대한 REST API는 표준 VM REST API와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-147">The REST API for **osProfile** is similar to the standard VM REST API.</span></span> 

<span data-ttu-id="cff84-148">템플릿에 **osProfile**을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="cff84-149">이 JSON 블록은 [101-vm-sshkey GitHub 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-149">This JSON block is used in [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="cff84-150">또한 OS 프로필은 [grelayhost.json GitHub 빠른 시작 템플릿](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json)에서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-150">The OS profile also is used in [the grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="cff84-151">자세한 내용은 [가상 컴퓨터 확장 집합 만들기 또는 업데이트](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="cff84-152">사용되지 않는 인증서를 제거하려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="cff84-153">사용되지 않는 인증서를 제거하려면 자격 증명 모음 인증서 목록에서 이전 인증서를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-153">To remove deprecated certificates, remove the old certificate from the vault certificates list.</span></span> <span data-ttu-id="cff84-154">목록에서 컴퓨터에 유지하려는 모든 인증서를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-154">Leave all the certificates that you want to remain on your computer in the list.</span></span> <span data-ttu-id="cff84-155">이렇게 하면 모든 VM에서 인증서가 제거되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-155">This does not remove the certificate from all your VMs.</span></span> <span data-ttu-id="cff84-156">또한 가상 컴퓨터 확장 집합에서 만들어진 새 VM에 인증서가 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-156">It also does not add the certificate to new VMs that are created in the virtual machine scale set.</span></span> 

<span data-ttu-id="cff84-157">기존 VM에서 인증서를 제거하려면 인증서 저장소에서 인증서를 수동으로 제거하는 사용자 지정 스크립트 확장을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-157">To remove the certificate from existing VMs, write a custom script extension to manually remove the certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-the-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-to-store-the-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="cff84-158">프로비전하는 동안 기존 SSH 공개 키를 가상 컴퓨터 확장 집합 SSH 계층에 삽입하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-158">How do I inject an existing SSH public key into the virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="cff84-159">SSH 공개 키 값을 Azure Key Vault에 저장하고 이를 내 Resource Manager 템플릿에서 활용하고 싶습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-159">I want to store the SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="cff84-160">VM에 공개 SSH 키만 프로비전하는 경우 Key Vault에 공개 키를 적용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-160">If you are providing the VMs only with a public SSH key, you don't need to put the public keys in Key Vault.</span></span> <span data-ttu-id="cff84-161">공개 키는 비밀이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="cff84-162">Linux VM을 만들 때 일반 텍스트로 SSH 공개 키를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="cff84-163">linuxConfiguration 요소 이름</span><span class="sxs-lookup"><span data-stu-id="cff84-163">linuxConfiguration element name</span></span> | <span data-ttu-id="cff84-164">필수</span><span class="sxs-lookup"><span data-stu-id="cff84-164">Required</span></span> | <span data-ttu-id="cff84-165">형식</span><span class="sxs-lookup"><span data-stu-id="cff84-165">Type</span></span> | <span data-ttu-id="cff84-166">설명</span><span class="sxs-lookup"><span data-stu-id="cff84-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="cff84-167">ssh</span><span class="sxs-lookup"><span data-stu-id="cff84-167">ssh</span></span> | <span data-ttu-id="cff84-168">아니요</span><span class="sxs-lookup"><span data-stu-id="cff84-168">No</span></span> | <span data-ttu-id="cff84-169">컬렉션</span><span class="sxs-lookup"><span data-stu-id="cff84-169">Collection</span></span> | <span data-ttu-id="cff84-170">Linux OS용 SSH 키 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-170">Specifies the SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="cff84-171">path</span><span class="sxs-lookup"><span data-stu-id="cff84-171">path</span></span> | <span data-ttu-id="cff84-172">예</span><span class="sxs-lookup"><span data-stu-id="cff84-172">Yes</span></span> | <span data-ttu-id="cff84-173">String</span><span class="sxs-lookup"><span data-stu-id="cff84-173">String</span></span> | <span data-ttu-id="cff84-174">SSH 키 또는 인증서를 배치해야 하는 Linux 파일 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-174">Specifies the Linux file path where the SSH keys or certificate should be located</span></span>
<span data-ttu-id="cff84-175">keyData</span><span class="sxs-lookup"><span data-stu-id="cff84-175">keyData</span></span> | <span data-ttu-id="cff84-176">예</span><span class="sxs-lookup"><span data-stu-id="cff84-176">Yes</span></span> | <span data-ttu-id="cff84-177">String</span><span class="sxs-lookup"><span data-stu-id="cff84-177">String</span></span> | <span data-ttu-id="cff84-178">base64로 인코딩된 SSH 공개 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="cff84-179">예를 들어 [101-vm-sshkey GitHub 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-179">For an example, see [the 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-the-same-key-vault-i-see-the-following-message"></a><span data-ttu-id="cff84-180">동일한 Key Vault에서 둘 이상의 인증서를 추가한 후에 `Update-AzureRmVmss`를 실행하면 다음과 같은 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-180">When I run `Update-AzureRmVmss` after adding more than one certificate from the same key vault, I see the following message:</span></span>
 
><span data-ttu-id="cff84-181">Update-AzureRmVmss: 허용되지 않는 /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev의 반복된 인스턴스를 포함하고 있는 비밀을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="cff84-182">이 기존 원본 자격 증명 모음에 대해 새 자격 증명 모음 인증서를 사용하는 대신, 동일한 자격 증명 모음을 다시 추가하려고 하면 이러한 현상이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-182">This can happen if you try to re-add the same vault instead of using a new vault certificate for the existing source vault.</span></span> <span data-ttu-id="cff84-183">다른 비밀을 더 추가하는 경우 `Add-AzureRmVmssSecret` 명령은 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-183">The `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="cff84-184">동일한 키 자격 증명 모음에서 더 많은 비밀을 추가하려면 $vmss.properties.osProfile.secrets[0].vaultCertificates 목록을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-184">To add more secrets from the same key vault, update the $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="cff84-185">필요한 입력 구조에 대한 자세한 내용은 [가상 컴퓨터 설정 만들기 또는 업데이트](https://msdn.microsoft.com/library/azure/mt589035.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-185">For the expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="cff84-186">Key Vault에 있는 가상 컴퓨터 확장 집합 개체에서 암호를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-186">Find the secret in the virtual machine scale set object that is in the key vault.</span></span> <span data-ttu-id="cff84-187">그런 다음 인증서 참조(비밀 저장소 이름 및 URL)를 자격 증명 모음과 관련된 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-187">Then, add your certificate reference (the URL and the secret store name) to the list associated with the vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="cff84-188">현재 가상 컴퓨터 확장 집합 API를 사용하여 VM에서 인증서를 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-188">Currently, you cannot remove certificates from VMs by using the virtual machine scale set API.</span></span>
>

<span data-ttu-id="cff84-189">새 VM은 이전 인증서를 갖지 않게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-189">New VMs will not have the old certificate.</span></span> <span data-ttu-id="cff84-190">그러나 인증서가 있는 있고 이미 배포된 VM은 이전 인증서를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-190">However, VMs that have the certificate and which are already deployed will have the old certificate.</span></span>
 
### <a name="can-i-push-certificates-to-the-virtual-machine-scale-set-without-providing-the-password-when-the-certificate-is-in-the-secret-store"></a><span data-ttu-id="cff84-191">인증서가 현재 SecretStore에 있을 때 암호를 제공하지 않고 인증서를 가상 컴퓨터 확장 집합에 푸시할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-191">Can I push certificates to the virtual machine scale set without providing the password, when the certificate is in the secret store?</span></span>

<span data-ttu-id="cff84-192">스크립트에 하드 코드된 암호를 포함할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-192">You do not need to hard-code passwords in scripts.</span></span> <span data-ttu-id="cff84-193">배포 스크립트를 실행하는 데 사용하는 권한으로 암호를 동적으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-193">You can dynamically retrieve passwords with the permissions you use to run the deployment script.</span></span> <span data-ttu-id="cff84-194">인증서를 비밀 저장소에서 Key Vault로 이동하는 스크립트가 있는 경우 secret store `get certificate` 명령을 실행하면 .pfx 파일의 암호도 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-194">If you have a script that moves a certificate from the secret store key vault, the secret store `get certificate` command also outputs the password of the .pfx file.</span></span>
 
### <a name="how-does-the-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-the-sourcevault-value-when-i-have-to-specify-the-absolute-uri-for-a-certificate-by-using-the-certificateurl-property"></a><span data-ttu-id="cff84-195">가상 컴퓨터 확장 집합에 대한 virtualMachineProfile.osProfile의 Secrets 속성은 어떻게 작동합니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-195">How does the Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="cff84-196">certificateUrl 속성을 사용하여 인증서에 대한 절대 URI를 지정해야 하는 경우 sourceVault 값이 필요한 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="cff84-196">Why do I need the sourceVault value when I have to specify the absolute URI for a certificate by using the certificateUrl property?</span></span> 

<span data-ttu-id="cff84-197">Win RM(Windows 원격 관리) 인증서 참조는 OS 프로필의 Secrets 속성에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-197">A Windows Remote Management (WinRM) certificate reference must be present in the Secrets property of the OS profile.</span></span> 

<span data-ttu-id="cff84-198">원본 자격 증명 모음을 지정하는 이유는 사용자의 Azure 클라우드 서비스 모델에 존재하는 ACL(액세스 제어 목록) 정책을 적용한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-198">The purpose of indicating the source vault is to enforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="cff84-199">원본 자격 증명 모음을 지정하지 않으면 키 자격 증명 모음에 비밀을 배포하고 액세스할 수 있는 권한이 없는 사용자는 CRP(Compute 리소스 공급자)를 통해 배포하고 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-199">If the source vault isn't specified, users who do not have permissions to deploy or access secrets to a key vault would be able to through a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="cff84-200">ACL은 존재하지 않는 리소스에 대해서도 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="cff84-201">잘못된 sourceVault ID를 제공했지만 유효한 Key Vault URL을 제공한 경우 작업을 폴링할 때 오류가 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll the operation.</span></span>
 
### <a name="if-i-add-secrets-to-an-existing-virtual-machine-scale-set-are-the-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="cff84-202">기존 가상 컴퓨터 확장 집합에 비밀을 추가하면 비밀이 기존 VM에 삽입되나요? 아니면 새 VM에만 삽입되나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-202">If I add secrets to an existing virtual machine scale set, are the secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="cff84-203">인증서는 기존 VM을 포함하여 모든 VM에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-203">Certificates are added to all your VMs, even preexisting ones.</span></span> <span data-ttu-id="cff84-204">가상 컴퓨터 확장 집합 upgradePolicy 속성을 **manual**로 설정하면 VM에서 수동 업데이트를 수행할 때 인증서가 해당 VM에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-204">If your virtual machine scale set upgradePolicy property is set to **manual**, the certificate is added to the VM when you perform a manual update on the VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="cff84-205">Linux VM에 대한 인증서는 어디에서 추가하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="cff84-206">Linux VM에 대한 인증서를 배포하는 방법을 알아보려면 [고객이 관리하는 Key Vault에서 VM에 인증서 배포](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-206">To learn how to deploy certificates for Linux VMs, see [Deploy certificates to VMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-to-a-new-certificate-object"></a><span data-ttu-id="cff84-207">새 자격 증명 모음 인증서는 새 인증서 개체에 추가하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-207">How do I add a new vault certificate to a new certificate object?</span></span>

<span data-ttu-id="cff84-208">기존 비밀에 자격 증명 모음 인증서를 추가하려면 다음 PowerShell 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-208">To add a vault certificate to an existing secret, see the following PowerShell example.</span></span> <span data-ttu-id="cff84-209">비밀 개체를 하나만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-to-certificates-if-you-reimage-a-vm"></a><span data-ttu-id="cff84-210">VM을 이미지로 다시 설치하면 인증서는 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-210">What happens to certificates if you reimage a VM?</span></span>

<span data-ttu-id="cff84-211">VM을 이미지로 다시 설치할 경우 인증서는 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="cff84-212">이미지로 다시 설치하면 전체 OS 디스크가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-212">Reimaging deletes the entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-the-key-vault"></a><span data-ttu-id="cff84-213">키 자격 증명 모음에서 인증서를 삭제하면 어떻게 됩니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-213">What happens if you delete a certificate from the key vault?</span></span>

<span data-ttu-id="cff84-214">Key Vault에서 비밀을 삭제하고 모든 VM의 `stop deallocate`를 실행한 다음 다시 시작하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-214">If the secret is deleted from the key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="cff84-215">이 오류는 CRP가 Key Vault에서 비밀을 검색해야 하기 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-215">The failure occurs because the CRP needs to retrieve the secrets from the key vault, but it cannot.</span></span> <span data-ttu-id="cff84-216">이 시나리오에서는 가상 컴퓨터 확장 집합 모델에서 인증서를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-216">In this scenario, you can delete the certificates from the virtual machine scale set model.</span></span> 

<span data-ttu-id="cff84-217">CRP 구성 요소는 고객 비밀을 유지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-217">The CRP component does not persist customer secrets.</span></span> <span data-ttu-id="cff84-218">가상 컴퓨터 확장 집합의 모든 VM에 대해 `stop deallocate`를 실행하면 캐시가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-218">If you run `stop deallocate` for all VMs in the virtual machine scale set, the cache is deleted.</span></span> <span data-ttu-id="cff84-219">이 시나리오에서는 Key Vault에서 비밀이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-219">In this scenario, secrets are retrieved from the key vault.</span></span>

<span data-ttu-id="cff84-220">Azure Service Fabric에 비밀의 캐시 복사본이 있으므로 확장할 때 이 문제가 발생하지 않습니다(단일 패브릭 테넌트 모델).</span><span class="sxs-lookup"><span data-stu-id="cff84-220">You don't encounter this problem when scaling out because there is a cached copy of the secret in Azure Service Fabric (in the single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-to-specify-the-exact-location-for-the-certificate-url-httpsname-of-the-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="cff84-221">[Service Fabric 클러스터 보안 시나리오](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)에 나오는 것처럼 인증서 URL(https://<name of the vault>.vault.azure.net:443/secrets/<exact location>)에 대한 정확한 위치를 지정해야 하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="cff84-221">Why do I have to specify the exact location for the certificate URL (https://<name of the vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="cff84-222">Azure Key Vault 설명서에 따르면, 버전이 지정되지 않은 경우 Get Secret REST API는 최신 버전의 암호를 반환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-222">The Azure Key Vault documentation states that the Get Secret REST API should return the latest version of the secret if the version is not specified.</span></span>
 
<span data-ttu-id="cff84-223">메서드</span><span class="sxs-lookup"><span data-stu-id="cff84-223">Method</span></span> | <span data-ttu-id="cff84-224">URL</span><span class="sxs-lookup"><span data-stu-id="cff84-224">URL</span></span>
--- | ---
<span data-ttu-id="cff84-225">GET</span><span class="sxs-lookup"><span data-stu-id="cff84-225">GET</span></span> | <span data-ttu-id="cff84-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span><span class="sxs-lookup"><span data-stu-id="cff84-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="cff84-227">{*secret-name*}을 검색하려는 비밀의 이름으로 바꾸고 {*secret-version*}을 해당 버전으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-227">Replace {*secret-name*} with the name, and replace {*secret-version*} with the version of the secret you want to retrieve.</span></span> <span data-ttu-id="cff84-228">암호 버전은 제외할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-228">The secret version might be excluded.</span></span> <span data-ttu-id="cff84-229">이 경우 현재 버전이 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-229">In that case, the current version is retrieved.</span></span>
  
### <a name="why-do-i-have-to-specify-the-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="cff84-230">Key Vault를 사용할 때 인증서 버전을 지정해야 하는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-230">Why do I have to specify the certificate version when I use Key Vault?</span></span>

<span data-ttu-id="cff84-231">Key Vault에서 인증서 버전을 지정하도록 요구하는 이유는 해당 VM에 배포된 인증서를 사용자에게 명확히 알리기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-231">The purpose of the Key Vault requirement to specify the certificate version is to make it clear to the user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="cff84-232">VM을 만든 다음 Key Vault에서 비밀을 업데이트하면 새 인증서가 VM에 다운로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-232">If you create a VM and then update your secret in the key vault, the new certificate is not downloaded to your VMs.</span></span> <span data-ttu-id="cff84-233">그러나 VM에서 새 인증서를 참조하는 것처럼 보일 것이며, 새 VM에서 새 비밀을 가져오게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-233">But your VMs appear to reference it, and new VMs get the new secret.</span></span> <span data-ttu-id="cff84-234">이를 방지하려면 비밀 버전을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-234">To avoid this, you are required to reference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-to-us-as-cer-public-keys-what-is-the-recommended-approach-for-deploying-these-certificates-to-a-virtual-machine-scale-set"></a><span data-ttu-id="cff84-235">여기서는 .cer 공개 키로 배포되는 여러 인증서로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-235">My team works with several certificates that are distributed to us as .cer public keys.</span></span> <span data-ttu-id="cff84-236">가상 컴퓨터 확장 집합에 이러한 인증서를 배포하는 권장 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="cff84-236">What is the recommended approach for deploying these certificates to a virtual machine scale set?</span></span>

<span data-ttu-id="cff84-237">.cer 공개 키를 가상 컴퓨터 확장 집합에 배포하려면 .cer 파일만 포함하는 .pfx 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-237">To deploy .cer public keys to a virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="cff84-238">이렇게 하려면 `X509ContentType = Pfx`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-238">To do this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="cff84-239">예를 들어 C# 또는 PowerShell에서 .cer 파일을 x509Certificate2 개체로 로드하고 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-239">For example, load the .cer file as an x509Certificate2 object in C# or PowerShell, and then call the method.</span></span> 

<span data-ttu-id="cff84-240">자세한 내용은 [X509Certificate.Export 메서드(X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx))를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-to-pass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="cff84-241">사용자가 인증서를 base64 문자열로 전달하는 옵션이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-241">I do not see an option for users to pass in certificates as base64 strings.</span></span> <span data-ttu-id="cff84-242">대부분의 다른 리소스 공급자는 이 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="cff84-243">인증서를 base64 문자열로 전달하는 것을 에뮬레이트하려면 Resource Manager 템플릿에서 최신 버전이 지정된 URL을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-243">To emulate passing in a certificate as a base64 string, you can extract the latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="cff84-244">Resource Manager 템플릿에 다음 JSON 속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-244">Include the following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-to-wrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="cff84-245">Key Vault의 JSON 개체에서 인증서를 래핑해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-245">Do I have to wrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="cff84-246">가상 컴퓨터 확장 집합 및 VM에서 인증서가 JSON 개체에 래핑되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="cff84-247">또한 콘텐츠 형식 application/x-pkcs12도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-247">We also support the content type application/x-pkcs12.</span></span> <span data-ttu-id="cff84-248">application/x-pkcs12 사용에 대한 지침을 보려면 [Azure Key Vault의 PFX 인증서](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="cff84-249">현재 .cer 파일은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-249">We currently do not support .cer files.</span></span> <span data-ttu-id="cff84-250">.cer 파일을 사용하려면 .pfx 컨테이너로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-250">To use .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="cff84-251">규정 준수</span><span class="sxs-lookup"><span data-stu-id="cff84-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="cff84-252">가상 컴퓨터 확장 집합은 PCI 규정을 준수하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="cff84-253">가상 컴퓨터 확장 집합은 CRP 위의 얇은 API 계층에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-253">Virtual machine scale sets are a thin API layer on top of the CRP.</span></span> <span data-ttu-id="cff84-254">두 구성 요소 모두 Azure 서비스 트리에서 Compute 플랫폼에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-254">Both components are part of the compute platform in the Azure service tree.</span></span>

<span data-ttu-id="cff84-255">따라서 규정 준수 관점에서 볼 때 가상 컴퓨터 확장 집합은 Azure Compute 플랫폼의 기본 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-255">From a compliance perspective, virtual machine scale sets are a fundamental part of the Azure compute platform.</span></span> <span data-ttu-id="cff84-256">이들은 CRP 자체와 팀, 도구, 프로세스, 배포 방법, 보안 제어, JIT(Just-In-Time) 컴파일, 모니터링, 경고 등을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with the CRP itself.</span></span> <span data-ttu-id="cff84-257">가상 컴퓨터 확장 집합은 CRP가 현재 PCI DSS(데이터 보안 표준) 증명의 일부이므로 PCI(Payment Card Industry) 규격입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because the CRP is part of the current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="cff84-258">자세한 내용은 [Microsoft 보안 센터](https://www.microsoft.com/TrustCenter/Compliance/PCI)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-258">For more information, see [the Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="cff84-259">확장</span><span class="sxs-lookup"><span data-stu-id="cff84-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="cff84-260">가상 컴퓨터 확장 집합 확장을 삭제하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="cff84-261">가상 컴퓨터 확장 집합 확장을 삭제하려면 다음 PowerShell 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-261">To delete a virtual machine scale set extension, use the following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="cff84-262">`$vmss`에서 extensionName 값을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-262">You can find the extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="cff84-263">Operations Management Suite와 통합되는 가상 컴퓨터 확장 집합 템플릿 예제가 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="cff84-264">Operations Management Suite와 통합되는 가상 컴퓨터 확장 집합 템플릿 예제의 경우 [Log Analytics를 사용하여 Azure Service Fabric 클러스터 배포 및 모니터링 사용](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric)의 두 번째 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see the second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-to-run-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-to-fail-what-can-i-do-to-fix-this"></a><span data-ttu-id="cff84-265">여러 확장이 가상 컴퓨터 확장 집합에서 병렬로 실행되는 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-265">Extensions seem to run in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="cff84-266">이로 인해 사용자 지정 스크립트 확장이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-266">This causes my custom script extension to fail.</span></span> <span data-ttu-id="cff84-267">이 문제를 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-267">What can I do to fix this?</span></span>

<span data-ttu-id="cff84-268">가상 컴퓨터 확장 집합에서 확장 시퀀싱에 대한 자세한 내용은 [Azure Virtual Machine Scale Sets의 확장 시퀀싱](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-268">To learn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-the-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="cff84-269">가상 컴퓨터 확장 집합에서 VM에 대한 암호를 다시 설정하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-269">How do I reset the password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="cff84-270">가상 컴퓨터 확장 집합에서 VM에 대한 암호를 다시 설정하려면 VM 액세스 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-270">To reset the password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="cff84-271">다음 PowerShell 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-271">Use the following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-to-all-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="cff84-272">가상 컴퓨터 확장 집합의 모든 VM에 확장을 추가하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-272">How do I add an extension to all VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="cff84-273">업데이트 정책이 **자동**으로 설정된 경우 템플릿을 새 확장 속성으로 다시 배포하면 모든 VM이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-273">If update policy is set to **automatic**, redeploying the template with the new extension properties updates all VMs.</span></span>

<span data-ttu-id="cff84-274">업데이트 정책이 **수동**으로 설정된 경우 먼저 확장을 업데이트한 다음 VM의 모든 인스턴스를 수동으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-274">If update policy is set to **manual**, first update the extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-the-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-the-vms-not-match-the-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-the-scripts-that-are-currently-configured-on-the-virtual-machine-scale-set-executed-or-are-the-scripts-that-were-configured-when-the-vm-was-first-created-used"></a><span data-ttu-id="cff84-275">기존 가상 컴퓨터 확장 집합과 연결된 확장이 업데이트되면 기존 VM에 영향을 주나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-275">If the extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="cff84-276">(즉, VM이 가상 컴퓨터 확장 집합 모델과 일치하지 *않나요*?) 또는 무시되나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-276">(That is, will the VMs *not* match the virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="cff84-277">기존 컴퓨터에 대해 서비스 복구, 이미지로 다시 설치 등을 수행할 때 현재 가상 컴퓨터 확장 집합에 구성된 스크립트를 실행하나요? 아니면 VM에서 처음 만들었을 때 구성된 스크립트를 사용하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-277">When an existing machine is service-healed or reimaged, are the scripts that are currently configured on the virtual machine scale set executed, or are the scripts that were configured when the VM was first created used?</span></span>

<span data-ttu-id="cff84-278">가상 컴퓨터 확장 집합 모델의 확장 정의가 업데이트되고 upgradePolicy 속성이 **자동**으로 설정되면 VM이 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-278">If the extension definition in the virtual machine scale set model is updated and the upgradePolicy property is set to **automatic**, it updates the VMs.</span></span> <span data-ttu-id="cff84-279">UpgradePolicy 속성을 **수동**으로 설정하면 확장은 모델과 일치하지 않는 것으로 플래그가 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-279">If the upgradePolicy property is set to **manual**, extensions are flagged as not matching the model.</span></span> 

<span data-ttu-id="cff84-280">기존 VM이 서비스 복구되면 다시 부팅하는 것처럼 보이며 확장이 다시 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-280">If an existing VM is service-healed, it appears as a reboot, and the extensions are not rerun.</span></span> <span data-ttu-id="cff84-281">이미지로 다시 설치되는 경우 OS 드라이브를 원본 이미지로 바꾸는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-281">If it is reimaged, it's like replacing the OS drive with the source image.</span></span> <span data-ttu-id="cff84-282">확장과 같은 최신 모델의 모든 특수화가 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-282">Any specialization from the latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-to-an-azure-ad-domain"></a><span data-ttu-id="cff84-283">가상 컴퓨터 확장 집합을 Azure AD 도메인에 가입하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-283">How do I join a virtual machine scale set to an Azure AD domain?</span></span>

<span data-ttu-id="cff84-284">가상 컴퓨터 확장 집합을 Azure AD(Azure Active Directory) 도메인에 가입하려면 확장을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-284">To join a virtual machine scale set to an Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="cff84-285">확장을 정의하려면 JsonADDomainExtension 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-285">To define an extension, use the JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-to-install-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="cff84-286">내 가상 컴퓨터 확장 집합은 설치를 시도하며 이로 인해 재부팅이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-286">My virtual machine scale set extension is trying to install something that requires a reboot.</span></span> <span data-ttu-id="cff84-287">예: "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span><span class="sxs-lookup"><span data-stu-id="cff84-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="cff84-288">가상 컴퓨터 확장 집합 확장이 설치를 시도하며 이로 인해 재부팅이 필요한 경우 Azure Automation DSC(필요한 상태 구성) 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-288">If your virtual machine scale set extension is trying to install something that requires a reboot, you can use the Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="cff84-289">운영 체제가 Windows Server 2012 R2인 경우 Azure는 WMF(Windows Management Framework) 5.0 설치를 시작하고, 재부팅한 후 구성을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-289">If the operating system is Windows Server 2012 R2, Azure pulls in the Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with the configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="cff84-290">가상 컴퓨터 확장 집합에 대해 맬웨어 방지를 설정하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="cff84-291">가상 컴퓨터 확장 집합에 대해 맬웨어 방지를 설정하려면 다음 PowerShell 예제를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-291">To turn on antimalware on your virtual machine scale set, use the following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve the most recent version number of the extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-to-execute-a-custom-script-thats-hosted-in-a-private-storage-account-the-script-runs-successfully-when-the-storage-is-public-but-when-i-try-to-use-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="cff84-292">개인 저장소 계정에서 호스트되는 사용자 지정 스크립트를 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-292">I need to execute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="cff84-293">이 스크립트는 저장소가 공용일 때 성공적으로 실행되지만 SAS(공유 액세스 서명)을 사용하려고 하면 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-293">The script runs successfully when the storage is public, but when I try to use a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="cff84-294">“올바른 공유 액세스 서명에 대한 필수 매개 변수가 없음” 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="cff84-295">Link+SAS는 로컬 브라우저에서 잘 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="cff84-296">개인 저장소 계정에 호스트되는 사용자 지정 스크립트를 실행하려면 저장소 계정 키 및 이름을 사용하여 보호 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-296">To execute a custom script that's hosted in a private storage account, set up protected settings with the storage account key and name.</span></span> <span data-ttu-id="cff84-297">자세한 내용은 [Windows용 사용자 지정 스크립트 확장](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="cff84-298">네트워킹</span><span class="sxs-lookup"><span data-stu-id="cff84-298">Networking</span></span>
 
### <a name="is-it-possible-to-assign-a-network-security-group-nsg-to-a-scale-set-so-that-it-will-apply-to-all-the-vm-nics-in-the-set"></a><span data-ttu-id="cff84-299">집합의 모든 VM NIC에 적용되도록 확장 집합에 NSG(네트워크 보안 그룹)를 할당할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-299">Is it possible to assign a Network Security Group (NSG) to a scale set, so that it will apply to all the VM NICs in the set?</span></span>

<span data-ttu-id="cff84-300">예.</span><span class="sxs-lookup"><span data-stu-id="cff84-300">Yes.</span></span> <span data-ttu-id="cff84-301">네트워크 프로필의 networkInterfaceConfigurations 섹션에서 참조하여 네트워크 보안 그룹을 확장 집합에 직접 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-301">A Network Security Group can be applied directly to a scale set by referencing it in the networkInterfaceConfigurations section of the network profile.</span></span> <span data-ttu-id="cff84-302">예제:</span><span class="sxs-lookup"><span data-stu-id="cff84-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-the-same-subscription-and-same-region"></a><span data-ttu-id="cff84-303">동일한 구독 및 동일한 지역에서 가상 컴퓨터 확장 집합에 대해 VIP 교환을 수행하려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-303">How do I do a VIP swap for virtual machine scale sets in the same subscription and same region?</span></span>

<span data-ttu-id="cff84-304">Azure Load Balancer 프런트 엔드가 포함된 두 개의 가상 컴퓨터 확장 집합이 있고 해당 항목이 동일한 구독 및 지역에 있는 경우 각 항목의 공용 IP 주소 할당을 취소하고 다른 항목에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in the same subscription and region, you could deallocate the public IP addresses from each one, and assign to the other.</span></span> <span data-ttu-id="cff84-305">예제는 [VIP 교체: Azure Resource Manager에서 청록색 배포](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="cff84-306">리소스가 네트워크 수준에서 할당 취소/할당되지만 지연되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-306">This does imply a delay though as the resources are deallocated/allocated at the network level.</span></span> <span data-ttu-id="cff84-307">더 빠른 옵션은 두 개의 백 엔드 풀 및 라우팅 규칙과 함께 Azure Application Gateway를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-307">A faster option is to use Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="cff84-308">또는 스테이징 및 프로덕션 슬롯 간의 빠른 전환을 지원하는 [Azure App service](https://azure.microsoft.com/en-us/services/app-service/)를 사용하여 응용 프로그램을 호스트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-to-use-for-static-private-ip-address-allocation"></a><span data-ttu-id="cff84-309">정적 개인 IP 주소를 할당하는 데 사용할 개인 IP 주소의 범위를 지정하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-309">How do I specify a range of private IP addresses to use for static private IP address allocation?</span></span>

<span data-ttu-id="cff84-310">IP 주소는 사용자가 지정한 서브넷에서 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="cff84-311">가상 컴퓨터 확장 집합 설정 IP 주소를 할당하는 방법은 항상 "동적"이지만 이러한 IP 주소를 변경할 수 있다는 뜻은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-311">The allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="cff84-312">이 경우 "동적"은 PUT 요청에서 IP 주소를 지정하지 않는다는 것을 의미할 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-312">In this case, "dynamic" only means that you do not specify the IP address in a PUT request.</span></span> <span data-ttu-id="cff84-313">서브넷을 사용하여 정적 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-313">Specify the static set by using the subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-to-an-existing-azure-virtual-network"></a><span data-ttu-id="cff84-314">기존 Azure Virtual Network에 가상 컴퓨터 확장 집합을 배포하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-314">How do I deploy a virtual machine scale set to an existing Azure virtual network?</span></span> 

<span data-ttu-id="cff84-315">기존 Azure Virtual Network에 가상 컴퓨터 확장 집합을 배포하려면 [기존 가상 네트워크에 가상 컴퓨터 확장 집합 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-315">To deploy a virtual machine scale set to an existing Azure virtual network, see [Deploy a virtual machine scale set to an existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-the-ip-address-of-the-first-vm-in-a-virtual-machine-scale-set-to-the-output-of-a-template"></a><span data-ttu-id="cff84-316">가상 컴퓨터 확장 집합에 포함된 첫 번째 VM의 IP 주소를 템플릿의 출력에 추가하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-316">How do I add the IP address of the first VM in a virtual machine scale set to the output of a template?</span></span>

<span data-ttu-id="cff84-317">가상 컴퓨터 확장 집합에 포함된 첫 번째 VM의 IP 주소를 템플릿의 출력에 추가하려면 [ARM: VMSS 개인 IP 가져오기](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-317">To add the IP address of the first VM in a virtual machine scale set to the output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="cff84-318">가속 네트워킹을 포함한 확장 집합을 사용할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="cff84-319">예.</span><span class="sxs-lookup"><span data-stu-id="cff84-319">Yes.</span></span> <span data-ttu-id="cff84-320">가속된 네트워킹을 사용하려면 확장 집합의 networkInterfaceConfigurations 설정에서 enableAcceleratedNetworking을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-320">To use accelerated networking, set enableAcceleratedNetworking to true in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="cff84-321">예:</span><span class="sxs-lookup"><span data-stu-id="cff84-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-the-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="cff84-322">확장 집합에서 사용하는 DNS 서버를 구성하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-322">How can I configure the DNS servers used by a scale set?</span></span>

<span data-ttu-id="cff84-323">사용자 지정 DNS 구성을 포함한 VM 확장 집합을 만들려면 dnsSettings JSON 패킷을 확장 집합 networkInterfaceConfigurations 섹션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-323">To create a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="cff84-324">예제:</span><span class="sxs-lookup"><span data-stu-id="cff84-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-to-assign-a-public-ip-address-to-each-vm"></a><span data-ttu-id="cff84-325">각 VM에 공용 IP 주소를 할당하도록 확장 집합을 구성하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-325">How can I configure a scale set to assign a public IP address to each VM?</span></span>

<span data-ttu-id="cff84-326">각 VM에 공용 IP 주소를 할당하는 VM 확장 집합을 만들려면 Microsoft.Compute/virtualMAchineScaleSets 리소스의 API 버전이 2017-03-30인지 확인하고 _publicipaddressconfiguration_ JSON 패킷을 확장 집합 ipConfigurations 섹션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-326">To create a VM scale set that assigns a public IP address to each VM, make sure the API version of the Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet to the scale set ipConfigurations section.</span></span> <span data-ttu-id="cff84-327">예제:</span><span class="sxs-lookup"><span data-stu-id="cff84-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-to-work-with-multiple-application-gateways"></a><span data-ttu-id="cff84-328">여러 Application Gateway를 사용하도록 확장 집합을 구성할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-328">Can I configure a scale set to work with multiple Application Gateways?</span></span>

<span data-ttu-id="cff84-329">예.</span><span class="sxs-lookup"><span data-stu-id="cff84-329">Yes.</span></span> <span data-ttu-id="cff84-330">여러 Application Gateway 백 엔드 주소 풀에 대한 리소스 ID를 확장 집합 네트워크 프로필의 _ipConfigurations_ 섹션에 있는 _applicationGatewayBackendAddressPools_ 목록에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-330">You can add the resource id's for multiple Application Gateway backend address pools to the _applicationGatewayBackendAddressPools_ list in the _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="cff84-331">확장</span><span class="sxs-lookup"><span data-stu-id="cff84-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="cff84-332">어떤 경우에 VM이 2개 미만인 가상 컴퓨터 확장 집합을 만들어야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="cff84-333">VM이 2개 미만인 가상 컴퓨터 확장 집합을 만드는 한 가지 이유는 가상 컴퓨터 확장 집합의 탄력적 속성을 사용해야 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-333">One reason to create a virtual machine scale set with fewer than two VMs would be to use the elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="cff84-334">예를 들어 VM 실행 비용을 지불하지 않고 인프라를 정의하기 위해 VM이 없는 가상 컴퓨터 확장 집합을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-334">For example, you could deploy a virtual machine scale set with zero VMs to define your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="cff84-335">그런 다음 VM을 배포할 준비가 되면 가상 컴퓨터 확장 집합의 "용량"을 프로덕션 인스턴스 수로 늘립니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-335">Then, when you are ready to deploy VMs, increase the “capacity” of the virtual machine scale set to the production instance count.</span></span>

<span data-ttu-id="cff84-336">VM이 2개 미만인 가상 컴퓨터 확장 집합을 만드는 또 다른 경우는 개별 VM이 있는 가용성 집합을 사용하는 것보다 가용성에 별 관심이 없을 때입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="cff84-337">가상 컴퓨터 확장 집합은 대체할 수 있는 미분화된 계산 단위로 작업하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-337">Virtual machine scale sets give you a way to work with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="cff84-338">이 일관성은 가상 컴퓨터 확장 집합과 가용성 집합의 주요 차별 요인이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="cff84-339">다양한 상태 비저장 워크로드는 개별 단위를 추적하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="cff84-340">워크로드가 감소하면 하나의 Compute 단위로 축소하고, 워크로드가 증가하면 여러 단위로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-340">If the workload drops, you can scale down to one compute unit, and then scale up to many when the workload increases.</span></span>

### <a name="how-do-i-change-the-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="cff84-341">가상 컴퓨터 확장 집합의 VM 수를 변경하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-341">How do I change the number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="cff84-342">가상 컴퓨터 확장 집합의 VM 수를 변경하려면 [가상 컴퓨터 확장 집합의 인스턴스 수 변경](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-342">To change the number of VMs in a virtual machine scale set, see [Change the instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="cff84-343">특정 임계값에 도달하는 경우 사용자 지정 경고를 정의하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="cff84-344">지정된 임계값에 대한 경고를 처리하는 방법은 다소 유연한 편입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="cff84-345">예를 들어 사용자 지정 웹후크를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="cff84-346">다음 웹후크 예제는 Resource Manager 템플릿에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-346">The following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="cff84-347">이 예제에서는 임계값에 도달될 경우 경고가 Pagerduty.com으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-347">In this example, an alert goes to Pagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="cff84-348">패치 및 작업</span><span class="sxs-lookup"><span data-stu-id="cff84-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="cff84-349">기존 리소스 그룹에서 확장 집합을 만들려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="cff84-350">기존 리소스 그룹에서 확장 집합을 만드는 것은 아직 Azure Portal에서 할 수는 없지만 Azure Resource Manager 템플릿에서 확장 집합을 배포할 때에는 기존 리소스 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-350">Creating scale sets in an existing resource group is not yet possible from the Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="cff84-351">또한 Azure PowerShell 또는 CLI를 사용하여 확장 집합을 만들 때에도 기존 리소스 그룹을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-to-another-resource-group"></a><span data-ttu-id="cff84-352">확장 집합을 다른 리소스 그룹으로 이동할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-352">Can we move a scale set to another resource group?</span></span>

<span data-ttu-id="cff84-353">예. 확장 집합 리소스를 새 구독 또는 리소스 그룹에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-353">Yes, you can move scale set resources to a new subscription or resource group.</span></span>

### <a name="how-to-i-update-my-virtual-machine-scale-set-to-a-new-image-how-do-i-manage-patching"></a><span data-ttu-id="cff84-354">내 가상 컴퓨터 확장 집합을 새 이미지로 업데이트하는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="cff84-354">How to I update my virtual machine scale set to a new image?</span></span> <span data-ttu-id="cff84-355">패치는 어떻게 관리해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-355">How do I manage patching?</span></span>

<span data-ttu-id="cff84-356">가상 컴퓨터 확장 집합을 새 이미지로 업데이트하고 패치를 관리하려면 [가상 컴퓨터 확장 집합 업그레이드](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-356">To update your virtual machine scale set to a new image, and to manage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-the-reimage-operation-to-reset-a-vm-without-changing-the-image-that-is-i-want-reset-a-vm-to-factory-settings-rather-than-to-a-new-image"></a><span data-ttu-id="cff84-357">이미지로 다시 설치 작업을 사용하여 이미지를 변경하지 않고 VM을 다시 설정할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-357">Can I use the reimage operation to reset a VM without changing the image?</span></span> <span data-ttu-id="cff84-358">(즉 VM을 새 이미지가 아닌 출하 시 설정으로 다시 설정하려고 합니다.)</span><span class="sxs-lookup"><span data-stu-id="cff84-358">(That is, I want reset a VM to factory settings rather than to a new image.)</span></span>

<span data-ttu-id="cff84-359">예. 이미지로 다시 설치 작업을 사용하여 이미지를 변경하지 않고 VM을 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-359">Yes, you can use the reimage operation to reset a VM without changing the image.</span></span> <span data-ttu-id="cff84-360">그러나 가상 컴퓨터 확장 집합이 `version = latest`인 플랫폼 이미지를 참조하면 `reimage`를 호출할 때 VM에서 최신 OS 이미지로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update to a later OS image when you call `reimage`.</span></span>

<span data-ttu-id="cff84-361">자세한 내용은 [가상 컴퓨터 확장 집합의 모든 VM 관리](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cff84-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="cff84-362">문제 해결</span><span class="sxs-lookup"><span data-stu-id="cff84-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="cff84-363">부팅 진단을 켜려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="cff84-364">부팅 진단을 켜려면 먼저 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-364">To turn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="cff84-365">그런 후 이 JSON 블록을 가상 컴퓨터 확장 집합 **virtualMachineProfile**에 배치하고 해당 가상 컴퓨터 확장 집합을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update the virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="cff84-366">새 VM이 만들어지면 VM의 InstanceView 속성에 스크린샷 등에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-366">When a new VM is created, the InstanceView property of the VM shows the details for the screenshot, and so on.</span></span> <span data-ttu-id="cff84-367">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="cff84-368">가상 컴퓨터 속성</span><span class="sxs-lookup"><span data-stu-id="cff84-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-the-fault-domain-for-each-of-the-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="cff84-369">여러 번 호출하지 않고도 각 VM에 대한 속성 정보를 얻으려면 어떻게 합니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="cff84-370">예를 들어 가상 컴퓨터 확장 집합에서 100개의 VM 각각에 대해 장애 도메인을 얻으려면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="cff84-370">For example, how would I get the fault domain for each of the 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="cff84-371">여러 번 호출하지 않고 각 VM에 대한 속성 정보를 가져오려면 다음 리소스 URI에 대해 REST API `GET`을 수행하여 `ListVMInstanceViews`를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-371">To get property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on the following resource URI:</span></span>

<span data-ttu-id="cff84-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span><span class="sxs-lookup"><span data-stu-id="cff84-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-to-different-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="cff84-373">가상 컴퓨터 확장 집합의 다른 VM에 다른 확장 인수를 전달할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="cff84-373">Can I pass different extension arguments to different VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="cff84-374">아니요. 가상 컴퓨터 확장 집합의 다른 VM에 다른 확장 인수를 전달할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-374">No, you cannot pass different extension arguments to different VMs in a virtual machine scale set.</span></span> <span data-ttu-id="cff84-375">그렇지만 확장은 컴퓨터 이름과 같이 실행 중인 VM의 고유한 속성에 따라 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-375">However, extensions can act based on the unique properties of the VM they are running on, such as on the machine name.</span></span> <span data-ttu-id="cff84-376">또한 확장은 http://169.254.169.254에 있는 인스턴스 메타데이터를 쿼리하여 VM에 대한 자세한 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-376">Extensions also can query instance metadata on http://169.254.169.254 to get more information about the VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="cff84-377">가상 컴퓨터 확장 집합 VM 컴퓨터 이름과 VM ID 간에 차이가 발생하는 이유는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="cff84-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="cff84-378">예를 들어 0, 1, 3...입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="cff84-379">가상 컴퓨터 확장 집합 **overprovision** 속성은 기본값인 **true**로 설정되어 있으므로 가상 컴퓨터 확장 집합 VM 컴퓨터 이름 간에는 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set to the default value of **true**.</span></span> <span data-ttu-id="cff84-380">과도 프로비저닝이 **true**로 설정되면 요청된 것보다 더 많은 VM이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-380">If overprovisioning is set to **true**, more VMs than requested are created.</span></span> <span data-ttu-id="cff84-381">그런 후에 추가 VM은 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="cff84-382">이 경우 배포 안정성은 향상되지만 연속된 이름 지정 및 연속된 NAT(Network Address Translation) 규칙은 준수되지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-382">In this case, you gain increased deployment reliability, but at the expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="cff84-383">이 속성을 **false**로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-383">You can set this property to **false**.</span></span> <span data-ttu-id="cff84-384">소규모 가상 컴퓨터 확장 집합의 경우 이렇게 해도 배포 안정성에 큰 영향을 주지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-the-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-the-vm-when-should-i-choose-one-over-the-other"></a><span data-ttu-id="cff84-385">가상 컴퓨터 확장 집합에서 VM을 삭제하는 것과 VM을 할당 취소하는 것 사이의 차이점은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-385">What is the difference between deleting a VM in a virtual machine scale set and deallocating the VM?</span></span> <span data-ttu-id="cff84-386">언제 다른 하나를 선택해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="cff84-386">When should I choose one over the other?</span></span>

<span data-ttu-id="cff84-387">가상 컴퓨터 확장 집합에서 VM을 삭제하는 것과 VM을 할당 취소하는 것 사이의 주요 차이점은 `deallocate`로는 VHD(가상 하드 디스크)가 삭제되지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-387">The main difference between deleting a VM in a virtual machine scale set and deallocating the VM is that `deallocate` doesn’t delete the virtual hard disks (VHDs).</span></span> <span data-ttu-id="cff84-388">`stop deallocate` 실행과 관련된 저장소 비용이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="cff84-389">다음과 같은 이유 중 하나로 두 가지 방법 중 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-389">You might use one or the other for one of the following reasons:</span></span>

- <span data-ttu-id="cff84-390">Compute 비용은 더 이상 지불하지 않고, VM의 디스크 상태는 유지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-390">You want to stop paying compute costs, but you want to keep the disk state of the VMs.</span></span>
- <span data-ttu-id="cff84-391">가상 컴퓨터 확장 집합을 확장하는 것보다 더 빠르게 VM 집합을 시작하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-391">You want to start a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="cff84-392">이 시나리오와 관련하여 사용자 고유의 자동 크기 조정 엔진을 만들고 더 빠른 종단 간 확장을 원했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-392">Related to this scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="cff84-393">장애 도메인이나 업데이트 도메인 간에 고르게 분산되지 않은 가상 컴퓨터 확장 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="cff84-394">이러한 상황은 과도한 프로비저닝 후에 선택적으로 VM을 삭제했거나 VM이 삭제되었기 때문에 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="cff84-395">가상 컴퓨터 확장 집합에 대해 `stop deallocate`를 실행한 후 `start`를 실행하면 장애 도메인 또는 업데이트 도메인 간에 VM이 균일하게 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="cff84-395">Running `stop deallocate` followed by `start` on the virtual machine scale set evenly distributes the VMs across fault domains or update domains.</span></span>

