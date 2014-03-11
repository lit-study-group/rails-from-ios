##  ログイン機能の追加

<br />
POSTするよ
<br />

```objectivec
/* models/ModelManager.m */
...

@implementation ModelManager

...

- (void)login:(NSDictionary *)params
{
    NSString *url = [NSString stringWithFormat:@"%@/sessions",BASE_URL];
    NSError *err;
    NSMutableURLRequest *request = [[AFJSONRequestSerializer serializer] requestWithMethod:@"POST"
                                                                                 URLString:url
                                                                                parameters:params
                                                                                     error:&err];

    [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
    AFHTTPRequestOperation *apiClient = [[AFHTTPRequestOperation alloc] initWithRequest:request];
    apiClient.responseSerializer = [AFJSONResponseSerializer serializer];

    [apiClient setCompletionBlockWithSuccess:^(AFHTTPRequestOperation *operation, id response) {
        [self willChangeValueForKey:@"user"];
        _user = response;
        [self didChangeValueForKey:@"user"];
    } failure:^(AFHTTPRequestOperation *operation, NSError *error) {
        NSLog(@"Error: %@", error);
    }];
    AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
    [manager.operationQueue addOperation:apiClient];
}

...

```