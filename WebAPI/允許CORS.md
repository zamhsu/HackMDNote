# 允許CORS

.Net 6

只需在Program.cs中設定即可
```csharp=
var allowSpecificOrigins = "_allowSpecificOrigins";

var builder = WebApplication.CreateBuilder(args);

// CORS
builder.Services.AddCors(opt =>
{
    // 從appsettings.json中取得允許的來源
    string[] allowOrigins =  builder.Configuration.GetValue<string>("Cors:AllowOrigins").Split(',',  StringSplitOptions.RemoveEmptyEntries);
    opt.AddPolicy(name: allowSpecificOrigins,
                  b =>
                  {
                      b.WithOrigins(allowOrigins)
                       .AllowAnyHeader()
                       .WithMethods("GET", "POST", "PUT", "DELETE", "OPTIONS");
                  });
});

// Add services to the container.

builder.Services.AddControllers()
    .ConfigureApiBehaviorOptions(opt =>
    {
        opt.SuppressModelStateInvalidFilter = true;
    });

// 略

// 有順序，要在app.UseRouting()後，app.UseAuthentication()前
// app.UseRouting()
app.UseCors(allowSpecificOrigins);
// UseAuthentication()
```

要注意在Middleware中使用UseCors時，有順序限制
https://docs.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-6.0#middleware-order

參考資料：
https://blog.johnwu.cc/article/ironman-day26-asp-net-core-cross-origin-requests.html
https://docs.microsoft.com/en-us/aspnet/core/security/cors?view=aspnetcore-6.0#cors-with-named-policy-and-middleware

###### tags: `.Net 6` `Web API`