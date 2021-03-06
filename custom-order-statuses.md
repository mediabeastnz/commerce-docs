# Custom Order Statuses

## Overview

When a customer completes a cart it becomes an order.

The only differences between an order and a cart is:

- A cart has an empty `dateOrdered` attribute.
- A cart has its `isCompleted` attribute set to `false`.
- An order has a custom status set.

When a customer completes their order, the `dateOrdered` is set to the current time and date and it gets a custom order status. The custom order status set depends on which order status you’ve established as the default.

Custom order statuses can be managed from Commerce → Settings → Order Statuses in the control panel. There you can choose the default order status for new orders.

## Functionality

Order statuses allow a store owner to track an order through the various stages of its life cycle.

For example you may use default status of “Received”, set when the order is completed. Once you’ve packaged the order for shipment, you might update to “Packed” status. Or if you’re waiting to receive product stock you might use a “Pending Stock” status. When you’ve shipped the order you might set the status to “Completed”. Every year you might change all “Completed” orders to an “Archived” status.

You can set up as many statuses as you want, with any meaning ascribed to them, and you can move your order between statuses freely.

This allows you to manage your orders and organise them easily.

Whenever you change the status of an order, the change from one status to another is recorded in an Order History record on the order. This allows you to see the history of the order over time.

In addition to setting a new status, you can record a message that gets stored with the status change. For example, you might place an order into a status called “Pending Stock”, and in the message write which product you’re waiting on. This is a good way to allow multiple store managers to better understand why a particular status was set on an order.

## Changing the status of an order

### In the control panel

An order’s status can be changed on the Edit Order Page in the control panel. Choosing “Update Order Status” will present you with a modal window that allows the selection of the new status and a message associated with the change. After choosing “Submit”, the order’s status will be updated and a new order history record will be created.

You can change the status of multiple orders at the same time on the Order Index Page using the checkbox selection and then choosing “Update Order Status” from the action menu.

### In code

```php
$order = Plugin::getInstance()->getOrders()->getOrderById(ID);
$order->orderStatusId = $orderStatus->id; // new status ID
$order->message = $message; // new message
$result = Craft::$app->getElements()->saveElement($order);
```

By updating `orderStatusId` and saving the order, the status change event will be triggered and a new order status history record will be created.

## Email

In addition to using order statuses to manage your orders, you can choose emails that will be sent when an order moves into that status.

See [Order Status Emails](order-status-emails.md).

## Line item statuses

Line item statuses are not the same as order statuses: they cannot trigger emails and are only for internal management of the order. Line items do not get a status by default, and can have a `null` or “None” status.
