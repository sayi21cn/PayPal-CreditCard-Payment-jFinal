Paypal-jfinal
=============
This is a very simple demo[SDK] for PayPal with **Credit Card Payment Only**.   
[[jFinal](https://github.com/jfinal/jfinal) is a light, powerful Java framework]

<h3>How to setup?</h3>
1. Get a PayPal Account   
2. Create an App in https://developer.paypal.com/, then you can get `REST API CREDENTIALS`    ![](docs/img/clientID.png)
3. Update [`sdk_config.properties`](src/main/resources/sdk_config.properties)

<h3>How to run?</h3>
1. Import this project into your Eclipse
2. Naviage to [`MyConfig.java`](src/main/java/me/hzhou/paypal/config/MyConfig.java)
```
public static void main(String[] args) {
	JFinal.start("src/main/webapp", 80, "/", 5);
}
```	
3. Run this as *Java Application*

<h3>Unit Test</h3>
I provide a usage demo in [Unit test](src/main/java/me/hzhou/paypal/test/UnitTest.java)
```
	@Test
	public void paymentTest() {
		PayPal paypal = new PayPal();
		paypal.setBillAddress("52 N Main ST", "Johnstown", "US", "OH", "43210");
		
		// Never mind, this is a fake information from PayPal Developer Center
		// sorry
		paypal.setCreditCard("4417119669820331", "visa", 11, 2018, "874", "Joe", "Shopper");
		
		// 1.50 doesn't include tax
		paypal.setAmount(1.50);
		
		// output details as
		/*{
		  "shipping": "0",
		  "subtotal": "1.50",
		  "tax": "0.09"
		}
		*/
		System.out.println(paypal.getDetails().toJSON());
		
		Payment payment = paypal.pay();
		System.out.println(payment.toJSON());
		
	}
```
!["Result"](docs/img/test_result.png "Result")
Issues:
====
1. You may not eligible for Accepting payments from customers directly using their credit cards on your web or mobile app in prodcution [Direct credit cards].
!["Direct credit cards"](docs/img/cannot_get_paid_by_CC.png "Direct credit cards")

<h3>Contact me</h3>
Feel free to contact me about any question: royhzhou@gmail.com