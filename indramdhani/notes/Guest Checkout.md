# Guest Checkout
## Notes

-   Guest checkout is a feature that allows the customer to directly checkout their shopping item without creating an account on the site.
-   user data should not be used for:
    -   email remarketing

### Guest checkout pros

-   reduce customer's account fatigue that can increase abandonment rates
-   relatively easier for mobile users
-   reduce blocker on checkout process / faster checkout process
-   it makes checkout seem like less work
-   still can provide a registration option
-   easyness of repeat purchases
-   order history tracking

### Guest checkout cons

-   difficulty reviewing, modifying or tracking orders
-   the inability to easily reorder products
-   a manual vs automatic processes needed for returns, exchanges or refund/credits
-   the inability to link a customer's order history/loyalty with other programs where accounts are necessary
-   customer service finding it time-consuming or difficult to assist shoppers with their orders

### Things to check before implementing guest checkout

-   Consider how often your customers are likely to shop with you. This will be related with
    
    -   customer loyalty
    -   repeated order (monthly order vs annual order)
    
    Guest checkout will be beneficial to those who are least likely to have frequent order from the same customers.
    
-   Think about whether or not reorders are likely
    
-   Returns, exchanges, and refunds are a hassle without an account
    
    -   frequency of items returns / refunds
-   Accounts are multi-purpose: consider the needs for memberships ...
    
-   Guest checkout is a great fit for some stores, but not for others
    

### Example

-   [Lowe's](https://www.lowes.com/)
-   [Bellroy](https://bellroy.com/checkout)
-   [Nixon](https://www.nixon.com/us/en/checkout)
-   [Nike](https://www.nike.com/sg/)
-   [Urban Outfitters](https://sg.urbanoutfitters.com/)
-   [asos](https://asos.com)

### Payment alternatives that support address collection

-   visa checkout
-   google pay
-   paypal
-   apple pay

---

## To Consider if Paperlust will apply guest checkout

-   Guest checkout is safe as long as Paperlust does not provide un-needed data to customer.
-   Don't use user-provided data for non-order related email communication ( remarketing email ).
-   Paperlust cannot offer full guest checkout since, after the purchase/payment process, customised product Paperlust still need to contact the customer for the next order process ( approval ).
-   If Paperlust is going to offer a guest checkout
    -   Need to provide a page/function where customer able to access their order stage ( approval stage, address manager stage) without login until the order stage is completed.
        
    -   Need to update on how to save user temporary data since several pages like my saved design will be accessible without login.
        
    -   Customer who re order should be treated as different customer.
        
        -   Update customer email to be anonymous in order to treat returning customer as new customer without losing track of order data.
        
        OR
        
        -   Create an order log table that is not connected to any database table to retain order data.
-   Another consideration / option
    -   Add more beneficial information why customer need to have an account.
        -   convince customer that registration process is worth their time
        -   provide incentive/promotional code.
    -   Add `Save detail for later` action as a change of register.
        -   simplified version on register form, e.g only email field.
        -   password is auto generated and send to email.
    -   **Add option to create a user based on the payment data (billing/shipping data ) / Fake Guest Checkout.**
        -   add tickbox/callout on the payment data that inform the customer that they will have an account after the payment process.
        -   add benefit / incentive for customer who create an account.
        -   password is auto-generated and sends to email OR we can provide a single link to direct login.
        -   (optional) customer should be excluded from remarketing email
    -   Adding more social login register to reduce register blocker.
        -   let's use the social login plugin if it is available to reduce the stress of managing permission.
    -   Adding more payment method as alternatives, and get the address information from the payment gateway ( apple, google and PayPal should have this ).
        -   may need to update the current payment alternative integration.
    -   Only enable guest checkout for simple product or non customised product.
        -   since we will not need to contact customer again for approval process etc,
        -   the payment process would be similar like get sample action.

### [Diagram](http://url.kraftha.us/pl-diagram-guest-checkout)

-   **Fake Guest with user creation on payment page**
-   **Fake Guest with user creation on save design process**
-   
#research #ecommerce #paypal #apple-pay #google-pay #social-login