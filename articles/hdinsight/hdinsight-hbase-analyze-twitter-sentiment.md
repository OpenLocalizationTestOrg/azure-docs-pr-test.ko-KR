---
title: "HBase-Azure와 실시간 Twitter 감성 aaaAnalyze | Microsoft Docs"
description: "자세한 방법 (Hadoop) HDInsight 클러스터의 HBase를 사용 하 여 Twitter에서 빅 데이터의 toodo 실시간 감성 분석 합니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5c798ad3-a20d-4385-a463-f4f7705f9566
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jgao
ms.openlocfilehash: 87e5c0c0a90d222a3f0bc3c3f3fce1e938320480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-real-time-twitter-sentiment-with-hbase-in-hdinsight"></a>HDInsight에서 HBase를 사용하여 Twitter 데이터 실시간 분석
자세한 방법을 toodo 실시간 [감성 분석](http://en.wikipedia.org/wiki/Sentiment_analysis) HDInsight에서 HBase 클러스터를 사용 하 여 Twitter에서 큰 데이터입니다.

소셜 웹 사이트는 빅 데이터 채택에 대 한 주요 추진 배경과 hello 중 하나입니다. Twitter와 같은 사이트에서 제공하는 공개 API는 대중적인 추세를 분석하고 이해하는 데 유용한 데이터 원본입니다. 이 자습서에서는 서비스 응용 프로그램 및 ASP.NET 웹 응용 프로그램 tooperform hello 다음 스트리밍 콘솔을 개발할 수 있습니다.

![HDInsight HBase에서 Twitter 데이터 분석][img-app-arch]

* 응용 프로그램 스트리밍을 hello

  * 스트리밍 API를 실시간으로 hello Twitter를 사용 하 여 트 윗 지역 태그가 지정 된 가져오기
  * 이러한 트 윗의 hello 정서를 평가 합니다.
  * 사용 하 여 HBase에서 정보 hello Microsoft HBase SDK hello 정서를 저장 합니다.
* hello Azure 웹 사이트 응용 프로그램

  * ASP.NET 웹 응용 프로그램을 사용 하 여 Bing 지도에서 hello 실시간 통계 결과 그립니다. Hello 트 윗의 시각화는 비슷한 toohello 다음 스크린 샷:

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]

    모르는와 특정 키워드 tooget 수 tooquery 트 윗의 의미 hello 트 윗에 표현 된 hello 견해는 양수, 음수 또는 중립 하는 경우.

