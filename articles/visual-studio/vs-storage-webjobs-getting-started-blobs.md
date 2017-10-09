---
title: "blob 저장소 및 Visual Studio 시작 aaaGet 연결 된 서비스 (WebJob 프로젝트) | Microsoft Docs"
description: "Tooget은 tooan Visual Studio를 사용 하 여 Azure 저장소 연결 서비스를 연결한 다음 웹 작업 프로젝트에 Blob 저장소를 사용 하 여 시작 하는 방법"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 29f2d5e19426d37d815cdf9a1e00abfb1e07ccf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a>Azure Blob 저장소 및 Visual Studio 연결된 서비스 시작(WebJob 프로젝트)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>개요
이 문서에서는 C# 코드 샘플 표시 하는 방법을 tootrigger Azure blob를 만들거나 업데이트할 때 사용 하는 프로세스입니다. hello 코드 예제는 hello 사용 [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) 버전 1.x 합니다. Hello Visual Studio를 사용 하 여 저장소 계정 tooa 웹 작업 프로젝트를 추가 하면 **연결 된 서비스 추가** 대화 상자에서 hello 적절 한 Azure 저장소 NuGet 패키지를 설치, hello 적절 한.NET 참조는 추가 된 toohello 프로젝트 및 hello 저장소 계정에 대 한 연결 문자열 hello App.config 파일에 업데이트 됩니다.

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a>어떻게 tootrigger blob를 만들거나 업데이트할 때 함수
이 섹션에서는 어떻게 toouse hello **BlobTrigger** 특성입니다.

 **참고:** hello WebJobs SDK 새롭거나 변경 된 blob에 대 한 로그 파일 toowatch 검색 합니다. 이 프로세스는 기본적으로 느린; 함수 수 트리거되지 몇 분까지 또는 그 이상 hello blob가 생성 한 후 합니다.  권장 되는 메서드는 hello blob를 만들고 hello를 사용 하는 경우 큐 메시지 toocreate hello 응용 프로그램에서 tooprocess blob를 즉시 필요한 경우 [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) hello 대신 특성 **BlobTrigger** hello blob을 처리 하는 hello 함수에는 특성입니다.

### <a name="single-placeholder-for-blob-name-with-extension"></a>확장명을 포함하는 Blob 이름에 대한 단일 자리 표시자
hello 다음 코드 샘플 표시 되는 텍스트 blob에에서 복사 hello *입력* 컨테이너 toohello *출력* 컨테이너:

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

hello 특성 생성자 hello 컨테이너 이름 및 hello blob 이름에 대 한 자리 표시자를 지정 하는 문자열 매개 변수를 사용 합니다. 이 예제에서는 라는 blob *Blob1.txt* hello에 만들어집니다 *입력* 컨테이너 hello 함수 만듭니다 라는 blob *Blob1.txt* hello에 *출력*  컨테이너입니다.

아래의 코드 예제는 hello와 같이 hello blob 이름 자리 표시자와 이름 패턴을 지정할 수 있습니다.

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

이 코드는 이름이 "original-"로 시작하는 Blob만 복사합니다. 예를 들어 *원래 Blob1.txt* hello에 *입력* 컨테이너 너무 복사*복사 Blob1.txt* hello에 *출력* 컨테이너입니다.

중괄호 hello 이름에 포함 된 blob 이름에 대 한 toospecify 이름 패턴을 필요한 경우 중괄호 hello를 두 번입니다. 예를 들어, toofind blob을 hello *이미지* 다음과 같은 이름을 가진 컨테이너:

        {20140101}-soundfile.mp3

패턴에 다음을 사용합니다.

        images/{{20140101}}-{name}

Hello 예에서 hello *이름* 자리 표시자 값이 없을 *soundfile.mp3*합니다.

