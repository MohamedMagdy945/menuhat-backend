# Use Cases

## Customer

### UC-01: Browse Restaurants

The customer can browse restaurants available on Menuhat.

### UC-02: Browse Restaurant Menu

The customer can view the menu of an available restaurant.

### UC-03: Place Order

The customer can place an order from a restaurant.

### UC-04: Track Order

The customer can view the current status of an order.

### UC-05: Review Restaurant

The customer can submit a review for a restaurant.

---

### UC-03: Place Order

**Actor:** Customer

**Goal:**  
The Customer creates an order containing items from a restaurant menu.

#### Main Flow

1. Customer selects a restaurant.
2. Customer browses the restaurant menu.
3. Customer selects one or more menu items.
4. Customer specifies the quantity of each item.
5. Customer confirms the order.
6. The system validates the order.
7. The system calculates the order total.
8. The system creates the order.
9. The system assigns the initial order status.
10. The system confirms the order to the Customer.

#### Business Rules

- Customer must be authenticated to place an order.
- The restaurant must be `Active`.
- The order must contain at least one item.
- Every ordered item must belong to the selected restaurant.
- Every ordered item must be `Available`.
- Quantity must be greater than zero.
- The price used in the order must be determined when the order is created.
- The order total must be calculated by the system.
- Customer cannot directly set the order total.

---

## Restaurant Owner

### UC-06: Register Restaurant

**Actor:** Restaurant Owner

**Goal:**  
The restaurant owner wants to register a restaurant on Menuhat.

#### Main Flow

1. Restaurant Owner starts the restaurant registration process.
2. Restaurant Owner provides the required restaurant information.
3. The system validates the provided information.
4. The system creates the restaurant registration.
5. The restaurant is created with a `Pending` status.
6. The system informs the Restaurant Owner that the registration is pending review.

#### Business Rules

- A restaurant must have the required information before registration.
- A newly registered restaurant starts with `Pending` status.
- A `Pending` restaurant is not visible to customers.
- Only an Admin can approve a restaurant.

#### Alternative Flows

- If required information is missing, the system rejects the registration.
- If the provided information is invalid, the system asks the Restaurant Owner to correct it.

---

## Admin

### UC-11: Review Restaurant Registration

The admin can review restaurant registration requests.

### UC-12: Approve Restaurant

The admin can approve a restaurant registration.

### UC-13: Manage Restaurants

The admin can manage restaurants on the platform.

### UC-14: Manage Users

The admin can manage users on the platform.

### UC-11: Review Restaurant Registration

**Actor:** Admin

**Goal:**  
The Admin reviews a restaurant registration submitted by a Restaurant Owner.

#### Main Flow

1. Admin opens the restaurant registration requests.
2. The system displays restaurants waiting for review.
3. Admin selects a restaurant registration.
4. The system displays the restaurant information.
5. Admin reviews the provided information.
6. Admin can approve or reject the registration.

#### Business Rules

- Only an Admin can review restaurant registrations.
- Only restaurants with `Pending` status can be reviewed.
- An approved restaurant becomes `Active`.
- A rejected restaurant must not be available to customers.

#### Alternative Flows

- If the restaurant is no longer `Pending`, the Admin cannot review it as a pending registration.


---

### UC-08: Manage Menu

**Actor:** Restaurant Owner

**Goal:**  
The Restaurant Owner manages the menu of their restaurant.

#### Main Flow

1. Restaurant Owner opens their restaurant.
2. The system displays the restaurant menu.
3. Restaurant Owner can create a menu.
4. Restaurant Owner can update the menu information.
5. Restaurant Owner can manage the menu items belonging to the menu.

#### Business Rules

- Only the Restaurant Owner can manage the menu of their own restaurant.
- A Restaurant Owner cannot manage another restaurant's menu.
- A menu belongs to a restaurant.
- A menu item belongs to a menu.
- Only menu items belonging to the restaurant's menu can be managed by that Restaurant Owner.

#### Alternative Flows	

- If the restaurant does not exist, the operation is rejected.
- If the Restaurant Owner does not own the restaurant, the operation is rejected.

---

### UC-09: Manage Menu Items

**Actor:** Restaurant Owner

**Goal:**  
The Restaurant Owner manages the items offered by their restaurant.

#### Main Flow

