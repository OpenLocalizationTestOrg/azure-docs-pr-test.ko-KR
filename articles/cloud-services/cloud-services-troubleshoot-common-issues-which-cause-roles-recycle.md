---
title: "클라우드 서비스 역할 재활용의 일반적인 원인 | Microsoft Docs"
description: "재활용이 중요한 가동 중지 시간을 갑작스럽게 발생시킬 수 있는 클라우드 서비스 역할입니다. 역할이 재활용되도록 하는 일반적인 문제는 다음과 같으며 이는 가동 중지를 줄이는 데 도움이 될 수 있습니다."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e55009c72b977ee4a30f6c71043bde483849f78f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="common-issues-that-cause-roles-to-recycle"></a><span data-ttu-id="62aa5-104">역할을 재활용하게 하는 일반적인 문제</span><span class="sxs-lookup"><span data-stu-id="62aa5-104">Common issues that cause roles to recycle</span></span>
<span data-ttu-id="62aa5-105">이 문서에서는 배포 문제의 일반적인 몇 가지 원인을 설명하고 이러한 문제를 해결하기 위한 문제 해결 팁을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-105">This article discusses some of the common causes of deployment problems and provides troubleshooting tips to help you resolve these problems.</span></span> <span data-ttu-id="62aa5-106">응용 프로그램에 문제가 있다는 것을 역할 인스턴스가 시작에 실패하거나 초기화, 사용 중, 및 중지 상태를 반복할 경우에 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-106">An indication that a problem exists with an application is when the role instance fails to start, or it cycles between the initializing, busy, and stopping states.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a><span data-ttu-id="62aa5-107">런타임 종속성 누락</span><span class="sxs-lookup"><span data-stu-id="62aa5-107">Missing runtime dependencies</span></span>
<span data-ttu-id="62aa5-108">응용 프로그램의 역할이 .NET Framework 또는 Azure 관리된 라이브러리의 일부가 아닌 어셈블리를 사용하는 경우 응용 프로그램 패키지에 해당 어셈블리를 명시적으로 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-108">If a role in your application relies on any assembly that is not part of the .NET Framework or the Azure managed library, you must explicitly include that assembly in the application package.</span></span> <span data-ttu-id="62aa5-109">기타 Microsoft 프레임워크가 기본적으로 Azure에서 사용할 수 없다는 사실을 염두에 두십시오.</span><span class="sxs-lookup"><span data-stu-id="62aa5-109">Keep in mind that other Microsoft frameworks are not available on Azure by default.</span></span> <span data-ttu-id="62aa5-110">역할이 이러한 프레임워크를 사용하는 경우 응용 프로그램 패키지에 해당 어셈블리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-110">If your role relies on such a framework, you must add those assemblies to the application package.</span></span>

<span data-ttu-id="62aa5-111">응용 프로그램을 작성하고 포장하기 전에 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-111">Before you build and package your application, verify the following:</span></span>

* <span data-ttu-id="62aa5-112">Visual studio를 사용하는 경우 **로컬 복사** 속성이 Azure SDK 또는.NET Framework의 일부가 아닌 프로젝트에서 참조된 각 어셈블리에 대해 **True**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-112">If using Visual studio, make sure the **Copy Local** property is set to **True** for each referenced assembly in your project that is not part of the Azure SDK or the .NET Framework.</span></span>
* <span data-ttu-id="62aa5-113">web.config 파일이 컴파일 요소에서 사용되지 않은 어셈블리를 참조하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-113">Make sure the web.config file does not reference any unused assemblies in the compilation element.</span></span>
* <span data-ttu-id="62aa5-114">모든 .cshtml 파일의 **빌드 작업**은 **콘텐츠**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-114">The **Build Action** of every .cshtml file is set to **Content**.</span></span> <span data-ttu-id="62aa5-115">이렇게 하면 패키지에서 파일이 올바르게 표시되고 기타 참조된 파일이 표시되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-115">This ensures that the files will appear correctly in the package and enables other referenced files to appear in the package.</span></span>

## <a name="assembly-targets-wrong-platform"></a><span data-ttu-id="62aa5-116">어셈블리가 잘못된 플랫폼을 목표로 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-116">Assembly targets wrong platform</span></span>
<span data-ttu-id="62aa5-117">Azure는 64비트 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-117">Azure is a 64-bit environment.</span></span> <span data-ttu-id="62aa5-118">따라서 32비트 대상에 컴파일된 .NET 어셈블리는 Azure에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-118">Therefore, .NET assemblies compiled for a 32-bit target won't work on Azure.</span></span>

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a><span data-ttu-id="62aa5-119">초기화하거나 중지하는 동안 처리되지 않은 예외를 throw하는 역할</span><span class="sxs-lookup"><span data-stu-id="62aa5-119">Role throws unhandled exceptions while initializing or stopping</span></span>
<span data-ttu-id="62aa5-120">[OnStart], [OnStop] 및 [실행] 메서드를 포함하는 [RoleEntryPoint] 클래스의 메서드에서 throw되는 예외는 처리되지 않은 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-120">Any exceptions that are thrown by the methods of the [RoleEntryPoint] class, which includes the [OnStart], [OnStop], and [Run] methods, are unhandled exceptions.</span></span> <span data-ttu-id="62aa5-121">이러한 메서드에서 처리되지 않은 예외가 발생하면 역할이 재활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-121">If an unhandled exception occurs in one of these methods, the role will recycle.</span></span> <span data-ttu-id="62aa5-122">역할이 반복적으로 재활용되면 시작하려 할 때마다 처리되지 않은 예외가 throw될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-122">If the role is recycling repeatedly, it may be throwing an unhandled exception each time it tries to start.</span></span>

