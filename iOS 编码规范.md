# iOS 编码规范

> 2019.01.02，该文档为纯编码规范，大部分是统一编码习惯，并不会涉及到代码规则：比如 NSInteger 替代 Int，NSArray 作为属性需要用 copy 关键字等。

###核心原则

1. 使用 US 英语命名（类，方法，宏，ImageSet，Localizable.string，配置，#pragma mark）。

   ```objective-c
   Colour，YanSe，颜色 //不建议(英式英语，拼音，中文)
   Color //推荐
   
   #pragma mark - 懒加载 //不建议
   #pragma mark - Property Method //推荐
   ```


2. 代码易懂，逻辑清晰。清晰永远比简洁更重要。

   ```objective-c
   insertObject:at: //不建议
   insertObject:atIndex: //推荐
   
   setBGColor: //不建议
   setBackgroundColor:  //推荐
   
   [button setTitle:@"title" forState:0]; //不建议
   [button setTitle:@"title" forState:UIControlStateNormal]; //推荐
   
   result = a > b ? x = c > d ? c : d : y; //不建议(多个表达式嵌套)
   //推荐
   x = c > d ? c : d;
   result = a > b ? x : y; 
   ```

3. 严格遵守项目架构各层的职责划分



### 命名规范

1. 遵从驼峰命名法

   - 变量
      ```objective-c
      NSUInteger Index = 2; //不建议
      NSUInteger index = 2; //推荐
      ```
   - 方法

     ```objective-c
     + (void)ResetStandardUserDefaults; //不建议
     + (void)resetStandardUserDefaults; //推荐
     ```

   - 类
     ```objective-c
     @interface myCouponVC () //不建议(首字母没有大写，且没有前缀)
     @interface RGMyCouponVC () //推荐
     ```

   - 常量
     ```objective-c
     static NSString * const CouponCellID = @"CouponCell"; //不建议
     static NSString * const kCouponCellID = @"kCouponCellID"; //推荐
     ```

   - 宏
     ```objective-c
     //常量宏
     #define useLocalhost 0 //不建议
     #define kUseLocalhost 0 //推荐

     //操作宏
     #define NullFilterString(s) //不建议
     s#define RGNullFilterString(s) //推荐
     ```

2. 全局/局部变量不应该包含下划线

    ```objective-c
    BOOL  _isAddToCartNeedPopConfirm; //不建议
    BOOL  isAddToCartNeedPopConfirm; //推荐
    ```

3. 前缀
    - 前缀以全大写命名。比如 RG；
    - 类、分类、协议、操作宏、枚举使用前缀，但不要为成员变量，方法使用前缀；
    - 命名前缀不要与 Cocoa 框架与第三方组件冲突。

4. 不要使用 “and” 和 “width” 来连接参数

    ```objective-c
    initWithTitle:withImage:andColor: //不建议
    initWithTitle:image:color: //推荐
    ```

5. 组件名称不建议缩写

    ```objective-c
    //不建议
    UILabel * name;
    UIViewController * homeVC;
    UICollectionViewCell * productCCell; //TODO:待定
    
    //推荐
    UILabel * nameLabel;
    UIViewController * homeViewController;
    ```

6. 常用缩写

| 类型             | 缩写           |
| :--------------- | -------------- |
| Dictionary       | Dict           |
| Bool             | isXXXX/canXXXX |
| UITableViewCell  | Cell           |
| UICollectionCell | CCell          |
| Calculate        | calc           |
| Information      | info           |
| Initialize       | init           |
| Integer          | int            |
| Maximum          | max            |
| Minimum          | min            |
| Message          | msg            |
| Temporary        | temp           |
|                  |                |
|                  |                |
|                  |                |



###通用规范

1. 大括号

- 开始于行尾，结束于行首，包括 `Method`，`if`，`else`，`switch`，`while` 等；
  ```objective-c
  //不建议
  if (condition)
  {
   	...   
  }
  //推荐
  if (condition){
      ...
  }
  ```

- 所有流程控制语句必须加上括号，即使只要一行。

  ```objective-c
  //不建议
  if (condition) ... else ...   
  //推荐
  if (condition) {
      ...
  }else {
      ...
  }
  ```



2. 代码长度

   - 一个方法内部最多五十行，如果超过就精简代码。方便之后进行热修复和代码重构。

   - 每行**代码长度**不超过 **80** Column

       ```objective-c
       //不建议
       [self.contentLabel.text boundingRectWithSize:CGSizeMake(MAXFLOAT,MAXFLOAT) options:NSStringDrawingUsesLineFragmentOrigin | NSStringDrawingUsesFontLeading attributes:@{NSFontAttributeName:self.contentLabel.font} context:nil];
       
       //推荐
       NSDictionary * attributes = @{NSFontAttributeName:self.contentLabel.font};
       NSStringDrawingOptions options = NSStringDrawingUsesLineFragmentOrigin | NSStringDrawingUsesFontLeading;
       CGSize size = CGSizeMake(MAXFLOAT,MAXFLOAT);
       //冒号对齐(Block 除外)
       [self.contentLabel.text boundingRectWithSize:size
                                            options:options
                                         attributes:attributes
                                            context:nil];
       //推荐
       NSArray *array = @[
                          @"This",
                          @"is",
                          @"an",
                          @"array"
                          ];
       ```
       > Xcode -> Preferences -> Text Editing -> Page guide at column: **80**

