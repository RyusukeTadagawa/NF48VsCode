## NF48VsCode
VSCodeで.netframeworkのビルドとデバックをするためのサンプルプロジェクト

以下のコマンドを入力
dotnet new console  --target-framework-override net48  -lang c# --langVersion 7.3 -o NF48VsCode

--target-framework-override
ターゲットになるフレームワークを指定

 -lang 
 開発言語を指定
 
 --langVersion
 言語のバージョンを指定。
 デフォルト指定だと最新のバージョンになってしまい、コンパイルが通らず
 修正しないといけないので7.3の指定を推奨
 
 -o 
 プロジェクト名を指定

## ２．プロジェクトファイルを編集する

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net48</TargetFramework>
    <LangVersion>7.3</LangVersion>
  </PropertyGroup>

</Project>
```

↓

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net48</TargetFramework>
    <LangVersion>7.3</LangVersion>
    <PlatformTarget>x64</PlatformTarget>
    <DebugType>portable</DebugType>
  </PropertyGroup>

</Project>
```

***PlatformTarget***と***DebugType***を追加します。

## ３．launch.jsonの作成と修正

```
{
    // IntelliSense を使用して利用可能な属性を学べます。
    // 既存の属性の説明をホバーして表示します。
    // 詳細情報は次を確認してください: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": ".NET Core Launch (console)",
            "type": "coreclr",
            "request": "launch",
            "警告01": "*********************************************************************************",
            "警告02": "The C# extension was unable to automatically decode projects in the current",
            "警告03": "workspace to create a runnable launch.json file. A template launch.json file has",
            "警告04": "been created as a placeholder.",
            "警告05": "",
            "警告06": "If the server is currently unable to load your project, you can attempt to",
            "警告07": "resolve this by restoring any missing project dependencies (example: run 'dotnet",
            "警告08": "restore') and by fixing any reported errors from building the projects in your",
            "警告09": "workspace.",
            "警告10": "If this allows the server to now load your project then --",
            "警告11": "  * Delete this file",
            "警告12": "  * Open the Visual Studio Code command palette (View->Command Palette)",
            "警告13": "  * run the command: '.NET: Generate Assets for Build and Debug'.",
            "警告14": "",
            "警告15": "If your project requires a more complex launch configuration, you may wish to",
            "警告16": "delete this configuration and pick a different template using the 'Add",
            "警告17": "Configuration...' button at the bottom of this file.",
            "警告18": "*********************************************************************************",
            "preLaunchTask": "build",
            "program": "${workspaceFolder}/bin/Debug/<insert-target-framework-here>/<insert-project-name-here>.dll",
            "args": [],
            "cwd": "${workspaceFolder}",
            "console": "internalConsole",
            "stopAtEntry": false
        },
        {
            "name": ".NET Core Attach",
            "type": "coreclr",
            "request": "attach"
        }
    ]
}
```


↓

```
{
    // IntelliSense を使用して利用可能な属性を学べます。
    // 既存の属性の説明をホバーして表示します。
    // 詳細情報は次を確認してください: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": ".NET Core Launch (console)",
            "type": "clr",
            "request": "launch",
            "preLaunchTask": "build",
            "program": "${workspaceFolder}/bin/Debug/net48/NF48VsCode.exe",
            "args": [],
            "cwd": "${workspaceFolder}",
            "console": "internalConsole",
            "stopAtEntry": false
        },
        {
            "name": ".NET Core Attach",
            "type": "clr",
            "request": "attach"
        }
    ]
}
```

警告文の削除
typeをcoreclrから**clr**に変更
programを実行環境とプロジェクトファイルに合わせて変更する。
拡張子は**exe**に変更する。

## ４．tasks.jsonの作成と修正
ターミナル　
　→　「タスクの構成」を選択　
　→　「テンプレートからtasks.jsonを生成」を選択　
　→　「.Net Core」を選択
　　
## ５．実行とデバッグ
F5キーでデバッグ実行が出来ます。
またコードの任意の場所にブレイクポイントを設定できます。
