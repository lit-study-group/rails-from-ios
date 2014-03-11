##  ヘッダファイルの編集



```objectivec
/* models/ModelManager.h */

@interface ModelManager : NSObject

@property(nonatomic,readonly) NSDictionary *user;
@property(nonatomic,readonly) NSArray *posts;

+ (instancetype)sharedManager;

- (void)login:(NSDictionary *)params;
- (void)getPosts;

@end
```