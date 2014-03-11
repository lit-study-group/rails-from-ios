##  Podfileの作成

xcodeprojのあるフォルダに作成。<br />

RailsでいうGemfile。

```
$ subl Podfile
```

```
platform :ios, '6.0'
pod 'AFNetworking', '~> 2.0'
pod 'SVProgressHUD'
pod 'MGBox2', '~> 2.0.0'
```