1. Restaurant Owner opens a menu.
2. The system displays the menu items.
3. Restaurant Owner can add a new menu item.
4. Restaurant Owner provides the menu item information.
5. The system validates the information.
6. The system creates the menu item.
7. Restaurant Owner can update the menu item.
8. Restaurant Owner can change the availability of the menu item.

#### Business Rules

- A menu item must belong to a menu.
- A Restaurant Owner can manage only menu items belonging to their restaurant.
- A menu item must have a name.
- A menu item must have a price.
- A menu item can be Available or Unavailable.
- An Unavailable menu item cannot be added to a new order.

#### Alternative Flows

- If the menu item information is invalid, the operation is rejected.
- If the menu item does not belong to the Restaurant Owner's restaurant, the operation is rejected.

---

### UC-04: Checkout

**Actor:** Customer

**Goal:**  
The Customer confirms the items in the cart and creates orders for the selected restaurants.

#### Main Flow

1. Customer opens the cart.
2. The system displays the cart items grouped by restaurant.
3. Customer reviews the cart.
4. Customer confirms the checkout.
5. The system validates the cart items.
6. The system groups cart items by restaurant.
7. The system creates a separate order for each restaurant.
8. The system calculates the total for each order.
9. The system clears the successfully ordered items from the cart.
10. The system confirms the created orders to the Customer.

#### Business Rules

- A cart can contain items from multiple restaurants.
- Each cart item belongs to exactly one restaurant through its menu item.
- Items from different restaurants must result in separate orders.
- Each restaurant receives only the order containing its own items.
- An order must contain at least one item.
- The restaurant must be `Active` when the order is created.
- Menu items must be `Available` when the order is created.
- The system calculates order totals.
- The customer cannot directly set the order total.
- The order stores the item price at the time the order is created.

---

### UC-10: Manage Order

**Actor:** Restaurant Owner

**Goal:**  
The Restaurant Owner manages orders received from customers.

#### Main Flow

1. Restaurant Owner opens the restaurant orders.
2. The system displays the restaurant's orders.
3. Restaurant Owner selects an order.
4. Restaurant Owner views the order details.
5. Restaurant Owner updates the order status.
6. The system validates the status transition.
7. The system saves the new order status.
8. The Customer can view the updated order status.

---
### UC-15: Cancel Order

**Actor:** Customer

**Goal:**  
The Customer cancels an order that has not started processing.

#### Main Flow

1. Customer opens an order.
2. Customer requests to cancel the order.
3. The system checks whether the order can be cancelled.
4. The system changes the order status to `Cancelled`.
5. The system informs the Customer that the order has been cancelled.

#### Business Rules

- A Customer can cancel only their own order.
- An order can be cancelled only before a defined processing stage.
- A delivered order cannot be cancelled.
- A cancelled order cannot return to an active order status.
- The system must record when the order was cancelled.
- The system should record who cancelled the order.

#### Alternative Flows

- If the order cannot be cancelled, the system rejects the cancellation request.
- If the order does not belong to the Customer, the system rejects the request.
---
## Open Questions

- Should a newly registered restaurant always start with `Pending` status?
- What information is required to register a restaurant?
- Can a Restaurant Owner register multiple restaurants?
- Can multiple owners manage the same restaurant?
-  Can a restaurant have more than one menu?
- Does every restaurant have a menu automatically after approval?
- Can an empty menu exist?
- Can a menu be disabled?
- Can a Restaurant Owner delete a menu?
- 
- What are the possible Order statuses?
- Can a Customer cancel an order?
- Until which Order status can it be cancelled?
- Can an order contain items from multiple restaurants?
- Is delivery address required?
- Is delivery fee supported?
- Are taxes supported?
- Are discounts or promo codes supported?
- What happens if a MenuItem becomes unavailable after it was added to the cart?
- Does placing an order require payment immediately?

- What are the exact order statuses?
- Who can change each order status?
- Is there a Delivery Driver actor?
- Does each restaurant manage its own delivery drivers?
- Who marks an order as `OutForDelivery`?
- Who marks an order as `Delivered`?
- Can a restaurant reject an order?
- Can a customer cancel an order?
- Until which status can an order be cancelled?

- Until which order status can the customer cancel an order?
- Does cancelling an order require a reason?
- Can the Restaurant Owner cancel an order?
- If a restaurant cancels an order, should the customer receive a notification?
- If payment has already been made, what happens to the payment when an order is cancelled?