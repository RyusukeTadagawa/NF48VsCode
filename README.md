# NF48VsCode
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
