[Back](../index.md)

# My Transitions iOS
## Technical Documentation



### GETTING STARTED
myTransitions iOS requires Xcode 11.0 and above for development. This project uses Swift 5 as the Programming Language, Storyboard for the Interface and CocoaPods for Third Party Libraries. The app also uses CoreData to store offline information. The current Xcode version used for development is 11.5. The minimum iOS Version required is iOS 11.0


### INSTALLATION AND DEVELOPMENT
In order to start with the development, first, you will need an Apple account for development. It must be under the team **Rogomi, Inc.** Then, open the **myTransitions.xcworkspace** under the repository root directory. If possible, do a **pods repo update** in order to avoid missing library errors.


### PROGRAMMING LANGUAGE 
myTransitions iOS uses the latest Swift version, Swift 5, for development.


### MINIMUM VERSION 
myTransitions iOS requires devices with at least iOS 12.0


### APPLICATION ID
com.transitions.transitionsworld


### DEBUGGING
We use a few debugging tools to test myTransition’s functionalities.  

For the Native App, we use Xcode's debugging console to create breakpoints and test variables, API responses, and identify null objects which sometimes causes the crash.

To test the API before integrating for app usage, we use [Postman](https://www.getpostman.com/). Postman is a very reliable REST API tool. We can test different HTTP Methods especially POST, PATCH, PUT, DELETE and GET. We can also add header variables to test SSO and token authentications.

We also use iOS Simulator in order to test the apps in different screen sizes and iOS Versions.


### WEB API
Google Sign In API, Azure


### THIRD PARTY LIBRARIES
#### Linked Libraries
**AdSupport.framework** - Used for Google Analytics  
**AppTrackingTransparency.framework** - Required by apple for iOS 14 and above to allow the user to decide whether they let the app have access to IDFA or not.

#### Cocoapods
Most of the third party libraries are installed using CocoaPods. They can be added by searching library names found in https://cocoapods.org/, inserting them in the Podfile and running the pod install command in the Terminal.

##### Important Libraries
**Alamofire** - For Web API Communications  
**SwiftyJSON** - To ease up processing of response data  
**ObjectMapper** - To easily create models for response data

##### Firebase Platform Libraries.
**Firebase/Analytics** - Used for App Analytics  
**Firebase/Crashlytics** - Used to identify causes of crashes from users  
**Firebase/Performance** - Used to monitor application performance

##### UI Libraries
**IQKeyboardManagerSwift** - To automatically scroll up the UITextView on screen when the keyboard is up.  
**IBAnimatable** - To easily add special UI Designs on specific views, and see them reflected on the Interface Builder. Also has methods to animate views.  
**SDWebImage** - To easily load Images from URL and has caching functions.  
**MBProgressHUD** - Used to add heads up display on screen to indicate loading while user is waiting for data to be loaded from the API  
**JTAppleCalendar** - Used for the Calendar module
**FlagKit** - Used for profile country
##### Other Useful Libraries 
**ReachabilitySwift** - Used to check internet connection status   
**SwiftDate** - Used to easily process Date objects in swift   
**Fakery** - To easily create dummy data.   
**GoogleSignIn** - Used to sign in to Google  
**GoogleAPIClientForREST/Calendar** -  To connect to Google Calendar. 
**SwiftAudio** - Used to play podcasts  
**SkeletonView** - Used to display a loading view for incoming data  
**SwiftyCam** - Used for custom camera actions
### ANALYTICS
Details for analytics event names and actions: https://docs.google.com/spreadsheets/d/1b39XXshTeR9Vf-GV5kpHwhlMN2Dtb0cQopGR8mq9ryU/edit#gid=0

* **Event Name Format:**	<action><content_type>_<epic_name>_<screen_name>	
* **Example:**	likecomment_podcast_commentsview	
* **Parameters:**	userid, platform, action, contenttype	
* **Optional Parameters:** 	targetdata, logdata	
		
**REMARKS:**	
* _Target data_ pertains to the target of the action, while the _Log Data_ pertains to the content of the action	
* _Target Data_ and _Log Data_ can be null, but _Target Data_ will most of time be filled with the targeted item.
* _Log Data_ will often be used when adding posts and comments.
### ACTIVITIES AND CONTROLLERS

#### Core Classes
- **AppDelegate** - manages most of the pre-startup items like Firebase configurations, etc.
  ##### Configured items
  - Firebase Configuration - Analytics and crashlytics.
  - IDFA Permission - Asks the user for permission to track for analytics.
  - Google Sign In - Sets the API key for Google Sign In
  - IQKeyboardManager - enables the global usage of IQKeyboardManager.
  - Web Configuration - sets the globally used domain for API access.
#### View Controllers

- **AppTabBarController** - manages the app access, redirects to Login screen when user is not logged in.    
  ##### Methods
  - `openLogin()`
  - `clearTabs()`
  - `gotToLanding()`

- **AuthViewController** - contains functions that allows the user to sign in via their Google account. Handles offline error and checking user credentials  
  ##### Methods
  - `ssign(... didSignInFor user: GIDGoogleUser!)`
  - `showOfflineAlert()`
  - `validDomain()`
  - `showInvalidEmailAlert()`

- **SocialViewController** - contains functions that manages different Social pages (e.g., Feed, Events, Community).
  ##### Methods
  - `collectionView(... numberOfItemsInSection section: Int)`
  - `collectionView(... cellForItemAt indexPath: IndexPath)`
  - `collectionView(... didSelectItemAt indexPath: IndexPath)`  
  
- **CreatePostViewController** - controls the display of podcast information details  
  ##### Methods  
  - `didTapAudienceButton(_ sender: Any)`
  - `didTapCloseButton(_ sender: Any)`
  - `didTapPostButton(_ sender: Any)`
  - `didTapPictureButton(_ sender: Any)`
  - `didTapLocationButton(_ sender: Any)`
  - `didTapPollButton(_ sender: Any)`
  - `savePostAz()`
  - `collectionView(... numberOfItemsInSection section: Int)`
  - `collectionView(... cellForItemAt indexPath: IndexPath)`
  - `collectionView(... didSelectItemAt indexPath: IndexPath)`  
  
- **CreateCommunityPostViewController** 
  ##### Methods  
  - `viewDidLoad()`
  - `didTapAudienceButton(_ sender: Any)`
  - `didTapPostType(_ sender: Any)`
  - `didTapCloseButton(_ sender: Any)`
  - `didTapPostButton(_ sender: Any)`
  - `didTapPictureButton(_ sender: Any)`
  - `savePostImages(_ images: [UIImage?], with post: String, ...)`
  - `savePost(_ post: String, fileObjects: [[String: Any]]?, ...)`
  - `textViewDidChange(_ textView: UITextView)`
  - `shouldDismissPhotoPicker(withTLPHAssets: [TLPHAsset])`
  - `handleNoAlbumPermissions(picker: TLPhotosPickerViewController)`
  - `handleNoCameraPermissions(picker: TLPhotosPickerViewController)`
  - `askPermissions(message:String)`
  - `collectionView(... cellForItemAt indexPath: IndexPath)`
  - `collectionView(... didSelectItemAt indexPath: IndexPath)`  
    
- **CommunityPickerViewController** 
  ##### Methods  
  - `didTapFilterButton(_ sender: Any)`
  - `getFollowedCommunities()`
  - `getAllCommunities()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  
  
- **AddLocationViewController** 
  ##### Methods  
  - `didTapBackButton(_ sender: Any)`
  - `getNearbyPlaces(with location: CLLocationCoordinate2D, keyword: String?)`
  - `locationManager(... didUpdateLocations locations: [CLLocation])`
  - `searchBarTextDidBeginEditing(_ searchBar: UISearchBar)`
  - `searchBar(_ searchBar: UISearchBar, textDidChange searchText: String)`
  - `searchBarSearchButtonClicked(_ searchBar: UISearchBar)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  
  
- **CommunityViewController** 
  ##### Methods  
  - `tableViewRefresh(_ sender: Any)`
  - `postDidSubmit(_ object: Any)`
  - `didTapCreatePostButton(_ sender: Any)`
  - `getFollowedCommunities()`
  - `getAllCommunities()`
  - `loadActivities(pageCursor: String?, ...)`
  - `likeLumappContent(_ content: ContentListObject, cell: FeedTextPostTableViewCell)`
  - `unlikeLumappContent(_ content: ContentListObject, ...)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  
  
- **CommunitiesDetailsViewController** 
  ##### Methods  
  - `viewDidLoad()`
  - `didTapBackButton(_ sender: Any)`
  - `collectionView(... cellForItemAt indexPath: IndexPath)`  
  
- **SelectedCommunityViewController** 
  ##### Methods  
  - `viewDidLoad()`
  - `tableViewRefresh(_ sender: Any)`
  - `postDidSubmit(_ object: Any)`
  - `didTapCreatePostButton(_ sender: Any)`
  - `didTapDetailsButton(_ sender: Any)`
  - `didTapBackButton(_ sender: Any)`
  - `loadActivities(pageCursor: String? ...)`
  - `likeLumappContent(_ content: ContentListObject, cell: FeedTextPostTableViewCell)`
  - `unlikeLumappContent(_ content: ContentListObject, ...)`
  - `tableView(... cellForItemAt indexPath: IndexPath)`  
  
- **SeeAllCommunitiesViewController** 
  ##### Methods  
  - `didTapNotReadyButton(_ sender: Any)`
  - `viewDidLoad()`
  - `getFollowedCommunities()`
  - `getAllCommunities()`
  - `collectionView(... cellForItemAt indexPath: IndexPath)`  
  
- **PeopleFinderViewController**  - controls the "People Finder" view from the "Network" tab of the app which is responsible for allowing the user to search people from the app by their name and/or group/s
  ##### Methods  
  - `searchEditingDidEnd(_ sender: Any)`
  - `viewDidLoad()`
  - `unwindFromGroupFilter(_ sender: UIStoryboardSegue)`
  - `getData()`
  - `checkFollowStatus(for user: UserDetailsObject, ...)`
  - `tableView(... cellForItemAt indexPath: IndexPath)`  
  
- **SearchGroupViewController**  - controls the "Search Group Filter" view presented by the "People Finder" view to filter the people by groups. This view controller allows the user to search a group and select it and uses the selcted group to filter the results in the "People Finder" view.
  ##### Methods  
  - `editingDidEndGroupSearch(_ sender: Any)`
  - `viewDidLoad()`
  - `getData()`
  - `tableView(... cellForItemAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  
  
- **ActivityViewController** 
  ##### Methods  
  - `viewDidLoad()`  
  
- **ActivityPhotoViewController** 
  ##### Methods  
  - `viewDidLoad()`
  - `didTapBackButton(_ sender: Any)`
  - `didTapOverflowButton(_ sender: Any)`
  - `didTapAuthorButton(_ sender: Any)`
  - `didTapSeeMoreButton(_ sender: Any)`
  - `didTapLikeButton(_ sender: UIButton)`
  - `didTapCommentButton(_ sender: UIButton)`
  - `didTapShareButton(_ sender: UIButton)`
  - `loadActivity()`
  - `likeLumappContent()`
  - `unlikeLumappContent()`
  - `updateLikesUI()`
  - `updateCommentsUI()`  
  
- **ActivityCommunityPhotoViewController** 
  ##### Methods  
  - `viewDidLoad()`
  - `didTapBackButton(_ sender: Any)`
  - `didTapOverflowButton(_ sender: Any)`
  - `didTapAuthorButton(_ sender: Any)`
  - `didTapSeeMoreButton(_ sender: Any)`
  - `didTapLikeButton(_ sender: UIButton)`
  - `didTapCommentButton(_ sender: UIButton)`
  - `didTapShareButton(_ sender: UIButton)`
  - `loadActivity()`
  - `likeLumappContent()`
  - `unlikeLumappContent()`
  - `updateLikesUI()`
  - `updateCommentsUI()`  
  
- **FeedViewController** - contains functions that loads the newsfeed for the user (contains 3 sections, the User Stories, TW Highlights and Activities)
  ##### Methods
  - `loadTWH()`
  - `tableViewRefresh(_ sender: Any)`
  - `postDidSubmit(_ object: Any)`
  - `storiesDidUpdate(_ object: Any)`
  - `didTapCreatePostButton(_ sender: Any)`
  - `addSwipe()`
  - `handleSwipe(sender: UISwipeGestureRecognizer)`
  - `openCamera(withAnimation: Bool = false)`
  - `loadStories(willShowSkeleton: Bool)`
  - `loadActivities(pageCursor: String?, currentPage: Int?, willShowSkeleton: Bool, isFromPostSubmit: Bool)`
  - `likeAzContent(_ content: AzContentObject, cell: FeedTextPostTableViewCell)`
  - `unlikeAzContent(_ content: AzContentObject, cell: FeedTextPostTableViewCell)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... viewForHeaderInSection section: Int)`

- **TWHighlightsSeeAllViewController** - contains functions that loads all of the contents from either the LumApps API or Azure API and displays to the user. Currently used when browing to all of TWHighlights or Financial News.
  ##### Methods
  - `func didTapBackButton(_ sender: Any)`
  - `func tappedUnavailableButton(_ sender: Any)`
  - `loadTWH(pageCursor: String, willShowSkeleton: Bool)`
  - `loadAzContents(pageCursor: String, willShowSkeleton: Bool)`
  - `tableView(... numberOfRowsInSection section: Int)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`
  - `tableView(... viewForHeaderInSection section: Int)`
  
- **ContentDetailsViewController** - contains functions that loads a content and loads a brief list of news from the API. It can use the contents coming from either the LumApps web server, or the Azure web server. This is currently used for TWHighlights and Financial News.
  ##### Methods
  - `loadContent()`
  - `loadAzContent()`
  - `loadNews()`
  - `loadAzNews()`
  - `didTapBackButton(_ sender: Any)`
  - `didTapOverflowButton(_ sender: Any)`
  - `didTapLikesButton(_ sender: Any)`
  - `didTapLikeButton(_ sender: Any)`
  - `didTapCommentsButton(_ sender: Any)`
  - `updateLikesUI()`
  - `updateCommentsUI()`
  - `numberOfSections(in tableView: UITableView)`
  - `tableView(... numberOfRowsInSection section: Int)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`
  - `tableView(... viewForHeaderInSection section: Int)`
  - `likeLumappContent(_ content: ContentListObject)`
  - `likeAzContent(_ content: AzContentObject)`
  - `unlikeLumappContent(_ content: ContentListObject)`
  - `unlikeAzContent(_ content: AzContentObject)`  
  
- **TWHighlightActionsViewController**
  ##### Methods
  - `didTapScreen(_ sender: Any)`
  - `dismissScreen()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`
  - `activityViewControllerPlaceholderItem(_ activityViewController: UIActivityViewController)`
  - `activityViewController(... itemForActivityType activityType: UIActivity.ActivityType?)`
  - `activityViewController(... subjectForActivityType activityType: UIActivity.ActivityType?)`
  
- **TWWebViewController**
  ##### Methods
  - `viewDidLoad()`
  - `didTapCloseButton(_ sender: Any)`  
  
- **UserSocialProfileViewController** - contains functions that displays a specific user's profile information and timeline for activities, groups and comments.
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `didTapOverflowButton(_ sender: Any)`
  - `numberOfSections(in tableView: UITableView)`
  - `tableView(... numberOfRowsInSection section: Int)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`

- **LikesViewController** - contains functions that displays list of users that liked a social item (Posts, Comments, Podcast, Financial News)
  ##### Methods
  - `didTapCloseButton(_ sender: Any)`
  - `loadLikes()`
  - `checkFollowStatus(_ idx: Int = 0, for users: [UserDetailsObject])`
  - `tableView(... numberOfRowsInSection section: Int)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`
  
- **CommentsViewController** - contains functions that displays list of comments and their specific replies. Currently used for TWHighlights, Podcasts and Financial News.
  ##### Methods
  - `didTapCloseButton(_ sender: Any)`
  - `didTapCommentCamera(_ sender: UIButton)`
  - `didTapSendCommentButton(_ sender: Any)`
  - `didTapCancelReplyingButton(_ sender: Any)`
  - `loadComments()`
  - `selectImage(sender: UIButton)`
  - `toggleSendButton()`
  - `retrieveReplies(for comment: CommentListObject, completion: @escaping(Error?) -> Void)`
  - `saveCommentImage(_ image: UIImage?, with comment: String, completion: @escaping(Error?) -> Void)`
  - `saveComment(_ comment: String, fileObjects: [[String: Any]]? = nil, completion: @escaping(Error?) -> Void)`
  - `postCommentOnAzure(_ comment: String, completion: @escaping(Error?) -> Void)`
  - `numberOfSections(in tableView: UITableView)`
  - `tableView(... numberOfRowsInSection section: Int)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  
  
- **StoryViewersViewController**
  ##### Methods
  - `viewDidLoad()`
  - `didTapCloseButton(_ sender: Any)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`  
  
- **PhotoViewController**
  ##### Methods
  - `viewDidLoad()`
  - `didTapCloseButton(_ sender: Any)`
  - `didTapSaveButton(_ sender: Any)`
  - `didTapShareButton(_ sender: Any)`
  - `handleDidCompleteSavingToLibrary(image: UIImage?, error: Error?, contextInfo: Any?)`  
  
- **VideoViewController**
  ##### Methods
  - `viewDidLoad()`
  - `playerItemDidReachEnd(_ notification: Notification)`
  - `didTapCloseButton(_ sender: Any)`
  - `didTapSaveButton(_ sender: Any)`
  - `didTapShareButton(_ sender: Any)`
  - `handleDidCompleteSavingToLibrary(image: UIImage?, error: Error?, contextInfo: Any?)`
  - `convertFromAVAudioSessionCategory(_ input: AVAudioSession.Category)`  
  
- **StoriesCameraViewController**
  ##### Methods
  - `viewDidLoad()`
  - `swiftyCamSessionDidStartRunning(_ swiftyCam: SwiftyCamViewController)`
  - `swiftyCamSessionDidStopRunning(_ swiftyCam: SwiftyCamViewController)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didTake photo: UIImage)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didBeginRecordingVideo camera: SwiftyCamViewController.CameraSelection)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didFinishRecordingVideo camera: SwiftyCamViewController.CameraSelection)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didFinishProcessVideoAt url: URL)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didFocusAtPoint point: CGPoint)`
  - `swiftyCamDidFailToConfigure(_ swiftyCam: SwiftyCamViewController)`
  - `didTapCancelButton(_ sender: Any)`
  - `didTapGalleryButton(_ sender: Any)`
  - `addSwipe()`
  - `handleSwipe(sender: UISwipeGestureRecognizer)`
  - `openPicker()`
  - `openPhotos()`
  - `openVideos()`
  - `imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [UIImagePickerController.InfoKey : Any])`
  - `hideButtons()`
  - `showButtons()`
  - `toggleFlashAnimation()`
  - `startTimer()`
  - `stopTimer()`
  - `fireTimer()`  
  
- **StoriesCameraViewController**
  ##### Methods
  - `viewDidLoad()`
  - `swiftyCamSessionDidStartRunning(_ swiftyCam: SwiftyCamViewController)`
  - `swiftyCamSessionDidStopRunning(_ swiftyCam: SwiftyCamViewController)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didTake photo: UIImage)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didBeginRecordingVideo camera: SwiftyCamViewController.CameraSelection)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didFinishRecordingVideo camera: SwiftyCamViewController.CameraSelection)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didFinishProcessVideoAt url: URL)`
  - `swiftyCam(_ swiftyCam: SwiftyCamViewController, didFocusAtPoint point: CGPoint)`
  - `swiftyCamDidFailToConfigure(_ swiftyCam: SwiftyCamViewController)`
  - `didTapCancelButton(_ sender: Any)`
  - `didTapGalleryButton(_ sender: Any)`
  - `addSwipe()`
  - `handleSwipe(sender: UISwipeGestureRecognizer)`
  - `openPicker()`
  - `openPhotos()`
  - `openVideos()`
  - `imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [UIImagePickerController.InfoKey : Any])`
  - `hideButtons()`
  - `showButtons()`
  - `toggleFlashAnimation()`
  - `startTimer()`
  - `stopTimer()`
  - `fireTimer()`  
  
- **EventsDashboardViewController** 
  ##### Methods
  - `viewDidLoad()`
  - `getEvents()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)`  
  
- **UpcomingEventsViewController**
  ##### Methods
  - `viewDidLoad()`
  - `didTapBackButton(_ sender: Any)`
  - `collectionView(... cellForItemAt indexPath: IndexPath)`  
  
- **PodcastSearchViewController** - contains functions that allows the user to search through podcasts
  ##### Methods
  - `searchPodcasts()`
  - `getFilteredPodcast()`
  - `didTapEraseButton(_ sender: Any)`
  - `didTapDoneCancelButton(_ sender: Any)`
  - `editingChanged(_ sender: UITextField)`
  - `tableView(... numberOfRowsInSection section: Int)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`
  - `textFieldDidEndEditing(_ textField: UITextField)`

- **PodcastPlayerViewController** - contains functions that allows the user to play podcasts
  ##### Methods
  - `didTapOverflowButton(_ sender: Any)`
  - `didTapCloseButton(_ sender: Any)`
  - `didTapLikes(_ sender: Any)`
  - `didTapComments(_ sender: Any)`
  - `didTapLikeButton(_ sender: Any)`
  - `togglePlay(_ sender: Any)`
  - `previous(_ sender: Any)`
  - `next(_ sender: Any)`
  - `startScrubbing(_ sender: UISlider)`
  - `scrubbing(_ sender: UISlider)`
  - `scrubbingValueChanged(_ sender: UISlider)`
  - `updateTimeValues()`
  - `updateMetaData()`
  - `setPlayButtonState(forAudioPlayerState state: AudioPlayerState) `
  - `handleAudioPlayerStateChange(data: AudioPlayer.StateChangeEventData)`
  - `handlePlayerFailure(data: AudioPlayer.FailEventData)`

- **PodcastCategoryViewController** - contains functions that allows the user to view podcasts in a category
  ##### Methods
  - `didTapCloseButton(_ sender: Any)`
  - `tableView(... numberOfRowsInSection section: Int)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  
  
