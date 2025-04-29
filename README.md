# 35174

Reproduction for [Renovate issue 35174](https://github.com/renovatebot/renovate/discussions/35174).

## Current behavior

Renovate updates the version of `OpenTelemetry.Instrumentation.Http` even if it is pinned down to `[1.9.0]` in the ItemGroup for net8.0.

``` xml
<Project Sdk="Microsoft.NET.Sdk">
    <PropertyGroup>
        <TargetFrameworks>net8.0;net9.0</TargetFrameworks>
    </PropertyGroup>
    <ItemGroup  Condition="'$(TargetFramework)' == 'net9.0'" >
        <PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.11.0" />
    </ItemGroup>
    <ItemGroup  Condition="'$(TargetFramework)' == 'net8.0'" >
        <PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="[1.9.0]" />
    </ItemGroup>
</Project>

```
PullRequest: https://github.com/bjuraga/renovate-reproduce-nuget-pinning/pull/1/files

## Expected behavior

Renovate should respect the pinned version of `OpenTelemetry.Instrumentation.Http` in the ItemGroup for `net8.0` and should not updated it. Updating the net9.0 ItemGroup is as expected because in that ItemGroup the version is not pinned.

## Somewhat of a solution
Sadly i got banned from the Renovate project, i think for a month only. 

But, if someone stumbles upon this repro, i found what i was asking for as a workaround, strangely enough in the Renovate docs. 

Already confirmed it works on this repo and in AzureDevops on a self hosted Renovate bot, so here it is:

https://docs.renovatebot.com/modules/manager/nuget/#disabling-updates-for-pinned-versions

I personaly don't like the solution, but it works and i can justify choosing Renovate (the tool). 

Good luck!
