---
title: iOS 调用系统相册 相机获取图片
date: 2017-07-18 13:59:40
categories:
- iOS
tags:
- iOS
- 调用相册
---


实现调用系统相册，相机获取图片功能。
<!-- more -->


``` swift
/*调用系统相册，相机获取图片信息
 *1、首先，swift3.0中调用相机和相册会导致崩溃，需要在info.plist文件中加入两个键值对，如下：
 *
 * Privacy - Photo Library Usage Description  和 Privacy - Camera Usage Description ，都是String类型，内容任意的字符串即可。
 *
 */

import UIKit

//选择图片成功后，调用该代理方法获取图片信息
protocol CCYAcquireImageDelegate {
    func imagePickerDidSelectedImage(imagePick: CCYAcquireImage, didFinishPickingMediaWithInfo info: [String : Any])
}

class CCYAcquireImage:NSObject, UINavigationControllerDelegate{
    
    //设置代理对象
    var delegate: CCYAcquireImageDelegate!
    //设置视图控制器对象
    var viewController: UIViewController!
    //弹出ActionSheet ，让用户选择图片来源：相机或相册
    public func showImagePick() {
        let alertview = UIAlertController(title: nil, message: nil, preferredStyle: .actionSheet)
        let cancelAction = UIAlertAction(title: "取消", style: UIAlertActionStyle.destructive, handler:nil)
        let action1 = UIAlertAction(title: "相册", style: UIAlertActionStyle.default) {
            (action: UIAlertAction!) -> Void in
            self.openAlbum()
        }
        let action2 = UIAlertAction(title: "拍照", style: UIAlertActionStyle.default) {
            (action: UIAlertAction!) -> Void in
            self.openCamera()
        }
        alertview.addAction(action1)
        alertview.addAction(action2)
        alertview.addAction(cancelAction)
        viewController.present(alertview, animated: true, completion: nil)
    }
    
    private func openAlbum(){
        if UIImagePickerController.isSourceTypeAvailable(.photoLibrary){
            let picker = UIImagePickerController()
            picker.delegate = self
            picker.sourceType = UIImagePickerControllerSourceType.photoLibrary
            picker.allowsEditing = false
            viewController.present(picker, animated: true, completion: nil)
        }else{
            //此处可做优化，弹出提示框提示用户错误
            print("读取相册错误")
        }
    }
    
    private func openCamera(){
        if UIImagePickerController.isSourceTypeAvailable(.camera){
            let picker = UIImagePickerController()
            picker.delegate = self
            picker.sourceType = UIImagePickerControllerSourceType.camera
            picker.allowsEditing = false
            viewController.present(picker, animated: true, completion: nil)
        }else{
            //此处可做优化，弹出提示框提示用户错误
            print("找不到相机")
        }
    }
    
}
//MARK: - UIImagePickerControllerDelegate
extension CCYAcquireImage: UIImagePickerControllerDelegate{
    //系统的代理方法返回图片信息，将图片信息传递给自身代理对象，根据需要可对图片进行相应的处理，
    func imagePickerController(_ picker: UIImagePickerController, didFinishPickingMediaWithInfo info: [String : Any]) {
        self.delegate.imagePickerDidSelectedImage(imagePick: self, didFinishPickingMediaWithInfo: info)
        self.viewController.dismiss(animated: true, completion: nil)
    }
}


```

### 使用方法，将 CCYAcquireImage.swift 文件导入项目。

``` swift
//
//  ViewController.swift
//  CameraDemo
//
//  Created by adults on 2017/7/18.
//  Copyright © 2017年 adults. All rights reserved.
//

import UIKit

class ViewController: UIViewController, CCYAcquireImageDelegate{

    @IBOutlet weak var imageView: UIImageView!
    
    var acquireImage: CCYAcquireImage!

    override func viewDidLoad() {
        super.viewDidLoad()
        acquireImage = CCYAcquireImage()
        acquireImage.delegate = self
        acquireImage.viewController = self
    }

    @IBAction func selectImage(_ sender: Any) {
        acquireImage.showImagePick()
    }
    
    //MARK:- CCYAcquireImageDelegate
    func imagePickerDidSelectedImage(imagePick: CCYAcquireImage, didFinishPickingMediaWithInfo info: [String : Any]) {
        //获取选择的原图
        let image = info[UIImagePickerControllerOriginalImage] as! UIImage
        imageView.image = image
        
    }
}
```