### <a name="separate-blob-name-and-extension-placeholders"></a>Blob 이름과 확장명에 대한 별도의 자리 표시자
hello 다음 코드 샘플 변경 hello 파일 확장명 hello에 표시 되는 blob를 복사 하는 대로 *입력* 컨테이너 toohello *출력* 컨테이너입니다. hello 코드 기록 hello의 hello 확장 *입력* hello의 hello 확장명을 설정 하 고 blob *출력* 너무 blob*.txt*합니다.

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a name="types-that-you-can-bind-tooblobs"></a>Tooblobs를 바인딩할 수 형식
Hello를 사용할 수 있습니다 **BlobTrigger** 특성 유형만 hello에:

* **string**
* **TextReader**
* **Stream**
* **ICloudBlob**
* **CloudBlockBlob**
* **CloudPageBlob**
* [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)

원하는 경우 toowork hello Azure 저장소 계정 사용 하 여 직접 추가할 수도 있습니다는 **CloudStorageAccount** toohello 메서드 서명 매개 변수입니다.

## <a name="getting-text-blob-content-by-binding-toostring"></a>바인딩 toostring 여 텍스트 blob 콘텐츠 가져오기
텍스트 blob 예상 되는 경우 **BlobTrigger** 적용된 tooa 수 **문자열** 매개 변수입니다. hello 다음 코드 샘플 바인딩합니다 텍스트 blob tooa **문자열** 라는 매개 변수 **logMessage**합니다. hello 함수는 해당 매개 변수 toowrite hello 내용의 hello blob toohello WebJobs SDK 대시보드를 사용합니다.

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a>ICloudBlobStreamBinder를 사용하여 serialize된 Blob 콘텐츠 가져오기
hello 다음 코드 예제에서는 구현 하는 클래스 **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind blob toohello 특성 **WebImage** 유형입니다.

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK",
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

hello **WebImage** 바인딩 코드에서 제공 되는 **WebImageBinder** 에서 파생 된 클래스 **ICloudBlobStreamBinder**합니다.

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input,
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="how-toohandle-poison-blobs"></a>Toohandle 포이즌 blob 하는 방법
경우는 **BlobTrigger** 함수 실패 hello SDK 호출 다시 경우 일시적인 오류가 발생 한 여 hello 오류가 발생 했습니다. Hello 오류 hello blob의 hello 내용에 의해 발생 하는 경우 tooprocess hello blob를 열려고 할 때마다 hello 함수가 실패 합니다. 기본적으로 hello SDK는 지정된 된 blob에 대 한 too5 시간 함수를 호출합니다. SDK hello 라는 tooa 큐 메시지 추가 hello 다섯 번째 시도 실패 하면 *webjobs-blobtrigger-포이즌*합니다.

hello 최대 재시도 횟수는 구성할 수 있습니다. 동일한 hello [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) 설정은 포이즌 blob 처리 및 포이즌 큐의 메시지 처리에 사용 됩니다.

포이즌 blob에 대 한 hello 큐 메시지는 hello 다음과 같은 속성을 포함 하는 JSON 개체:

* FunctionId (hello 형태로 표시 *{WebJob 이름}*합니다. 함수입니다. *{함수 이름}*예를 들면: WebJob1.Functions.CopyBlob)
* BlobType("BlockBlob" 또는 "PageBlob")
* ContainerName
* BlobName
* ETag(Blob 버전 식별자, 예: "0x8D1DC6E70A277EF")

Hello 다음 코드 샘플에서는 hello **CopyBlob** 함수에 호출 될 때마다 toofail 발생 한 코드는 합니다. Hello SDK hello 최대 재시도 횟수에 대 한 호출 하 고 hello blob 포이즌 큐에 메시지를 만들 hello 해당 메시지를 처리 후 **LogPoisonBlob** 함수입니다.

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

hello SDK hello JSON 메시지를 자동으로 역직렬화합니다. 여기에 hello **PoisonBlobMessage** 클래스:

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a>Blob 폴링 알고리즘
로 지정 된 모든 컨테이너를 검색 하는 hello WebJobs SDK **BlobTrigger** 응용 프로그램 시작 시 특성입니다. 대용량 저장소 계정의 경우 이러한 검사에 약간의 시간이 걸릴 수 있으므로 새 Blob을 찾고 **BlobTrigger** 함수를 실행하기까지 조금 기다려야 할 수 있습니다.