- **PodcastDetailsViewController** - controls the display of podcast information details  
  ##### Methods
  - `didTapCloseButton(_ sender: Any)`
  - `getDetails()`
  - `updateDetails()`  
  
- **MyAppsViewController** - controls the display of the "My Apps" view
  ##### Methods
  - `collectionView(... cellForItemAt indexPath: IndexPath)`
  - `collectionView(... didSelectItemAt indexPath: IndexPath)`
  - `didTapSearchButton(_ sender: Any)`  
  
- **CalendarViewController** - controls the display of the user calendar and events of the selected date
  ##### Methods
  - `getList(date: Date)`
  - `setDateSelection(startDate: Date, endDate: Date)`
  - `tableViewDidRefresh(_ sender: Any)`
  - `openMonthPicker()`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `presentationController(... viewControllerForAdaptivePresentationStyle style: UIModalPresentationStyle)`
  - `presentationController(... viewControllerForAdaptivePresentationStyle style: UIModalPresentationStyle)`
  
- **EventViewController** - controls the display of event webview
  ##### Methods
  - `loadView()`
  
- **CalendarDatePickerViewController** - controls the display of the date picker for th calendar date selection
  ##### Methods
  - `setupDatePicker(current: Date, start: Date, end: Date)`
  - `didTapConfirm(_ sender: Any)`
  
