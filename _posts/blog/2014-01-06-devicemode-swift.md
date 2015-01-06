---
layout: post
category : blog
title: iOS Device Model Name By Swift
tagline: "2014-01-06"
tags : [swift, device,model,name]
---
import UIKit

extension UIDevice{

    class func machineModel() -> String{
        let name = UnsafeMutablePointer<utsname>.alloc(1)
        uname(name)
        let machine = withUnsafePointer(&name.memory.machine, { (ptr) -> String? in
            let int8Ptr = unsafeBitCast(ptr, UnsafePointer<CChar>.self)
            return String.fromCString(int8Ptr)
        })
        name.dealloc(1)
        return machine!
    }
    
    func machineModelName() -> String{
        let machineModel = UIDevice.machineModel()
        let machineModelDic = [
            //iPhone
            "iPhone1,1":"iPhone 1G",
            "iPhone1,2":"iPhone 3G",
            "iPhone2,1":"iPhone 3GS",
            "iPhone3,1":"iPhone 4(GSM)",
            "iPhone3,2":"Verizon iPhone 4",
            "iPhone3,3":"iPhone 4(CDMA)",
            "iPhone4,1":"iPhone 4S",
            "iPhone5,1":"iPhone 5",
            "iPhone5,2":"iPhone 5",
            "iPhone5,3":"iPhone 5C",
            "iPhone5,4":"iPhone 5C",
            "iPhone6,1":"iPhone 5S",
            "iPhone6,2":"iPhone 5S",
            "iPhone7,1":"iPhone 6 Plus",
            "iPhone7,2":"iPhone 6",
            //iPod
            "iPod1,1":"iPod Touch 1G",
            "iPod2,1":"iPod Touch 2G",
            "iPod3,1":"iPod Touch 3G",
            "iPod4,1":"iPod Touch 4G",
            "iPod5,1":"iPod Touch 5G",
            //iPad
            "iPad1,1":"iPad 1",
            "iPad2,1":"iPad 2(Wifi)",
            "iPad2,2":"iPad 2(GSM)",
            "iPad2,3":"iPad 2(CDMA)",
            "iPad2,4":"iPad 2",
            "iPad2,5":"iPad mini 1G",
            "iPad2,6":"iPad mini 1G",
            "iPad2,7":"iPad mini 1G",
            "iPad3,1":"iPad 3 (Wifi)",
            "iPad3,2":"iPad 3 (4G)",
            "iPad3,3":"iPad 3 (4G)",
            "iPad3,4":"iPad 4",
            "iPad3,5":"iPad 4",
            "iPad3,6":"iPad 4",
            "iPad4,1":"iPad air",
            "iPad4,2":"iPad air",
            "iPad4,3":"iPad air",
            "iPad4,4":"iPad mini 2G",
            "iPad4,5":"iPad mini 2G",
            //Simulator
            "i386":"Simulator",
            "x86_64":"Simulator"
        ]
        var modelName = machineModelDic[machineModel]
        if modelName == nil{
            modelName = machineModel
        }
        return modelName!
     }
}