3. 语句中留有合适的空格

   - 类方法和实例方法的 “+” 和 “-” 需要留一个空格

     ```objective-c
     //不建议
     +(void)resetStandardUserDefaults;
     //推荐
     + (void)resetStandardUserDefaults;
     ```

   - 运算符之间留有空格

     ```objective-c
     //不建议
     NSString * title=self.isViewLoaded?@"title":@"loading";
     //推荐
     NSString * title = self.isViewLoaded ? @"title" : @"loading";
     ```

   - 方法调用之间留有空格

     ```objective-c
     //不建议
     [[NSUserDefaults standardUserDefaults]objectForKey:@"name"];
     //推荐
     [[NSUserDefaults standardUserDefaults] objectForKey:@"name"];
     ```


4. @Class

   ```objective-c
   //不建议
   @class UIView, UINavigationItem, UIBarButtonItem, UITabBarItem, UISearchDisplayController;
   
   //推荐
   @class UIView;
   @class UINavigationItem, UIBarButtonItem, UITabBarItem;
   @class UISearchDisplayController;
   ```

5. @property

   ```objective-c
   //不建议
   @property(readonly, copy, nullable, nonatomic) NSString *nibName;
   
   //推荐(保证特性关键字顺序一致)
   @property(nullable, nonatomic, readonly, copy) NSString *nibName;
   ```


6. .h 文件

   ```objective-c
   //不建议
   @property(nullable, nonatomic, readonly, copy) NSString *nibName;
   @property(nullable, nonatomic, readonly, strong) NSBundle *nibBundle;
   //TODO: 暂未想好
   
   ```



7. 变量

   - 尽量用变量，取代属性

     ```objective-c
     //TODO:待定
     @interface ViewController (){
         UILabel * nameLabel;
     }
     @property (nonatomic, strong) UIView * nameLabel;
     @end
     ```

   - 变量定义的位置

     ```objective-c
     //TODO:待定
     @interface ViewController (){
         UILabel * nameLabel;
     }
     @end
     
     @implementation ViewController{
         UILabel * nameLabel;
     }
     @end
     ```

8. 布尔值

   - OC 使用 YES 和 NO

   - nil 会解析成 NO

     ```objective-c
     //不建议
     if (obj == nil) {}
     //推荐
     if (obj) {}
     ```

   - 不要拿变量跟 YES 和 NO 比较

     ```objective-c
     //不建议
     if (isAwesome == YES) {}
     //推荐
     if (isAwesome) {}
     ```

9. Init 方法，应该遵循 Apple 生成代码模板的命名规则。应该使用 instancetype，而不是 id。

   ```objective-c
   //不建议
   - (id)init {}
   //推荐
   
   ```

10. 使用 `NS_ENUM` 替代 `enum`，`NS_ENUM` 不要全部写在一个文件里面。

   ```objective-c
   //不建议
   typedef enum PathPHPTypes{
       PathPHPTypeNone,
       PathPHPTypeCommand,
       PathPHPTypeUser
   }PathPHPType;
   
   //推荐
   typedef NS_ENUM(NSUInteger, PathPHPTypes){
       PathPHPTypeNone = 0,
       PathPHPTypeCommand,
       PathPHPTypeUser
   };
   ```


8. 分类，使用 NSString+Cateogry 替换 NSStringUtils。

9. \#import 的顺序

      ```objective-c
      //模板
      #import <系统库>
      #import <第三方库>
      #import "其它类"
      
      //不建议
      #import "RGModel.h"
      #import <UIKit/UIKit.h>
      #import <Google/Analytics.h>
      
      //推荐
      #import <UIKit/UIKit.h>
      #import <Google/Analytics.h>
      #import "RGModel.h"
      ```




###代码组织

1. 生命周期

   ```objective-c
   #pragma mark - Life Cycle
   - (instancetype)init;
   - (void)dealloc {}
   - (void)viewDidLoad {}
   - (void)viewWillAppear:(BOOL)animated {}
   - (void)viewDidLayoutSubviews {}
   - (void)didReceiveMemoryWarning {}
   ```

3. 协议实现

   ```objective-c
   #pragma mark - NSCopying
   + (id)copyWithZone:(struct _NSZone *)zone
       
   #pragma mark - NSObject    
   - (BOOL)isEqual:(id)object;
   
   #pragma mark - UITableViewDelegate
   #pragma mark - WKNavigationDelegate
   #pragma mark - YYModel
   ```

4. 事件处理（UIContol Action，Notification，KVO，UIGestureRecognizer）

   ```objective-c
   #pragma mark - UIControl Action
   -(void)submitAction:(id)sender {}
   
   #pragma mark - Notification Action
   - (void)userSignOutAction:(NSNotification *)notification {}
   
   #pragma mark - Touch Action
   - (void)touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {}
   ```


4. 私有方法，#pragma mark - Private Method

5. 公共方法，#pragma mark - Public Method

6. 属性方法（Getter and Setters）

   ```objective-c
   #pragma mark - Property Method
   - (UILabel *)centerLabel {
       if (!_centerLabel) {
           _centerLabel = [UILabel new];
       }
       return _centerLabel;
   }
   ```



### 注释

1. .h 文件建议所有的公共属性，方法，变量都必须加上注释；

2. protocol 必须加上注释；

3. 属性或变量有默认值，必须要注明；

4. Block 和 方法注释必须注明其主要用途，参数和返回值必须也要注明。

   ```objective-c
   //不建议
   //Note that NSArray objects are not like C arrays...
   
   //推荐
   /**
   Note that NSArray objects are not like C arrays...
    
    @param anObject <#anObject description#>
    @param index <#index description#>
    @return <#return value description#>
    */
   - (NSUInteger)insertObject:(ObjectType)anObject atIndex:(NSUInteger)index;
   ```

   > 快捷键：alt + command + / 自动生成上述注释模板