- **FinancialsViewController** - controls the display of the Financials view
  ##### Methods
  - `refreshStockPrice()`
  - `refreshFinancialNews()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`
  
- **FinancialsSeeMoreViewController** - controls the display of the Financials view
  ##### Methods
  - `didTapBackButton(_ sender: Any)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  
- **MyCareerViewController** - controls the display of the My Career views (Welcome to Teansitions, Wiki-Essi, E-Tslent, University)
  ##### Methods
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `collectionView(... didSelectItemAt indexPath: IndexPath)`
  - `prepare(for segue: UIStoryboardSegue, sender: Any?)`
  
- **WelcomeViewController** - controls the display of the "Welcome to Transitions" view
  - `viewWillAppear(_ animated: Bool)`
  
- **WikiViewController** - controls the display of the "Wiki-Essi" view
  - `viewWillAppear(_ animated: Bool)`
  
- **TalentViewController** - controls the display of the "E-Talent" view
  - `viewWillAppear(_ animated: Bool)`
  
- **UniversityViewController** - controls the display of the "University" view
  - `viewWillAppear(_ animated: Bool)`
  
- **ProfileViewController** - controls the display of the "Profile" view which contains the buttons to link to the Profile views (Activity, History, Subscriptions, My Settings, Send Feedback, About the app, Logout)
  ##### Methods
  - `loadProfile()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  

