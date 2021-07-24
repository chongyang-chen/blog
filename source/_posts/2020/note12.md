---
title: 实现APP首页
date: 2017-06-23 16:55:12
categories:
- iOS
tags:
- iOS
- code
---

实现APP首页功能

代码如下：

<!-- more -->

```swift
    override func viewWillAppear(_ animated: Bool) {
        self.navigationController?.navigationBar.isHidden = true
    }
    
    var selectedButton: UIButton! {
        willSet{
            newValue.setTitleColor(UIColor.brown, for: .normal)
            newValue.titleLabel?.font = UIFont.systemFont(ofSize: 14)
        }
        
        didSet{
            if oldValue != nil && oldValue != selectedButton {
                oldValue.setTitleColor(UIColor.darkText, for: .normal)
                oldValue.titleLabel?.font = UIFont.systemFont(ofSize: 14)
            }
        }
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        let leftView = UIImageView(frame: CGRect(x: 0, y: 0, width: 24, height: 24))
        leftView.image = UIImage(named: "003.png")
        searchTF.leftView = leftView
        searchTF.delegate = self
        searchTF.leftViewMode = .always

        createTopButtonsView()
    }
    
    func createTopButtonsView(){
        
        for (index, title) in titles.enumerated() {
            let button = buttonWithFrame(CGRect(x: 0 + index * buttonWidth, y: 0, width: buttonWidth, height: buttonHeight), title: title)
            topScrollView.addSubview(button)
            button.tag = index + 200
            button.addTarget(self, action: #selector(topButtonClicked(sender:)), for: .touchUpInside)
            if index == 0 {
                selectedButton = button
            }
        }
        topScrollView.contentSize = CGSize(width: buttonWidth * titles.count, height: buttonHeight)
        topScrollView.showsHorizontalScrollIndicator = false
        createSliderView()
    }
    
    func buttonWithFrame(_ frame: CGRect, title: String) -> UIButton {
        
        let button = UIButton(frame: frame)
        button.setTitle(title, for: .normal)
        button.setTitleColor(UIColor.darkText, for: .normal)
        button.titleLabel?.font = UIFont.systemFont(ofSize: 14)
        return button
    }
    
    func createSliderView(){
        
        sliderView = UIView(frame: CGRect(x: (buttonWidth - sliderViewWidth) / 2 - 2, y: 30, width: sliderViewWidth, height: sliderViewHeight))
        sliderView.backgroundColor = UIColor.brown
        topScrollView.addSubview(sliderView)
    }
    

    
    func topButtonClicked(sender: UIButton){
        
        selectedButton = sender
        
        let originX = (sender.tag - 200) * buttonWidth + (buttonWidth - sliderViewWidth) / 2 - 2
        updateSliderViewPosition(originX: originX)
        
        let contentOffsetX = originX - (Int(view.bounds.width) - buttonWidth) / 2
        centerSelectedButton(contentOffsetX: contentOffsetX)
    }
    
    func updateSliderViewPosition(originX: Int){
        
        UIView.animate(withDuration: 0.3) {
            self.sliderView.frame.origin = CGPoint(x: originX, y: 30)
        }
    }
    
    
    func centerSelectedButton(contentOffsetX : Int) {
        
        var offSetX = contentOffsetX
        let maxScrollContentOffsetX = titles.count * buttonWidth - Int(view.bounds.width)
        let minScrollContentOffsetX = 0
        offSetX = offSetX < minScrollContentOffsetX ? minScrollContentOffsetX : offSetX
        offSetX = offSetX > maxScrollContentOffsetX ? maxScrollContentOffsetX : offSetX
        
        topScrollView.setContentOffset(CGPoint(x: offSetX, y: 0), animated: true)
    }
```



