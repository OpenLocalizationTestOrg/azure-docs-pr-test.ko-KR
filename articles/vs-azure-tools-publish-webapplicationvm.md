---
title: Publish-WebApplicationVM | Microsoft Docs
description: "가상 컴퓨터에 웹 응용 프로그램을 배포하는 방법을 알아봅니다. 없는 경우 이 스크립트는 Azure 구독에 필요한 리소스를 만듭니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 2738fc1dff50a177a227ae2c7719bd9a192d82ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="1ff6a-104">Publish-WebApplicationVM (Windows PowerShell 스크립트)</span><span class="sxs-lookup"><span data-stu-id="1ff6a-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="1ff6a-105">가상 컴퓨터에 웹 응용 프로그램을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="1ff6a-106">없는 경우 스크립트는 Azure 구독에 필요한 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="1ff6a-107">구성</span><span class="sxs-lookup"><span data-stu-id="1ff6a-107">Configuration</span></span>
<span data-ttu-id="1ff6a-108">배포의 세부 정보를 설명하는 JSON 구성 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="1ff6a-109">Aliases</span><span class="sxs-lookup"><span data-stu-id="1ff6a-109">Aliases</span></span> | <span data-ttu-id="1ff6a-110">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="1ff6a-111">Required?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-111">Required?</span></span> |<span data-ttu-id="1ff6a-112">true</span><span class="sxs-lookup"><span data-stu-id="1ff6a-112">true</span></span> |
| <span data-ttu-id="1ff6a-113">Position</span><span class="sxs-lookup"><span data-stu-id="1ff6a-113">Position</span></span> |<span data-ttu-id="1ff6a-114">named</span><span class="sxs-lookup"><span data-stu-id="1ff6a-114">named</span></span> |
| <span data-ttu-id="1ff6a-115">기본값</span><span class="sxs-lookup"><span data-stu-id="1ff6a-115">Default value</span></span> |<span data-ttu-id="1ff6a-116">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-116">none</span></span> |
| <span data-ttu-id="1ff6a-117">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-117">Accept pipeline input?</span></span> |<span data-ttu-id="1ff6a-118">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-118">false</span></span> |
| <span data-ttu-id="1ff6a-119">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-119">Accept wildcard characters?</span></span> |<span data-ttu-id="1ff6a-120">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="1ff6a-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="1ff6a-121">SubscriptionName</span></span>
<span data-ttu-id="1ff6a-122">가상 컴퓨터를 만들려는 Azure 구독의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="1ff6a-123">Aliases</span><span class="sxs-lookup"><span data-stu-id="1ff6a-123">Aliases</span></span> | <span data-ttu-id="1ff6a-124">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="1ff6a-125">Required?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-125">Required?</span></span> |<span data-ttu-id="1ff6a-126">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-126">false</span></span> |
| <span data-ttu-id="1ff6a-127">Position</span><span class="sxs-lookup"><span data-stu-id="1ff6a-127">Position</span></span> |<span data-ttu-id="1ff6a-128">named</span><span class="sxs-lookup"><span data-stu-id="1ff6a-128">named</span></span> |
| <span data-ttu-id="1ff6a-129">기본값</span><span class="sxs-lookup"><span data-stu-id="1ff6a-129">Default value</span></span> |<span data-ttu-id="1ff6a-130">구독 파일의 첫 번째 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="1ff6a-131">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-131">Accept pipeline input?</span></span> |<span data-ttu-id="1ff6a-132">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-132">false</span></span> |
| <span data-ttu-id="1ff6a-133">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-133">Accept wildcard characters?</span></span> |<span data-ttu-id="1ff6a-134">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="1ff6a-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="1ff6a-135">WebDeployPackage</span></span>
<span data-ttu-id="1ff6a-136">가상 컴퓨터에 게시하는 웹 배포 패키지에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="1ff6a-137">Visual Studio에서 웹 게시 마법사를 사용하여 이 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="1ff6a-138">[방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="1ff6a-139">Aliases</span><span class="sxs-lookup"><span data-stu-id="1ff6a-139">Aliases</span></span> | <span data-ttu-id="1ff6a-140">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="1ff6a-141">Required?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-141">Required?</span></span> |<span data-ttu-id="1ff6a-142">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-142">false</span></span> |
| <span data-ttu-id="1ff6a-143">Position</span><span class="sxs-lookup"><span data-stu-id="1ff6a-143">Position</span></span> |<span data-ttu-id="1ff6a-144">named</span><span class="sxs-lookup"><span data-stu-id="1ff6a-144">named</span></span> |
| <span data-ttu-id="1ff6a-145">기본값</span><span class="sxs-lookup"><span data-stu-id="1ff6a-145">Default value</span></span> |<span data-ttu-id="1ff6a-146">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-146">none</span></span> |
| <span data-ttu-id="1ff6a-147">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-147">Accept pipeline input?</span></span> |<span data-ttu-id="1ff6a-148">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-148">false</span></span> |
| <span data-ttu-id="1ff6a-149">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-149">Accept wildcard characters?</span></span> |<span data-ttu-id="1ff6a-150">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="1ff6a-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="1ff6a-151">AllowUntrusted</span></span>
<span data-ttu-id="1ff6a-152">True인 경우 신뢰할 수 있는 루트 인증 기관에서 서명되지 않은 인증서 사용을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="1ff6a-153">Aliases</span><span class="sxs-lookup"><span data-stu-id="1ff6a-153">Aliases</span></span> | <span data-ttu-id="1ff6a-154">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="1ff6a-155">Required?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-155">Required?</span></span> |<span data-ttu-id="1ff6a-156">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-156">false</span></span> |
| <span data-ttu-id="1ff6a-157">Position</span><span class="sxs-lookup"><span data-stu-id="1ff6a-157">Position</span></span> |<span data-ttu-id="1ff6a-158">named</span><span class="sxs-lookup"><span data-stu-id="1ff6a-158">named</span></span> |
| <span data-ttu-id="1ff6a-159">기본값</span><span class="sxs-lookup"><span data-stu-id="1ff6a-159">Default value</span></span> |<span data-ttu-id="1ff6a-160">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-160">false</span></span> |
| <span data-ttu-id="1ff6a-161">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-161">Accept pipeline input?</span></span> |<span data-ttu-id="1ff6a-162">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-162">false</span></span> |
| <span data-ttu-id="1ff6a-163">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-163">Accept wildcard characters?</span></span> |<span data-ttu-id="1ff6a-164">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="1ff6a-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="1ff6a-165">VMPassword</span></span>
<span data-ttu-id="1ff6a-166">가상 컴퓨터 계정에 대한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="1ff6a-167">예: VMPassword @{Name = "admin"; 암호 = "password"}</span><span class="sxs-lookup"><span data-stu-id="1ff6a-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="1ff6a-168">Aliases</span><span class="sxs-lookup"><span data-stu-id="1ff6a-168">Aliases</span></span> | <span data-ttu-id="1ff6a-169">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="1ff6a-170">Required?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-170">Required?</span></span> |<span data-ttu-id="1ff6a-171">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-171">false</span></span> |
| <span data-ttu-id="1ff6a-172">Position</span><span class="sxs-lookup"><span data-stu-id="1ff6a-172">Position</span></span> |<span data-ttu-id="1ff6a-173">named</span><span class="sxs-lookup"><span data-stu-id="1ff6a-173">named</span></span> |
| <span data-ttu-id="1ff6a-174">기본값</span><span class="sxs-lookup"><span data-stu-id="1ff6a-174">Default value</span></span> |<span data-ttu-id="1ff6a-175">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-175">none</span></span> |
| <span data-ttu-id="1ff6a-176">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-176">Accept pipeline input?</span></span> |<span data-ttu-id="1ff6a-177">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-177">false</span></span> |
| <span data-ttu-id="1ff6a-178">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-178">Accept wildcard characters?</span></span> |<span data-ttu-id="1ff6a-179">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="1ff6a-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="1ff6a-180">DatabaseServerPassword</span></span>
<span data-ttu-id="1ff6a-181">Azure에서 SQL 데이터베이스에 대한 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="1ff6a-182">예: DatabaseServerPassword @{Name = "admin"; 암호 = "password"}</span><span class="sxs-lookup"><span data-stu-id="1ff6a-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="1ff6a-183">Aliases</span><span class="sxs-lookup"><span data-stu-id="1ff6a-183">Aliases</span></span> | <span data-ttu-id="1ff6a-184">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="1ff6a-185">Required?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-185">Required?</span></span> |<span data-ttu-id="1ff6a-186">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-186">false</span></span> |
| <span data-ttu-id="1ff6a-187">Position</span><span class="sxs-lookup"><span data-stu-id="1ff6a-187">Position</span></span> |<span data-ttu-id="1ff6a-188">named</span><span class="sxs-lookup"><span data-stu-id="1ff6a-188">named</span></span> |
| <span data-ttu-id="1ff6a-189">기본값</span><span class="sxs-lookup"><span data-stu-id="1ff6a-189">Default value</span></span> |<span data-ttu-id="1ff6a-190">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-190">none</span></span> |
| <span data-ttu-id="1ff6a-191">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-191">Accept pipeline input?</span></span> |<span data-ttu-id="1ff6a-192">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-192">false</span></span> |
| <span data-ttu-id="1ff6a-193">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-193">Accept wildcard characters?</span></span> |<span data-ttu-id="1ff6a-194">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="1ff6a-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="1ff6a-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="1ff6a-196">True이면 스크립트에서 출력 스트림으로 메시지를 프린트합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="1ff6a-197">Aliases</span><span class="sxs-lookup"><span data-stu-id="1ff6a-197">Aliases</span></span> | <span data-ttu-id="1ff6a-198">없음</span><span class="sxs-lookup"><span data-stu-id="1ff6a-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="1ff6a-199">Required?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-199">Required?</span></span> |<span data-ttu-id="1ff6a-200">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-200">false</span></span> |
| <span data-ttu-id="1ff6a-201">Position</span><span class="sxs-lookup"><span data-stu-id="1ff6a-201">Position</span></span> |<span data-ttu-id="1ff6a-202">named</span><span class="sxs-lookup"><span data-stu-id="1ff6a-202">named</span></span> |
| <span data-ttu-id="1ff6a-203">기본값</span><span class="sxs-lookup"><span data-stu-id="1ff6a-203">Default value</span></span> |<span data-ttu-id="1ff6a-204">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-204">false</span></span> |
| <span data-ttu-id="1ff6a-205">Accept Pipeline Input?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-205">Accept pipeline input?</span></span> |<span data-ttu-id="1ff6a-206">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-206">false</span></span> |
| <span data-ttu-id="1ff6a-207">Accept Wildcard Characters?</span><span class="sxs-lookup"><span data-stu-id="1ff6a-207">Accept wildcard characters?</span></span> |<span data-ttu-id="1ff6a-208">false</span><span class="sxs-lookup"><span data-stu-id="1ff6a-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="1ff6a-209">설명</span><span class="sxs-lookup"><span data-stu-id="1ff6a-209">Remarks</span></span>
<span data-ttu-id="1ff6a-210">스크립트를 사용하여 개발 및 테스트 환경을 만드는 방법에 대한 전체 설명은 [Windows PowerShell 스크립트를 사용하여 개발 및 테스트 환경에 게시](vs-azure-tools-publishing-using-powershell-scripts.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="1ff6a-211">JSON 구성 파일은 배포될 내용의 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="1ff6a-212">프로젝트를 만들 때 지정한 정보(예: 가상 컴퓨터의 이름, 선호도 그룹, VHD 이미지, 크기)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="1ff6a-213">또한 가상 컴퓨터의 끝점, 프로비전할 데이터베이스(있는 경우), 웹 배포 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="1ff6a-214">다음 코드에서는 JSON 구성 파일을 예로 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-214">The following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="1ff6a-215">프로비전한 내용을 변경하도록 JSON 구성 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="1ff6a-216">가상 컴퓨터 및 클라우드 서비스는 필요하지만 데이터베이스 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="1ff6a-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

