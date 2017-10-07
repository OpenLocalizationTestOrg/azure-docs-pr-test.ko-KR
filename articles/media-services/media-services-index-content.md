---
title: "Azure Media Indexer를 사용 하 여 미디어 파일 aaaIndexing"
description: "Azure Media Indexer 하면 toomake 콘텐츠 검색 가능한 미디어 파일 및 전체 텍스트 대 본 toogenerate 닫힌 캡션 및 키워드에 대 한 있습니다. 이 항목에서는 방법을 toouse Media Indexer 합니다."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Azure 미디어 인덱서를 사용하여 미디어 파일 인덱싱
Azure Media Indexer 하면 toomake 콘텐츠 검색 가능한 미디어 파일 및 전체 텍스트 대 본 toogenerate 닫힌 캡션 및 키워드에 대 한 있습니다. 하나의 미디어 파일 또는 일괄 처리에서 여러 미디어 파일을 처리할 수 있습니다.  

> [!IMPORTANT]
> 콘텐츠를 인덱싱할 때는 (배경 음악, 노이즈, 효과 또는 마이크 소음이 없어야 함) 없이 음성이 명확한 미디어 파일 toouse 있는지 확인 합니다. 적절한 콘텐츠의 예: 회의, 강의 또는 프레젠테이션 녹음. hello 다음 콘텐츠 맞지 않을 인덱싱: 영화, TV 쇼 혼합된 오디오와 소리 효과가 있는 어느 것에 저하 배경 노이즈 (소음)로 콘텐츠를 기록 합니다.
> 
> 

한 인덱싱 작업 hello 다음 출력을 생성할 수 있습니다.

* 선택 캡션 파일 형식에 따라 hello에: **SAMI**, **TTML**, 및 **WebVTT**합니다.
  
    닫힌된 캡션 파일 hello 원본 비디오에서 hello 음성 인식 가능한 정도에 따라 한 인덱싱 작업 하는 점수는 Recognizability 라는 태그가 포함 됩니다.  성이 Recognizability tooscreen 출력 파일의 hello 값을 사용할 수 있습니다. 낮은 점수는 tooaudio 품질 인해 인덱싱 결과가 나쁜를 의미 합니다.
* 키워드 파일(XML).
* SQL server에서 사용할 AIB(오디오 인덱싱 Blob) 파일.
  
    자세한 내용은 [Azure 미디어 인덱서 및 SQL Server에서 AIB 파일 사용](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)(영문)을 참조하세요.

이 항목에서는 방법을 너무 작업 toocreate 인덱싱**자산 인덱싱** 및 **파일을 여러 인덱싱할**합니다.

