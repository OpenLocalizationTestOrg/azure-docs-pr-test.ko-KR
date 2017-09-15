## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="69bea-101">Azure 리소스 관리자 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="69bea-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="69bea-102">Azure Resource Manager 템플릿을 사용하면 리소스 간의 종속성을 정의하여 JSON 언어에서 Azure IaaS 인프라를 선언적으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69bea-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="69bea-103">Azure Resource Manager 템플릿에 대한 자세한 개요는 아래 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69bea-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="69bea-104">리소스 그룹 개요</span><span class="sxs-lookup"><span data-stu-id="69bea-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="69bea-105">VM 확장에 대한 샘플 템플릿 코드 조각</span><span class="sxs-lookup"><span data-stu-id="69bea-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="69bea-106">Azure Resource Manager 템플릿의 일부로 VM 확장을 배포하려면 템플릿에 확장 구성을 선언적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69bea-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="69bea-107">다음은 확장 구성을 지정하는 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="69bea-107">Here is the format for specifying the extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="69bea-108">위에서 볼 수 있는 것처럼 확장 템플릿은 다음 두 주요 부분으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="69bea-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="69bea-109">확장 이름, 게시자 및 버전</span><span class="sxs-lookup"><span data-stu-id="69bea-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="69bea-110">확장 구성</span><span class="sxs-lookup"><span data-stu-id="69bea-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="69bea-111">모든 확장에 대한 게시자, 유형 및 typeHandlerVersion 식별</span><span class="sxs-lookup"><span data-stu-id="69bea-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="69bea-112">Azure VM 확장은 Microsoft 및 신뢰할 수 있는 타사 게시자가 게시하며 각 확장은 게시자, 유형 및 typeHandlerVersion으로 고유하게 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="69bea-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="69bea-113">다음과 같이 결정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69bea-113">These can be determined as following:</span></span>  

