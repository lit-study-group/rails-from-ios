##  使ってみる

<br />
ログインして、成功したら投稿を取得してみよう。
<br />

```objectivec
/* controllers/ViewController.m */

#import "ViewController.h"
#import "ModelManager.h"

@interface ViewController ()
{
    ModelManager *_modelManager;
}
@end

@implementation ViewController

- (void)viewDidLoad
{
    [super viewDidLoad];
  // Do any additional setup after loading the view, typically from a nib.

    _modelManager = [ModelManager sharedManager];

    [_modelManager addObserver:self forKeyPath:@"user" options:0 context:nil];
    [_modelManager addObserver:self forKeyPath:@"posts" options:0 context:nil];

    NSDictionary *params = @{
                                @"user":@{
                                     @"email": @"iwark@iwark.com",
                                     @"password": @"iwark",
                                     @"password_confirmation": @"iwark"
                                }
                             };

    [_modelManager login:params];

}

- (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void *)context
{
    if([keyPath isEqualToString:@"user"]){
        NSLog(@"user:%@",_modelManager.user);
        [_modelManager getPosts];
    }else if([keyPath isEqualToString:@"posts"]){
        NSLog(@"posts:%@",_modelManager.posts);
    }
}

- (void)dealloc
{
    [_modelManager removeObserver:self forKeyPath:@"user"];
    [_modelManager removeObserver:self forKeyPath:@"posts"];
}

...

```