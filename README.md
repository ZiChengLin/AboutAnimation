# AboutAnimation
使用代码实现动画、block块实现动画（常用）

/*******************不要犯困哦😂*********************/

//
//  ViewController.h
//  Lesson-UI0612
//
//  Created by 林梓成 on 15/6/12.
//  Copyright (c) 2015年 lin. All rights reserved.
//

#import <UIKit/UIKit.h>

@interface ViewController : UIViewController

@property (weak, nonatomic) IBOutlet UIView *toView;
- (IBAction)doButton1:(id)sender;
- (IBAction)doButton2:(id)sender;
- (IBAction)doButton3:(id)sender;
- 
@end


//
//  ViewController.m
//  Lesson-UI0612
//
//  Created by 林梓成 on 15/6/12.
//  Copyright (c) 2015年 lin. All rights reserved.
//

#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

#pragma mark 使用代码实现动画
- (IBAction)doButton1:(id)sender {
    
    // 开始动画 (动画名称和传值的内容)
    [UIView beginAnimations:nil context:nil];
    // 设置动画持续的时间
    [UIView setAnimationDuration:3];
    // 动画曲线 (先快后慢EaseInOut)
    [UIView setAnimationCurve:UIViewAnimationCurveEaseInOut];
    // 设置动画延迟的方法
    [UIView setAnimationDelay:2];
    // 位置移动
    [self.myView setCenter:CGPointMake(180, 400)];
    // 颜色改变 alpha值改变
    self.myView.backgroundColor = [UIColor redColor];
    self.myView.alpha = 0.2;
    /*
        
      常用做动画效果的属性还有 alpha frame bounds
      只要可以改变的属性都可以做动画
    */
    
    // 设置动画代理
    [UIView setAnimationDelegate:self];
    // 设置动画结束时执行的方法
    [UIView setAnimationDidStopSelector:@selector(doStop)];

    
    // 执行动画
    [UIView commitAnimations];
}

- (void)doStop {
    
    // 在动画结束时可以开启另外一个动画 达到两个动画衔接的效果
    [UIView beginAnimations:nil context:nil];
    [UIView setAnimationDuration:2];
    [self.myView setCenter:CGPointMake(180, 100)];
    [UIView commitAnimations];
}

#pragma mark 使用block块实现动画

- (IBAction)doButton2:(id)sender {
    
    // 使用动画块实现动画效果
    
/*
    // 第一种方法（弊 只能实现一个动画）
    [UIView animateWithDuration:3 animations:^{
        
        self.myView.center = CGPointMake(180, 400);
    }];
*/
    
/*
    // 第二种方法
    [UIView animateWithDuration:3 animations:^{
        
        self.myView.center = CGPointMake(180, 400);

    } completion:^(BOOL finished) {
        
        self.myView.center = CGPointMake(180, 100);

    }];
*/
    
    // 第三种方法（常用）
    [UIView animateWithDuration:3 delay:1 options:UIViewAnimationOptionCurveEaseInOut animations:^{
        
        self.myView.center = CGPointMake(180, 400);
        
    } completion:^(BOOL finished) {   // 动画执行结束时执行的代码
       
        [UIView beginAnimations:nil context:nil];
        [UIView setAnimationDuration:2];
        self.myView.center = CGPointMake(180, 100);
        self.myView.backgroundColor = [UIColor yellowColor];
        [UIView commitAnimations];
    }];
    
    
}

- (IBAction)doButton3:(id)sender {
    
    // 系统的动画效果（该方法是myView和toView的父视图执行动画 将myView移动到toView）
    [UIView transitionFromView:self.myView toView:self.toView duration:2 options:UIViewAnimationOptionTransitionFlipFromRight completion:nil];
    
    
}
@end
