# ApolloX V1 Python API

Currently there is no interface for withdrawal / depositing from a hotstorage wallet. I may use web3 to wrap this later. V1 is great for strategies that require more frequent purchase orders to make an aggregated position such as in a DCA strategy.


Example usage:
```python
    import apolloxv1
    import logging

    logger = logging.logger('root_logger')

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



