# SKServicesManger
  SKServiceManger is a networking framework for executing HTTP requests for IOS apps it's a simple, efficient and easy to use IOS networking framework which is full of great and helpful features 

## Features :-
    1. Single networking queue for your whole app.
    2. Depending on the request type it would take the needed data to complete the request successfully.
    3. Requests are executed in the background while maintaining thread-safety.
    4. Once a request is done, the enqueuer will be notified and the response object should be passed to it.
    5. Requests continue to run when app goes to the background.
    6. Auto queue sizing and auto network indicator support.
    7. Requests run concurrently based on network condition, and the number of concurrent
    requests that can be fired is customizable for each network condition whether it’s via WIFI or cellular.
    8. Has a UIImageView category for downloading images asynchronously using a url and spinner color while loading image and an image for    failed requests.
   
## Requirements :-
   o IOS 8.0+
   
   
## Installation

  ### a) Using Framework file:-
        1. Drag the SKServicesManger.framework file into your project check copy items if needed.
        2. Go to your target settings in General tap -> embedded binaries click + and select the SKServicesManger framework.
        3. Add #import <SKServicesManger/SKServicesManger.h> in the class you want to use it in.

  ### b) Using source code files:-
        1. Drag the SKServicesManger directory into your project.
        2. Add #import “SKServicesManger.h” in the class you want to use it in.
    
    
## Usage:-
    1. You will need to set your coming requests base URL using the SKSessionManger shared manager instance

    [[SKSessionManger sharedSessionManger] setBaseUrl :@"Base URL"];

    2. Use the correct request object depending on your request type: - 
      o SKGetRequest
      o SKPostRequest
      o SKPutRequest
      o SKPatchRequest
      o SKDeleteRequest
      o SKDownloadRequest o SKUploadRequest
      o SKMultiPartFormUploadRequest
    3. Initialize the request object with it’s data in the parameterized initializer
    4. Use the SKSessionManger shared manager instance to add a request to the requests queue
    
    [[SKSessionManger sharedSessionManger] addRequestToQueue:getRequest];
    
    5. You can control the number of concurrent request for different network status
    
    [[SKSessionManger sharedSessionManger] setmaxWiFiTasks:6];
    [[SKSessionManger sharedSessionManger] setmaxCellularTasks:2];
    
    6 The SKSessionManger will handle the requests to run simultaneously even if the app goes to the background it would continue to get the request’s results also it shows a network activity indicator in the status bar while there’s any request running in the queue.
    
    
    
## Examples:-

### • SKGetRequest
    [[SKSessionManger sharedSessionManger] setBaseUrl:@"http://qc.abwab.com/api/v1/"];
    SKGetRequest* getRequest = [[SKGetRequest alloc] initWithPath:@"property/SearchReturnMarkers?" headers:[NSDictionary new] successHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",[[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding]);
    } failureHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
        NSLog(@"%@",error.localizedDescription); }
    urlParameters:@""];
    [[SKSessionManger sharedSessionManger] addRequestToQueue:getRequest];
### • SKPostRequest
    NSMutableDictionary* parameters = [[NSMutableDictionary alloc] init];
    parameters[@"country_id"] = @"1";
    [[SKSessionManger sharedSessionManger] setBaseUrl:@"http://www.goldmarket.xapps.co/frontend/web"];
    SKPostRequest* postRequest = [[SKPostRequest alloc] initWithPath:@"/api/v1/country/get-country-cities" headers:[NSDictionary new] successHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",[[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding]);
    } failureHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",error.localizedDescription); } parameters:parameters];
    [[SKSessionManger sharedSessionManger] addRequestToQueue: postRequest];
### • SKPutRequest
    NSMutableDictionary* parameters = [[NSMutableDictionary alloc] init];
    parameters[@"country_id"] = @"1";
    [[SKSessionManger sharedSessionManger] setBaseUrl:@"http://www.goldmarket.xapps.co/frontend/web"];
    SKPutRequest* putRequest = [[SKPutRequestalloc] initWithPath:@"/api/v1/country/get- country-cities" headers:[NSDictionary new] successHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",[[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding]);
    } failureHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) { NSLog(@"%@",error.localizedDescription);
    } parameters:parameters];
    [[SKSessionManger sharedSessionManger] addRequestToQueue: putRequest];
