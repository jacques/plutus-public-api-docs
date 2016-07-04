## API Endpoints

Here’s a quick overview of our API endpoints:

Method | Endpoint | Usage | Returns
------ | -------- | ----- | -------
GET | <a href="#get-all-users-customers">`/api/v1/users`</a> | Gets users | users
GET | <a href="#get-a-specific-user">`/api/v1/users/USER`</a> | Gets specified user | user
POST | <a href="#create-a-customer">`/api/v1/users`</a> | Create a customer | user
DELETE | <a href="#delete-a-customer">`/api/v1/users/USER`</a> | Delete a customer |
GET | <a href="#listing-wallets-for-a-user">`/api/v1/users/USER/accounts`</a> | Get wallets for the specified user | wallets
GET | <a href="#fetching-a-mini-statement-for-a-users-wallet">`/api/v1/users/USER/accounts/ACCOUNT/ministatement`</a> | Gets a ministatement for the specified wallet | transactions
GET | <a href="#listing-transactions-for-a-users-wallet">`/api/v1/users/USER/accounts/ACCOUNT/transactions`</a> | Gets the transactions for the wallet which can be paginated | transactions
GET | <a href="#list-debit-cards-allocated-to-a-user">`/api/v1/users/USER/debitcards`</a> | Gets debit cards for the specified user | debitcards
GET | <a href="#fetch-mini-statement-for-a-debit-card"></a> |  |
GET | <a href="#fetch-statement-for-a-debit-card"></a> |  |
GET | <a href="#report-debit-card-as-being-lost-stolen"></a> |  |
POST | <a href="#list-beneficiaries-for-a-user">`/api/v1/users/USER/beneficiaries`</a> |  |
POST | <a href="#create-beneficiary">`/api/v1/users/USER/beneficiaries`</a> |  |
DELETE | <a href="#delete-beneficiary">`/api/v1/users/USER/beneficiaries/BENEFICIARY`</a> |  |
POST | <a href="#pay-a-beneficiary"></a> |  |
GET | <a href="#list-banks-for-use-when-creating-a-beneficiary">`/api/v1/banks`</a> | Get banks configured on the platform | banks
GET | <a href="#list-mobile-networks"></a> | Gets the list of mobile networks | networks
GET | <a href="#list-available-vouchers-for-a-network"></a> | Gets the list of vouchers available for purchase on a given network | vouchers
POST | <a href="#vend-an-airtime-voucher">`/api/v1/users/USER/prepaid/airtime</a> | Vends an airtime voucher | voucher
GET | <a href="#lookup-electricity-customer-information">`/api/v1/users/USER/prepaid/electricity/METERNO`</a> | Gets customer information for the specified meter number | meterinfo
POST | <a href="#vend-electricity-sts-token">`/api/v1/users/USER/prepaid/electricity/METERNO`</a> | Vends electricity for the specified meter number and amount | ststokens
POST | <a href="#sms-messaging"></a> | Sends a SMS message to the specified mobile numbers |