- **ProfileActivityViewController** - controls the display of the "Activity" view in the "Profile" tab
  ##### Methods
  - `viewDidLoad()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `getData()`

- **ProfileHistoryViewController** - controls the display of the "History" view in the "Profile" tab
  ##### Methods
  - `viewDidLoad()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `getData()`  

- **MySettingsViewController** - controls the display of the "My Settings" view in the "Profile" tab (UI only)  

- **SettingsNotificationViewController** - controls the display of the "Notification Settings" view in the "Profile" tab (UI only)  

- **AboutViewController** - controls the display of the "About" view in the "Profile" tab (UI only)
  ##### Methods
  - `viewDidLoad()`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `getData()`   

- **SendFeedbackViewController** - controls the display of the "Send Feedback" view in the "Profile" tab
  ##### Methods
  - `prepare(for segue: UIStoryboardSegue, sender: Any?)`
  - `tableView(... cellForRowAt indexPath: IndexPath)`
  - `tableView(... didSelectRowAt indexPath: IndexPath)`  

- **FeedbackEmailViewController** - controls the display of the "Suggest Something" and "Report a bug" views in the "Profile" tab. This view is also responsible for sending the user's review to the [support email](transitionsmobile_support@transitions.com) via email. 
  ##### Methods
  - `viewDidLoad()`
  - `didTapDoneButton(_ sender: Any)`
  - `didTapPhotosButton(_ sender: Any)`  
  - `generateRawReply (reply: String)`
  - `sendFeedback(email: GTLRGmail_Message)`