### • SKPatchRequest
    NSMutableDictionary* parameters = [[NSMutableDictionary alloc] init]; 
    parameters[@"country_id"] = @"1";
    [[SKSessionManger sharedSessionManger] setBaseUrl:@"http://www.goldmarket.xapps.co/frontend/web"];
    SKPatchRequest* patchRequest = [[SKPatchRequest] initWithPath:@"/api/v1/country/get- country-cities" headers:[NSDictionary new] successHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",[[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding]);
    } failureHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) { NSLog(@"%@",error.localizedDescription);
    } parameters:parameters];
    [[SKSessionManger sharedSessionManger] addRequestToQueue: patchRequest];
### • SKDeleteRequest
    [[SKSessionManger sharedSessionManger] setBaseUrl:@"http://qc.abwab.com/api/v1/"];
    SKDeleteRequest* deleteRequest = [[SKDeleteRequestalloc] initWithPath:@"property/SearchReturnMarkers?"
    headers:[NSDictionary new]
    successHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",[[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding]);
    }
    failureHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",error.localizedDescription); }];
    [[SKSessionManger sharedSessionManger] addRequestToQueue: deleteRequest];
### • SKDownloadRequest
    [[SKSessionManger sharedSessionManger] setBaseUrlValue:@""];
    SKDownloadRequest* downloadRequest = [[SKDownloadRequest alloc] initWithPath:imageUrl headers:[NSDictionary new] successHandler:^(NSData* response, NSError *error) {
    if (response != nil) {
    UIImage* image = [UIImage imageWithData:response]; }
    } failureHandler:^(NSData* response, NSError *error) { }];
    [[SKSessionManger sharedSessionManger] addRequestToQueue:downloadRequest];
### • SKUploadRequest
    NSURL *imgPath = [[NSBundle mainBundle] URLForResource:@"unavailable" withExtension:@"png"];
    NSString*stringPath = [imgPath absoluteString];
    NSData* fileData = [NSData dataWithContentsOfURL:[NSURL URLWithString:stringPath]]; [[SKSessionManger sharedSessionManger] setBaseUrl:@"http://www.goldmarket.xapps.co/frontend/web"];
    SKUploadRequest* uploadRequest = [[SKUploadRequest alloc] initWithPath:@"" headers:[NSDictionary new] successHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",[[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding]);
    } failureHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",error.localizedDescription); } fileData:fileData];
    [[SKSessionManger sharedSessionManger] addRequestToQueue:multipartRequest];
### • SKMultiPartFormUploadRequest
    NSURL *imgPath = [[NSBundle mainBundle] URLForResource:@"image" withExtension:@"jpg"];
    NSString*stringPath = [imgPath absoluteString];
    [[SKSessionManger sharedSessionManger] setBaseUrl:@"http://www.goldmarket.xapps.co/frontend/web"];
    SKMultiPartFormUploadRequest* multipartRequest = [[SKMultiPartFormUploadRequest alloc] initWithPath:@"/api/v1/image/upload" headers:[NSDictionary new] successHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",[[NSString alloc] initWithData:responseData encoding:NSUTF8StringEncoding]);
    } failureHandler:^(NSData* responseData,NSURLResponse* urlResponse, NSError *error) {
    NSLog(@"%@",error.localizedDescription);
    } parameters:[NSDictionary new] filePath:stringPath fieldName:@"image"];
    [[SKSessionManger sharedSessionManger] addRequestToQueue:multipartRequest];
### • UIImageView image downloader [self.imageView
    setImageWithUrl:@"http://www.hdwallpapers.in/download/ashe_league_of_legends_4k _8k-750x1334.jpg" activtyIndicatorTintColor:[UIColor blackColor] failureImage:[UIImage imageNamed:@"unavailable.png"]];

