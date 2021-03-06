EMAccordionTableViewController
==============================
![](https://dl.dropboxusercontent.com/u/37783784/EMAccordionTableViewController/iPhone.png)
![](https://dl.dropboxusercontent.com/u/37783784/EMAccordionTableViewController/iPad.png)

EMAccordionTableViewController is a easy to use Expandable / Collapsable UITableView for iOS. Under the hood it works as a proxy for the UITableView and leaves
to the delegate the responsability to implement tableView:cellForRowAtIndexPath and tableView:didSelectRowAtIndexPath.

* Built to be Universal
* Uses ARC (Automatic Reference Counting)
* Support iOS > 5.0
* Support rotation
* Completely reusable component

## Apps that use the controller
* [my Soldier for Battlefield 4](https://itunes.apple.com/us/app/my-soldier-for-battlefield-4/id718845676)

## How to install it?

Simply copy all the files included in the folder [EMAccordionTable](https://githubcom/ennioma/EMAccordionTableViewController/tree/master/EMAccordionTableViewController/EMAccordionTableViewController/Classes/EMAccordionTable) and start playing with it!

## How it works?
### EMAccordionTableViewController Class

```objective-c
@interface EMAccordionTableViewController : UIViewController<UITableViewDataSource, UITableViewDelegate>

@property (nonatomic, strong) UIImage * closedSectionIcon;
@property (nonatomic, strong) UIImage * openedSectionIcon;
@property (nonatomic, strong) UITableView *tableView;

- (id) initWithTable:(UITableView *)tableView;

- (void) addAccordionSection: (EMAccordionSection *) section;
- (void) setDelegate: (NSObject <EMAccordionTableDelegate> *) delegate;

- (void) setHeaderHeight:(CGFloat)height;

@end
```
    
### EMAccordionTableDelegate Protocol

```objective-c
@protocol EMAccordionTableDelegate
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath;
- (void) tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath;
@end

```

## How to use it?
### Example
    // Setup the EMAccordionTableViewController
    origin = 20.0f;
    if ([[UIDevice currentDevice].model hasPrefix:@"iPad"])
        origin = 100.0f;
  
    UITableView *tableView = [[UITableView alloc] initWithFrame:CGRectMake(origin, origin, self.view.bounds.size.width - origin*2, self.view.bounds.size.height - origin*2) style:UITableViewStylePlain];
    [tableView setSectionHeaderHeight:kTableHeaderHeight];
    /*
     ... set here some other tableView properties ...
     */
    
    // Setup the EMAccordionTableViewController
    emTV = [[EMAccordionTableViewController alloc] initWithTable:tableView];
    [emTV setDelegate:self];
    
    [emTV setClosedSectionIcon:[UIImage imageNamed:@"closedIcon"]];
    [emTV setOpenedSectionIcon:[UIImage imageNamed:@"openedIcon"]];
    
    // Setup some test data
    dataSection01 = [[NSMutableArray alloc] initWithObjects:@"Dog", @"Cat", @"Pig", nil];
    dataSection02 = [[NSMutableArray alloc] initWithObjects:@"Federer", @"Nadal", nil];
    //
    
    // Section graphics
    UIColor *sectionsColor = [UIColor colorWithRed:62.0f/255.0f green:119.0f/255.0f blue:190.0f/255.0f alpha:1.0f];
    UIColor *sectionTitleColor = [UIColor whiteColor];
    UIFont *sectionTitleFont = [UIFont fontWithName:@"Futura" size:24.0f];

    // Add the sections to the controller
    EMAccordionSection *section01 = [[EMAccordionSection alloc] init];
    [section01 setBackgroundColor:sectionsColor];
    [section01 setItems:dataSection01];
    [section01 setTitle:@"Animals"];
    [section01 setTitleFont:sectionTitleFont];
    [section01 setTitleColor:sectionTitleColor];
    [emTV addAccordionSection:section01];
    
    EMAccordionSection *section02 = [[EMAccordionSection alloc] init];
    [section02 setBackgroundColor:sectionsColor];
    [section02 setItems:dataSection02];
    [section02 setTitle:@"Tennis players"];
    [section02 setTitleColor:sectionTitleColor];
    [section01 setTitleFont:sectionTitleFont];
    [emTV addAccordionSection:section02];
    
    EMAccordionSection *section03 = [[EMAccordionSection alloc] init];
    [section03 setBackgroundColor:sectionsColor];
    [section03 setTitle:@"Buh!"];
    [section03 setTitleColor:sectionTitleColor];
    [section01 setTitleFont:sectionTitleFont];
    [emTV addAccordionSection:section03];
    
    sections = [[NSArray alloc] initWithObjects:section01, section02, section03, nil];
    
    [self.view addSubview:emTV.tableView];

## Help me improving this!
How? Simply feel free to fork the project and improve it!

If you would like to contact me:
Twitter: [ennioma](https://twitter.com/ennioma).
Email: ennio.masi@gmail.com