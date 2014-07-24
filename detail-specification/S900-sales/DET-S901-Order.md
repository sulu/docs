##![S900 SALES](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/shop.png)DET-S902 Order

Main Purpose of SuluSalesOrderBundle is the handling of orders.

### Order Status
An order can have different status:
1 `cart` Order currently is in a users cart
2 `created` Order was manually created
4 `confirmed` Order was confirmed and an order confirmation was sent
8 `closed` Order was manually closed
16 `completed` Order is completed

Status are defined by a bitmask (see prefixed number).


### Api
Api Output should look like this:

#### Flat list

```
orders: {
	number: 1000
	type: 'manual' [defined by current status]
	customerNumber: '123'
	customer: John Doe [can either be an account or a contact]
	status: 'confirmed'
}
```

#### Order API 

```
order: {
	number:
	termsOfDelivery:
	termsOfPayment:
	costCentre:
	commission:
	created:
	changed:
	creator: 
	changer:
	desiredDeliveryDate:
	currency: 
	sessionId:
	taxfree:
	addressDelivery: 
	addressInvoice: 
	status: [LANGUAGE_SPECIFIC]
	responsiblePerson: 
}
```

