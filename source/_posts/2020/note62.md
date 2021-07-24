---
title: iOS 视图的折叠和展开功能
date: 2017-07-18 11:44:07
categories:
- iOS
tags:
- iOS
- 折叠视图
---

实现视图的折叠和展开效果。


<!-- more -->

实现方法：

``` swift 
import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var container: UIView!
    @IBOutlet weak var topView: UIView!
    @IBOutlet weak var midView: UIView!
    @IBOutlet weak var bottomView: UIView!
    
    private var isFold = false
    private var viewHeight: Int = 150
    private let padding: Int = 4
    private let margin: Int = 8
    private let cornerRadius: CGFloat = 4
    private let durationTime: TimeInterval = 0.3
    private let SCREENWIDTH: Int = Int(UIScreen.main.bounds.width)
    private let SCREENHEIGHT: Int = Int(UIScreen.main.bounds.height)
    private var originMidViewFrame: CGRect!
    private var originBottomViewFrame: CGRect!
    private var originContainerViewFrame: CGRect!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        prepareView(view: topView)
        prepareView(view: midView)
        prepareView(view: bottomView)
    }
 
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        topView.frame = CGRect(x: margin, y: margin, width: SCREENWIDTH - 2 * margin, height: viewHeight)
        midView.frame = CGRect(x: margin, y: margin + viewHeight + margin, width: SCREENWIDTH - 2 * margin, height: viewHeight)
        bottomView.frame = CGRect(x: margin, y: 2 * (margin + viewHeight) + margin, width: SCREENWIDTH - 2 * margin, height: viewHeight)
        container.frame = CGRect(x: 0, y: 64, width: SCREENWIDTH, height: 3 * viewHeight + 4 * margin)
        originMidViewFrame = midView.frame
        originBottomViewFrame = bottomView.frame
        originContainerViewFrame = container.frame
        viewHeight = Int(topView.frame.height)
    }

    func prepareView(view: UIView){
        view.layer.cornerRadius = CGFloat(cornerRadius)
        view.layer.borderWidth = 1
        view.layer.borderColor = UIColor.brown.cgColor
    }
    
    func foldViews(){
        
        UIView.animate(withDuration: durationTime, animations: { 
            self.midView.frame = CGRect(x: self.margin + self.padding, y: self.margin + self.padding, width: self.SCREENWIDTH - 2 * self.margin - 2 * self.padding, height: self.viewHeight)
            self.bottomView.frame = CGRect(x: self.margin + 2 * self.padding, y: self.margin + 2 * self.padding, width: self.SCREENWIDTH - 2 * self.margin - 4 * self.padding, height: self.viewHeight)
            
            self.container.frame = CGRect(x: 0, y: 64, width: self.SCREENWIDTH, height: self.viewHeight + 2 * self.margin + 2 * self.padding)
        })
    }
    
    func unfoldViews(){
        UIView.animate(withDuration: durationTime) {

            self.midView.frame = self.originMidViewFrame
            self.bottomView.frame = self.originBottomViewFrame
            self.container.frame = self.originContainerViewFrame
        }
    }

    @IBAction func topButtonClick(_ sender: Any) {
        isFold = !isFold
        isFold ? foldViews() : unfoldViews()
    }
}
```