전체 Visual Studio 솔루션 샘플은 GitHub [실시간 소셜 데이터 분석 앱](https://github.com/maxluk/tweet-sentiment)에서 확인할 수 있습니다.

### <a name="prerequisites"></a>필수 조건
이 자습서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **HDInsight의 HBase 클러스터**. 클러스터 만들기에 대한 지침은 [HDInsight에서 Hadoop을 통해 HBase 사용 시작][hbase-get-started]을 참조하세요. 

* Visual Studio 2013/2015/2017이 설치된 **워크스테이션**입니다. 관련 지침은 [Visual Studio 설치](http://msdn.microsoft.com/library/e2h7fzkw.aspx)를 참조하세요.

## <a name="create-a-twitter-application-id-and-secrets"></a>Twitter 응용 프로그램 ID 및 암호 만들기
Twitter 스트리밍 Api 사용 하 여 hello [OAuth](http://oauth.net/) tooauthorize 요청 합니다. hello 첫 번째 단계 toouse OAuth toocreate hello Twitter 개발자 사이트에서 새 응용 프로그램입니다.

**toocreate Twitter 응용 프로그램 ID 및 암호**

1. 역시 로그인[Twitter 앱](https://apps.twitter.com/)합니다. Hello 클릭 **지금 등록** Twitter 계정이 없는 경우 연결 합니다.
2. **Create New App**을 클릭합니다.
3. **Name**, **Description** 및 **Website**를 입력합니다. hello Twitter 응용 프로그램 이름에는 고유한 이름 이어야 합니다. hello 웹 사이트 필드를 실제로 사용 되지 않습니다. 올바른 URL toobe 되어 있지 않습니다.
4. **Yes, I agree**를 선택한 후 **Create your Twitter application**을 클릭합니다.
5. Hello 클릭 **권한을** 탭을 클릭 한 다음 **읽기 전용**합니다. hello 읽기 전용 권한이이 자습서에 충분 합니다.
6. Hello 클릭 **키와 액세스 토큰이** 탭 합니다.
7. 클릭 **내 액세스 토큰 만들기** hello hello 페이지 아래쪽에 있습니다.
9. 복사 hello **소비자 키 (API 키)**, **소비자 암호 (API Secret)**, **액세스 토큰**, 및 **액세스 토큰 암호** 값입니다. Hello 자습서의 뒷부분에서 이러한 값이 있어야합니다.

    > ! [참고] hello 테스트 OAuth 단추 더 이상 작동 하지 않습니다.

## <a name="create-twitter-streaming-service"></a>Twitter 스트리밍 서비스 만들기
응용 프로그램 tooget 트 윗 toocreate 필요 윗 감성 점수를 계산 하 고 처리 하는 hello 윗 단어 tooHBase 보냅니다.

**응용 프로그램 스트리밍을 toocreate hello**

1. **Visual Studio**를 열고 **TweetSentimentStreaming**이라는 Visual C# 콘솔 응용 프로그램을 만듭니다.
2. **패키지 관리자 콘솔**실행 hello 다음 명령을:

        Install-Package Microsoft.HBase.Client -version 0.4.2.0
        Install-Package TweetinviAPI -version 1.0.0.0

    이 명령은 설치 hello [HBase.NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) hello 클라이언트 라이브러리 tooaccess hello HBase 클러스터 및 hello 패키지 [Tweetinvi API](https://www.nuget.org/packages/TweetinviAPI/) Twitter API hello 사용 되는 tooaccess 변수인, 패키지 합니다.

   > [!NOTE]
   > 이 문서에서 사용 하는 hello 예제는 위에 명시 된 hello 버전을 사용 하 여 테스트 되었습니다.  제거할 수 있습니다 hello-버전 스위치 tooinstall hello 최신 버전입니다.
   >
   >
3. **솔루션 탐색기**, 추가 **System.Configuration** toohello 참조 합니다.
4. 라는 새 클래스 파일 toohello 프로젝트를 추가 **HBaseWriter.cs**, 다음 hello 코드 hello 다음으로 바꿉니다.

        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Text;
        using System.Threading;
        using Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling;
        using org.apache.hadoop.hbase.rest.protobuf.generated;
        using Microsoft.HBase.Client;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class HBaseWriter
            {
                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "https://<Enter Your Cluster Name>.azurehdinsight.net/";
                const string HADOOPUSERNAME = "admin"; //hello default name is "admin"
                const string HADOOPUSERPASSWORD = "<Enter hello Hadoop User Password>";

                const string HBASETABLENAME = "tweets_by_words";
                const string COUNT_ROW_KEY = "~ROWCOUNT";
                const string COUNT_COLUMN_NAME = "d:COUNT";

                long rowCount = 0;

                // Sentiment dictionary file and hello punctuation characters
                const string DICTIONARYFILENAME = @"..\..\dictionary.tsv";
                private static char[] _punctuationChars = new[] {
            ' ', '!', '\"', '#', '$', '%', '&', '\'', '(', ')', '*', '+', ',', '-', '.', '/',   //ascii 23--47
            ':', ';', '<', '=', '>', '?', '@', '[', ']', '^', '_', '`', '{', '|', '}', '~' };   //ascii 58--64 + misc.

                // For writting tooHBase
                HBaseClient client;

                // a sentiment dictionary for estimate sentiment. It is loaded from a physical file.
                Dictionary<string, DictionaryItem> dictionary;

                // use multithread write
                Thread writerThread;
                Queue<ITweet> queue = new Queue<ITweet>();
                bool threadRunning = true;

                // This function connects tooHBase, loads hello sentiment dictionary, and starts hello thread for writting.
                public HBaseWriter()
                {
                    ClusterCredentials credentials = new ClusterCredentials(new Uri(CLUSTERNAME), HADOOPUSERNAME, HADOOPUSERPASSWORD);
                    client = new HBaseClient(credentials);

                    // create hello HBase table if it doesn't exist
                    if (!client.ListTablesAsync().Result.name.Contains(HBASETABLENAME))
                    {
                        TableSchema tableSchema = new TableSchema();
                        tableSchema.name = HBASETABLENAME;
                        tableSchema.columns.Add(new ColumnSchema { name = "d" });
                        client.CreateTableAsync(tableSchema).Wait();
                        Console.WriteLine("Table \"{0}\" is created.", HBASETABLENAME);
                    }

                    // Read current row count cell
                    rowCount = GetRowCount();

                    // Load sentiment dictionary from a file
                    LoadDictionary();

                    // Start a thread for writting tooHBase
                    writerThread = new Thread(new ThreadStart(WriterThreadFunction));
                    writerThread.Start();
                }

                ~HBaseWriter()
                {
                    threadRunning = false;
                }

                private long GetRowCount()
                {
                    try
                    {
                        RequestOptions options = RequestOptions.GetDefaultOptions();
                        options.RetryPolicy = RetryPolicy.NoRetry;
                        var cellSet = client.GetCellsAsync(HBASETABLENAME, COUNT_ROW_KEY, null, null, options).Result;
                        if (cellSet.rows.Count != 0)
                        {
                            var countCol = cellSet.rows[0].values.Find(cell => Encoding.UTF8.GetString(cell.column) == COUNT_COLUMN_NAME);
                            if (countCol != null)
                            {
                                return Convert.ToInt64(Encoding.UTF8.GetString(countCol.data));
                            }
                        }
                    }
                    catch(Exception ex)
                    {
                        if (ex.InnerException.Message.Equals("hello remote server returned an error: (404) Not Found.", StringComparison.OrdinalIgnoreCase))
                        {
                            return 0;
                        }
                        else
                        {
                            throw ex;
                        }

                    }

                    return 0;
                }

                // Enqueue hello Tweets received
                public void WriteTweet(ITweet tweet)
                {
                    lock (queue)
                    {
                        queue.Enqueue(tweet);
                    }
                }

                // Load sentiment dictionary from a file
                private void LoadDictionary()
                {
                    List<string> lines = File.ReadAllLines(DICTIONARYFILENAME).ToList();
                    var items = lines.Select(line =>
                    {
                        var fields = line.Split('\t');
                        var pos = 0;
                        return new DictionaryItem
                        {
                            Type = fields[pos++],
                            Length = Convert.ToInt32(fields[pos++]),
                            Word = fields[pos++],
                            Pos = fields[pos++],
                            Stemmed = fields[pos++],
                            Polarity = fields[pos++]
                        };
                    });

                    dictionary = new Dictionary<string, DictionaryItem>();
                    foreach (var item in items)
                    {
                        if (!dictionary.Keys.Contains(item.Word))
                        {
                            dictionary.Add(item.Word, item);
                        }
                    }
                }

                // Calculate sentiment score
                private int CalcSentimentScore(string[] words)
                {
                    Int32 total = 0;
                    foreach (string word in words)
                    {
                        if (dictionary.Keys.Contains(word))
                        {
                            switch (dictionary[word].Polarity)
                            {
                                case "negative": total -= 1; break;
                                case "positive": total += 1; break;
                            }
                        }
                    }
                    if (total > 0)
                    {
                        return 1;
                    }
                    else if (total < 0)
                    {
                        return -1;
                    }
                    else
                    {
                        return 0;
                    }
                }

                // Popular a CellSet object toobe written into HBase
                private void CreateTweetByWordsCells(CellSet set, ITweet tweet)
                {
                    // Split hello Tweet into words
                    string[] words = tweet.Text.ToLower().Split(_punctuationChars);

                    // Calculate sentiment score base on hello words
                    int sentimentScore = CalcSentimentScore(words);
                    var word_pairs = words.Take(words.Length - 1)
                                        .Select((word, idx) => string.Format("{0} {1}", word, words[idx + 1]));
                    var all_words = words.Concat(word_pairs).ToList();

                    // For each word in hello Tweet add a row toohello HBase table
                    foreach (string word in all_words)
                    {
                        string time_index = (ulong.MaxValue - (ulong)tweet.CreatedAt.ToBinary()).ToString().PadLeft(20) + tweet.IdStr;
                        string key = word + "_" + time_index;

                        // Create a row
                        var row = new CellSet.Row { key = Encoding.UTF8.GetBytes(key) };

                        // Add columns toohello row, including Tweet identifier, language, coordinator(if available), and sentiment
                        var value = new Cell { column = Encoding.UTF8.GetBytes("d:id_str"), data = Encoding.UTF8.GetBytes(tweet.IdStr) };
                        row.values.Add(value);

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:lang"), data = Encoding.UTF8.GetBytes(tweet.Language.ToString()) };
                        row.values.Add(value);

                        if (tweet.Coordinates != null)
                        {
                            var str = tweet.Coordinates.Longitude.ToString() + "," + tweet.Coordinates.Latitude.ToString();
                            value = new Cell { column = Encoding.UTF8.GetBytes("d:coor"), data = Encoding.UTF8.GetBytes(str) };
                            row.values.Add(value);
                        }

                        value = new Cell { column = Encoding.UTF8.GetBytes("d:sentiment"), data = Encoding.UTF8.GetBytes(sentimentScore.ToString()) };
                        row.values.Add(value);

                        set.rows.Add(row);
                    }
                }

                // Write a Tweet (CellSet) tooHBase
                public void WriterThreadFunction()
                {
                    try
                    {
                        while (threadRunning)
                        {
                            if (queue.Count > 0)
                            {
                                CellSet set = new CellSet();
                                lock (queue)
                                {
                                    do
                                    {
                                        ITweet tweet = queue.Dequeue();
                                        CreateTweetByWordsCells(set, tweet);
                                    } while (queue.Count > 0);
                                }

                                // Write hello Tweet by words cell set toohello HBase table
                                client.StoreCellsAsync(HBASETABLENAME, set).Wait();
                                Console.WriteLine("\tRows written: {0}", set.rows.Count);
                            }
                            Thread.Sleep(100);
                        }
                    }
                    catch (Exception ex)
                    {
                        Console.WriteLine("Exception: " + ex.Message);
                    }
                }
            }
            public class DictionaryItem
            {
                public string Type { get; set; }
                public int Length { get; set; }
                public string Word { get; set; }
                public string Pos { get; set; }
                public string Stemmed { get; set; }
                public string Polarity { get; set; }
            }
        }
5. 집합 hello 상수 hello 이전 코드에서 포함 하 여 **CLUSTERNAME**, **HADOOPUSERNAME**, **HADOOPUSERPASSWORD**, 및 DICTIONARYFILENAME 합니다. hello DICTIONARYFILENAME hello 파일 이름 및 hello direction.tsv의 hello 위치는입니다.  hello 파일에서 다운로드할 수 있습니다 **https://hditutorialdata.blob.core.windows.net/twittersentiment/dictionary.tsv**합니다. Toochange hello HBase 테이블 이름을 지정할 경우 그에 따라 hello 웹 응용 프로그램에서 hello 테이블 이름을 변경 해야 합니다.
6. 열기 **Program.cs**, hello 코드 hello 다음과 같이 바꿉니다.

        using System;
        using System.Diagnostics;
        using Tweetinvi;
        using Tweetinvi.Models;

        namespace TweetSentimentStreaming
        {
            class Program
            {
                const string TWITTERAPPACCESSTOKEN = "<Enter Twitter App Access Token>";
                const string TWITTERAPPACCESSTOKENSECRET = "<Enter Twitter Access Token Secret>";
                const string TWITTERAPPAPIKEY = "<Enter Twitter App API Key>";
                const string TWITTERAPPAPISECRET = "<Enter Twitter App API Secret>";

                static void Main(string[] args)
                {
                    Auth.SetUserCredentials(TWITTERAPPAPIKEY, TWITTERAPPAPISECRET, TWITTERAPPACCESSTOKEN, TWITTERAPPACCESSTOKENSECRET);

                    Stream_FilteredStreamExample();
                }

                private static void Stream_FilteredStreamExample()
                {
                    for (;;)
                    {
                        try
                        {
                            HBaseWriter hbase = new HBaseWriter();
                            var stream = Stream.CreateFilteredStream();
                            stream.AddLocation(new Coordinates(90, -180), new Coordinates(-90,180));

                            var tweetCount = 0;
                            var timer = Stopwatch.StartNew();

                            stream.MatchingTweetReceived += (sender, args) =>
                            {
                                tweetCount++;
                                var tweet = args.Tweet;

                                // Write Tweets tooHBase
                                hbase.WriteTweet(tweet);

                                if (timer.ElapsedMilliseconds > 1000)
                                {
                                    if (tweet.Coordinates != null)
                                    {
                                        Console.ForegroundColor = ConsoleColor.Green;
                                        Console.WriteLine("\n{0}: {1} {2}", tweet.Id, tweet.Language.ToString(), tweet.Text);
                                        Console.ForegroundColor = ConsoleColor.White;
                                        Console.WriteLine("\tLocation: {0}, {1}", tweet.Coordinates.Longitude, tweet.Coordinates.Latitude);
                                    }

                                    timer.Restart();
                                    Console.WriteLine("\tTweets/sec: {0}", tweetCount);
                                    tweetCount = 0;
                                }
                            };

                            stream.StartStreamMatchingAllConditions();
                        }
                        catch (Exception ex)
                        {
                            Console.WriteLine("Exception: {0}", ex.Message);
                        }
                    }
                }

            }
        }
7. Hello 상수를 포함 하 여 설정 **TWITTERAPPACCESSTOKEN**, **TWITTERAPPACCESSTOKENSECRET**, **TWITTERAPPAPIKEY** 및 **TWITTERAPPAPISECRET**.

서비스 키를 눌러 스트리밍을 toorun hello **F5**합니다. hello 다음은 hello 콘솔 응용 프로그램의 스크린샷입니다.

![hdinsight.hbase.twitter.sentiment.streaming.service][img-streaming-service]

더 많은 데이터 toouse 갖도록 hello 웹 응용 프로그램을 개발 하는 동안 실행 되는 콘솔 응용 프로그램 스트리밍을 hello를 유지 합니다. hello 테이블에 삽입 tooexamine hello 데이터 HBase 셸을 사용할 수 있습니다. [HDInsight에서 HBase 시작](hdinsight-hbase-tutorial-get-started-linux.md#create-tables-and-insert-data)을 참조하세요.

## <a name="visualize-real-time-sentiment"></a>실시간 데이터 시각화
이 섹션에서는 Bing 지도에서 HBase 및 도면을 hello 데이터에서는 ASP.NET MVC 웹 응용 프로그램 tooread hello 실시간/도별로 인지 데이터를 만듭니다.

**toocreate ASP.NET MVC 웹 응용 프로그램**

1. Visual Studio를 엽니다.
2. **파일**, **새로 만들기**를 클릭한 후 **프로젝트**를 클릭합니다.
3. Hello 다음 정보를 입력 합니다.

   * 템플릿 범주: **Visual C#/웹**
   * 템플릿: **ASP.NET 웹 응용 프로그램**
   * 이름: **TweetSentimentWeb**
   * 위치: **C:\Tutorials**
4. **확인**을 클릭합니다.
5. **템플릿 선택**에서 **MVC**를 클릭합니다.
6. **Microsoft Azure**에서 **구독 관리**를 클릭합니다.
7. **Microsoft Azure 구독 관리**에서 **로그인**을 클릭합니다.
8. Azure 자격 증명을 입력합니다. Hello에 Azure 구독 정보를 표시 하는 **계정** 탭 합니다.
9. 클릭 **닫기** tooclose hello **Microsoft Azure 구독 관리** 창.
10. **새 ASP.NET 프로젝트 - TweetSentimentWeb**에서 **확인**을 클릭합니다.
11. **Microsoft Azure 사이트 설정 구성**선택, hello **지역** 가장 가까운 tooyou 즉 합니다. 데이터베이스 서버 toospecify가 필요는 없습니다.
12. **확인**을 클릭합니다.

**tooinstall NuGet 패키지**

1. Hello에서 **도구** 메뉴를 클릭 하 여 **Nuget 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다. hello 콘솔 패널 hello hello 페이지 맨 아래에 열립니다.
2. 사용 하 여 hello 다음 명령은 tooinstall hello [HBase.NET SDK](https://www.nuget.org/packages/Microsoft.HBase.Client/) hello 클라이언트 라이브러리 tooaccess HBase 클러스터입니다.

        Install-Package Microsoft.HBase.Client

**tooadd HBaseReader 클래스**

1. **솔루션 탐색기**에서 **TweetSentiment**를 확장합니다.
2. **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 차례로 클릭합니다.
3. Hello에 **이름** 필드를 입력 **HBaseReader.cs**, 클릭 하 고 **추가**합니다.
4. Hello 다음과 같이 hello 코드를 바꿉니다.

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Web;

        using System.Configuration;
        using System.Threading.Tasks;
        using System.Text;
        using Microsoft.HBase.Client;
        using org.apache.hadoop.hbase.rest.protobuf.generated;

        namespace TweetSentimentWeb.Models
        {
            public class HBaseReader
            {
                // For reading Tweet sentiment data from HDInsight HBase
                HBaseClient client;

                // HDinsight HBase cluster and HBase table information
                const string CLUSTERNAME = "<HBaseClusterName>";
                const string HADOOPUSERNAME = "<HBaseClusterHadoopUserName>"
                const string HADOOPUSERPASSWORD = "<HBaseCluserUserPassword>";
                const string HBASETABLENAME = "tweets_by_words";

                // hello constructor
                public HBaseReader()
                {
                    ClusterCredentials creds = new ClusterCredentials(
                                    new Uri(CLUSTERNAME),
                                    HADOOPUSERNAME,
                                    HADOOPUSERPASSWORD);
                    client = new HBaseClient(creds);
                }

                // Query Tweets sentiment data from hello HBase table asynchronously
                public async Task<IEnumerable<Tweet>> QueryTweetsByKeywordAsync(string keyword)
                {
                    List<Tweet> list = new List<Tweet>();

                    // Demonstrate Filtering hello data from hello past 6 hours hello row key
                    string timeIndex = (ulong.MaxValue -
                        (ulong)DateTime.UtcNow.Subtract(new TimeSpan(6, 0, 0)).ToBinary()).ToString().PadLeft(20);
                    string startRow = keyword + "_" + timeIndex;
                    string endRow = keyword + "|";
                    Scanner scanSettings = new Scanner
                    {
                        batch = 100000,
                        startRow = Encoding.UTF8.GetBytes(startRow),
                        endRow = Encoding.UTF8.GetBytes(endRow)
                    };

                    // Make async scan call
                    ScannerInformation scannerInfo =
                        await client.CreateScannerAsync(HBASETABLENAME, scanSettings);

                    CellSet next;

                    while ((next = await client.ScannerGetNextAsync(scannerInfo)) != null)
                    {
                        foreach (CellSet.Row row in next.rows)
                        {
                            // find hello cell with string pattern "d:coor"
                            var coordinates =
                                row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:coor");

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');

                                var sentimentField =
                                    row.values.Find(c => Encoding.UTF8.GetString(c.column) == "d:sentiment");
                                Int32 sentiment = 0;
                                if (sentimentField != null)
                                {
                                    sentiment = Convert.ToInt32(Encoding.UTF8.GetString(sentimentField.data));
                                }

                                list.Add(new Tweet
                                {
                                    Longtitude = Convert.ToDouble(lonlat[0]),
                                    Latitude = Convert.ToDouble(lonlat[1]),
                                    Sentiment = sentiment
                                });
                            }

                            if (coordinates != null)
                            {
                                string[] lonlat = Encoding.UTF8.GetString(coordinates.data).Split(',');
                            }
                        }
                    }

                    return list;
                }
            }

            public class Tweet
            {
                public string IdStr { get; set; }
                public string Text { get; set; }
                public string Lang { get; set; }
                public double Longtitude { get; set; }
                public double Latitude { get; set; }
                public int Sentiment { get; set; }
            }
        }
5. 내부 hello **HBaseReader** 클래스 hello 상수 값을 다음과 같이 변경 합니다.

   * **CLUSTERNAME**: hello HBase 클러스터 이름, 예를 들어 *https://<HBaseClusterName>.azurehdinsight.net/*합니다.
   * **HADOOPUSERNAME**: hello HBase 클러스터 Hadoop 사용자 사용자 이름입니다. 기본 이름은 hello *admin*합니다.
   * **HADOOPUSERPASSWORD**: hello HBase 클러스터 Hadoop 사용자 암호입니다.
   * **HBASETABLENAME** = "tweets_by_words";

     hello HBase 테이블 이름이 **"tweets_by_words";**합니다. hello 값에는 hello 웹 응용 프로그램에서 hello hello 데이터를 읽을 수 있도록 hello 스트리밍 서비스를 전송 하는 hello 값과 일치 해야 동일한 HBase 테이블입니다.

**tooadd TweetsController 컨트롤러**

1. **솔루션 탐색기**에서 **TweetSentimentWeb**을 확장합니다.
2. **컨트롤러**를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 후 **컨트롤러**를 클릭합니다.
3. **웹 API 2 컨트롤러 - 비어 있음**을 클릭한 다음 **추가**를 클릭합니다.
4. Hello에 **컨트롤러 이름** 필드를 입력 **TweetsController**, 클릭 하 고 **추가**합니다.
5. **솔루션 탐색기**, TweetsController.cs tooopen hello 파일을 두 번 클릭 합니다.
6. Hello 다음과 같이 되도록 hello 파일을 수정 합니다.

        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Http;

        using System.Threading.Tasks;
        using TweetSentimentWeb.Models;

        namespace TweetSentimentWeb.Controllers
        {
            public class TweetsController : ApiController
            {
                HBaseReader hbase = new HBaseReader();

                public async Task<IEnumerable<Tweet>> GetTweetsByQuery(string query)
                {
                    return await hbase.QueryTweetsByKeywordAsync(query);
                }
            }
        }

**tooadd heatmap.js**

1. **솔루션 탐색기**에서 **TweetSentimentWeb**을 확장합니다.
2. **스크립트**를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **JavaScript 파일**을 클릭합니다.
3. Hello에 **항목 이름** 필드를 입력 **heatmap.js**합니다.
4. Hello를 hello 파일에 코드를 다음에 붙여 넣습니다. hello 코드 Alastair Aitchison 썼습니다. 자세한 내용은 [Bing Maps AJAX v7 HeatMap 라이브러리](http://alastaira.wordpress.com/2011/04/15/bing-maps-ajax-v7-heatmap-library/)를 참조하세요.

        /*******************************************************************************
        * Author: Alastair Aitchison
        * Website: http://alastaira.wordpress.com
        * Date: 15th April 2011
        *
        * Description:
        * This JavaScript file provides an algorithm that can be used tooadd a heatmap
        * overlay on a Bing Maps v7 control. hello intensity and temperature palette
        * of hello heatmap are designed toobe easily customisable.
        *
        * Requirements:
        * hello heatmap layer itself is created dynamically on hello client-side using
        * hello HTML5 &lt;canvas> element, and therefore requires a browser that supports
        * this element. It has been tested on IE9, Firefox 3.6/4 and
        * Chrome 10 browsers. If you can confirm whether it works on other browsers or
        * not, I'd love toohear from you!
        *
        * Usage:
        * hello HeatMapLayer constructor requires:
        * - A reference tooa map object
        * - An array or Microsoft.Maps.Location items
        * - Optional parameters toocustomise hello appearance of hello layer
        *  (Radius,, Unit, Intensity, and ColourGradient), and a callback function
        */

        var HeatMapLayer = function (map, locations, options) {

            /* Private Properties */
            var _map = map,
                _canvas,
                _temperaturemap,
                _locations = [],
                _viewchangestarthandler,
                _viewchangeendhandler;

            // Set default options
            var _options = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 1000,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'meters',

                // Colour temperature gradient of hello map
                colourgradient: {
                    "0.00": 'rgba(255,0,255,20)',  // Magenta
                    "0.25": 'rgba(0,0,255,40)',    // Blue
                    "0.50": 'rgba(0,255,0,80)',    // Green
                    "0.75": 'rgba(255,255,0,120)', // Yellow
                    "1.00": 'rgba(255,0,0,150)'    // Red
                },

                // Callback function toobe fired after heatmap layer has been redrawn
                callback: null
            };

            /* Private Methods */
            function _init() {
                var _mapDiv = _map.getRootElement();

                if (_mapDiv.childNodes.length >= 3 && _mapDiv.childNodes[2].childNodes.length >= 2) {
                    // Create hello canvas element
                    _canvas = document.createElement('canvas');
                    _canvas.style.position = 'relative';

                    var container = document.createElement('div');
                    container.style.position = 'absolute';
                    container.style.left = '0px';
                    container.style.top = '0px';
                    container.appendChild(_canvas);

                    _mapDiv.childNodes[2].childNodes[1].appendChild(container);

                    // Override defaults with any options passed in hello constructor
                    _setOptions(options);

                    // Load array of location data
                    _setPoints(locations);

                    // Create a colour gradient from hello suppied colourstops
                    _temperaturemap = _createColourGradient(_options.colourgradient);

                    // Wire up hello event handler tooredraw heatmap canvas
                    _viewchangestarthandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangestart', _clearHeatMap);
                    _viewchangeendhandler = Microsoft.Maps.Events.addHandler(_map, 'viewchangeend', _createHeatMap);

                    _createHeatMap();

                    delete _init;
                } else {
                    setTimeout(_init, 100);
                }
            }

            // Resets hello heat map
            function _clearHeatMap() {
                var ctx = _canvas.getContext("2d");
                ctx.clearRect(0, 0, _canvas.width, _canvas.height);
            }

            // Creates a colour gradient from supplied colour stops on initialisation
            function _createColourGradient(colourstops) {
                var ctx = document.createElement('canvas').getContext('2d');
                var grd = ctx.createLinearGradient(0, 0, 256, 0);
                for (var c in colourstops) {
                    grd.addColorStop(c, colourstops[c]);
                }
                ctx.fillStyle = grd;
                ctx.fillRect(0, 0, 256, 1);
                return ctx.getImageData(0, 0, 256, 1).data;
            }

            // Applies a colour gradient toohello intensity map
            function _colouriseHeatMap() {
                var ctx = _canvas.getContext("2d");
                var dat = ctx.getImageData(0, 0, _canvas.width, _canvas.height);
                var pix = dat.data; // pix is a CanvasPixelArray containing height x width x 4 bytes of data (RGBA)
                for (var p = 0, len = pix.length; p < len;) {
                    var a = pix[p + 3] * 4; // get hello alpha of this pixel
                    if (a != 0) { // If there is any data tooplot
                        pix[p] = _temperaturemap[a]; // set hello red value of hello gradient that corresponds toothis alpha
                        pix[p + 1] = _temperaturemap[a + 1]; //set hello green value based on alpha
                        pix[p + 2] = _temperaturemap[a + 2]; //set hello blue value based on alpha
                    }
                    p += 4; // Move on toohello next pixel
                }
                ctx.putImageData(dat, 0, 0);
            }

            // Sets any options passed in
            function _setOptions(options) {
                for (attrname in options) {
                    _options[attrname] = options[attrname];
                }
            }

            // Sets hello heatmap points from an array of Microsoft.Maps.Locations  
            function _setPoints(locations) {
                _locations = locations;
            }

            // Main method toodraw hello heatmap
            function _createHeatMap() {
                // Ensure hello canvas matches hello current dimensions of hello map
                // This also has hello effect of resetting hello canvas
                _canvas.height = _map.getHeight();
                _canvas.width = _map.getWidth();

                _canvas.style.top = -_canvas.height / 2 + 'px';
                _canvas.style.left = -_canvas.width / 2 + 'px';

                // Calculate hello pixel radius of each heatpoint at hello current map zoom
                if (_options.unit == "pixels") {
                    radiusInPixel = _options.radius;
                } else {
                    radiusInPixel = _options.radius / _map.getMetersPerPixel();
                }

                var ctx = _canvas.getContext("2d");

                // Convert lat/long toopixel location
                var pixlocs = _map.tryLocationToPixel(_locations, Microsoft.Maps.PixelReference.control);
                var shadow = 'rgba(0, 0, 0, ' + _options.intensity + ')';
                var mapWidth = 256 * Math.pow(2, _map.getZoom());

                // Create hello Intensity Map by looping through each location
                for (var i = 0, len = pixlocs.length; i < len; i++) {
                    var x = pixlocs[i].x;
                    var y = pixlocs[i].y;

                    if (x < 0) {
                        x += mapWidth * Math.ceil(Math.abs(x / mapWidth));
                    }

                    // Create radial gradient centred on this point
                    var grd = ctx.createRadialGradient(x, y, 0, x, y, radiusInPixel);
                    grd.addColorStop(0.0, shadow);
                    grd.addColorStop(1.0, 'transparent');

                    // Draw hello heatpoint onto hello canvas
                    ctx.fillStyle = grd;
                    ctx.fillRect(x - radiusInPixel, y - radiusInPixel, 2 * radiusInPixel, 2 * radiusInPixel);
                }

                // Apply hello specified colour gradient toohello intensity map
                _colouriseHeatMap();

                // Call hello callback function, if specified
                if (_options.callback) {
                    _options.callback();
                }
            }

            /* Public Methods */

            this.Show = function () {
                if (_canvas) {
                    _canvas.style.display = '';
                }
            };

            this.Hide = function () {
                if (_canvas) {
                    _canvas.style.display = 'none';
                }
            };

            // Sets options for intensity, radius, colourgradient etc.
            this.SetOptions = function (options) {
                _setOptions(options);
            }

            // Sets an array of Microsoft.Maps.Locations from which hello heatmap is created
            this.SetPoints = function (locations) {
                // Reset hello existing heatmap layer
                _clearHeatMap();
                // Pass in hello new set of locations
                _setPoints(locations);
                // Recreate hello layer
                _createHeatMap();
            }

            // Removes hello heatmap layer from hello DOM
            this.Remove = function () {
                _canvas.parentNode.parentNode.removeChild(_canvas.parentNode);

                if (_viewchangestarthandler) { Microsoft.Maps.Events.removeHandler(_viewchangestarthandler); }
                if (_viewchangeendhandler) { Microsoft.Maps.Events.removeHandler(_viewchangeendhandler); }

                _locations = null;
                _temperaturemap = null;
                _canvas = null;
                _options = null;
                _viewchangestarthandler = null;
                _viewchangeendhandler = null;
            }

            // Call hello initialisation routine
            _init();
        };

        // Call hello Module Loaded method
        Microsoft.Maps.moduleLoaded('HeatMapModule');

**tooadd twitterStream.js**

1. **솔루션 탐색기**에서 **TweetSentimentWeb**을 확장합니다.
2. **스크립트**를 마우스 오른쪽 단추로 클릭하고 **추가**를 클릭한 다음 **JavaScript 파일**을 클릭합니다.
3. Hello에 **항목 이름** 필드를 입력**twitterStream.js**합니다.
4. 복사한 hello 파일에 코드를 다음 hello를 붙여넣습니다.

        var liveTweetsPos = [];
        var liveTweets = [];
        var liveTweetsNeg = [];
        var map;
        var heatmap;
        var heatmapNeg;
        var heatmapPos;

        function initialize() {
            // Initialize hello map
            var options = {
                credentials: "AvFJTZPZv8l3gF8VC3Y7BPBd0r7LKo8dqKG02EAlqg9WAi0M7la6zSIT-HwkMQbx",
                center: new Microsoft.Maps.Location(23.0, 8.0),
                mapTypeId: Microsoft.Maps.MapTypeId.ordnanceSurvey,
                labelOverlay: Microsoft.Maps.LabelOverlay.hidden,
                zoom: 2.5
            };
            var map = new Microsoft.Maps.Map(document.getElementById('map_canvas'), options);

            // Heatmap options for positive, neutral and negative layers

            var heatmapOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels'
            };

            var heatmapPosOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 255, 191, 1)',
                    0.3: 'rgba(0, 255, 127, 1)',
                    0.4: 'rgba(0, 255, 63, 1)',
                    0.5: 'rgba(0, 127, 0, 1)',
                    0.7: 'rgba(0, 159, 0, 1)',
                    0.8: 'rgba(0, 191, 0, 1)',
                    0.9: 'rgba(0, 223, 0, 1)',
                    1.0: 'rgba(0, 255, 0, 1)'
                }
            };

            var heatmapNegOptions = {
                // Opacity at hello centre of each heat point
                intensity: 0.5,

                // Affected radius of each heat point
                radius: 15,

                // Whether hello radius is an absolute pixel value or meters
                unit: 'pixels',

                colourgradient: {
                    0.0: 'rgba(0, 255, 255, 0)',
                    0.1: 'rgba(0, 255, 255, 1)',
                    0.2: 'rgba(0, 191, 255, 1)',
                    0.3: 'rgba(0, 127, 255, 1)',
                    0.4: 'rgba(0, 63, 255, 1)',
                    0.5: 'rgba(0, 0, 127, 1)',
                    0.7: 'rgba(0, 0, 159, 1)',
                    0.8: 'rgba(0, 0, 191, 1)',
                    0.9: 'rgba(0, 0, 223, 1)',
                    1.0: 'rgba(0, 0, 255, 1)'
                }
            };

            // Register and load hello Client Side HeatMap Module
            Microsoft.Maps.registerModule("HeatMapModule", "scripts/heatmap.js");
            Microsoft.Maps.loadModule("HeatMapModule", {
                callback: function () {
                    // Create heatmap layers for positive, neutral and negative tweets
                    heatmapPos = new HeatMapLayer(map, liveTweetsPos, heatmapPosOptions);
                    heatmap = new HeatMapLayer(map, liveTweets, heatmapOptions);
                    heatmapNeg = new HeatMapLayer(map, liveTweetsNeg, heatmapNegOptions);
                }
            });

            $("#searchbox").val("xbox");
            $("#searchBtn").click(onsearch);
            $("#positiveBtn").click(onPositiveBtn);
            $("#negativeBtn").click(onNegativeBtn);
            $("#neutralBtn").click(onNeutralBtn);
            $("#neutralBtn").button("toggle");
        }

        function onsearch() {
            var uri = 'api/tweets?query=';
            var query = $('#searchbox').val();
            $.getJSON(uri + query)
                .done(function (data) {
                    liveTweetsPos = [];
                    liveTweets = [];
                    liveTweetsNeg = [];

                    // On success, 'data' contains a list of tweets.
                    $.each(data, function (key, item) {
                        addTweet(item);
                    });

                    if (!$("#neutralBtn").hasClass('active')) {
                        $("#neutralBtn").button("toggle");
                    }
                    onNeutralBtn();
                })
                .fail(function (jqXHR, textStatus, err) {
                    $('#statustext').text('Error: ' + err);
                });
        }

        function addTweet(item) {
            //Add tweet toohello heat map arrays.
            var tweetLocation = new Microsoft.Maps.Location(item.Latitude, item.Longtitude);
            if (item.Sentiment > 0) {
                liveTweetsPos.push(tweetLocation);
            } else if (item.Sentiment < 0) {
                liveTweetsNeg.push(tweetLocation);
            } else {
                liveTweets.push(tweetLocation);
            }
        }

        function onPositiveBtn() {
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmapPos.SetPoints(liveTweetsPos);
            heatmapPos.Show();
            heatmapNeg.Hide();
            heatmap.Hide();

            $('#statustext').text('Tweets: ' + liveTweetsPos.length + "   " + getPosNegRatio());
        }

        function onNeutralBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#negativeBtn").hasClass('active')) {
                $("#negativeBtn").button("toggle");
            }

            heatmap.SetPoints(liveTweets);
            heatmap.Show();
            heatmapNeg.Hide();
            heatmapPos.Hide();

            $('#statustext').text('Tweets: ' + liveTweets.length + "   " + getPosNegRatio());
        }

        function onNegativeBtn() {
            if ($("#positiveBtn").hasClass('active')) {
                $("#positiveBtn").button("toggle");
            }
            if ($("#neutralBtn").hasClass('active')) {
                $("#neutralBtn").button("toggle");
            }

            heatmapNeg.SetPoints(liveTweetsNeg);
            heatmapNeg.Show();
            heatmap.Hide();;
            heatmapPos.Hide();;

            $('#statustext').text('Tweets: ' + liveTweetsNeg.length + "\t" + getPosNegRatio());
        }

        function getPosNegRatio() {
            if (liveTweetsNeg.length == 0) {
                return "";
            }
            else {
                var ratio = liveTweetsPos.length / liveTweetsNeg.length;
                var str = parseFloat(Math.round(ratio * 10) / 10).toFixed(1);
                return "Positive/Negative Ratio: " + str;
            }
        }

