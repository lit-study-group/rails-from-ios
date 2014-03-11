##  初期化

```objectivec
/* models/ModelManager.m */
#import "ModelManager.h"
#import "AFNetworking.h"

#define BASE_URL @"http://localhost:3000/api/v1"

@implementation ModelManager

...

- (id)init
{
    if(self = [super init]){
        _user = @{};
        _posts = @[];
    }
    return self;
}

//手動でKVOの通知をする
+ (BOOL)automaticallyNotifiesObserversForKey:(NSString *)theKey {
    return NO;
}

...

```