- **RatingViewController** - controls the display of the "Rate us" view in the "Profile" tab. This view is also responsible for sending the user's rating to the server. 
  ##### Methods
  - `viewDidLoad()`
  - `ddidTapStarX(_ sender: Any)` - (Replace X with any number from 1 to 5)
  - `didTapDone(_ sender: Any)`  
  - `centerDescription (starNumber: Int)`
  - `changeRating(starNumber: Int)`
  - `decreaseStar(starNumber: Int)`
  - `increaseStar(starNumber: Int)`   

- **FeedbackSuccessViewController** - controls the display of the "Send Feedback Success" view in the "Profile" tab. 
  ##### Methods
  - `viewDidLoad()`

- **SubscriptionViewController** - controls the display of the "Subscriptions" view in the "Profile" tab which displays the Subscription views (All, Community, Events, Following). 
  ##### Methods
  - `viewDidLoad()`
  - `prepare(for segue: UIStoryboardSegue, sender: Any?)`
  - `collectionView(... cellForItemAt indexPath: IndexPath)`
  - `collectionView(... didSelectItemAt indexPath: IndexPath)`   

- **AllSubscriptionsViewController** - controls the display of the "All" view in the "Subscriptions" module which displays 3 user subscriptions in each subscription category. 
  ##### Methods
  - `viewDidLoad()`
  - `getData()`
  - `getCommunities()`
  - `getEvents()`
  - `getFollowing()`
  - `tableView(_ tableView: UITableView, viewForHeaderInSection section: Int)`
  - `tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath)`  

