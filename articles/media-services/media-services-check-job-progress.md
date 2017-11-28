---
title: "작업 진행률 aaaMonitor.NET을 사용 하 여"
description: "Toouse 이벤트 처리기 코드 tootrack 작업 진행률 및 상태 업데이트를 전송 방법에 대해 알아봅니다. hello 코드 예제는 C#으로 작성 하 고 hello Media Services SDK for.NET 사용."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee720ed6-8ce5-4434-b6d6-4df71fca224e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 530aa1d78437cd7c41b4d9a895f9a0e9de0ad49d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-job-progress-using-net"></a><span data-ttu-id="2ac6c-104">.NET을 사용하여 작업 진행 상태 모니터링</span><span class="sxs-lookup"><span data-stu-id="2ac6c-104">Monitor Job Progress using .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ac6c-105">포털</span><span class="sxs-lookup"><span data-stu-id="2ac6c-105">Portal</span></span>](media-services-portal-check-job-progress.md)
> * [<span data-ttu-id="2ac6c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="2ac6c-106">.NET</span></span>](media-services-check-job-progress.md)
> * [<span data-ttu-id="2ac6c-107">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="2ac6c-107">REST</span></span>](media-services-rest-check-job-progress.md)
> 
> 

<span data-ttu-id="2ac6c-108">작업을 실행 하면 일반적 방법을 tootrack 작업 진행 상황을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac6c-108">When you run jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="2ac6c-109">(이 항목에서 설명)으로 StateChanged 이벤트 처리기를 정의 하 여 hello 진행률을 확인할 수 있습니다 또는 Azure 큐 저장소 toomonitor를 사용 하 여 미디어 서비스 작업 알림 (에 설명 된 대로 [이](media-services-dotnet-check-job-progress-with-queues.md) 항목).</span><span class="sxs-lookup"><span data-stu-id="2ac6c-109">You can check hello progress by defining a StateChanged event handler (as described in this topic) or using Azure Queue storage toomonitor Media Services job notifications (as described in [this](media-services-dotnet-check-job-progress-with-queues.md) topic).</span></span>

## <a name="define-statechanged-event-handler-toomonitor-job-progress"></a><span data-ttu-id="2ac6c-110">StateChanged 이벤트 처리기 toomonitor 작업 진행 상황을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac6c-110">Define StateChanged event handler toomonitor job progress</span></span>
<span data-ttu-id="2ac6c-111">다음 코드 예제는 hello hello StateChanged 이벤트 처리기를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac6c-111">hello following code example defines hello StateChanged event handler.</span></span> <span data-ttu-id="2ac6c-112">이 이벤트 처리기는 작업 진행률을 추적 하 고 hello 상태에 따라 업데이트 된 상태를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac6c-112">This event handler tracks job progress and provides updated status, depending on hello state.</span></span> <span data-ttu-id="2ac6c-113">또한 hello 코드 hello LogJobStop 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac6c-113">hello code also defines hello LogJobStop method.</span></span> <span data-ttu-id="2ac6c-114">이 도우미 메서드는 오류 세부 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac6c-114">This helper method logs error details.</span></span>

    private static void StateChanged(object sender, JobStateChangedEventArgs e)
    {
        Console.WriteLine("Job state changed event:");
        Console.WriteLine("  Previous state: " + e.PreviousState);
        Console.WriteLine("  Current state: " + e.CurrentState);

        switch (e.CurrentState)
        {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("********************");
                Console.WriteLine("Job is finished.");
                Console.WriteLine("Please wait while local tasks or downloads complete...");
                Console.WriteLine("********************");
                Console.WriteLine();
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                LogJobStop(job.Id);
                break;
            default:
                break;
        }
    }

    private static void LogJobStop(string jobId)
    {
        StringBuilder builder = new StringBuilder();
        IJob job = GetJob(jobId);

        builder.AppendLine("\nThe job stopped due toocancellation or an error.");
        builder.AppendLine("***************************");
        builder.AppendLine("Job ID: " + job.Id);
        builder.AppendLine("Job Name: " + job.Name);
        builder.AppendLine("Job State: " + job.State.ToString());
        builder.AppendLine("Job started (server UTC time): " + job.StartTime.ToString());
        builder.AppendLine("Media Services account name: " + _accountName);
        builder.AppendLine("Media Services account location: " + _accountLocation);
        // Log job errors if they exist.  
        if (job.State == JobState.Error)
        {
            builder.Append("Error Details: \n");
            foreach (ITask task in job.Tasks)
            {
                foreach (ErrorDetail detail in task.ErrorDetails)
                {
                    builder.AppendLine("  Task Id: " + task.Id);
                    builder.AppendLine("    Error Code: " + detail.Code);
                    builder.AppendLine("    Error Message: " + detail.Message + "\n");
                }
            }
        }
        builder.AppendLine("***************************\n");
        // Write hello output tooa local file and toohello console. hello template 
        // for an error output file is:  JobStop-{JobId}.txt
        string outputFile = _outputFilesFolder + @"\JobStop-" + JobIdAsFileName(job.Id) + ".txt";
        WriteToFile(outputFile, builder.ToString());
        Console.Write(builder.ToString());
    }

    private static string JobIdAsFileName(string jobID)
    {
        return jobID.Replace(":", "_");
    }



## <a name="next-step"></a><span data-ttu-id="2ac6c-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2ac6c-115">Next step</span></span>
<span data-ttu-id="2ac6c-116">미디어 서비스 학습 경로를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="2ac6c-116">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2ac6c-117">피드백 제공</span><span class="sxs-lookup"><span data-stu-id="2ac6c-117">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

