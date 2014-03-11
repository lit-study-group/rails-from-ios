##  フィードの取得

<br />
GETするよ
<br />

```objectivec
/* models/ModelManager.m */
...

@implementation ModelManager

...

- (void)getPosts
{
    NSString *url = [NSString stringWithFormat:@"%@/posts",BASE_URL];

    NSError *err;
    NSMutableURLRequest *request = [[AFJSONRequestSerializer serializer] requestWithMethod:@"GET"
                                                                                 URLString:url
                                                                                parameters:nil
                                                                                     error:&err];

    [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
    [request addValue:_user[@"token"] forHTTPHeaderField:@"X-Token"];
    AFHTTPRequestOperation *apiClient = [[AFHTTPRequestOperation alloc] initWithRequest:request];
    apiClient.responseSerializer = [AFJSONResponseSerializer serializer];

    [apiClient setCompletionBlockWithSuccess:^(AFHTTPRequestOperation *operation, id response) {
        if(response[@"error"]) return;
        [self willChangeValueForKey:@"posts"];
        _posts = response;
        [self didChangeValueForKey:@"posts"];
    } failure:^(AFHTTPRequestOperation *operation, NSError *error) {
        NSLog(@"Error: %@", error);
    }];
    AFHTTPRequestOperationManager *manager = [AFHTTPRequestOperationManager manager];
    [manager.operationQueue addOperation:apiClient];
}

...

```