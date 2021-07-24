---
title: ios 本地生成数字验证码
date: 2017-07-20 10:14:24
categories:
- iOS
tags:
- iOS
- 数字验证码
---
一个简单的数字验证码生成器。

<!-- more -->

代码如下：

``` swift

import UIKit

class CCYVerifyPicView: UIView {
    
    var verifyCode: String = ""
    
    private var bgView: UIView!
    private var array = ["0","1","2","3","4","5","6","7","8","9","0"]
    private var fontSizeArray: Array<CGFloat> = [14, 16, 18, 20, 22]
    private var randCode = [String]()
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
    }
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        backgroundColor = UIColor.clear
        createRandomCode()
    }
    
    func createRandomCode(){
        
        clearData()
        
        for _ in 0...3 {
            randCode.append(array[Int(arc4random() % UInt32(array.count))])
        }
        
        createBgView()
        createVerifyCode()
        createVerifyPic()
    }
    
    private func clearData(){
        for view in subviews {
            view.removeFromSuperview()
        }
        randCode.removeAll()
        verifyCode = ""
    }
    
    private func createBgView(){
        bgView = UIView(frame: bounds)
        bgView.backgroundColor = randomColor()
        bgView.layer.cornerRadius = 4
        addSubview(bgView)
    }
    
    private func createVerifyCode(){
        for str in randCode {
            verifyCode += str
        }
    }
    
    private func createVerifyPic(){
        for (index, str) in randCode.enumerated() {
            let label = UILabel(frame: CGRect(x: index * 20 + 8, y: Int(0 + arc4random() % 12), width: 20, height: 20))
            label.text = str
            label.textAlignment = .center
            label.font = UIFont.systemFont(ofSize: fontSizeArray[Int(arc4random() % UInt32(fontSizeArray.count))])
            label.textColor = randomColor()
            bgView.addSubview(label)
        }
    }
    
    private func randomColor() -> UIColor {
        return UIColor.init(red: CGFloat(arc4random() % 256) / 255.0, green: CGFloat(arc4random() % 256) / 255.0, blue: CGFloat(arc4random() % 256) / 255.0, alpha: 1.0)
    }
}



```

使用方法：

``` swift
import UIKit

class ViewController: UIViewController {
    
    var verifyView: CCYVerifyPicView!
    @IBOutlet weak var textField: UITextField!

    override func viewDidLoad() {
        super.viewDidLoad()
        verifyView = CCYVerifyPicView(frame: CGRect(x: 20, y: 30, width: 96, height: 34))
        view.addSubview(verifyView)
    }
    
    @IBAction func resetVerifyCode(_ sender: Any) {
        verifyView.createRandomCode()
    }

    @IBAction func comfirm(_ sender: Any) {
        textField.text == verifyView.verifyCode ? alertMessage(message: "验证成功") : alertMessage(message: "验证失败")
    }
    
    func alertMessage(message: String){
        let controller = UIAlertController(title: message, message: nil, preferredStyle: .alert)
        controller.addAction(UIAlertAction(title: "OK", style: .default, handler: nil))
        present(controller, animated: true, completion: nil)
    }
}
```