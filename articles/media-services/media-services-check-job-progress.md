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
# <a name="monitor-job-progress-using-net"></a>.NET을 사용하여 작업 진행 상태 모니터링
> [!div class="op_single_selector"]
> * [포털](media-services-portal-check-job-progress.md)
> * [.NET](media-services-check-job-progress.md)
> * [REST (영문)](media-services-rest-check-job-progress.md)
> 
> 

작업을 실행 하면 일반적 방법을 tootrack 작업 진행 상황을 필요 합니다. (이 항목에서 설명)으로 StateChanged 이벤트 처리기를 정의 하 여 hello 진행률을 확인할 수 있습니다 또는 Azure 큐 저장소 toomonitor를 사용 하 여 미디어 서비스 작업 알림 (에 설명 된 대로 [이](media-services-dotnet-check-job-progress-with-queues.md) 항목).

## <a name="define-statechanged-event-handler-toomonitor-job-progress"></a>StateChanged 이벤트 처리기 toomonitor 작업 진행 상황을 정의 합니다.
다음 코드 예제는 hello hello StateChanged 이벤트 처리기를 정의 합니다. 이 이벤트 처리기는 작업 진행률을 추적 하 고 hello 상태에 따라 업데이트 된 상태를 제공 합니다. 또한 hello 코드 hello LogJobStop 메서드를 정의합니다. 이 도우미 메서드는 오류 세부 정보를 기록합니다.

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



## <a name="next-step"></a>다음 단계
미디어 서비스 학습 경로를 검토합니다.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

