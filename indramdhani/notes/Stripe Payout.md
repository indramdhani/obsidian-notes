# Stripe Payout

If we are going to automate some accounting tasks, Stripe Payout Report can be used to get the needed data, the result would be a file (probably in CSV). We need to translate it to the required Xero task and check the Xero documentation. Based on the dev team that works on Xero, we cannot add a meta field on Xero. The team use the description field.

## Payout

The process to send funds from Stripe to the merchant bank account

The first payout will be received after 7-14 days after the first successful payment

Payout schedule is managed in dashboard

Standard payout timing is different for each country and the business risk

The payout list and expectation date to be received is available in the dashboard

Merchant should add bank account information in order to receive payout

Multiple bank accounts for different settlement currencies are supported, with one bank account as a default

Payout type:

-   automatic payout
-   manual payout
-   instant payout
-   negative payout

## Financial Reports

### Payout reconciliation

-   Break down the individual transactions included in each payout to your bank account
-   Only available for merchant with automatic payout enabled
-   Download the detail for multiple payouts at a time
-   Available columns based on report type:
    -   Balance summary
    -   Payouts reconciliation summary
    -   Itemized payout reconciliation
    -   Ending balance reconciliation summary
    -   Itemized ending balance reconciliation

### Balance Reports

-   Download monthly transaction history
-   View monthly totals by transaction category
-   **[Reconcile](https://stripe.com/docs/reports/select-a-report#reconciliation)** your Stripe balance like a bank account
-   Download a list of your payouts
-   Available columns based on report type
    -   Balance summary
    -   Balance change from activity summary
    -   Itemized balance change from activity
    -   Payouts summary
    -   Itemized payouts

Both can be used to reconcile the transaction. _Balance Reports_ is for the customer who treats Stripe as another bank account. _Payout Reconciliation_ is for the customer who treats Stripe as a temporary account.

## Report API

Stripe prepares report data on a daily basis ( the range is activity starts from 12.00 am UTC → 11.59 pm UTC )

All of the financial report also available via report API

Certain report types can only be run based on live-data

The API result is reference to a report file to download, if we are going to create Stripe → Xero automation, may need to check Xero API and the current accounting tasks that related with Stripe and Xero

## Current Accounting Tasks

1.  Manual Job: collect & check data for International Custom Order, based on invoice custom reference
2.  Half manual + Xero, Reconcile Bank Account
    1.  Login to Stripe
        1.  Go to Dashboard → Payment->Payout->Export Earning everyday. The result would be .CSV
    2.  Prepare Google Sheets as a reference for Xero:
        1.  Upload payout report to google doc
        2.  Copy, paste & organize the data export to google sheets
    3.  Input the data for the bank account reconcile process in Xero
        1.  Approve all sales invoices,
        2.  Adjust Amount for all International Sales Invoices,
        3.  Add Bills for Merchant fee, Refunds,
        4.  Add Invoices for International Sample Packs earnings
    4.  Access Reconcile menu for every bank Account,
        1.  Find & Match with google sheet as a references
        2.  Reconcile/OK

## References

[](https://stripe.com/docs/payouts)[https://stripe.com/docs/payouts](https://stripe.com/docs/payouts)

[](https://stripe.com/docs/reports)[https://stripe.com/docs/reports](https://stripe.com/docs/reports)

[](https://stripe.com/docs/reports/api)[https://stripe.com/docs/reports/api](https://stripe.com/docs/reports/api)

[](https://stripe.com/docs/reports/options)[https://stripe.com/docs/reports/options](https://stripe.com/docs/reports/options)

[](https://stripe.com/docs/api/reporting/report_run)[https://stripe.com/docs/api/reporting/report\_run](https://stripe.com/docs/api/reporting/report_run)

[](https://stripe.com/partners/xero)[https://stripe.com/partners/xero](https://stripe.com/partners/xero)

[](https://developer.xero.com/documentation/api/invoices)[https://developer.xero.com/documentation/api/invoices](https://developer.xero.com/documentation/api/invoices)

#ecommerce #stripe #payout #research 