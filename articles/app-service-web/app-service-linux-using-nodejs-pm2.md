---
title: "Linux의 Azure Web App에서 Node.js용 PM2 구성 사용 | Microsoft Docs"
description: "Linux의 Azure Web App에서 Node.js용 PM2 구성 사용"
keywords: "azure app service, 웹앱, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 5002400a673e2c5cc4290bab488b839fb2282966
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a><span data-ttu-id="18d14-104">Linux의 Azure Web App에서 Node.js용 PM2 구성 사용</span><span class="sxs-lookup"><span data-stu-id="18d14-104">Use PM2 configuration for Node.js in Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


<span data-ttu-id="18d14-105">Linux의 Azure Web App용 Node.js에 대해 응용 프로그램 스택을 설정한 경우 다음 이미지와 같이 Node.js 시작 파일을 설정하는 옵션이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-105">If you set the application stack to Node.js for Azure Web App on Linux, you get the option to set a Node.js startup file as shown in the following image:</span></span>

![Node.js 시작 파일 설정][1]

<span data-ttu-id="18d14-107">이 옵션을 사용하여 다음 작업 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-107">You can use this option to do one of the following tasks:</span></span>

* <span data-ttu-id="18d14-108">Node.js 앱용 시작 스크립트 지정(예: /bin/server.js)</span><span class="sxs-lookup"><span data-stu-id="18d14-108">Specify the startup script for your Node.js app (for example: /bin/server.js).</span></span>
* <span data-ttu-id="18d14-109">Node.js 앱에 사용할 PM2 구성 파일 지정(예: /foo/process.json)</span><span class="sxs-lookup"><span data-stu-id="18d14-109">Specify the PM2 configuration file to use for your Node.js app (for example: /foo/process.json).</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="18d14-110">특정 파일이 수정될 때 Node.js 프로세스를 자동으로 다시 시작하려면 PM2 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-110">If you want your Node.js processes to restart automatically when certain files are modified, use the PM2 configuration.</span></span> <span data-ttu-id="18d14-111">그러지 않으면 응용 프로그램은 변경 알림의 받을 때(예: 응용 프로그램 코드가 변경될 때) 다시 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-111">Otherwise, your application won't restart when it receives change notifications (for example, when your application code changes).</span></span>
  > 
  > 

<span data-ttu-id="18d14-112">전체 옵션은 [프로세스 파일 설명서](http://pm2.keymetrics.io/docs/usage/application-declaration/)에서 확인할 수 있으며, 다음에 나오는 내용은 process.json 파일로 사용할 수 있는 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-112">You can check the Node.js [process file documentation](http://pm2.keymetrics.io/docs/usage/application-declaration/) for all the options, but following is a sample of what you can use as your process.json file:</span></span>

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

<span data-ttu-id="18d14-113">이 구성에서 유의할 사항:</span><span class="sxs-lookup"><span data-stu-id="18d14-113">Important things to note in this configuration are:</span></span>

* <span data-ttu-id="18d14-114">"Script" 속성은 응용 프로그램의 시작 스크립트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-114">The "script" property specifies your application's start script.</span></span>
* <span data-ttu-id="18d14-115">"instances" 속성은 시작할 노드 프로세스의 인스턴스 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-115">The "instances" property specifies how many instances of the node process to launch.</span></span> <span data-ttu-id="18d14-116">여러 코어가 있는 더 큰 VM에서 응용 프로그램을 실행하는 경우 여기에서 더 높은 값을 설정하여 리소스를 최대화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-116">If you are running your application on larger VMs that have multiple cores, it's a good idea to maximize your resources by setting a higher value here.</span></span>
* <span data-ttu-id="18d14-117">"watch" 배열은 변경 시 노드 프로세스를 다시 시작하려는 모든 파일을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-117">The "watch" array specifies all files that you want to restart the node process for when they change.</span></span>
* <span data-ttu-id="18d14-118">"watch_options"의 경우 응용 프로그램 콘텐츠가 탑재되는 방식 때문에 "usePolling"을 true로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="18d14-118">For the "watch_options", you currently need to specify "usePolling" as true because of the way your application content is mounted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18d14-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="18d14-119">Next steps</span></span>
* [<span data-ttu-id="18d14-120">Linux에서 Azure Web App이란?</span><span class="sxs-lookup"><span data-stu-id="18d14-120">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="18d14-121">Linux의 Azure App Service Web App에 대한 FAQ</span><span class="sxs-lookup"><span data-stu-id="18d14-121">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