## <a name="role-returns-from-run-method"></a><span data-ttu-id="62aa5-123">역할은 실행 메서드에서 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-123">Role returns from Run method</span></span>
<span data-ttu-id="62aa5-124">[실행] 메서드는 무기한 실행되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-124">The [Run] method is intended to run indefinitely.</span></span> <span data-ttu-id="62aa5-125">코드가 [실행] 메서드를 재정의하는 경우 무기한 대기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-125">If your code overrides the [Run] method, it should sleep indefinitely.</span></span> <span data-ttu-id="62aa5-126">[실행] 메서드가 반환되는 경우 역할은 재활용됩니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-126">If the [Run] method returns, the role recycles.</span></span>

## <a name="incorrect-diagnosticsconnectionstring-setting"></a><span data-ttu-id="62aa5-127">잘못된 DiagnosticsConnectionString 설정</span><span class="sxs-lookup"><span data-stu-id="62aa5-127">Incorrect DiagnosticsConnectionString setting</span></span>
<span data-ttu-id="62aa5-128">응용 프로그램이 Azure 진단을 사용하는 경우 서비스 구성 파일은 `DiagnosticsConnectionString` 구성 설정을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-128">If application uses Azure Diagnostics, your service configuration file must specify the `DiagnosticsConnectionString` configuration setting.</span></span> <span data-ttu-id="62aa5-129">이 설정은 Azure에서 저장소 계정에 HTTPS 연결을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-129">This setting should specify an HTTPS connection to your storage account in Azure.</span></span>

<span data-ttu-id="62aa5-130">Azure에 응용 프로그램 패키지를 배포하기 전에 `DiagnosticsConnectionString` 설정이 올바른지 확인하려면 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-130">To ensure that your `DiagnosticsConnectionString` setting is correct before you deploy your application package to Azure, verify the following:</span></span>  

* <span data-ttu-id="62aa5-131">`DiagnosticsConnectionString` 설정이 Azure의 유효한 저장소 계정을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-131">The `DiagnosticsConnectionString` setting points to a valid storage account in Azure.</span></span>  
  <span data-ttu-id="62aa5-132">기본적으로 이 설정은 에뮬레이트된 저장소 계정을 가리키므로 응용 프로그램 패키지를 배포하기 전에 이 설정을 명시적으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-132">By default, this setting points to the emulated storage account, so you must explicitly change this setting before you deploy your application package.</span></span> <span data-ttu-id="62aa5-133">이 설정을 변경하지 않는 경우 역할 인스턴스가 진단 모니터링을 시작하려고 할 때 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-133">If you do not change this setting, an exception is thrown when the role instance attempts to start the diagnostic monitor.</span></span> <span data-ttu-id="62aa5-134">역할 인스턴스가 무기한 재활용되게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-134">This may cause the role instance to recycle indefinitely.</span></span>
* <span data-ttu-id="62aa5-135">연결 문자열은 다음과 같은 [형식](../storage/common/storage-configure-connection-string.md)으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-135">The connection string is specified in the following [format](../storage/common/storage-configure-connection-string.md).</span></span> <span data-ttu-id="62aa5-136">(HTTPS 프로토콜을 지정해야 합니다.) *MyAccountName*을 저장소 계정의 이름으로 바꾸고 *MyAccountKey*를 선택키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-136">(The protocol must be specified as HTTPS.) Replace *MyAccountName* with the name of your storage account, and *MyAccountKey* with your access key:</span></span>    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  <span data-ttu-id="62aa5-137">Microsoft Visual Studio용 Azure Tools를 사용하여 응용 프로그램을 개발하는 경우 속성 페이지를 사용하여 이 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-137">If you are developing your application by using Azure Tools for Microsoft Visual Studio, you can use the property pages to set this value.</span></span>

## <a name="exported-certificate-does-not-include-private-key"></a><span data-ttu-id="62aa5-138">내보낸 인증서는 개인 키를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-138">Exported certificate does not include private key</span></span>
<span data-ttu-id="62aa5-139">SSL에서 웹 역할을 실행하려면 내보낸 관리 인증서가 개인 키를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-139">To run a web role under SSL, you must ensure that your exported management certificate includes the private key.</span></span> <span data-ttu-id="62aa5-140">*Windows 인증서 관리자*를 사용하여 인증서를 내보내는 경우 **개인 키 내보내기** 옵션에 대해 **예**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-140">If you use the *Windows Certificate Manager* to export the certificate, be sure to select **Yes** for the **Export the private key** option.</span></span> <span data-ttu-id="62aa5-141">인증서는 현재 지원되는 유일한 형식인 PFX 형식으로 내보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-141">The certificate must be exported in the PFX format, which is the only format currently supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62aa5-142">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62aa5-142">Next steps</span></span>
<span data-ttu-id="62aa5-143">클라우드 서비스에 대한 [문제해결 문서](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 를 더 봅니다.</span><span class="sxs-lookup"><span data-stu-id="62aa5-143">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="62aa5-144">[Kevin Williamson의 블로그 시리즈](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)에서 더 많은 역할 재활용 시나리오를 보세요.</span><span class="sxs-lookup"><span data-stu-id="62aa5-144">View more role recycling scenarios at [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[실행]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
