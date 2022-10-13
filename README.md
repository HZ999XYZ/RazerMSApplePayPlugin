<!--
 # license: Copyright © 2011-2022 Razer Merchant Services Sdn Bhd. All Rights Reserved. 
 -->

# [Mobile Plugin] - RazerMS Apple Pay Plugin

This is the complete and functional Razer Merchant Services Apple Pay Plugin payment module that is ready to be implemented into XCode application project through Cocoapods framework.

## Recommended configurations

    - Xcode version: 14 ++

    - Minimum target version: iOS 15.5

## Installation Guidance

**Installation**

### CocoaPods

CocoaPods is a dependency manager for Cocoa projects. For usage and installation instructions, visit their website. To integrate RazerMS Apple Pay Plugin into your Xcode project using CocoaPods, specify it in your Podfile:

    pod 'razerms_applepay_plugin', '~> 1.0.1'

### For Swift

    Step 1 - Add import RazerMSApplePayPlugin

    Step 2 - Declare let ap = APManager.shared

    Step 3 - Prepare payment detail object

    Step 4 - Start ApplePay payment module & callback response

## Prepare the Payment detail object

    // Mandatory String. Values obtained from Razer Merchant Services.
    ap.paymentData.setValue("", forKey: "merchantID")
    ap.paymentData.setValue("", forKey: "verifyKey")

    // Mandatory String. Payment values.
    ap.paymentData.setValue("1.10", forKey: "amount") // Minimum 1.01
    ap.paymentData.setValue("order123", forKey: "orderID")
    ap.paymentData.setValue("MYR", forKey: "currency")
    ap.paymentData.setValue("MY", forKey: "countryCode")

    // Optional, but required payment values. User input will be required when values not passed.
    ap.paymentData.setValue("", forKey: "description")
    ap.paymentData.setValue("", forKey: "billName")
    ap.paymentData.setValue("", forKey: "billEmail")
    ap.paymentData.setValue("", forKey: "billMobile")

    // Mandatory String, ApplePay config
    ap.paymentData.setValue("", forKey: "merchantIdentifier")
    ap.paymentData.setValue("SALS", forKey: "tcctype") // default value
    
## Start ApplePay payment module & callback response

    ap.startPayment(completion: { (success) -> Void in
        print(ap.resultPayment) // response from ApplePay Plugin
        if success {
            print("sucess")
        } else {
            print("failure")
        }
    })

## Payment results

    =========================================
    Sample transaction result in JSON string:
    =========================================

    {
        amount = "1.10";
        appcode = 179367;
        channel = CREDIT;
        currency = MYR;
        domain = "rmsxdk_mobile_Dev";
        orderid = order54;
        paydate = "2022-09-22 17:49:08";
        skey = 54f0a059227b1609a788cd988dd2845d;
        status = 00;
        tranID = 1278569348;
        xdkHTMLRedirection = "xxxxxxxxxx";
    };

    Parameter and meaning:
    
    "status_code" - "00" for Success, "11" for Failed, "22" for *Pending. 
    (*Pending status only applicable to cash channels only)
    "amount" - The transaction amount
    "paydate" - The transaction date
    "order_id" - The transaction order id
    "channel" - The transaction channel description
    "txn_ID" - The transaction id generated by MOLPay
    
    * Notes: You may ignore other parameters and values not stated above

    =====================================
    * Sample error result in JSON string:
    =====================================
    
    {
        "error_code" = A01;
        "error_desc" = "Fail to detokenize Apple Pay Token given";
        status = 0;
    }
    
    Parameter and meaning:
    
    "Fail to detokenize Apple Pay Token given" - Error starting a payment process due to several possible reasons, please contact Razer Merchant Services support should the error persists.
    1) Misconfigure ApplePay setup
    2) API credentials (username, password, merchant id, verify key)
    3) Razer Merchant Services server offline.

## Resources

- GitHub:     https://github.com/RazerMS
- Website:    https://merchant.razer.com/
- Twitter:    https://twitter.com/Razer_MS
- YouTube:    https://www.youtube.com/c/RazerMerchantServices
- Facebook:   https://www.facebook.com/RazerMerchantServices/
- Instagram:  https://www.instagram.com/RazerMerchantServices/


## Support

Submit issue to this repository or email to our support-sa@razer.com

Merchant Technical Support / Customer Care : suppor-sa@razer.com<br>
Sales/Reseller Enquiry : sales-sa@razer<br>
Marketing Campaign : marketing-sa@razer<br>
Channel/Partner Enquiry : channel-sa@razer<br>
Media Contact : media-sa@razer.com<br>
R&D and Tech-related Suggestion : technical-sa@razer.com<br>
Abuse Reporting : abuse-sa@razer.com