**toomodify hello layout.cshtml**

1. **솔루션 탐색기**에서 **TweetSentimentWeb**, **뷰**, **공유**를 차례로 확장하고 _**Layout.cshtml**을 두 번 클릭합니다.
2. Hello 콘텐츠를 hello 다음 코드로 바꿉니다.

        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>@ViewBag.Title</title>
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
            <!-- Bing Maps -->
            <script type="text/javascript" src="http://ecn.dev.virtualearth.net/mapcontrol/mapcontrol.ashx?v=7.0&mkt=en-gb"></script>
            <!-- Spatial Dashboard JavaScript -->
            <script src="~/Scripts/twitterStream.js" type="text/javascript"></script>
        </head>
        <body onload="initialize()">
            <div class="navbar navbar-inverse navbar-fixed-top">
                <div class="container">
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                    </div>
                    <div class="navbar-collapse collapse">
                        <div class="row">
                            <ul class="nav navbar-nav col-lg-5">
                                <li class="col-lg-12">
                                    <div class="navbar-form">
                                        <input id="searchbox" type="search" class="form-control">
                                        <button type="button" id="searchBtn" class="btn btn-primary">Go</button>
                                    </div>
                                </li>
                            </ul>
                            <ul class="nav navbar-nav col-lg-7">
                                <li>
                                    <div class="navbar-form">
                                        <div class="btn-group" data-toggle="buttons-radio">
                                            <button type="button" id="positiveBtn" class="btn btn-primary">Positive</button>
                                            <button type="button" id="neutralBtn" class="btn btn-primary">Neutral</button>
                                            <button type="button" id="negativeBtn" class="btn btn-primary">Negative</button>
                                        </div>
                                    </div>
                                </li>
                                <li><span id="statustext" class="navbar-text"></span></li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
            <div class="map_container">
                @RenderBody()
            </div>
            @Scripts.Render("~/bundles/jquery")
            @Scripts.Render("~/bundles/bootstrap")
            @RenderSection("scripts", required: false)
        </body>
        </html>