응용 프로그램 시작 후 toodetect 새롭거나 변경 된 blob, SDK hello blob 저장소에서 주기적으로 읽어서 hello를 기록 합니다. hello 로그 blob는 버퍼링 되 고만 10 분 마다 기록 물리적으로 있거나, 하므로 지연 시간이 상당한 blob를 만들거나 hello에 해당 하기 전에 업데이트 후 **BlobTrigger** 함수를 실행 합니다.

Hello를 사용 하 여 만든 blob에 대 한 예외가 **Blob** 특성입니다. 새 blob hello 즉시 전달 hello WebJobs SDK를 새 blob을 만들면 tooany 일치 **BlobTrigger** 함수입니다. 따라서 blob 입 / 출력 체인이 있는 경우 SDK hello 수 효과적으로 처리 합니다. 그러나 다른 방법으로 만들거나 업데이트한 Blob에 대해 Blob 처리 함수를 실행할 때 대기 시간을 줄이려면 **BlobTrigger**보다 **QueueTrigger**를 사용하는 것이 좋습니다.

### <a name="blob-receipts"></a>Blob 수신 확인
WebJobs SDK hello 하면 없는 **BlobTrigger** 함수 호출 두 번 이상 hello에 대 한 동일한 새로운 또는 blob를 업데이트 합니다. 유지 관리 하 여이 작업을 수행 *수령액 blob* 순서 toodetermine 특정된 blob 버전 처리 된 경우에 합니다.

라는 컨테이너에 저장 된 blob 수령액 *azure webjobs 호스트* hello AzureWebJobsStorage 연결 문자열에서 지정한 hello Azure 저장소 계정에 있습니다. Blob 수신 확인에는 다음 정보는 hello에 있습니다.

* hello blob에 대 한 호출 된 함수 hello ("*{WebJob 이름}*합니다. 함수입니다. *{함수 이름}*", 예:"WebJob1.Functions.CopyBlob")
* hello 컨테이너 이름
* hello blob 유형 ("BlockBlob" 또는 "PageBlob")
* hello blob 이름
* hello ETag (예: blob 버전 식별자: "0x8D1DC6E70A277EF")

해당 blob에 대 한 hello blob 확인 hello에서 수동으로 삭제할 수는 blob의 tooforce 다시 처리 하려면 *azure webjobs 호스트* 컨테이너입니다.

## <a name="related-topics-covered-by-hello-queues-article"></a>Hello 큐 문서에서 다루는 관련된 항목
어떻게 toohandle blob 처리도 트리거된 큐 메시지 또는 WebJobs에 대 한 SDK 시나리오에 대 한 정보를 처리 하는 특정 tooblob 참조 [toouse Azure WebJobs SDK hello 사용 하 여 저장소를 대기 하는 방법을](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md)합니다.

Hello 다음 포함 하는 해당 문서에서 다루는 관련된 항목:

* 비동기 함수
* 여러 인스턴스
* 정상 종료
* WebJobs SDK 특성 hello 함수 본문에서 사용 하 여
* 코드에서 hello SDK 연결 문자열을 설정 합니다.
* 코드에서 WebJobs SDK 생성자 매개 변수 값 설정
* 포이즌 Blob 처리를 위한 **MaxDequeueCount** 구성
* 수동으로 함수 트리거
* 로그 작성

## <a name="next-steps"></a>다음 단계
이 문서의 Azure 사용에 대 한 일반적인 시나리오 toohandle blob 하는 방법을 보여 주는 코드 샘플을 제공 했습니다. Azure WebJobs toouse 및 hello WebJobs SDK를 참조 하는 방법에 대 한 자세한 내용은 [Azure WebJobs 설명서 리소스](http://go.microsoft.com/fwlink/?linkid=390226)합니다.

