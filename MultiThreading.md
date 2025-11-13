  using System;
using System.Collections.Concurrent;
using System.Collections.Generic;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    // HttpClient is thread-safe, reuse for all requests
    private static readonly HttpClient httpClient = new HttpClient();

    static async Task Main()
    {
        var urls = new List<string>
        {
            "https://example.com/",
            "https://api.github.com/",
            "https://httpstat.us/500",
            "https://httpstat.us/404",
            "https://nonexistentdomain12345.com"
        };

        httpClient.DefaultRequestHeaders.UserAgent.ParseAdd("Mozilla/5.0");

        Console.WriteLine("\n=== Parallel.ForEachAsync (Optimized with ConcurrentBag) ===");
        await RunUsingParallelForEachAsync(urls);
    }

    // ✅ Using Parallel.ForEachAsync with ConcurrentBag (Thread-safe, no locks)
    private static async Task RunUsingParallelForEachAsync(List<string> urls)
    {
        var results = new ConcurrentBag<UrlResult>();

        await Parallel.ForEachAsync(urls, new ParallelOptions { MaxDegreeOfParallelism = 5 }, async (url, ct) =>
        {
            var result = await FetchUrlAsync(url);
            results.Add(result);
        });

        Console.WriteLine("\n=== Results ===");
        foreach (var res in results)
        {
            Console.WriteLine($"{res.Url,-40} => {res.Status,-8} | {res.Message}");
        }
    }

    // Common reusable fetch method
    private static async Task<UrlResult> FetchUrlAsync(string url)
    {
        try
        {
            var response = await httpClient.GetAsync(url);

            if (response.IsSuccessStatusCode)
            {
                var content = await response.Content.ReadAsStringAsync();
                return new UrlResult
                {
                    Url = url,
                    Status = "Success",
                    Message = $"Length={content.Length}"
                };
            }
            else
            {
                return new UrlResult
                {
                    Url = url,
                    Status = "Failed",
                    Message = $"HTTP {(int)response.StatusCode}"
                };
            }
        }
        catch (Exception ex)
        {
            return new UrlResult
            {
                Url = url,
                Status = "Error",
                Message = ex.Message.Split('\n')[0]
            };
        }
    }
}

// Thread-safe result container
public class UrlResult
{
    public string Url { get; set; }
    public string Status { get; set; }
    public string Message { get; set; }
}
      await RunUsingTaskFactory(urls);

        Console.WriteLine("\n=== Method 3: Parallel.ForEachAsync ===");
        await RunUsingParallelForEachAsync(urls);
    }

    // -------------------------------------------
    // 1️⃣ Modern Async with Task.WhenAll
    // -------------------------------------------
    private static async Task RunAsyncTaskWhenAll(List<string> urls)
    {
        var tasks = new List<Task<UrlResult>>();

        foreach (var url in urls)
            tasks.Add(FetchUrlAsync(url));

        var results = await Task.WhenAll(tasks);

        foreach (var res in results)
            Console.WriteLine($"{res.Url,-40} => {res.Status,-8} | {res.Message}");
    }

    // -------------------------------------------
    // 2️⃣ Using TaskFactory (Legacy Control)
    // -------------------------------------------
    private static async Task RunUsingTaskFactory(List<string> urls)
    {
        var factory = new TaskFactory(TaskCreationOptions.LongRunning, TaskContinuationOptions.None);
        var tasks = new List<Task<UrlResult>>();

        foreach (var url in urls)
        {
            var task = factory.StartNew(async () => await FetchUrlAsync(url))
                              .Unwrap(); // Important to unwrap nested Task<Task>
            tasks.Add(task);
        }

        var results = await Task.WhenAll(tasks);

        foreach (var res in results)
            Console.WriteLine($"{res.Url,-40} => {res.Status,-8} | {res.Message}");
    }

    // -------------------------------------------
    // 3️⃣ Using Parallel.ForEachAsync (.NET 6+)
    // -------------------------------------------
    private static async Task RunUsingParallelForEachAsync(List<string> urls)
    {
        var results = new List<UrlResult>();
        var lockObj = new object();

        await Parallel.ForEachAsync(urls, new ParallelOptions { MaxDegreeOfParallelism = 5 }, async (url, ct) =>
        {
            var result = await FetchUrlAsync(url);
            lock (lockObj)
            {
                results.Add(result);
            }
        });

        foreach (var res in results)
            Console.WriteLine($"{res.Url,-40} => {res.Status,-8} | {res.Message}");
    }

    // -------------------------------------------
    // Common Fetch Method
    // -------------------------------------------
    private static async Task<UrlResult> FetchUrlAsync(string url)
    {
        try
        {
            var response = await httpClient.GetAsync(url);

            if (response.IsSuccessStatusCode)
            {
                var content = await response.Content.ReadAsStringAsync();
                return new UrlResult
                {
                    Url = url,
                    Status = "Success",
                    Message = $"Length={content.Length}"
                };
            }
            else
            {
                return new UrlResult
                {
                    Url = url,
                    Status = "Failed",
                    Message = $"HTTP {(int)response.StatusCode}"
                };
            }
        }
        catch (Exception ex)
        {
            return new UrlResult
            {
                Url = url,
                Status = "Error",
                Message = ex.Message.Split('\n')[0]
            };
        }
    }
}

public class UrlResult
{
    public string Url { get; set; }
    public string Status { get; set; }
    public string Message { get; set; }
}