- **CommunitySubscriptionsViewController** - controls the display of the "Communities" view in the "Subscriptions" module which displays the Communities which the user are subscribed to. 
  ##### Methods
  - `viewDidLoad()`
  - `getCommunities()`
  - `tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath)`  

- **EventsSubscriptionViewController** - controls the display of the "Events" view in the "Subscriptions" module which displays the Events which the user are subscribed to. (UI only) 
  ##### Methods
  - `viewDidLoad()`
  - `getEvents()`
  - `tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath)`  
  
- **FollowingSubscriptionViewController** - controls the display of the "Following" view in the "Subscriptions" module which displays the People which the user are following. 
  ##### Methods
  - `viewDidLoad()`
  - `getFollowing()`
  - `tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath)`  
  
- **AboutViewController** - controls the display of the "About us" view in the "Profile" tab which displays the details about the application.
  ##### Methods
  - `viewDidLoad()`  
  
- **NotificationViewController** - controls the display of the "Notification" view.
  ##### Methods
  - `viewDidLoad()`  
  - `loadNotifications()`  
  - `attribute(fontName: String, string: String, size: CGFloat)`  
  - `generateNewTWHCell(notification: FinalNotificationObject, cell: NewTWHTableCell)`  
  - `collectionView(... cellForItemAt indexPath: IndexPath)`  
  


### APPLICATION FLOW DIAGRAM

