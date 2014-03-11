##  シングルトン

そのクラスのインスタンスが1つしか生成されない<br />

ことを保証するデザインパターン<br />

<br />

```objectivec
/* models/ModelManager.m */
+ (instancetype)sharedManager
{
    static ModelManager *_shared = nil;
    static dispatch_once_t oncePredicate;
    dispatch_once(&oncePredicate, ^{
        _shared = [[self alloc] init];
    });

    return _shared;
}
```

**コードスニペット**にしておくと便利