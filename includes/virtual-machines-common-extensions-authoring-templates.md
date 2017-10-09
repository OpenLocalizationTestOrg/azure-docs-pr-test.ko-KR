## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="3915e-101">Azure 리소스 관리자 템플릿 개요</span><span class="sxs-lookup"><span data-stu-id="3915e-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="3915e-102">Azure 리소스 관리자 템플릿을 사용 하면 toodeclaratively Json 언어에서 리소스 간의 종속성 hello를 정의 하 여 hello Azure IaaS 인프라를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3915e-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="3915e-103">Azure 리소스 관리자 템플릿 자세한 개요는 다음 toohello 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3915e-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="3915e-104">리소스 그룹 개요</span><span class="sxs-lookup"><span data-stu-id="3915e-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="3915e-105">VM 확장에 대한 샘플 템플릿 코드 조각</span><span class="sxs-lookup"><span data-stu-id="3915e-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="3915e-106">Azure 리소스 관리자 템플릿 부분 만들어야 하는 대로 VM 확장을 배포 toodeclaratively hello 확장 구성 hello 서식 파일에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3915e-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="3915e-107">다음은 확장 구성 hello를 지정 하는 hello 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3915e-107">Here is hello format for specifying hello extension configuration.</span></span>

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

<span data-ttu-id="3915e-108">위의 hello 알 수 있듯이 hello 확장 템플릿이 두 주요 부분을 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3915e-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="3915e-109">확장 이름, 게시자 및 버전</span><span class="sxs-lookup"><span data-stu-id="3915e-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="3915e-110">확장 구성</span><span class="sxs-lookup"><span data-stu-id="3915e-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="3915e-111">Hello 게시자, 형식 및 모든 확장에 대 한 typeHandlerVersion 식별</span><span class="sxs-lookup"><span data-stu-id="3915e-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="3915e-112">Azure VM 확장은 Microsoft에서 게시 하 고 신뢰할 수 있는 3rd 파티 게시자 및 각 확장의 게시자, 유형 및 hello typeHandlerVersion으로 고유 하 게 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="3915e-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="3915e-113">다음과 같이 결정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3915e-113">These can be determined as following:</span></span>  