**toomodify hello Index.cshtml**

1. **솔루션 탐색기**에서 **TweetSentimentWeb**, **뷰**, **홈**을 차례로 확장하고 _**Index.cshtml**을 두 번 클릭합니다.
2. Hello 콘텐츠를 hello 다음 코드로 바꿉니다.

        @{
            ViewBag.Title = "Tweet Sentiment";
        }

        <div class="map_container">
            <div id="map_canvas"/>
        </div>

**toomodify hello site.css 파일**

1. **솔루션 탐색기**에서 **TweetSentimentWeb**, **콘텐츠**를 차례로 확장하고 _**Site.css**를 두 번 클릭합니다.
2. 다음 코드 toohello 파일 hello를 추가 합니다.

        /* make container, and thus map, 100% width */
        .map_container {
            width: 100%;
            height: 100%;
        }

        #map_canvas{
          height:100%;
        }

        #tweets{
          position: absolute;
          top: 60px;
          left: 75px;
          z-index:1000;
          font-size: 30px;
        }

**toomodify hello global.asax 파일**

1. **Solution Explorer**에서 **TweetSentimentWeb**을 확장하고 **Global.asax**를 두 번 클릭합니다.
2. Hello 다음 추가 **를 사용 하 여** 문:

        using System.Web.Http;
