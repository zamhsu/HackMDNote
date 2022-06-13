# JWT ClockSkew

驗證JWT過期時間時，會預設時間偏差(clock skew)為5分鐘(類似緩衝時間)。
如果要取消需要到Program裡設定

```csharp=
app.UseJwtBearerAuthentication(new JwtBearerOptions()
{
    AuthenticationScheme = "Jwt",
    AutomaticAuthenticate = true,
    AutomaticChallenge = true,
    TokenValidationParameters = new TokenValidationParameters()
    {
        ValidAudience = Configuration["Tokens:Audience"],
        ValidIssuer = Configuration["Tokens:Issuer"],
        ValidateIssuerSigningKey = true,
        IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(Configuration["Tokens:Key"])),
        ValidateLifetime = true,
        ClockSkew = TimeSpan.Zero //在此設定
    }
});
```

參考資料：
https://stackoverflow.com/questions/43045035/jwt-token-authentication-expired-tokens-still-working-net-core-web-api
https://docs.microsoft.com/zh-tw/dotnet/api/microsoft.identitymodel.tokens.tokenvalidationparameters.clockskew?view=azure-dotnet

###### tags: `.Net 6` `Web API` `JWT`