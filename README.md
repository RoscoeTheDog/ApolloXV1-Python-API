# ApolloX V1 Python API

![image](https://github.com/RoscoeTheDog/ApolloXV1-Python-API/assets/54086262/26892865-376e-414d-ac24-ac066f55a01b)

APX V1 is a great decentralized solution for trading strategies that require more frequent purchase orders, such as in a DCA strategy, due to its low transactions costs and fast speeds.

Currently there is no wrapper for depositing / withdrawing to and from a vault via hotstorage wallet. I may use web3 to implement this later. Users can deposit money on the front end of the platforms website for now.

Example usage:
```python
    import apolloxv1
    import logging

    logger = logging.getLogger('root_logger')

    params = {
    	'api_key': 'api_key_val',
        'api_secret': 'api_secret_val',
    }
    
    APX = apolloxv1.ApolloXV1(kwargs=params)
    
    # if no price given, it will be a market order. Otherwise, limit order instead.
    request = APX.create_order(symbol='BTCUSDT', 'long', 100)	# $100 USDT purchase order
    
    # check order status
    receipt = APX.fetch_order(request.get('id'))
    order_status = receipt.get('status')
    
    # raise if key not found in receipt for whatever reason
    if order_status is None:
    	raise ValueError('order status None type')
    
    # do stuff dependent on state.
    order_status = str.upper(order_status)
    if order_status == 'CANCELED' or order_status == 'EXPIRED':
    	logger.warning('order status "canceled"')
    elif order_status == 'ACTIVE' or order_status == 'NEW':
    	logger.info('order status "active"')
    elif order_status == 'FILLED':
    	logger.info('order status "filled"')
```

Like my work? Buy me a drink! ☕🍺 <br>
[![](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/donate/?hosted_button_id=9TUKFAZRVLH4W)****
