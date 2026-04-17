```cs
class Container
{
	private readonly CartService _cartService;
	private readonly IPaymentService _paymentService;
	
	public Container()
	{}
	
	public CartService CartService => _cartService ?? (_cartService = new CartService());
	public IPaymentService PaymentService => _paymentService ?? (_paymentService = new PaymentService());
}
```

```cs
var container = new Container();
container.CartService.GetCartItems();
container.PaymentService.GetPaymentMethods();
```