# FlutterSDK
A guide on the integration of the Monnify Flutter SDK


### An Integration Guide for the Monnify Flutter SDK

With the Monnify Futter SDK, you are able to receive payments in your mobile application via:

* Card
* Bank Transfer
* USSD
* Phone Number

Outline below are the necessary steps required to integrate the Flutter SDK

1. ##### Add the latest Monnify SDK to your project
  You are to add the latest version of the Monnify Flutter sdk to the pubspec.yaml of your project
  ```flutter
  dependencies:
    monnify_payment_sdk: ^1.0.3
  ```  
  then you can run
  ```shell
  flutter pub add monnify_payment_sdk
  ```  

  Alternatively, you can run
  ```flutter
  flutter pub get monnify_payment_sdk
  ```
  

2. ##### Import the Flutter SDK
   Next you are to import the the monnify payment sdk in your code:

   ```flutter
   import 'package:monnify_payment_sdk/monnify_payment_sdk.dart';
   ```  

     
3. ##### Initialize the Flutter plugin
   You can now initialize the flutter plugin by passing your API key, Contract code and the desired environment to the initState() method

   ```flutter
   import 'package:monnify_payment_sdk/monnify_payment_sdk.dart';

   class _MyAppState extends State<MyApp> {

     ...

     late Monnify? monnify;

     @override
     void initState() {
       monnify = await Monnify.initialize(
         applicationMode: ApplicationMode.TEST,
         apiKey: 'YOUR API KEY',
         contractCode: 'YOUR CONTRACT CODE',
       );
       super.initState();
         }
     
     ...
    }
   ```

   
1. ##### Intialize the payment
   Finally, create an object of the Transaction class and pass it to the initializePayment function as shown below:
```flutter
   Future<void> initializePayment() async {
  final amount = '20.00';
    final paymentReference = 'YOUR PAYMENT REFERENCE';


    final transaction = TransactionDetails().copyWith(
      amount: amount,
      currencyCode: 'NGN',
      customerName: 'Customer Name',
      customerEmail: 'custo.mer@email.com',
      paymentReference: paymentReference,
      // metaData: {"ip": "0.0.0.0", "device": "mobile"},
      // paymentMethods: [PaymentMethod.CARD, PaymentMethod.ACCOUNT_TRANSFER, PaymentMethod.USSD],
      /*incomeSplitConfig: [SubAccountDetails("MFY_SUB_319452883968", 10.5, 500, true),
          SubAccountDetails("MFY_SUB_259811283666", 10.5, 1000, false)]*/
    );

    try {
      final response =
          await monnify?.initializePayment(transaction: transaction);
      } catch (e) { 
        // handle exceptions in here.
      }
    }
```

___
For further information, you can check out our [developer documentation](https://developers.monnify.com) and you can also join our [slack community](https://slack.monnify.com).


