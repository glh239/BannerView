
![image](https://github.com/glh239/GLHBannerView/blob/master/动图1.gif)
![image](https://github.com/glh239/GLHBannerView/blob/master/动图2.gif)
# GLHBannerView
tableview顶部视图无限自动滚动  下拉可放大

ViewController中

- (void)viewDidLoad {

    [super viewDidLoad];
    
    [self.view addSubview:self.tableView];
    
    NSString *imageStr = @"图片1,图片2,图片3";
//banner设置图片源
   
   [self.bannerView setBannerImageArray:imageStr];

}


-(void)scrollViewDidScroll:(UIScrollView *)scrollView{

   
   
   if (scrollView == _tableView) {
       
       CGPoint offset = scrollView.contentOffset;
        //下拉放大实现
       
       if (offset.y < 0) {
            [self.bannerView setOffSetY:offset.y];
        }else{
            [self.bannerView setOffSetY:0];
        }
   
   }

}



//bannerView中的实现


-(void)setOffSetY:(CGFloat)offSetY{
  
 if (offSetY == 0) {
 
        [_timer setFireDate:[NSDate dateWithTimeIntervalSinceNow:4.0]];
    }else{
    
        [_timer setFireDate:[NSDate distantFuture]];
    }
    
   CGFloat X =  _index * offSetY;
   
    CGFloat Y = offSetY;
    
    CGFloat W = self.frame.size.width - offSetY;
    
    CGFloat H = self.frame.size.height - offSetY;
    
    _headerView.frame = CGRectMake(0, Y / 2, W, H);
   
   
   if (_imageUrlArray.count > 1) {
   
        NSInteger  nextIndex  = _pageCtrl.currentPage + 2;
        if (nextIndex == _imageUrlArray.count)
        {
            nextIndex = 2;
        }
        _bannerScrollView.bounds = CGRectMake((nextIndex - 1) * W, 0, W, H);
        _pageCtrl.currentPage = _index;
    }else{
    
        _bannerScrollView.bounds = CGRectMake(0, 0, W, H);
    }
}

具体代码请下载附件查看
