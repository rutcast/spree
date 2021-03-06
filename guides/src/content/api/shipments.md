---
title: Shipments
description: Use the Spree Commerce storefront API to access Shipment data.
---

## Mine

Retrieve a list of the current user's shipments by making this request:

```text
GET /api/v1/shipments/mine
```

Shipments are paginated and can be iterated through by passing along a `page` parameter:

```text
GET /api/v1/shipments/mine?page=2
```

### Parameters

<params params='[
  {
    "name": "page",
    "description": "The page number of shipments to display."
  }, {
    "name": "per_page",
    "description": "The number of shipments to return per page."
  }
]'></params>

### Response

<status code="200"></status>
<json sample="shipments"></json>

## Create

<alert type="admin_only" kind="danger"></alert>

The following attributes are required when creating a shipment:

- order_id
- stock_location_id
- variant_id

To create a shipment, make a request like this:

```text
POST /api/v1/shipments?shipment[order_id]=R123456789
```

The `order_id` is the number of the order to create a shipment for and is provided as part of the URL string as shown above. The shipment will be created at the selected stock location and include the variant selected.

Assuming in this instance that you want to create a shipment with a stock_location_id of `1` and a variant_id of `10` for order `R1234567`, send through the parameters like this:

```json
{
  "order_id": "R1234567",
  "stock_location_id": "1",
  "variant_id": "10"
}
```

### Response

<status code="200"></status>
<json sample="shipment_small"></json>

## Update

<alert type="admin_only" kind="danger"></alert>

To update shipment information, make a request like this:

```text
PUT /api/v1/shipments/H123456789?shipment[tracking]=TRK9000
```

To update order ship method inspect order/shipments/shipping_rates for available shipping_rate_id values and use following api call:

    PUT /api/v1/shipments/H123456789?shipment[selected_shipping_rate_id]=1

### Response

<status code="200"></status>
<json sample="shipment_small"></json>

## Ready

<alert type="admin_only" kind="danger"></alert>

To mark a shipment as ready, make a request like this:

    PUT /api/v1/shipments/H123456789/ready

You may choose to update shipment attributes with this request as well:

    PUT /api/v1/shipments/H123456789/ready?shipment[number]=1234567

### Response

<status code="200"></status>
<json sample="shipment_small" merge='{"state": "ready"}'></json>

## Ship

<alert type="admin_only" kind="danger"></alert>

To mark a shipment as shipped, make a request like this:

    PUT /api/v1/shipments/H123456789/ship

You may choose to update shipment attributes with this request as well:

    PUT /api/v1/shipments/H123456789/ship?shipment[tracking]=1234567

### Response

<status code="200"></status>
<json sample="shipment_small" merge='{"state": "shipped"}'></json>

## Add Variant

<alert type="admin_only" kind="danger"></alert>

To add a variant to a shipment, make a request like this:

    PUT /api/v1/shipments/H123456789/add

```json
{
  "order_id": 123456,
  "stock_location_id": 1,
  "variant_id": 10
}
```

### Response

<status code="200"></status>
<json sample="shipment_small"></json>

## Remove Variant

<alert type="admin_only" kind="danger"></alert>

To remove a variant from a shipment, make a request like this:

    PUT /api/v1/shipments/H123456789/remove?variant_id=1&quantity=1

### Response

<status code="200"></status>
<json sample="shipment_small"></json>