3. Hello hello 안에 줄을 다음 추가 **application_start ()** 함수:

        // Register API routes
        GlobalConfiguration.Configure(WebApiConfig.Register);

    Hello API 경로 toomake hello Web API 컨트롤러 작업의 hello MVC 응용 프로그램 내 hello 등록을 수정 합니다.

**toorun hello 웹 응용 프로그램**

1. 서비스 콘솔 응용 프로그램 스트리밍 해당 hello 여전히 실행 되 고 hello 실시간 변경 사항은 볼 수 있도록 확인 합니다.
2. 키를 눌러 **F5** toorun hello 웹 응용 프로그램:

    ![hdinsight.hbase.twitter.sentiment.bing.map][img-bing-map]
3. Hello 텍스트 상자에 키워드를 입력 한 다음 클릭 **이동**합니다.  Hello HBase 테이블에 수집 하는 hello 데이터에 따라 일부 키워드를 찾을 수 있습니다. "love," "xbox," "playstation" 등의 일반적인 키워드를 사용해 보세요.
4. 간에 전환 **양의**, **중립**, 및 **음수** toocompare 감성 hello 주제에 합니다.
5. Hello 추가 1 시간 동안 실행 하는 스트리밍 서비스를 사용 하 고 검색 동일한 키워드 hello hello 결과 비교 합니다.