최신 Azure Media Indexer 업데이트 hello에 대 한 참조 [미디어 서비스 블로그](#preset)합니다.

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>인덱싱 태스크에 대한 구성 및 매니페스트 파일 사용
태스크 구성을 사용하여 인덱싱 태스크에 대한 세부 사항을 지정할 수 있습니다. 예를 들어 미디어 파일에는 메타 데이터 toouse를 지정할 수 있습니다. 이 메타 데이터는 hello 언어 엔진 tooexpand 해당 어휘를 사용 하 고 크게 hello 음성 인식 정확도 향상 시켜 줍니다.  사용자는 또한 수 toospecify 원하는 출력 파일입니다.

매니페스트 파일을 사용하여 여러 미디어 파일을 한 번에 처리할 수도 있습니다.

자세한 내용은 [Azure 미디어 인덱서의 작업 기본 설정](https://msdn.microsoft.com/library/dn783454.aspx)(영문)을 참조하세요.

## <a name="index-an-asset"></a>자산 인덱스
hello 다음 미디어 파일을 자산으로 업로드 메서드와 작업 tooindex hello 자산을 만듭니다.

참고가 지정 된 구성 파일이 없는 경우 hello 미디어 파일이 모든 기본 설정으로 보관 됩니다.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>출력 파일
기본적으로 한 인덱싱 작업 출력 파일을 다음 hello를 생성 합니다. hello 파일 hello 첫 번째 출력 자산에 저장 됩니다.

둘 이상의 입력된 미디어 파일이 있는 경우 인덱서 hello 작업 출력에 'JobResult.txt' 라는 매니페스트 파일을 생성 됩니다. 각 입력된 미디어 파일에 대 한 hello 결과 AIB, SAMI, TTML, WebVTT, 및 키워드 파일은 순차적으로 번호가 지정 및 명명 된 "별칭" hello를 사용 하 여 합니다.

| 파일 이름 | 설명 |
| --- | --- |
| **InputFileName.aib** |Audio indexing blob file. <br/><br/> AIB(Audio Indexing Blob) 파일은 전체 텍스트 검색을 사용하는 Microsoft SQL에서 검색할 수 있는 이진 파일입니다.  hello AIB 파일은 훨씬 더 풍부한 검색 환경을 수 있도록 각 단어에 대 한 대체 단어를 포함 하기 때문에 hello 간단한 캡션 파일 보다 더 강력 합니다. <br/> <br/>Hello 컴퓨터 실행 중인 Microsoft SQL server 2008 이상에서 hello Indexer SQL 추가 기능 설치를 해야합니다. Server 전체 텍스트 검색 hello Microsoft SQL을 사용 하 여 AIB를 검색 하면 WAMI에서 생성 된 캡션 파일을 닫을 hello 검색 보다 더 정확한 검색 결과 제공 합니다. Hello AIB에는 hello 오디오의 각 세그먼트에 대 한 hello 가장 높은 신뢰도 단어를 포함 하는 hello 선택 캡션 파일 반면 비슷한 들리는 대체 단어가 포함 되어 때문입니다. 이면 검색 단어에 대 한 가장 중요 것이 좋습니다 toouse hello AIB에 Microsoft SQL Server와 함께 합니다.<br/><br/> toodownload hello 추가 기능을 클릭 <a href="http://aka.ms/indexersql">Azure Media Indexer SQL 추가 기능</a>합니다. <br/><br/>것 가능한 tooutilize 다른 검색 엔진 같은 되어 Apache Lucene/Solr toosimply 인덱스 hello 비디오 hello 닫힌 캡션 및 키워드 XML 파일 기반 이지만이 덜 정확한 검색 결과에서 발생 됩니다. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |SAMI, TTML 및 WebVTT 형식의 CC(선택 자막) 파일.<br/><br/>사용 되는 toomake 오디오 될 수 있습니다 및 비디오 파일 청각 장애가 있는 액세스 가능한 toopeople 합니다.<br/><br/>닫힌된 캡션 파일 라는 태그가 포함 <b>Recognizability</b> 는 hello 원본 비디오에서 hello 음성 인식 가능한 정도에 인덱싱 작업의 점수입니다.  hello 값을 사용할 수 <b>Recognizability</b> tooscreen 유용한 파일을 출력 합니다. 낮은 점수는 tooaudio 품질 인해 인덱싱 결과가 나쁜를 의미 합니다. |
| **InputFileName.kw.xml<br/>InputFileName.info** |키워드 및 정보 파일입니다. <br/><br/>키워드 파일은 빈도 및 오프셋된 정보와 함께 hello 음성 콘텐츠에서 추출 된 키워드가 포함 된 XML 파일입니다. <br/><br/>정보 파일은 인식된 각 용어에 대한 세부적인 정보를 포함한 일반 텍스트 파일입니다. hello 첫 번째 줄은 특수 하며 hello Recognizability 점수를 포함 합니다. 각 후속 줄은 탭으로 구분 된 목록이 같은 데이터가 hello: 시간, 종료 시간, 단어/구, 신뢰도 시작 합니다. hello 시간이 초 단위로 지정 됩니다. 그 hello 신뢰도 숫자 0-1에서입니다. <br/><br/>예제 줄: "1.20    1.45    word    0.67" <br/><br/>노출 된 toosearch 보다 적절 한 광고 Bing, Google 또는 Microsoft SharePoint toomake hello 미디어 파일 검색 가능성을 높이기 등도 사용 되는 toodeliver 엔진 또는 목적으로 tooperform 음성 분석을 같은 다양 한 이러한 파일을 사용할 수 있습니다. |
| **JobResult.txt** |출력 매니페스트를 hello 다음 정보를 포함 하는 여러 파일 인덱싱 하는 경우에 존재 합니다.<br/><br/><table border="1"><tr><th>InputFile</th><th>Alias</th><th>MediaLength</th><th>오류</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

그렇지 않은 경우 일부 입력된 미디어 파일이 성공적으로 인덱싱되지 않은, 오류 코드 4000 hello 인덱싱 작업이 실패 합니다. 자세한 내용은 [오류 코드](#error_codes)를 참조하세요.

## <a name="index-multiple-files"></a>여러 파일을 인덱싱
메서드를 다음 hello를 자산으로 여러 미디어 파일을 업로드 하 고 일괄 처리에서 작업 tooindex 이러한 모든 파일을 만듭니다.

Hello.lst 확장명의 매니페스트 파일이 생성 되어 hello 자산으로 업로드 합니다. hello 매니페스트 파일에는 hello 모든 hello 자산 파일 목록이 포함 되어 있습니다. 자세한 내용은 [Azure 미디어 인덱서의 작업 기본 설정](https://msdn.microsoft.com/library/dn783454.aspx)(영문)을 참조하세요.

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>부분적으로 성공된 작업
그렇지 않은 경우 일부 입력된 미디어 파일이 성공적으로 인덱싱되지 않은, 오류 코드 4000 hello 인덱싱 작업이 실패 합니다. 자세한 내용은 [오류 코드](#error_codes)를 참조하세요.

hello (성공한 작업과)과 동일한 출력을 생성 합니다. Toohello 출력 매니페스트 파일 toofind는 입력된 파일은 실패, toohello 오류 열 값에 따라 참조할 수 있습니다. 실패 한 입력된 파일에 대 한 결과 AIB, SAMI, TTML, WebVTT hello 및 키워드 파일이 생성 되지 않습니다.

### <a id="preset"></a> Azure 미디어 인덱서의 태스크 미리 설정
Azure Media Indexer에서 처리 하는 hello 함께 hello 작업 사전 설정 하는 선택적 작업을 제공 하 여 사용자 지정할 수 있습니다.  hello 다음이 구성 xml의 hello 형식에 설명 합니다.

| 이름 | 필요 | 설명 |
| --- | --- | --- |
| **input** |false |자산 파일 tooindex 되도록 합니다.</p><p>Azure Media Indexer 원하는 미디어 파일 확장명 따르는 hello: MP4, WMV, MP3, M4A, WMA, AAC, WAV 합니다.</p><p>Hello에 hello 파일 이름 (s)을 지정할 수 있습니다 **이름** 또는 **목록** hello 특성 **입력** 요소 중 (아래 참조). 자산 파일 tooindex를 지정 하지 않으면 hello 기본 파일이 선택 됩니다. 기본 자산 파일이 없습니다. 설정 된 경우 hello hello 입력된 자산의 첫 번째 파일이 인덱싱됩니다.</p><p>tooexplicitly는 hello 자산 파일 이름 지정을 수행 합니다.<br/>`<input name="TestFile.wmv">`<br/><br/>여러 자산 파일을 한 번에 (too10 파일을)를 인덱싱할 수 있습니다. toodo이:<br/><br/><ol class="ordered"><li><p>텍스트 파일(매니페스트 파일)을 만들고 .lst 확장명을 지정합니다. </p></li><li><p>모든 hello 자산 파일 이름 목록이 입력된 자산 toothis 매니페스트 파일에 추가 합니다. </p></li><li><p>매니페스트 파일 toohello 자산 (업로드) 추가 합니다.  </p></li><li><p>Hello 입력의 목록 특성 hello 매니페스트 파일의 hello 이름을 지정 합니다.<br/>`<input list="input.lst">`</li></ol><br/><br/>참고: 10 개 이상의 파일 toohello 매니페스트 파일을 추가 하는 경우 인덱싱 작업 hello hello 2006 오류 코드로 실패 합니다. |
| **metadata** |false |Hello에 대 한 메타 데이터는 어휘 조정에 사용 되는 자산 파일을 지정 합니다.  유용한 tooprepare 인덱서 toorecognize 비표준 어휘 등의 단어 명사.<br/>`<metadata key="..." value="..."/>` <br/><br/>미리 정의된 **키**에 대해 **값**을 제공할 수 있습니다. 현재 키 뒤 hello 지원 됩니다.<br/><br/>"제목" 및 "description"-어휘 적응 tootweak hello 언어에 사용 되는 작업에 대 한 모델 및 음성 인식 정확도 향상 합니다.  hello 값 초기값으로 사용할 인터넷 검색 toofind와 관련 텍스트 문서를 인덱싱 작업의 hello 기간에 대 한 hello 내용을 tooaugment hello 내부 사전을 사용 합니다.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **features** <br/><br/> 버전 1.2에 추가되었습니다. 현재 hello만 지원 기능은 음성 인식 ("ASR")입니다. |false |hello 음성 인식 기능에는 다음 설정 키 hello에 있습니다.<table><tr><th><p>키</p></th>        <th><p>설명</p></th><th><p>예제 값</p></th></tr><tr><td><p>언어</p></td><td><p>hello 자연어 toobe hello 멀티미디어 파일에서 인식 합니다.</p></td><td><p>English, Spanish</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>hello 원하는 출력 캡션 형식 (있는 경우)의 세미콜론으로 구분 된 목록</p></td><td><p>ttml;sami;webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>AIB 파일이 필요한 (SQL Server 및 hello 고객 Indexer IFilter 함께 사용) 인지 여부를 지정 하는 부울 플래그입니다.  자세한 내용은 <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">Azure 미디어 인덱서 및 SQL Server에서 AIB 파일 사용</a>(영문)을 참조하세요.</p></td><td><p>True; False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>키워드 XML 파일이 필요한지 여부를 지정하는 부울 플래그입니다.</p></td><td><p>True; False. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>(신뢰도 수준)에 관계 없이 전체 tooforce 캡션이 여부를 지정 하는 부울 플래그입니다.  </p><p>단어와 구에 50% 신뢰도 수준 보다 작음을 포함 하는 hello 최종 캡션 출력에서 생략 및 대신 줄임표가 표시 ("…")는 경우 기본값은 false입니다.  hello 줄임표 캡션 품질 관리 및 감사 하는 데 유용합니다.</p></td><td><p>True; False. </p></td></tr></table> |

### <a id="error_codes"></a>오류 코드
Azure Media Indexer를 보고 하는 오류의 경우 hello hello 오류 코드를 다음 중 하나를 백업 합니다.

| 코드 | 이름 | 가능한 이유 |
| --- | --- | --- |
| 2000 |유효하지 않은 구성 |유효하지 않은 구성 |
| 2001 |유효하지 않은 입력 자산 |입력 자산 유실 또는 빈 자산. |
| 2002 |유효하지 않은 매니페스트 |매니페스트가 비어 있거나 유효하지 않은 항목을 포함합니다. |
| 2003 |실패 한 toodownload 미디어 파일 |매니페스트 파일에 유효하지 않은 URL. |
| 2004 |지원되지 않는 프로토콜 |미디어 URL 프로토콜이 지원되지 않습니다. |
| 2005 |지원되지 않는 파일 유형 |입력 미디어 파일 유형이 지원되지 않습니다. |
| 2006 |너무 많은 입력 파일 |Hello 입력 매니페스트에 10 개 이상의 파일이 있습니다. |
| 3000 |실패 한 toodecode 미디어 파일 |지원되지 않는 미디어 코덱 <br/>또는<br/> 손상된 미디어 파일 <br/>또는<br/> 입력 미디어에 오디오 스트림 없음. |
| 4000 |인덱싱 일괄 처리 부분적으로 성공 |일부 hello 입력된 미디어 파일이 인덱싱되지 toobe 실패 했습니다. 자세한 내용은 <a href="#output_files">출력 파일</a>을 참조하세요. |
| 기타 |내부 오류 |지원 팀에 문의하시기 바랍니다. indexer@microsoft.com |

## <a id="supported_languages"></a>지원되는 언어
현재 hello 영어와 스페인어 언어 지원 됩니다. 자세한 내용은 참조 [v1.2 릴리스 블로그 게시물 hello](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/)합니다.

## <a name="media-services-learning-paths"></a>미디어 서비스 학습 경로
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>관련 링크
[Azure 미디어 서비스 분석 개요](media-services-analytics-overview.md)

[Azure 미디어 인덱서 및 SQL Server에서 AIB 파일 사용(영문)](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Azure 미디어 인덱서 2 미리 보기를 사용하여 미디어 파일 인덱싱](media-services-process-content-with-indexer2.md)

