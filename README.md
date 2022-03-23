# PMClient SDK in python


# Description
PMClient is a bunch of REST-APIs that can be used to build a fully functional investment and trading platform.
Real time execution of orders with simple HTTP API Collection.

# Install the Package

pip install pyPMClient

# API Usage

from pyPMClient import PMClient

##### User needs to create an object of sdk and pass apiKey & apiSecretKey
pm = PMClient(api_key="your_api_key", api_secret="your_api_secret")

##### User can call the login method and get the login URL.
pm.login()

##### User manually executes a login url in the browser and fetches requestToken after validating username, password, OTP and passcode. 
##### After a successful login user will be provided the request_token in the URL

##### Once the request_token is obtained you can generate access_token by calling generate_session
pm.generate_session(request_token="your_request_token")

##### After generating the access_token it will get set and any API can be called with same access_token.

# Place Order
##### Here you can place regular, cover and bracket order
##### For cover order in argument user has to add trigger_price
##### For bracket order in argument user has to add stoploss_value & profit_value
order = pm.place_order(txn_type, exchange, segment, product, security_id, quantity, validity, order_type, price, source, 
                    off_mkt_flag)

# Modify Order
#### Here you can modify orders
#### For cover order in argument user has to add leg_no
##### For bracket order in argument user has to add leg_no & algo_order_no
order = pm.modify_order(source, txn_type, exchange, segment, product, security_id, quantity, validity, order_type,
                     price, mkt_type, order_no, serial_no, group_id)

# Cancel Order
#### Here you can Cancel Orders
#### For cover order in argument user has to add leg_no
##### For bracket order in argument user has to add leg_no & algo_order_no
order = pm.cancel_order(source, txn_type, exchange, segment, product, security_id, quantity, validity, order_type,
                     price, mkt_type, order_no, serial_no, group_id)


# Convert Order
#### For converting through eDIS user needs to provide edis_txn_id & edis_auth_mode
#### The above details can be generated by TPIN APIs
order = pm.convert_regular(source, txn_type, exchange, mkt_type, segment, product_from, product_to, quantity,
                        security_id)

# Order Details
#### Fetch details of all the order
pm.order_book()

# Trade Details
##### Fetch Trade Details
pm.trade_details(order_no, leg_no, segment)

# Position
#### Get all the positions
pm.position()

# Position Details
#### Get position detail of specific stock
pm.position_details(security_id, product, exchange)

# Get Funds History
#### Get the funds history
pm.funds_summary(config=True)

# Scrip Margin
#### Calculate Scrip Margin
pm.scrip_margin(
                source="N"
                margin_list=[
                              {
                                 "exchange":"NSE",
                                 "segment":"D",
                                 "security_id":"46840",
                                 "txn_type":"B",
                                 "quantity":"250",
                                 "strike_price":"0",
                                 "trigger_price":"0",
                                 "instrument":"FUTSTK"
                              },
                              {
                                 "exchange":"",
                                 "segment":"",
                                 "security_id":"",
                                 "txn_type":"",
                                 "quantity":"",
                                 "strike_price":"",
                                 "trigger_price":"",
                                 "instrument":""
                              }...
                           ]
                )

# Order Margin
#### Calculate Order Margin
pm.order_margin(source, exchange, segment, security_id, txn_type, quantity, price, product, trigger_price)

# Holdings value
#### Get value of the holdings
pm.holdings_value()

# User Holdings Data
#### Get holdings data of User
#### isin will be provided in order details
pm.user_holdings_data(isin)

# Security Master
#### Data will be provided in CSV format
pm.security_master()

# User Details
#### Fetch user details
pm.get_user_details()

# Generate Tpin
pm.generate_tpin()

# Validate Tpin
pm.validate_tpin(exchange, segment, security_id, quantity)

# Status 
#### user can get the edis_request_id from the response of validate TPIN API
pm.status(edis_request_id)