필요에 따라 hello 응용 프로그램 tooAzure 웹 사이트를 배포할 수 있습니다. 관련 지침은 [Azure Websites 및 ASP.NET 시작][website-get-started]을 참조하세요.

## <a name="next-steps"></a>다음 단계
이 자습서에서는 tooget 트 윗 방식을 알아보았습니다, 그리고 트 윗 hello 감성 데이터 tooHBase 및 있는 hello 실시간 Twitter 감성 데이터 tooBing 맵 저장의 hello 감성 분석 합니다. toolearn 더 참조 하십시오.

* [HDInsight 시작][hdinsight-get-started]
* [HDInsight에서 HBase 복제 구성](hdinsight-hbase-replication.md)
* [HDInsight에서 Hadoop으로 Twitter 데이터 분석][hdinsight-analyze-twitter-data]
* [HDInsight를 사용하여 비행 지연 데이터 분석][hdinsight-analyze-flight-delay-data]
* [HDInsight용 Java MapReduce 프로그램 개발][hdinsight-develop-mapreduce]

[hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[website-get-started]: ../app-service-web/app-service-web-get-started-dotnet.md



[img-app-arch]: ./media/hdinsight-hbase-analyze-twitter-sentiment/AppArchitecture.png
[img-twitter-app]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterApp.png
[img-streaming-service]: ./media/hdinsight-hbase-analyze-twitter-sentiment/StreamingService.png
[img-bing-map]: ./media/hdinsight-hbase-analyze-twitter-sentiment/TwitterSentimentBingMap.png



[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-analyze-twitter-data]: hdinsight-analyze-twitter-data.md




[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
