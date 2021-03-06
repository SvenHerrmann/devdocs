---
layout: default
title: REST API - Orders Resource
github_link: developers-guide/rest-api/api-resource-orders/index.md
indexed: false
---

## Introduction

In this part of the documentation, you can learn more about the API's orders resource. With this resource, it is possible to retrieve and update any order in your shop. We will also have a look at the associated data structures.


## General Information

This resource supports the following operations:

|  Access URL                 | GET                   | GET (List)            | PUT                   | PUT (Batch)         | POST                | DELETE               | DELETE (Batch)      |
|-----------------------------|-----------------------|-----------------------|-----------------------|------------------- -|---------------------|----------------------|---------------------|
| /api/orders              	  | ![Yes](../img/yes.png) | ![Yes](../img/yes.png) | ![Yes](../img/yes.png) | ![No](../img/no.png) | ![No](../img/no.png) | ![No](../img/yes.png) | ![No](../img/no.png) |

If you want to access this resource, simply query the following URL:

* **http://my-shop-url/api/orders**

## GET

#### Required Parameters

This API call requires one of the following parameters to be defined:

| Identifier      | Parameter | DB column                    | Example call                           |
|-----------------|-----------|------------------------------|----------------------------------------|
| Order Id        | id        | s_order.id                   | /api/orders/2                          |
| Order number    | number    | s_order.number               | /api/orders/20003?useNumberAsId=true   |

* **useNumberAsId=true** - This tells the API to query the order's data by its number, instead of its actual identifier. Otherwise, the syntax is just **/api/orders/id**. It's not possible to provide both parameter at the same time.

### Return Value

| Model					             | Table			     |
|------------------------------------|-----------------------|
| Shopware\Models\Customer\Customer  | s_user                |

| Field                 | Type                  | Original Object                                                               |
|-----------------------|-----------------------|-------------------------------------------------------------------------------|
| id				    | integer (primary key) | 							                                                    |
| number				| string				|																				|
| customerId			| integer (foreign key) | **[Customer](../api-resource-customer)**										|
| paymentId				| integer (foreign key)	| **[PaymentData](../models/#payment-data)**										|
| dispatchId			| integer (foreign key)	| **[Dispatch](../models/#dispatch)**											|
| partnerId				| integer (foreign key)	|    																			|
| shopId				| integer (foreign key)	| **[Shop](../models/#shop)**													|
| invoiceAmount			| double				|																				|
| invoiceAmountNet		| double				|																				|
| invoiceShipping		| double				|																				|
| invoiceShippingNet	| double				|																				|
| orderTime				| date/time				|																				|
| transactionId			| string				|																				|
| comment				| string				|																				|
| customerComment		| string				|																				|
| internalComment		| string				|																				|
| net					| boolean				|																				|
| taxFree				| boolean				|																				|
| temporaryId			| string				|																				|
| referer				| string				|																				|
| clearedDate			| date/time				|																				|
| trackingCode			| string				|																				|
| languageIso			| integer (foreign key)	| **[Locale](../models/#locale)**												|
| currency				| string				|																				|
| currencyFactor		| double				|																				|
| remoteAddress			| string				|																				|
| details				| array					| **[Detail](../models/#article-detail)**										|
| documents				| array					| **[Document](../models/#document)**											|
| payment				| object				| **[Payment](../models/#payment-instance)**										|
| paymentStatus			| object				| **[PaymentStatus](../models/#payment-status)**									|
| orderStatus			| object				| **[OrderStatus](../models/#order-status)**										|
| customer				| object				| **[Customer](../models/#customer)**											|
| paymentInstances		| array					| **[PaymentInstance](../models/#payment-instance)**								|
| billing				| object				| **[Billing](../models/#billing)**												|
| shipping				| object				| **[Shipping](../models/#shipping)**											|
| shop					| object				| **[Shop](../models/#shop)**													|
| dispatch				| object				| **[Dispatch](../models/#dispatch)**											|
| attribute				| object				| **[Attribute](../models/#order-attribute)**									|
| languageSubShop		| object				| **[Shop](../models/#shop)**													|
| paymentStatusId   	| integer (foreign key)	| **[Status](../models/#payment-status)**										|
| orderStatusId			| integer (foreign key) | **[OrderStatus](../models/#order-status)**										|

## PUT (update)

Orders can be identified using the following:

| Identifier    | Parameter | DB column              | Example call                             |
|---------------|-----------|------------------------|------------------------------------------|
| Article Id    | id        | s_articles.id          | /api/articles/2                          |
| Detail Number | number    | s_articles.ordernumber | /api/articles/SW10003?useNumberAsId=true |

The data structure used is similar to the one returned in the`GET` request.
